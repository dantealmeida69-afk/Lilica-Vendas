# 09 modelagem de dados

## 9.1 Visão geral

A modelagem parte dos requisitos e das regras de negócio e evolui em três níveis:

**Conceitual (entidades e relacionamentos) → Lógico (tabelas, PKs, FKs) → Físico (SQL no SGBD)**

## 9.2 Entidades identificadas

| Entidade              | Papel no sistema                                                           |
| --------------------- | -------------------------------------------------------------------------- |
| USUARIO               | Pessoa que acessa o sistema (administrador ou vendedor).                   |
| CLIENTE               | Pessoa que compra.                                                         |
| CATEGORIA             | Agrupamento de produtos.                                                   |
| PRODUTO               | Item à venda, com preço e controle de estoque.                             |
| PEDIDO                | Uma venda: quem comprou, quem vendeu, quando e o total.                    |
| ITEM\_PEDIDO          | Cada produto dentro de um pedido, com quantidade e preço na hora da venda. |
| PAGAMENTO             | Forma e valor pagos de um pedido.                                          |
| MOVIMENTACAO\_ESTOQUE | Histórico de entradas, saídas e estornos de cada produto.                  |
| REGISTRO\_USO\_IA     | Registro de cada chamada ao Assistente Lilica.                             |

## 9.3 Decisões de modelagem

* **Preço congelado na venda:** `item_pedido.preco_unitario` guarda o preço da hora, preservando o histórico.
* **Um pedido, vários itens:** a relação PEDIDO ↔ PRODUTO é muitos-para-muitos e é resolvida pela tabela `item_pedido`.
* **Estoque com histórico:** além do saldo em `produto`, cada mudança fica em `movimentacao_estoque`, permitindo auditoria.
* **Inativar em vez de excluir:** produtos vendidos permanecem no banco.
* **Venda de balcão:** `pedido.id_cliente` é opcional.
* **Valores monetários** em `NUMERIC(10,2)`, nunca em ponto flutuante.

## 9.4 Evolução da modelagem

_Não apagar versões anteriores. Registrar cada mudança._

| Versão | Data       | O que mudou                                                | Motivo                                  | Responsável |
| ------ | ---------- | ---------------------------------------------------------- | --------------------------------------- | ----------- |
| v0.1   | 28/09/2026 | Primeira proposta com 9 entidades, gerada com apoio de IA. | Ponto de partida para revisão do grupo. | 🔲          |
| v0.2   | 🔲         | 🔲                                                         | 🔲                                      | 🔲          |

{% hint style="warning" %}
🔲 A v0.1 é uma **proposta** baseada em uma suposição sobre o negócio. O grupo deve revisar as entidades e registrar as alterações na tabela acima.
{% endhint %}
