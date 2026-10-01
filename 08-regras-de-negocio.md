# 08 regras de negocio

Regras que devem ser respeitadas **pelo sistema e pelo Banco de Dados**.

## 8.1 Regras do negócio

| ID   | Regra                                                                                                                         | Onde é garantida                                  |
| ---- | ----------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------- |
| RN01 | O total do pedido é a soma dos subtotais dos itens.                                                                           | Aplicação + conferência por consulta              |
| RN02 | O subtotal do item é `quantidade × preço unitário`.                                                                           | `CHECK` em `item_pedido`                          |
| RN03 | O preço unitário do item **fica registrado no momento da venda**; mudar o preço do produto depois não altera pedidos antigos. | Coluna `preco_unitario` em `item_pedido`          |
| RN04 | Não é possível vender mais do que o estoque disponível; o estoque nunca fica negativo.                                        | `CHECK (estoque_atual >= 0)` + validação na venda |
| RN05 | Toda entrada ou saída de estoque gera um registro de movimentação.                                                            | Tabela `movimentacao_estoque`                     |
| RN06 | Cancelar um pedido devolve os itens ao estoque (movimentação do tipo ESTORNO).                                                | Aplicação (transação)                             |
| RN07 | Um produto que já foi vendido **não é excluído**, apenas inativado.                                                           | `FK` sem exclusão em cascata + campo `ativo`      |
| RN08 | A quantidade vendida deve ser maior que zero e o preço não pode ser negativo.                                                 | `CHECK` em `item_pedido` e `produto`              |
| RN09 | Um produto aparece uma única vez em cada pedido.                                                                              | `UNIQUE (id_pedido, id_produto)`                  |
| RN10 | Um pedido só é marcado como PAGO quando a soma dos pagamentos confirmados cobre o total.                                      | Aplicação                                         |
| RN11 | O pedido pode ser de balcão, sem cliente cadastrado.                                                                          | `id_cliente` opcional em `pedido`                 |
| RN12 | Todo pedido tem um vendedor responsável.                                                                                      | `id_usuario` obrigatório em `pedido`              |
| RN13 | Somente o Administrador altera preços, inativa produtos e gerencia usuários.                                                  | Controle de acesso na aplicação                   |
| RN14 | O e-mail de cada usuário é único.                                                                                             | `UNIQUE` em `usuario.email`                       |
| RN15 | Produtos com estoque igual ou abaixo do mínimo entram no alerta de reposição.                                                 | Consulta de estoque baixo                         |
| RN16 | A IA recebe apenas dados agregados e suas respostas são sugestões, não decisões.                                              | Camada de integração com a IA                     |

## 8.2 Privacidade e segurança (LGPD)

* Os dados dos clientes (nome, telefone, e-mail) são **dados pessoais** e só devem ser coletados quando necessários para a venda.
* O acesso é restrito por login e perfil.
* Senhas são gravadas apenas como **hash**.



## 8.3 Ética no uso da IA

* A IA **sugere**; quem decide é o gestor.
* Todo texto gerado por IA é identificado como tal.
* As respostas são conferidas com os dados reais antes de serem usadas (a IA pode errar).
