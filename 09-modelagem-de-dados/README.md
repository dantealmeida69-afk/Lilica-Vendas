# 09 modelagem de dados

## 9.1 Visão geral

&#x20;Modelagem do Sistema Lilica Vendas. O sistema deve organizar informações de usuários, clientes, produtos, vendas, pagamentos, encomendas, fornecedores e repasses.

A evolução ocorre em três níveis:

**Conceitual (entidades e relacionamentos) → Lógico (tabelas, PKs e FKs) → Físico (SQL no SGBD).**

## 9.2 Entidades e atributos

| Entidade    | Atributos                                                                                        |
| ----------- | ------------------------------------------------------------------------------------------------ |
| USUARIO     | id\_usuario (PK), nome, email, senha                                                             |
| CLIENTE     | id\_cliente (PK), nome, celular, email, observacoes                                              |
| PRODUTO     | id\_produto (PK), nome, valor, descricao                                                         |
| VENDA       | id\_venda (PK), id\_cliente (FK), id\_usuario (FK), data\_venda, valor\_total, status\_pagamento |
| ITEM\_VENDA | id\_item\_venda (PK), id\_venda (FK), id\_produto (FK), quantidade, preco\_unitario, subtotal    |
| PAGAMENTO   | id\_pagamento (PK), id\_venda (FK), data\_pagamento, valor\_pago                                 |
| ENCOMENDA   | id\_encomenda (PK), id\_cliente (FK), id\_produto (FK), quantidade, data\_encomenda, status      |
| FORNECEDOR  | id\_fornecedor (PK), nome, telefone, email                                                       |
| REPASSE     | id\_repasse (PK), id\_fornecedor (FK), valor, data\_repasse, observacao                          |

**Observação:** embora o atributo de usuário seja denominado `senha`, o conteúdo armazenado deve ser o hash da senha.

## 9.3 Relacionamentos e cardinalidades

| Relacionamento        | Cardinalidade | Descrição                                                                                  |
| --------------------- | ------------: | ------------------------------------------------------------------------------------------ |
| CLIENTE — VENDA       |         1 : N | Um cliente pode realizar várias compras; cada venda pertence a um único cliente.           |
| USUARIO — VENDA       |         1 : N | Um usuário pode registrar várias vendas; cada venda possui um único usuário responsável.   |
| VENDA — ITEM\_VENDA   |         1 : N | Uma venda pode possuir vários itens; cada item pertence a uma única venda.                 |
| PRODUTO — ITEM\_VENDA |         1 : N | Um produto pode aparecer em vários itens de venda; cada item referencia um único produto.  |
| VENDA — PAGAMENTO     |         1 : N | Uma venda pode receber vários pagamentos; cada pagamento pertence a uma única venda.       |
| CLIENTE — ENCOMENDA   |         1 : N | Um cliente pode solicitar várias encomendas; cada encomenda pertence a um único cliente.   |
| PRODUTO — ENCOMENDA   |         1 : N | Um produto pode aparecer em várias encomendas; cada encomenda referencia um único produto. |
| FORNECEDOR — REPASSE  |         1 : N | Um fornecedor pode receber vários repasses; cada repasse pertence a um único fornecedor.   |

## ![](<../.gitbook/assets/image (1).png>)

## 9.4 Regras de negócio

1. Cada entidade possui um identificador único.
2. Toda venda deve estar vinculada a um cliente e a um usuário responsável.
3. Cada item de venda deve estar vinculado a uma venda e a um produto.
4. Cada pagamento deve estar vinculado a uma venda.
5. Cada encomenda deve identificar um cliente e um produto.
6. Cada repasse deve identificar o fornecedor destinatário.
7. O e-mail do usuário é obrigatório e único.
8. Os campos obrigatórios do modelo lógico devem ser preenchidos.
9. O preço unitário deve ser armazenado no item da venda para preservar o valor praticado no momento da operação.
10. O subtotal deve corresponder à quantidade multiplicada pelo preço unitário.
11. Valores monetários devem utilizar `DECIMAL(10,2)`, quantidades devem utilizar `INT` e datas devem utilizar `DATE`.
12. Telefones devem ser armazenados como texto.

## 9.5 Justificativa das decisões de modelagem

**Cadastro de usuário simplificado:** A tabela USUARIO armazena o nome de acesso e o hash da senha. Seu identificador&#x20;interno permite relacionar o usuário às vendas sem armazenar informações pessoais adicionais.

**Separação entre cliente e usuário:** O cliente realiza a compra, enquanto o usuário opera o sistema. Essa separação&#x20;permite identificar o comprador e o responsável pelo registro.

**Um produto por venda:** A tabela VENDA registra diretamente o produto, a quantidade e o preço unitário. Essa decisão&#x20;simplifica a estrutura, limitando cada venda a um produto.

\
**Preservação do preço da venda:** O preço unitário é armazenado na venda para preservar o histórico, mesmo que o&#x20;valor do produto seja atualizado.\
\
**Separação entre venda e pagamento:** Permite registrar pagamentos em diferentes datas e valores e calcular o saldo&#x20;pendente de cada venda.

\
**Separação entre encomenda e venda:** A encomenda registra uma solicitação e seu andamento. O modelo não&#x20;estabelece uma ligação direta entre encomenda e venda.

\
**Separação entre fornecedor e repasse:** Os dados do fornecedor são cadastrados uma única vez. Cada repasse registra&#x20;o valor transferido e a data da operação.

\
**Uso de chaves e tipos adequados :** As chaves identificam os registros e mantêm seus vínculos. INT é utilizado para&#x20;identificadores e quantidades, VARCHAR para textos curtos, DATE para datas e DECIMAL (10,2) para valores&#x20;monetários.

\
**Atualização dos valores calculados:** O valor total e o status de pagamento devem acompanhar as alterações nos&#x20;dados da venda e nos pagamentos, evitando divergências.



## 9.6 Evolução da modelagem

| Versão | Alteração                                                                                                | Motivo                                |
| ------ | -------------------------------------------------------------------------------------------------------- | ------------------------------------- |
| v0.1   | Modelo inicial com entidades diferentes da Entrega 2                                                     | Ponto de partida do projeto           |
| v0.2   | Adequação para USUARIO, CLIENTE, PRODUTO, VENDA, ITEM\_VENDA, PAGAMENTO, ENCOMENDA, FORNECEDOR e REPASSE | Alinhar o projeto ao PDF da Entrega 2 |

> A modelagem acima segue diretamente a estrutura apresentada na Entrega 2.
