# 10 der

## 10.1 Diagrama e estrutura

O DER deve representar as nove entidades definidas na Entrega 2 e suas cardinalidades:

```
CLIENTE 1 ─── N VENDA
USUARIO 1 ─── N VENDA

VENDA 1 ─── N ITEM_VENDA
PRODUTO 1 ─── N ITEM_VENDA

VENDA 1 ─── N PAGAMENTO

CLIENTE 1 ─── N ENCOMENDA
PRODUTO 1 ─── N ENCOMENDA

FORNECEDOR 1 ─── N REPASSE
```

## 10.2 Relacionamentos

| Relacionamento        | Cardinalidade | Explicação                                                                  |
| --------------------- | ------------: | --------------------------------------------------------------------------- |
| CLIENTE — VENDA       |         1 : N | Um cliente pode realizar várias compras e cada venda pertence a um cliente. |
| USUARIO — VENDA       |         1 : N | Um usuário pode registrar várias vendas e cada venda possui um responsável. |
| VENDA — ITEM\_VENDA   |         1 : N | Uma venda pode possuir vários itens e cada item pertence a uma venda.       |
| PRODUTO — ITEM\_VENDA |         1 : N | Um produto pode aparecer em vários itens de venda.                          |
| VENDA — PAGAMENTO     |         1 : N | Uma venda pode receber vários pagamentos.                                   |
| CLIENTE — ENCOMENDA   |         1 : N | Um cliente pode solicitar várias encomendas.                                |
| PRODUTO — ENCOMENDA   |         1 : N | Um produto pode aparecer em várias encomendas.                              |
| FORNECEDOR — REPASSE  |         1 : N | Um fornecedor pode receber vários repasses.                                 |

## 10.3 Fluxo principal

O fluxo principal da venda é:

**CLIENTE / USUARIO → VENDA → ITEM\_VENDA ← PRODUTO**

Os pagamentos ficam ligados à VENDA.

As encomendas relacionam CLIENTE e PRODUTO.

Os repasses relacionam FORNECEDOR e REPASSE.

## 10.4 Observação para a imagem do DER

A imagem do DER existente no projeto deve ser substituída por uma versão que contenha somente as nove entidades da Entrega 2. Não devem permanecer CATEGORIA, PEDIDO, MOVIMENTACAO\_ESTOQUE ou REGISTRO\_USO\_IA no diagrama desta entrega.
