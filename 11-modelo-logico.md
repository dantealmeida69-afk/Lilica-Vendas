# 11 modelo logico

Legenda: **PK** = chave primária · **FK** = chave estrangeira · **NN** = não nulo · **UQ** = único

## 11.1 usuario

| Atributo       | Tipo         | Restrições             |
| -------------- | ------------ | ---------------------- |
| id\_usuario    | BIGINT       | PK                     |
| nome           | VARCHAR(120) | NN                     |
| email          | VARCHAR(160) | NN, UQ                 |
| senha\_hash    | VARCHAR(255) | NN                     |
| perfil         | VARCHAR(10)  | NN; ADMIN ou VENDEDOR  |
| ativo          | BOOLEAN      | NN, padrão: verdadeiro |
| data\_cadastro | TIMESTAMPTZ  | NN                     |

## 11.2 cliente

| Atributo       | Tipo         | Restrições |
| -------------- | ------------ | ---------- |
| id\_cliente    | BIGINT       | PK         |
| nome           | VARCHAR(120) | NN         |
| telefone       | VARCHAR(20)  |            |
| email          | VARCHAR(160) |            |
| data\_cadastro | TIMESTAMPTZ  | NN         |

## 11.3 categoria

| Atributo      | Tipo        | Restrições |
| ------------- | ----------- | ---------- |
| id\_categoria | BIGINT      | PK         |
| nome          | VARCHAR(80) | NN, UQ     |

## 11.4 produto

| Atributo        | Tipo          | Restrições             |
| --------------- | ------------- | ---------------------- |
| id\_produto     | BIGINT        | PK                     |
| id\_categoria   | BIGINT        | FK → categoria, NN     |
| nome            | VARCHAR(120)  | NN                     |
| descricao       | TEXT          |                        |
| preco\_venda    | NUMERIC(10,2) | NN, ≥ 0                |
| estoque\_atual  | INTEGER       | NN, ≥ 0                |
| estoque\_minimo | INTEGER       | NN, ≥ 0                |
| ativo           | BOOLEAN       | NN, padrão: verdadeiro |

## 11.5 pedido

| Atributo     | Tipo          | Restrições                               |
| ------------ | ------------- | ---------------------------------------- |
| id\_pedido   | BIGINT        | PK                                       |
| id\_cliente  | BIGINT        | FK → cliente (opcional: venda de balcão) |
| id\_usuario  | BIGINT        | FK → usuario, NN                         |
| data\_pedido | TIMESTAMPTZ   | NN                                       |
| status       | VARCHAR(10)   | NN; ABERTO, PAGO, ENTREGUE ou CANCELADO  |
| valor\_total | NUMERIC(12,2) | NN, ≥ 0                                  |
| observacao   | VARCHAR(300)  |                                          |

## 11.6 item\_pedido

| Atributo        | Tipo          | Restrições                                |
| --------------- | ------------- | ----------------------------------------- |
| id\_item        | BIGINT        | PK                                        |
| id\_pedido      | BIGINT        | FK → pedido, NN                           |
| id\_produto     | BIGINT        | FK → produto, NN; UQ junto com id\_pedido |
| quantidade      | INTEGER       | NN, > 0                                   |
| preco\_unitario | NUMERIC(10,2) | NN, ≥ 0                                   |
| subtotal        | NUMERIC(12,2) | NN; = quantidade × preco\_unitario        |

## 11.7 pagamento

| Atributo        | Tipo          | Restrições                                  |
| --------------- | ------------- | ------------------------------------------- |
| id\_pagamento   | BIGINT        | PK                                          |
| id\_pedido      | BIGINT        | FK → pedido, NN                             |
| forma           | VARCHAR(10)   | NN; PIX, DINHEIRO, CREDITO, DEBITO ou OUTRO |
| valor           | NUMERIC(12,2) | NN, > 0                                     |
| status          | VARCHAR(10)   | NN; PENDENTE, CONFIRMADO ou ESTORNADO       |
| data\_pagamento | TIMESTAMPTZ   | NN                                          |

## 11.8 movimentacao\_estoque

| Atributo           | Tipo         | Restrições                           |
| ------------------ | ------------ | ------------------------------------ |
| id\_movimentacao   | BIGINT       | PK                                   |
| id\_produto        | BIGINT       | FK → produto, NN                     |
| id\_pedido         | BIGINT       | FK → pedido (opcional)               |
| tipo               | VARCHAR(10)  | NN; ENTRADA, SAIDA, ESTORNO ou PERDA |
| quantidade         | INTEGER      | NN, > 0                              |
| motivo             | VARCHAR(200) |                                      |
| data\_movimentacao | TIMESTAMPTZ  | NN                                   |

ENTRADA e ESTORNO **somam** ao estoque; SAIDA e PERDA **subtraem**.

## 11.9 registro\_uso\_ia

| Atributo       | Tipo        | Restrições                                       |
| -------------- | ----------- | ------------------------------------------------ |
| id\_registro   | BIGINT      | PK                                               |
| id\_usuario    | BIGINT      | FK → usuario (opcional)                          |
| funcionalidade | VARCHAR(20) | NN; RESUMO\_VENDAS, SUGESTAO\_REPOSICAO ou OUTRA |
| modelo         | VARCHAR(60) | NN                                               |
| tokens         | INTEGER     | NN, ≥ 0                                          |
| data\_chamada  | TIMESTAMPTZ | NN                                               |

## 11.10 Chaves estrangeiras

| Tabela filha          | Coluna FK     | Tabela pai |
| --------------------- | ------------- | ---------- |
| produto               | id\_categoria | categoria  |
| pedido                | id\_cliente   | cliente    |
| pedido                | id\_usuario   | usuario    |
| item\_pedido          | id\_pedido    | pedido     |
| item\_pedido          | id\_produto   | produto    |
| pagamento             | id\_pedido    | pedido     |
| movimentacao\_estoque | id\_produto   | produto    |
| movimentacao\_estoque | id\_pedido    | pedido     |
| registro\_uso\_ia     | id\_usuario   | usuario    |
