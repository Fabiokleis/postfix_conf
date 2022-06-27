Run
---
1. crie o arquivo secrets.yml e depois encryte com ansible-vault encrypt secrets.yml

```
user: "usuario_sasl_passwd@gmail.com"
password: "senha gerada nas configuracoes de seguranca do gmail"
mailtester_name: "nome do auth user que será criado"
mailtester_password: "crie uma hash com mkpasswd --method=sha-512 e copie aqui"
test_password: "senha criada no mkpasswd para testes" # crie caso teste com molecule
```

2. Apply
```
ansible-playbook -i inventory.yml postfix_example/deploy.yml -e @secrets.yml --vault-pass-file=~/.vault
```

Test
---

```
swaks --server node01.sysadmin.example -tls -p 25 --to example@gmail.com --auth plain --auth-user mailtester --auth-password 123
```

License
-------

BSD

Author Information
------------------

Fabio Kleis
