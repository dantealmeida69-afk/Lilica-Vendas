# 11 modelo logico

Legenda: **PK** = chave primária · **FK** = chave estrangeira · **NN** = não nulo · **UQ** = único.

## 11.1 USUARIO

| Atributo    | Tipo         | Restrições |
| ----------- | ------------ | ---------- |
| id\_usuario | INT          | PK         |
| nome        | VARCHAR(120) | NN         |
| email       | VARCHAR(160) | NN, UQ     |
| senha       | VARCHAR(255) | NN         |

> O conteúdo de `senha` deve ser o hash da senha.

## 11.2 CLIENTE

| Atributo    | Tipo         | Restrições |
| ----------- | ------------ | ---------- |
| id\_cliente | INT          | PK         |
| nome        | VARCHAR(120) | NN         |
| celular     | VARCHAR(20)  |            |
| email       | VARCHAR(160) |            |
| observacoes | VARCHAR(300) |            |

## 11.3 PRODUTO

| Atributo    | Tipo          | Restrições |
| ----------- | ------------- | ---------- |
| id\_produto | INT           | PK         |
| nome        | VARCHAR(120)  | NN         |
| valor       | DECIMAL(10,2) | NN         |
| descricao   | TEXT          |            |

## 11.4 VENDA

| Atributo          | Tipo          | Restrições       |
| ----------------- | ------------- | ---------------- |
| id\_venda         | INT           | PK               |
| id\_cliente       | INT           | FK → CLIENTE, NN |
| id\_usuario       | INT           | FK → USUARIO, NN |
| data\_venda       | DATE          | NN               |
| valor\_total      | DECIMAL(10,2) | NN               |
| status\_pagamento | VARCHAR(30)   | NN               |

## 11.5 ITEM\_VENDA

| Atributo        | Tipo          | Restrições       |
| --------------- | ------------- | ---------------- |
| id\_item\_venda | INT           | PK               |
| id\_venda       | INT           | FK → VENDA, NN   |
| id\_produto     | INT           | FK → PRODUTO, NN |
| quantidade      | INT           | NN               |
| preco\_unitario | DECIMAL(10,2) | NN               |
| subtotal        | DECIMAL(10,2) | NN               |

## 11.6 PAGAMENTO

| Atributo        | Tipo          | Restrições     |
| --------------- | ------------- | -------------- |
| id\_pagamento   | INT           | PK             |
| id\_venda       | INT           | FK → VENDA, NN |
| data\_pagamento | DATE          | NN             |
| valor\_pago     | DECIMAL(10,2) | NN             |

## 11.7 ENCOMENDA

| Atributo        | Tipo        | Restrições       |
| --------------- | ----------- | ---------------- |
| id\_encomenda   | INT         | PK               |
| id\_cliente     | INT         | FK → CLIENTE, NN |
| id\_produto     | INT         | FK → PRODUTO, NN |
| quantidade      | INT         | NN               |
| data\_encomenda | DATE        | NN               |
| status          | VARCHAR(30) | NN               |

## 11.8 FORNECEDOR

| Atributo       | Tipo         | Restrições |
| -------------- | ------------ | ---------- |
| id\_fornecedor | INT          | PK         |
| nome           | VARCHAR(120) | NN         |
| telefone       | VARCHAR(20)  |            |
| email          | VARCHAR(160) |            |

## 11.9 REPASSE

| Atributo       | Tipo          | Restrições          |
| -------------- | ------------- | ------------------- |
| id\_repasse    | INT           | PK                  |
| id\_fornecedor | INT           | FK → FORNECEDOR, NN |
| valor          | DECIMAL(10,2) | NN                  |
| data\_repasse  | DATE          | NN                  |
| observacao     | VARCHAR(300)  |                     |

## 11.10 Chaves estrangeiras

| Tabela filha | Coluna FK      | Tabela pai |
| ------------ | -------------- | ---------- |
| VENDA        | id\_cliente    | CLIENTE    |
| VENDA        | id\_usuario    | USUARIO    |
| ITEM\_VENDA  | id\_venda      | VENDA      |
| ITEM\_VENDA  | id\_produto    | PRODUTO    |
| PAGAMENTO    | id\_venda      | VENDA      |
| ENCOMENDA    | id\_cliente    | CLIENTE    |
| ENCOMENDA    | id\_produto    | PRODUTO    |
| REPASSE      | id\_fornecedor | FORNECEDOR |
