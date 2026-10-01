# 15 integracao sistema banco de dados

## 15.1 Como a aplicação acessa os dados

O servidor da aplicação acessa o PostgreSQL (o navegador **nunca** acessa o banco diretamente). As credenciais ficam em variáveis de ambiente e todas as consultas usam **parâmetros**, o que evita SQL injection.

🔲 O grupo deve definir se usará a biblioteca `pg` diretamente ou um ORM (ex.: Prisma) e ajustar esta página.

## 15.2 Registrar uma venda: uma única transação

A venda mexe em várias tabelas ao mesmo tempo. Por isso ela roda dentro de **uma transação**: se qualquer passo falhar, nada é gravado (RNF08).

| Passo | Ação                                 | Tabela                 |
| ----- | ------------------------------------ | ---------------------- |
| 1     | Cria o pedido                        | `pedido`               |
| 2     | Insere cada item com o preço da hora | `item_pedido`          |
| 3     | Baixa o estoque, só se houver saldo  | `produto`              |
| 4     | Registra a saída de estoque          | `movimentacao_estoque` |
| 5     | Registra o pagamento                 | `pagamento`            |
| 6     | Atualiza total e status do pedido    | `pedido`               |

### Exemplo em SQL

```sql
BEGIN;

INSERT INTO pedido (id_cliente, id_usuario, status)
VALUES (1, 2, 'ABERTO')
RETURNING id_pedido;   -- suponha que retornou 3

INSERT INTO item_pedido (id_pedido, id_produto, quantidade, preco_unitario, subtotal)
VALUES (3, 1, 2, 49.90, 99.80);

-- Baixa somente se houver saldo. Se 0 linhas forem afetadas, a aplicação faz ROLLBACK.
UPDATE produto
SET estoque_atual = estoque_atual - 2
WHERE id_produto = 1 AND estoque_atual >= 2;

INSERT INTO movimentacao_estoque (id_produto, id_pedido, tipo, quantidade, motivo)
VALUES (1, 3, 'SAIDA', 2, 'Venda pedido 3');

INSERT INTO pagamento (id_pedido, forma, valor, status)
VALUES (3, 'PIX', 99.80, 'CONFIRMADO');

UPDATE pedido SET valor_total = 99.80, status = 'PAGO' WHERE id_pedido = 3;

COMMIT;
```

### Exemplo ilustrativo no código da aplicação

```ts
import { Pool } from "pg";

const pool = new Pool({ connectionString: process.env.DATABASE_URL });

export async function baixarEstoque(client: any, idProduto: number, qtd: number) {
  const r = await client.query(
    `UPDATE produto
        SET estoque_atual = estoque_atual - $2
      WHERE id_produto = $1 AND estoque_atual >= $2`,
    [idProduto, qtd]
  );
  if (r.rowCount === 0) throw new Error("Estoque insuficiente");
}

export async function registrarVenda(/* dados do pedido */) {
  const client = await pool.connect();
  try {
    await client.query("BEGIN");
    // ... inserir pedido, itens, baixar estoque, pagamento
    await client.query("COMMIT");
  } catch (e) {
    await client.query("ROLLBACK");
    throw e;
  } finally {
    client.release();
  }
}
```

{% hint style="info" %}
Os exemplos são **didáticos**. 🔲 Substituir pelo código real do projeto (com link para o repositório) quando a integração estiver pronta.
{% endhint %}

## 15.3 Integração com a IA

Para o Assistente Lilica, o servidor executa consultas de **agregação** (por exemplo, total vendido por produto no mês), monta um texto com esses números e o envia ao serviço de IA. **Nomes, telefones e e-mails de clientes nunca entram nesse texto.** A chamada é registrada em `registro_uso_ia`.

## 15.4 Cuidados na integração

* consultas parametrizadas;
* senhas apenas como hash;
* acesso às telas e rotas conforme o perfil (ADMIN ou VENDEDOR);
* transações nas operações de venda, cancelamento e reposição.

## 15.5 Evidências

🔲 Inserir capturas mostrando o sistema gravando e lendo dados do banco (com legenda e explicação).
