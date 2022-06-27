Postfix Example
=========

Exemplo de como configurar postfix com cyrus-sasl em debian based systems

Requirements
------------
  postfix: [oefenweb.postfix](https://github.com/Oefenweb/ansible-postfix)
 
Role Variables
--------------

 `mech_list`: metodos de autenticacao para o postfix
 
 `mechanisms`: tipo de autenticacao para o sasl com postfix - smtpd
 
 `relay_host`: configuracao de relay para o postfix
 
 `smtpd_sasl_dir`: local onde fica o arquivo stmpd.conf pro sasl
 
 `pwcheck`: metodo de autenticacao 
 
 `saslauthd_default_path`: caminho onde fica o arquivo de instancia do saslauthd
 
 `relay_host`: servidor que o postfix irá utilizar como relay
 
 `smtpd_sasl_dir`: caminho onde fica o arquivo smtpd

Test
---
1. crie o arquivo ~/secrets.yml e depois encryte com ansible-vault encrypt ~/secrets.yml
```
user: "usuario_sasl_passwd@gmail.com"
password: "senha gerada nas configuracoes de seguranca do gmail"
mailtester_name: "nome do auth user que será criado"
mailtester_password: "crie uma hash com mkpasswd --method=sha-512 e copie aqui"
test_password: "senha criada no mkpasswd para testes"
```

2. verifique o arquivo molecule.yml e modifique a opcao `config_options`, coloque um arquivo com a senha do ansible-vault utilizada para encrytar o secrets.yml ou coloque para pedir a senha

 `vault_password_file: ~/.vault` # caminho para o arquivo com a senha

 `ask_vault_pass: true` # coloque a senha durante a execuçao

3. variaveis do molecule

 `test_password: "{{ vault_test_password }}"` # senha para testar a autenticacao

 `postfix_server: "postfixtest"` # nome do servidor smtp

 `mail: "coloque um email de testes"` # endereço de email que será enviado

 `auth: "plain"` # metodo para autenticar

 `auth_user: "mailtester"` # nome do usuario padrao para autenticacao
 
 `server_port: "25"` # porta aberta no container

4. Aplique e rode a verificação

 `molecule converge` # para subir o container e aplicar a role

 `molecule verify` # para rodar os testes dentro do arquivo verify.yml

License
-------

BSD

Author Information
------------------

Fabio Kleis
