Postfix Example
=========

Exemplo de como configurar postfix com cyrus-sasl em debian based systems

Requirements
------------
  postfix: [oefenweb.postfix](https://github.com/Oefenweb/ansible-postfix)
 
Role Variables
--------------

 `mechanisms`: tipos de authenticacao para o sasl
 
 `relay_host`: configuracao de relay para o postfix
 
 `smtpd_sasl_dir`: local onde fica o arquivo stmpd.conf pro sasl
 
 `pwcheck`: metodo de autenticacao 
 
 `saslauthd_default_path`: caminho onde fica o arquivo de instancia do saslauthd

Test
---
1. crie o arquivo ~/secrets.yml e depois encryte com ansible-vault encrypt ~/secrets.yml
```
user: "usuario_sasl_passwd@gmail.com"
password: "senha gerada nas configuracoes de seguranca do gmail"
mailtester_password: "crie uma hash com mkpasswd --method=sha-512 e copie aqui"
test_password: "senha criada no mkpasswd para testes"
```

2. verifique o arquivo molecule.yml e modifique a opcao `config_options`, coloque um arquivo com a senha do ansible-vault utilizada para encrytar o secrets.yml ou coloque para pedir a senha

`vault_password_file: ~/.vault` # caminho para o arquivo com a senha

`ask_vault_pass: true` # coloque a senha durante a execuçao

3. variaveis do molecule

`test_password: "{{ vault_test_password }}"`

`postfix_server: "postfixtest"`

`mail: "coloque um email de testes"`

`auth: "plain"`

`auth_user: "mailtester"`

`server_port: "25"`

4. Aplique e rode a verificação
`molecule converge` # para subir o container e aplicar a role

`molecule verify` # para rodar os testes dentro do arquivo verify.yml

License
-------

BSD

Author Information
------------------

Fabio Kleis
