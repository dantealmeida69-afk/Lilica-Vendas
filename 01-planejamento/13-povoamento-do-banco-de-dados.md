# 13 povoamento do banco de dados

## 13.1 Objetivo

Inserir dados de demonstração para permitir a execução das consultas e dos testes definidos no projeto.

## 13.2 Script de povoamento

```sql
INSERT INTO usuario (id_usuario, nome, email, senha) VALUES
(1, 'Administrador Teste', 'admin@exemplo.com', 'HASH_FICTICIO_1'),
(2, 'Vendedor Teste', 'vendedor@exemplo.com', 'HASH_FICTICIO_2');

INSERT INTO cliente (id_cliente, nome, celular, email, observacoes) VALUES
(1, 'Cliente Teste 01', '(31) 90000-0001', 'cliente01@exemplo.com', 'Cliente recorrente'),
(2, 'Cliente Teste 02', '(31) 90000-0002', 'cliente02@exemplo.com', 'Primeira compra');

INSERT INTO produto (id_produto, nome, valor, descricao) VALUES
(1, 'Camiseta básica', 49.90, 'Camiseta básica'),
(2, 'Caneca personalizada', 29.90, 'Caneca personalizada'),
(3, 'Boné', 39.90, 'Boné'),
(4, 'Chaveiro', 9.90, 'Chaveiro');

INSERT INTO fornecedor (id_fornecedor, nome, telefone, email) VALUES
(1, 'Fornecedor Teste 01', '(31) 98888-0001', 'fornecedor01@exemplo.com'),
(2, 'Fornecedor Teste 02', '(31) 98888-0002', 'fornecedor02@exemplo.com');

INSERT INTO venda
(id_venda, id_cliente, id_usuario, data_venda, valor_total, status_pagamento)
VALUES
(1, 1, 2, '2026-09-28', 129.70, 'PAGO'),
(2, 2, 2, '2026-09-29', 69.60, 'PENDENTE');

INSERT INTO item_venda
(id_item_venda, id_venda, id_produto, quantidade, preco_unitario, subtotal)
VALUES
(1, 1, 1, 2, 49.90, 99.80),
(2, 1, 2, 1, 29.90, 29.90),
(3, 2, 3, 1, 39.90, 39.90),
(4, 2, 4, 3, 9.90, 29.70);

INSERT INTO pagamento
(id_pagamento, id_venda, data_pagamento, valor_pago)
VALUES
(1, 1, '2026-09-28', 129.70),
(2, 2, '2026-09-29', 30.00);

INSERT INTO encomenda
(id_encomenda, id_cliente, id_produto, quantidade, data_encomenda, status)
VALUES
(1, 1, 2, 2, '2026-09-29', 'PENDENTE'),
(2, 2, 1, 1, '2026-09-30', 'EM_PRODUCAO');

INSERT INTO repasse
(id_repasse, id_fornecedor, valor, data_repasse, observacao)
VALUES
(1, 1, 150.00, '2026-09-29', 'Repasse referente às compras da semana'),
(2, 2, 75.00, '2026-09-30', 'Repasse de produtos personalizados');
```

## 13.3 Volume de dados

| Tabela      | Registros de demonstração |
| ----------- | ------------------------: |
| usuario     |                         2 |
| cliente     |                         2 |
| produto     |                         4 |
| venda       |                         2 |
| item\_venda |                         4 |
| pagamento   |                         2 |
| encomenda   |                         2 |
| fornecedor  |                         2 |
| repasse     |                         2 |
