Postfix Example
=========

Exemplo de como configurar postfix com cyrus-sasl em debian based systems

Requirements
------------
  postfix: [oefenweb.postfix](https://github.com/Oefenweb/ansible-postfix)
 
Role Variables
--------------

 `mechanisms` tipos de authenticacao para o sasl
 `relay_host` configuracao de relay para o postfix
 
Test
---
molecule converge # to up a docker container and apply the role contents

License
-------

BSD

Author Information
------------------

Fabio Kleis
