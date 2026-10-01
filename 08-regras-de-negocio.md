# 08 regras de negocio

Regras que devem ser respeitadas **pelo sistema e pelo Banco de Dados**.

## 8.1 Regras do negócio



1. Cada usuário deverá possuir credenciais próprias para acessar o sistema.
2. Um cliente poderá possuir várias compras cadastradas.
3. Uma compra deverá estar vinculada a um cliente.
4. Toda venda deverá possuir um valor total.
5. Uma venda poderá ser registrada como paga, parcialmente paga ou em aberto.
6. Quando houver pagamento parcial, o sistema deverá calcular e apresentar automaticamente o valor restante.
7. O usuário poderá registrar uma encomenda vinculada a um cliente.
8. Os repasses deverão ser registrados para permitir o acompanhamento dos valores pagos aos distribuidores.
9. O dashboard deverá apresentar informações atualizadas com base nos dados cadastrados no sistema.
10. O usuário somente poderá acessar e gerenciar as informações permitidas de acordo com seu acesso ao sistema



### 8.2 Privacidade e segurança (LGPD)

* Os dados dos clientes (nome, telefone, e-mail) são **dados pessoais** e só devem ser coletados quando necessários para a venda.
* O acesso é restrito por login e perfil.
* Senhas são gravadas apenas como **hash**.



## 8.3 Ética no uso da IA

* A IA **sugere**; quem decide é o gestor.
* Todo texto gerado por IA é identificado como tal.
* As respostas são conferidas com os dados reais antes de serem usadas (a IA pode errar).
