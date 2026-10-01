# 16 consultas sql

Principais consultas do sistema, com explicação. Os exemplos usam os dados da página [13](/broken/pages/55e092bf4e8f8e952a53dfa106bf384cd96445e1).

## 16.1 Itens de um pedido com produto e subtotal

```sql
SELECT p.nome, i.quantidade, i.preco_unitario, i.subtotal
FROM item_pedido i
JOIN produto p ON p.id_produto = i.id_produto
WHERE i.id_pedido = 1
ORDER BY p.nome;
```

**Para que serve:** montar o comprovante e a tela de detalhes do pedido.

## 16.2 Conferência do total do pedido

```sql
SELECT p.id_pedido, p.valor_total, SUM(i.subtotal) AS soma_itens
FROM pedido p
JOIN item_pedido i ON i.id_pedido = p.id_pedido
GROUP BY p.id_pedido, p.valor_total
HAVING p.valor_total <> SUM(i.subtotal);
```

**Para que serve:** auditar a regra RN01. O resultado esperado é **vazio**.

## 16.3 Faturamento por dia

```sql
SELECT date_trunc('day', data_pedido) AS dia,
       COUNT(*)         AS pedidos,
       SUM(valor_total) AS faturamento
FROM pedido
WHERE status IN ('PAGO', 'ENTREGUE')
GROUP BY dia
ORDER BY dia;
```

**Para que serve:** relatório de vendas por período e base do resumo do Assistente Lilica.

## 16.4 Produtos mais vendidos

```sql
SELECT pr.nome,
       SUM(i.quantidade) AS unidades,
       SUM(i.subtotal)   AS receita
FROM item_pedido i
JOIN pedido  p  ON p.id_pedido  = i.id_pedido
JOIN produto pr ON pr.id_produto = i.id_produto
WHERE p.status <> 'CANCELADO'
GROUP BY pr.nome
ORDER BY unidades DESC
LIMIT 10;
```

**Para que serve:** saber o que mais sai e o que mais rende.

## 16.5 Produtos com estoque baixo

```sql
SELECT nome, estoque_atual, estoque_minimo
FROM produto
WHERE ativo AND estoque_atual <= estoque_minimo
ORDER BY estoque_atual;
```

**Para que serve:** alerta de reposição (RF11).

## 16.6 Desempenho por vendedor

```sql
SELECT u.nome,
       COUNT(p.id_pedido) AS pedidos,
       SUM(p.valor_total) AS total_vendido
FROM pedido p
JOIN usuario u ON u.id_usuario = p.id_usuario
WHERE p.status <> 'CANCELADO'
GROUP BY u.nome
ORDER BY total_vendido DESC;
```

**Para que serve:** acompanhar o resultado de cada vendedor.

## 16.7 Ticket médio

```sql
SELECT ROUND(AVG(valor_total), 2) AS ticket_medio
FROM pedido
WHERE status IN ('PAGO', 'ENTREGUE');
```

**Para que serve:** indicador de quanto, em média, cada venda rende.

## 16.8 Histórico de compras de um cliente

```sql
SELECT p.id_pedido, p.data_pedido, p.status, p.valor_total
FROM pedido p
WHERE p.id_cliente = 1
ORDER BY p.data_pedido DESC;
```

**Para que serve:** ver as compras anteriores do cliente (RF14).

## 16.9 Vendas por forma de pagamento

```sql
SELECT forma, COUNT(*) AS pagamentos, SUM(valor) AS total
FROM pagamento
WHERE status = 'CONFIRMADO'
GROUP BY forma
ORDER BY total DESC;
```

**Para que serve:** entender como os clientes preferem pagar.

## 16.10 Pedidos com pagamento pendente

```sql
SELECT p.id_pedido, c.nome AS cliente, p.valor_total, p.data_pedido
FROM pedido p
LEFT JOIN cliente c ON c.id_cliente = p.id_cliente
WHERE p.status = 'ABERTO'
ORDER BY p.data_pedido;
```

**Para que serve:** cobrança de valores em aberto.

## 16.11 Produtos sem venda nos últimos 30 dias

```sql
SELECT pr.nome, pr.estoque_atual
FROM produto pr
WHERE pr.ativo
  AND NOT EXISTS (
    SELECT 1
    FROM item_pedido i
    JOIN pedido p ON p.id_pedido = i.id_pedido
    WHERE i.id_produto = pr.id_produto
      AND p.status <> 'CANCELADO'
      AND p.data_pedido >= now() - INTERVAL '30 days'
  );
```

**Para que serve:** identificar produtos parados. Este resultado alimenta as sugestões do Assistente Lilica.

{% hint style="warning" %}
🔲 As consultas foram escritas com apoio de IA. Execute no banco real, registre o resultado (com captura de tela e legenda) e corrija o que falhar.
{% endhint %}
