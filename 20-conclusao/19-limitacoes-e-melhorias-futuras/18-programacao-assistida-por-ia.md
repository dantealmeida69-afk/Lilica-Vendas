# 18 programacao assistida por ia

> **Não escrevam apenas "usamos IA".** Esta página mostra **como** o grupo trabalhou com IA.

Para cada uso importante, registre:

1. **O que pedimos à IA?**
2. **O que ela produziu?**
3. **O que estava errado?**
4. **Como corrigimos?**
5. **Qual foi o resultado?**
6. **Onde a IA entrou na solução?**

## 18.1 A IA no sistema: Assistente Lilica

O Assistente Lilica transforma números em texto simples para o dono do negócio.

| Função                | O que faz                                                                       | Dados usados                 |
| --------------------- | ------------------------------------------------------------------------------- | ---------------------------- |
| Resumo de vendas      | Descreve o período: faturamento, pedidos, produtos que mais saíram e variações. | Totais e rankings agregados  |
| Sugestão de reposição | Aponta produtos com estoque baixo ou com muita saída.                           | Estoque e vendas por produto |
| Sugestão de ação      | Indica produtos parados que poderiam entrar em promoção.                        | Produtos sem venda recente   |

### Como funciona

1. O servidor executa consultas de agregação no banco (ver [16. Consultas SQL](/broken/pages/5d01e3365679db32c386f71e0cb4df44ca7a688c)).
2. Monta um texto com os números, **sem dados pessoais de clientes**.
3. Envia ao modelo de IA com instruções (prompt) restritivas.
4. Recebe o texto e o exibe, identificado como _"Sugestão gerada com auxílio de Inteligência Artificial"_.
5. Registra a chamada em `registro_uso_ia`.

### Cuidados

* a IA **sugere**, o gestor decide;
* os números do texto devem bater com os relatórios (a IA pode errar cálculos);
* o prompt orienta a IA a usar só os dados fornecidos e a não inventar informações;
* nenhum dado pessoal é enviado.

## 18.2 A IA no desenvolvimento

| Etapa          | Uso da IA                                                            | Cuidado                                     |
| -------------- | -------------------------------------------------------------------- | ------------------------------------------- |
| Requisitos     | Levantamento de requisitos, regras de negócio e histórias de usuário | Revisão do grupo                            |
| Banco de dados | Proposta de modelo, scripts SQL e consultas                          | Executar e validar no SGBD real             |
| Código         | Geração e correção de código                                         | Revisão humana, principalmente em segurança |
| Testes         | Casos de teste e dados fictícios                                     | Conferir se refletem situações reais        |
| Design         | Ideias de layout e fluxos                                            | Checar acessibilidade                       |
| Prompts        | Testes iterativos do Assistente Lilica                               | Registrar cada versão                       |

## 18.3 Registro do uso da IA

_Registrar cada uso importante. Não apagar entradas antigas._

| Data       | IA                 | O que pedimos                                                                                                              | Resultado                                                                                            | Problema                                                                                                                        | Correção                                                                        |
| ---------- | ------------------ | -------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------- |
| 28/09/2026 | Claude (Anthropic) | Montar do zero o GitBook do Lilica Vendas com as 21 seções do roteiro, usando outro GitBook do grupo como modelo de estilo | 21 páginas com requisitos, regras de negócio, modelo de dados, DER, DDL, consultas e plano de testes | O conceito do sistema foi **suposto** (gestão de vendas para pequeno comércio); SQL não executado; catálogo de exemplo genérico | Itens a confirmar marcados com 🔲; SQL a validar no SGBD; catálogo a substituir |
| 🔲         | 🔲                 | 🔲                                                                                                                         | 🔲                                                                                                   | 🔲                                                                                                                              | 🔲                                                                              |
| 🔲         | 🔲                 | 🔲                                                                                                                         | 🔲                                                                                                   | 🔲                                                                                                                              | 🔲                                                                              |

## 18.4 Evolução dos prompts do Assistente Lilica

| Versão | Data | Regra principal do prompt | Problema encontrado | Ajuste |
| ------ | ---- | ------------------------- | ------------------- | ------ |
| p-0.1  | 🔲   | 🔲                        | 🔲                  | 🔲     |
| p-0.2  | 🔲   | 🔲                        | 🔲                  | 🔲     |
