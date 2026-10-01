# 13 povoamento do banco de dados

## 13.1 Estratégia

Os dados de demonstração são **fictícios**, gerados com apoio de IA, para testar o sistema sem expor informações reais de clientes.

🔲 Substituir os produtos e categorias de exemplo pelo catálogo real (ou próximo do real) da Lilica.

## 13.2 Script de povoamento (exemplo)

```sql
INSERT INTO usuario (id_usuario, nome, email, senha_hash, perfil) VALUES
  (1, 'Administrador Teste', 'admin@exemplo.com',    'HASH_FICTICIO_1', 'ADMIN'),
  (2, 'Vendedor Teste',      'vendedor@exemplo.com', 'HASH_FICTICIO_2', 'VENDEDOR');

INSERT INTO categoria (id_categoria, nome) VALUES
  (1, 'Vestuário'),
  (2, 'Acessórios');

INSERT INTO produto (id_produto, id_categoria, nome, preco_venda, estoque_atual, estoque_minimo) VALUES
  (1, 1, 'Camiseta básica',      49.90, 28, 5),
  (2, 2, 'Caneca personalizada', 29.90, 11, 10),
  (3, 1, 'Boné',                 39.90,  3, 5),
  (4, 2, 'Chaveiro',              9.90, 47, 10);

INSERT INTO cliente (id_cliente, nome, telefone, email) VALUES
  (1, 'Cliente Teste 01', '(31) 90000-0001', 'cliente01@exemplo.com'),
  (2, 'Cliente Teste 02', '(31) 90000-0002', 'cliente02@exemplo.com');

-- Pedido 1: pago
INSERT INTO pedido (id_pedido, id_cliente, id_usuario, status, valor_total) VALUES
  (1, 1, 2, 'PAGO', 129.70);
INSERT INTO item_pedido (id_pedido, id_produto, quantidade, preco_unitario, subtotal) VALUES
  (1, 1, 2, 49.90, 99.80),
  (1, 2, 1, 29.90, 29.90);
INSERT INTO pagamento (id_pedido, forma, valor, status) VALUES
  (1, 'PIX', 129.70, 'CONFIRMADO');

-- Pedido 2: aberto, com pagamento pendente
INSERT INTO pedido (id_pedido, id_cliente, id_usuario, status, valor_total) VALUES
  (2, 2, 2, 'ABERTO', 69.60);
INSERT INTO item_pedido (id_pedido, id_produto, quantidade, preco_unitario, subtotal) VALUES
  (2, 3, 1, 39.90, 39.90),
  (2, 4, 3,  9.90, 29.70);
INSERT INTO pagamento (id_pedido, forma, valor, status) VALUES
  (2, 'DINHEIRO', 69.60, 'PENDENTE');

-- Movimentações (o estoque_atual acima já considera estas saídas)
INSERT INTO movimentacao_estoque (id_produto, id_pedido, tipo, quantidade, motivo) VALUES
  (1, 1, 'SAIDA', 2, 'Venda pedido 1'),
  (2, 1, 'SAIDA', 1, 'Venda pedido 1'),
  (3, 2, 'SAIDA', 1, 'Venda pedido 2'),
  (4, 2, 'SAIDA', 3, 'Venda pedido 2');

-- Ajusta os contadores de identidade após inserir IDs manualmente
SELECT setval(pg_get_serial_sequence('usuario','id_usuario'),     (SELECT MAX(id_usuario) FROM usuario));
SELECT setval(pg_get_serial_sequence('categoria','id_categoria'), (SELECT MAX(id_categoria) FROM categoria));
SELECT setval(pg_get_serial_sequence('produto','id_produto'),     (SELECT MAX(id_produto) FROM produto));
SELECT setval(pg_get_serial_sequence('cliente','id_cliente'),     (SELECT MAX(id_cliente) FROM cliente));
SELECT setval(pg_get_serial_sequence('pedido','id_pedido'),       (SELECT MAX(id_pedido) FROM pedido));
```

## 13.3 Volume de dados

| Tabela                | Registros de demonstração |
| --------------------- | ------------------------- |
| usuario               | 2                         |
| categoria             | 2                         |
| produto               | 4                         |
| cliente               | 2                         |
| pedido                | 2                         |
| item\_pedido          | 4                         |
| pagamento             | 2                         |
| movimentacao\_estoque | 4                         |

🔲 Ampliar o volume (dezenas de produtos e centenas de pedidos) para tornar os relatórios e testes mais realistas.

{% hint style="info" %}
Neste exemplo o **Boné** está com estoque (3) abaixo do mínimo (5) e a **Caneca** (11) está perto do limite de 10, o que permite demonstrar o alerta de estoque baixo.
{% endhint %}
