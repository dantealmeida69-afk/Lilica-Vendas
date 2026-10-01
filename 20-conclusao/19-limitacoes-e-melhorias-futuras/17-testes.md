# 17 testes

{% hint style="danger" %}
**Não escondam os erros.** Eles fazem parte da documentação do desenvolvimento. Registre o que falhou, o problema e a correção.
{% endhint %}

Resultados possíveis: **OK**, **Erro**, **Parcial** ou **Pendente**.

## 17.1 Testes funcionais

| ID  | Teste                                                     | Resultado | Problema | Correção |
| --- | --------------------------------------------------------- | --------- | -------- | -------- |
| T01 | Login com dados corretos e incorretos                     | Pendente  | —        | —        |
| T02 | Vendedor tenta acessar tela de administrador (deve negar) | Pendente  | —        | —        |
| T03 | Cadastro de produto válido                                | Pendente  | —        | —        |
| T04 | Cadastro de produto com preço negativo (deve recusar)     | Pendente  | —        | —        |
| T05 | Cadastro de cliente                                       | Pendente  | —        | —        |
| T06 | Venda com um item                                         | Pendente  | —        | —        |
| T07 | Venda com vários itens: total correto                     | Pendente  | —        | —        |
| T08 | Venda de balcão sem cliente                               | Pendente  | —        | —        |
| T09 | Venda acima do estoque (deve bloquear)                    | Pendente  | —        | —        |
| T10 | Estoque baixado após a venda                              | Pendente  | —        | —        |
| T11 | Cancelamento devolve o estoque                            | Pendente  | —        | —        |
| T12 | Pagamento parcial e total                                 | Pendente  | —        | —        |
| T13 | Entrada de estoque (reposição)                            | Pendente  | —        | —        |
| T14 | Alerta de estoque baixo                                   | Pendente  | —        | —        |
| T15 | Relatórios batem com os dados do banco                    | Pendente  | —        | —        |

## 17.2 Testes de banco de dados

| ID  | Teste                                          | Resultado | Problema | Correção |
| --- | ---------------------------------------------- | --------- | -------- | -------- |
| T16 | Criação das tabelas sem erro                   | Pendente  | —        | —        |
| T17 | Estoque negativo é rejeitado                   | Pendente  | —        | —        |
| T18 | Item com quantidade zero é rejeitado           | Pendente  | —        | —        |
| T19 | Subtotal incorreto é rejeitado                 | Pendente  | —        | —        |
| T20 | Produto repetido no mesmo pedido é rejeitado   | Pendente  | —        | —        |
| T21 | E-mail de usuário duplicado é rejeitado        | Pendente  | —        | —        |
| T22 | Falha no meio da venda desfaz tudo (transação) | Pendente  | —        | —        |
| T23 | Consultas da página 16 retornam o esperado     | Pendente  | —        | —        |

## 17.3 Testes do Assistente Lilica (IA)

| ID  | Teste                                           | Resultado | Problema | Correção |
| --- | ----------------------------------------------- | --------- | -------- | -------- |
| T24 | Resumo do período confere com os relatórios     | Pendente  | —        | —        |
| T25 | Nenhum dado pessoal de cliente é enviado à IA   | Pendente  | —        | —        |
| T26 | Texto da IA vem identificado como gerado por IA | Pendente  | —        | —        |
| T27 | Sugestão de reposição coerente com o estoque    | Pendente  | —        | —        |
| T28 | Comportamento com período sem vendas            | Pendente  | —        | —        |

## 17.4 Testes de usabilidade e acessibilidade

| ID  | Teste                          | Resultado | Problema | Correção |
| --- | ------------------------------ | --------- | -------- | -------- |
| T29 | Concluir uma venda sem ajuda   | Pendente  | —        | —        |
| T30 | Uso no celular e no computador | Pendente  | —        | —        |
| T31 | Contraste e tamanho de letra   | Pendente  | —        | —        |

## 17.5 Validação com usuários

🔲 **RT04:** registrar quem testou, quando, o que foi observado e o que mudou.

| Data | Participante (perfil) | O que testou | Feedback | Ação tomada |
| ---- | --------------------- | ------------ | -------- | ----------- |
| 🔲   | 🔲                    | 🔲           | 🔲       | 🔲          |

## 17.6 Resumo

| Situação | Quantidade |
| -------- | ---------- |
| OK       | 0          |
| Parcial  | 0          |
| Erro     | 0          |
| Pendente | 31         |
