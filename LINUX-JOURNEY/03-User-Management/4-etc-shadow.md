# 4. /etc/shadow
O arquivo /etc/shadow é usado para armazenar informações sobre autenticação de usuários. Ele requer permissões de leitura de superusuário.
```bash
$ sudo cat /etc/shadow

root:MyEPTEa$6Nonsense:15000:0:99999:7:::
```

Você notará que ele se parece muito com o conteúdo de /etc/passwd, porém no campo de senha você verá uma senha criptografada. Os campos são separados por dois-pontos da seguinte forma:

**1 - Nome de usuário**
**2 - Senha criptografada**
**3 - Data da última alteração de senha** – expressa como o número de dias desde 1º de janeiro de 1970. Se houver um 0, isso significa que o usuário deverá alterar sua senha na próxima vez que fizer login.
**4 - Idade mínima da senha** – Dias que um usuário terá que esperar antes de poder alterar sua senha novamente
**5 - Idade máxima da senha** – Número máximo de dias antes que um usuário tenha que alterar sua senha
**6 - Período de aviso de senha** – Número de dias antes de uma senha expirar
**7 - Período de inatividade da senha** – Número de dias após uma senha expirar para ainda permitir login com essa senha
**8 - Data de expiração da conta** – data em que o usuário não poderá mais fazer login.
**9 - Campo reservado para uso futuro**

Na maioria das distribuições atuais, a autenticação de usuários não depende apenas do arquivo /etc/shadow, existem outros mecanismos em uso, como o PAM (Pluggable Authentication Modules), que substituem a autenticação
