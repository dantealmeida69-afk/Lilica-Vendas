# 17 testes

Os testes foram reorganizados para validar diretamente a modelagem apresentada na Entrega 2.

Resultados possíveis: **OK**, **Erro**, **Parcial** ou **Pendente**.

> Os resultados permanecem como **Pendente** até que os testes sejam executados no banco/sistema real. Não foram inventados resultados.

## 17.1 Testes funcionais

| ID  | Teste                                                   | Resultado | Problema | Correção |
| --- | ------------------------------------------------------- | --------- | -------- | -------- |
| T01 | Cadastrar usuário com nome, e-mail e senha/hash válidos | Pendente  | —        | —        |
| T02 | Impedir cadastro de usuário com e-mail duplicado        | Pendente  | —        | —        |
| T03 | Cadastrar cliente válido                                | Pendente  | —        | —        |
| T04 | Cadastrar produto com valor válido                      | Pendente  | —        | —        |
| T05 | Impedir produto com valor negativo                      | Pendente  | —        | —        |
| T06 | Registrar venda vinculada a cliente e usuário           | Pendente  | —        | —        |
| T07 | Registrar venda com vários itens                        | Pendente  | —        | —        |
| T08 | Calcular subtotal como quantidade × preço unitário      | Pendente  | —        | —        |
| T09 | Calcular valor total da venda pela soma dos subtotais   | Pendente  | —        | —        |
| T10 | Registrar pagamento vinculado à venda                   | Pendente  | —        | —        |
| T11 | Registrar mais de um pagamento para a mesma venda       | Pendente  | —        | —        |
| T12 | Consultar saldo pendente de uma venda                   | Pendente  | —        | —        |
| T13 | Cadastrar encomenda vinculando cliente e produto        | Pendente  | —        | —        |
| T14 | Alterar status de uma encomenda                         | Pendente  | —        | —        |
| T15 | Cadastrar fornecedor                                    | Pendente  | —        | —        |
| T16 | Registrar repasse para fornecedor existente             | Pendente  | —        | —        |

## 17.2 Testes de banco de dados

| ID  | Teste                                                          | Resultado | Problema | Correção |
| --- | -------------------------------------------------------------- | --------- | -------- | -------- |
| T17 | Criação das nove tabelas sem erro                              | Pendente  | —        | —        |
| T18 | FK de venda para cliente rejeita cliente inexistente           | Pendente  | —        | —        |
| T19 | FK de venda para usuário rejeita usuário inexistente           | Pendente  | —        | —        |
| T20 | FK de item\_venda para venda rejeita venda inexistente         | Pendente  | —        | —        |
| T21 | FK de item\_venda para produto rejeita produto inexistente     | Pendente  | —        | —        |
| T22 | FK de pagamento para venda rejeita venda inexistente           | Pendente  | —        | —        |
| T23 | FK de encomenda para cliente e produto funciona                | Pendente  | —        | —        |
| T24 | FK de repasse para fornecedor rejeita fornecedor inexistente   | Pendente  | —        | —        |
| T25 | Quantidade zero em item\_venda é rejeitada                     | Pendente  | —        | —        |
| T26 | Quantidade negativa em encomenda é rejeitada                   | Pendente  | —        | —        |
| T27 | Valor negativo de produto é rejeitado                          | Pendente  | —        | —        |
| T28 | Valor negativo de pagamento é rejeitado                        | Pendente  | —        | —        |
| T29 | Subtotal diferente de quantidade × preço\_unitario é rejeitado | Pendente  | —        | —        |
| T30 | E-mail de usuário duplicado é rejeitado                        | Pendente  | —        | —        |
| T31 | Consultas da página 16 retornam resultados coerentes           | Pendente  | —        | —        |

## 17.3 Testes de integridade dos relacionamentos

| ID  | Teste                                         | Resultado | Problema | Correção |
| --- | --------------------------------------------- | --------- | -------- | -------- |
| T32 | Uma venda pode possuir vários itens           | Pendente  | —        | —        |
| T33 | Um produto pode aparecer em várias vendas     | Pendente  | —        | —        |
| T34 | Uma venda pode possuir vários pagamentos      | Pendente  | —        | —        |
| T35 | Um cliente pode possuir várias encomendas     | Pendente  | —        | —        |
| T36 | Um produto pode aparecer em várias encomendas | Pendente  | —        | —        |
| T37 | Um fornecedor pode possuir vários repasses    | Pendente  | —        | —        |

## 17.4 Testes de regras de negócio

| ID  | Teste                                                                                   | Resultado | Problema | Correção |
| --- | --------------------------------------------------------------------------------------- | --------- | -------- | -------- |
| T38 | Toda venda possui cliente e usuário responsável                                         | Pendente  | —        | —        |
| T39 | Todo item de venda possui venda e produto                                               | Pendente  | —        | —        |
| T40 | Todo pagamento possui venda                                                             | Pendente  | —        | —        |
| T41 | Toda encomenda possui cliente e produto                                                 | Pendente  | —        | —        |
| T42 | Todo repasse possui fornecedor                                                          | Pendente  | —        | —        |
| T43 | Alteração do valor do produto não altera o preço\_unitario já registrado em item\_venda | Pendente  | —        | —        |

## 17.5 Testes de consultas e relatórios

| ID  | Teste                                                                             | Resultado | Problema | Correção |
| --- | --------------------------------------------------------------------------------- | --------- | -------- | -------- |
| T44 | Consulta de itens de uma venda retorna produtos, quantidades e subtotais corretos | Pendente  | —        | —        |
| T45 | Consulta de conferência do total não retorna divergências                         | Pendente  | —        | —        |
| T46 | Consulta de vendas por data apresenta faturamento correto                         | Pendente  | —        | —        |
| T47 | Consulta de produtos mais vendidos apresenta quantidades corretas                 | Pendente  | —        | —        |
| T48 | Consulta de pagamentos apresenta total pago e saldo corretos                      | Pendente  | —        | —        |
| T49 | Consulta de encomendas pendentes retorna apenas encomendas não concluídas         | Pendente  | —        | —        |
| T50 | Consulta de repasses apresenta total por fornecedor                               | Pendente  | —        | —        |

## 17.6 Registro de execução

| Data | Teste executado | Resultado | Evidência | Observação |
| ---- | --------------- | --------- | --------- | ---------- |
| —    | —               | —         | —         | —          |

## 17.7 Resumo

| Situação | Quantidade |
| -------- | ---------: |
| OK       |          0 |
| Parcial  |          0 |
| Erro     |          0 |
| Pendente |         50 |

> Após a execução real, atualizar o resumo e registrar os problemas encontrados. O PDF exige que erros sejam documentados e corrigidos, e não ocultados.
