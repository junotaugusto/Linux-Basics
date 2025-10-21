# 2. root

Já vimos uma maneira de obter acesso de superusuário usando o comando `sudo`.  
Você também pode executar comandos como superusuário com o comando `su`.  

Esse comando irá “substituir usuários” (*substitute users*) e abrir um shell root se nenhum nome de usuário for especificado.  
Você pode usar esse comando para alternar para qualquer usuário, desde que saiba a senha.

```
$ su
```

Existem algumas desvantagens nesse método: é muito mais fácil cometer um erro crítico executando tudo como root, você não terá registros dos comandos que usou para alterar configurações do sistema, etc.  
Basicamente, se você precisar executar comandos como superusuário, mantenha-se apenas no `sudo`.

Agora que você sabe quais comandos executar como superusuário, a questão é: **como saber quem tem acesso para fazer isso?**  
O sistema não permite que qualquer pessoa execute comandos como superusuário, então como ele sabe?  Existe um arquivo chamado `/etc/sudoers`, que lista os usuários que podem executar `sudo`.  

Você pode editar esse arquivo com o comando `visudo`.
