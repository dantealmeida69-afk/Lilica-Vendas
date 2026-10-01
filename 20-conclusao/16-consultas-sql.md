# 16 consultas sql

As consultas abaixo foram ajustadas para as tabelas definidas na Entrega 2.

## 16.1 Itens de uma venda

```sql
SELECT p.nome, i.quantidade, i.preco_unitario, i.subtotal
FROM item_venda i
JOIN produto p ON p.id_produto = i.id_produto
WHERE i.id_venda = 1
ORDER BY p.nome;
```

## 16.2 Conferência do total da venda

```sql
SELECT v.id_venda,
       v.valor_total,
       SUM(i.subtotal) AS soma_itens
FROM venda v
JOIN item_venda i ON i.id_venda = v.id_venda
GROUP BY v.id_venda, v.valor_total
HAVING v.valor_total <> SUM(i.subtotal);
```

**Resultado esperado:** nenhuma linha quando os dados estiverem consistentes.

## 16.3 Vendas por data

```sql
SELECT data_venda,
       COUNT(*) AS vendas,
       SUM(valor_total) AS faturamento
FROM venda
GROUP BY data_venda
ORDER BY data_venda;
```

## 16.4 Produtos mais vendidos

```sql
SELECT p.nome,
       SUM(i.quantidade) AS unidades,
       SUM(i.subtotal) AS receita
FROM item_venda i
JOIN venda v ON v.id_venda = i.id_venda
JOIN produto p ON p.id_produto = i.id_produto
GROUP BY p.nome
ORDER BY unidades DESC;
```

## 16.5 Histórico de compras de um cliente

```sql
SELECT v.id_venda,
       v.data_venda,
       v.valor_total,
       v.status_pagamento
FROM venda v
WHERE v.id_cliente = 1
ORDER BY v.data_venda DESC;
```

## 16.6 Pagamentos de uma venda

```sql
SELECT v.id_venda,
       v.valor_total,
       COALESCE(SUM(p.valor_pago), 0) AS total_pago,
       v.valor_total - COALESCE(SUM(p.valor_pago), 0) AS saldo
FROM venda v
LEFT JOIN pagamento p ON p.id_venda = v.id_venda
WHERE v.id_venda = 1
GROUP BY v.id_venda, v.valor_total;
```

## 16.7 Encomendas pendentes

```sql
SELECT e.id_encomenda,
       c.nome AS cliente,
       p.nome AS produto,
       e.quantidade,
       e.data_encomenda,
       e.status
FROM encomenda e
JOIN cliente c ON c.id_cliente = e.id_cliente
JOIN produto p ON p.id_produto = e.id_produto
WHERE e.status <> 'CONCLUIDA'
ORDER BY e.data_encomenda;
```

## 16.8 Repasses por fornecedor

```sql
SELECT f.nome,
       COUNT(r.id_repasse) AS quantidade_repasses,
       SUM(r.valor) AS total_repassado
FROM repasse r
JOIN fornecedor f ON f.id_fornecedor = r.id_fornecedor
GROUP BY f.nome
ORDER BY total_repassado DESC;
```

## 16.9 Vendas por usuário

```sql
SELECT u.nome,
       COUNT(v.id_venda) AS quantidade_vendas,
       SUM(v.valor_total) AS total_vendido
FROM venda v
JOIN usuario u ON u.id_usuario = v.id_usuario
GROUP BY u.nome
ORDER BY total_vendido DESC;
```

## 16.10 Vendas com pagamento pendente

```sql
SELECT v.id_venda,
       c.nome AS cliente,
       v.valor_total,
       COALESCE(SUM(p.valor_pago), 0) AS total_pago,
       v.valor_total - COALESCE(SUM(p.valor_pago), 0) AS saldo
FROM venda v
JOIN cliente c ON c.id_cliente = v.id_cliente
LEFT JOIN pagamento p ON p.id_venda = v.id_venda
GROUP BY v.id_venda, c.nome, v.valor_total
HAVING COALESCE(SUM(p.valor_pago), 0) < v.valor_total;
```
