# 10 der

## 10.1 Diagrama

**Figura 01 — Diagrama Entidade-Relacionamento (DER) do Lilica Vendas, em notação pé-de-galinha.**

O diagrama mostra as 9 entidades, seus principais atributos e como se relacionam. O traço simples indica o lado "1" e o pé-de-galinha, o lado "N".

## 10.2 Relacionamentos

| Relacionamento                  | Cardinalidade | Explicação                                                                                |
| ------------------------------- | ------------- | ----------------------------------------------------------------------------------------- |
| CLIENTE — PEDIDO                | 1 : N         | Um cliente faz vários pedidos; cada pedido tem no máximo um cliente (pode ser de balcão). |
| USUARIO — PEDIDO                | 1 : N         | Um vendedor registra vários pedidos; cada pedido tem um vendedor.                         |
| CATEGORIA — PRODUTO             | 1 : N         | Uma categoria reúne vários produtos.                                                      |
| PEDIDO — ITEM\_PEDIDO           | 1 : N         | Um pedido tem um ou mais itens.                                                           |
| PRODUTO — ITEM\_PEDIDO          | 1 : N         | Um produto aparece em itens de vários pedidos.                                            |
| PEDIDO — PAGAMENTO              | 1 : N         | Um pedido pode ser pago em mais de um pagamento (ex.: parte em dinheiro, parte em PIX).   |
| PRODUTO — MOVIMENTACAO\_ESTOQUE | 1 : N         | Cada produto tem seu histórico de movimentações.                                          |
| PEDIDO — MOVIMENTACAO\_ESTOQUE  | 1 : N         | Vendas e cancelamentos geram movimentações ligadas ao pedido.                             |
| USUARIO — REGISTRO\_USO\_IA     | 1 : N         | Cada usuário pode consultar o assistente várias vezes.                                    |

## 10.3 Como ler o diagrama

* O fluxo principal é **CLIENTE / USUARIO → PEDIDO → ITEM\_PEDIDO ← PRODUTO**.
* **PAGAMENTO** e **MOVIMENTACAO\_ESTOQUE** derivam do pedido.
* **CATEGORIA** organiza o catálogo de produtos.

🔲 Se o modelo mudar, **substituir a imagem** e registrar a mudança em [09. Modelagem de dados](/broken/pages/b31218f7367387bf70d87d4f005e1730fc311c94).
