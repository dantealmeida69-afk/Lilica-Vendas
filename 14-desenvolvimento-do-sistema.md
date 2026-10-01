# 14 desenvolvimento do sistema

## 14.1 Descrição da aplicação

Aplicação **web responsiva** para registrar vendas, controlar estoque, acompanhar pagamentos e consultar relatórios, com o **Assistente Lilica** (IA) para resumos e sugestões.

## 14.2 Principais funcionalidades

* **Registro de venda:** escolha do cliente, adição de produtos, cálculo automático do total e forma de pagamento.
* **Estoque automático:** baixa a cada venda, devolução em cancelamentos e alerta de estoque baixo.
* **Cadastros:** produtos, categorias, clientes e usuários.
* **Relatórios:** vendas por período, produtos mais vendidos, desempenho por vendedor e ticket médio.
* **Assistente Lilica:** resumo do período em linguagem simples e sugestões de reposição e de ação.
* **Perfis de acesso:** administrador e vendedor.

## 14.3 Tecnologias e ferramentas

🔲 **Proposta.** O grupo deve confirmar cada item.

| Categoria                 | Ferramenta / Tecnologia   | Justificativa                                                                                                     |
| ------------------------- | ------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| Interface e aplicação     | 🔲 Next.js + React        | Aplicação web moderna e responsiva.                                                                               |
| Banco de dados            | 🔲 PostgreSQL             | Transações e integridade para vendas e estoque. Ver [12](/broken/pages/7b27ffbad2e45aa16a4b079862092214a0fd1a00). |
| Inteligência Artificial   | 🔲 API de IA generativa   | Geração dos resumos e sugestões do Assistente Lilica.                                                             |
| Assistente de programação | 🔲 ferramenta(s) usada(s) | Apoio à escrita e à correção de código.                                                                           |
| Prototipação              | 🔲 Figma ou Canva         | Telas e fluxos.                                                                                                   |
| Documentação              | GitBook                   | Diário evolutivo do projeto.                                                                                      |
| Versionamento             | 🔲 GitHub + Git Sync      | Colaboração por branches e pull requests.                                                                         |

## 14.4 Arquitetura

**Figura 02 — Arquitetura do Lilica Vendas.**

O usuário acessa a interface web, que conversa com o servidor da aplicação. O servidor aplica as regras de negócio, consulta o banco de dados com SQL parametrizado e, quando o usuário pede, envia **apenas dados agregados** ao serviço de IA, recebendo de volta o texto sugerido.

## 14.5 Fluxo principal: registrar uma venda

**Figura 03 — Fluxo de registro de venda.**

O vendedor escolhe o cliente e adiciona os produtos. O sistema valida o estoque: se faltar, avisa e permite ajustar a quantidade; se estiver tudo certo, registra o pagamento, baixa o estoque e emite o comprovante.

## 14.6 Telas e protótipo

🔲 Inserir wireframes e capturas de tela. **Toda imagem precisa de legenda e explicação.** Modelo:

> **Figura 04 — Tela de nova venda.** Esta tela permite que o vendedor escolha o cliente, adicione produtos e veja o total da venda.

| Recurso                  | Link                    |
| ------------------------ | ----------------------- |
| Protótipo navegável      | 🔲 \[Acessar protótipo] |
| Sistema em funcionamento | 🔲 inserir link         |
| Repositório              | 🔲 inserir link         |

## 14.7 Funcionalidades implementadas por RT

| Requisito                              | RT02 | RT03 | RT04 |
| -------------------------------------- | ---- | ---- | ---- |
| RF01 Login e perfis                    | 🔲   | 🔲   | 🔲   |
| RF02/RF04 Cadastros                    | 🔲   | 🔲   | 🔲   |
| RF05/RF06 Venda e validação de estoque | 🔲   | 🔲   | 🔲   |
| RF07 Pagamento                         | 🔲   | 🔲   | 🔲   |
| RF13 Relatórios                        | 🔲   | 🔲   | 🔲   |
| RF16 Assistente Lilica                 | 🔲   | 🔲   | 🔲   |

## 14.8 Registro do desenvolvimento

_Atualizar a cada atividade relevante._

| Data       | Atividade                                     | Responsável | Resultado                     |
| ---------- | --------------------------------------------- | ----------- | ----------------------------- |
| 28/09/2026 | Estruturar o GitBook nas 21 seções do roteiro | 🔲          | Estrutura e rascunhos criados |
| 🔲         | 🔲                                            | 🔲          | 🔲                            |
| 🔲         | 🔲                                            | 🔲          | 🔲                            |
