# 5. /etc/group
Outro arquivo utilizado em na administração de usuários é o arquivo `/etc/group`. Este arquivo permite grupos diferentes com permissões diferentes.
```bash
$ cat /etc/group


root:*:0:pete
```

Muito parecido com o resultado de /etc/password, o resultado (output) do arquivo /etc/group é representado da seguinte maneira:

**1 - Group name**
**2 - Group password** - Não há necessidade de definir uma senha para um grupo, usar o privilégio como o sudo é o padrão. O "*" será inserido como valor padrão.
**3 - Group ID (GID)**
**4 - List of users** - Você pode especificar manualmente os usuários que quer dentro de um grupo específico.