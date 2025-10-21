# 3. /etc/passwd

Lembre-se de que nomes de usuário não são realmente identificações para usuários.  

O sistema usa um **ID de usuário (UID)** para identificar um usuário.  
Para descobrir quais usuários estão mapeados para quais IDs, veja o arquivo `/etc/passwd`.

```
$ cat /etc/passwd
```

Esse arquivo mostra uma lista de usuários e informações detalhadas sobre eles.  
Por exemplo, a primeira linha desse arquivo provavelmente se parece com isto:

```
root:x:0:0:root:/root:/bin/bash
```

Cada linha exibe informações de um usuário. Normalmente, você verá o usuário `root` como a primeira linha. Existem vários campos separados por dois-pontos que fornecem informações adicionais sobre o usuário. Vamos analisá-los:

1. **Nome de usuário**  
2. **Senha do usuário** – a senha não é realmente armazenada nesse arquivo, normalmente ela é armazenada no arquivo `/etc/shadow`.  
   - Vamos falar mais sobre o `/etc/shadow` na próxima lição, mas por enquanto saiba que ele contém as senhas de usuários criptografadas.  
   - Você pode ver diferentes símbolos nesse campo:  
     - `"x"` significa que a senha está no arquivo `/etc/shadow`.  
     - `"*"` significa que o usuário não tem acesso de login.  
     - Campo em branco significa que o usuário não tem senha.  
3. **ID do usuário (UID)** – como pode ver, o root tem UID igual a `0`.  
4. **ID do grupo (GID)**.  
5. **Campo GECOS** – usado para deixar comentários sobre o usuário ou conta, como nome real ou número de telefone. É delimitado por vírgulas.  
6. **Diretório home do usuário**.  
7. **Shell do usuário** – provavelmente verá muitos usuários usando `bash` como shell padrão.

Normalmente, em uma página de configurações de usuários, você esperaria ver apenas usuários humanos. No entanto, você notará que o `/etc/passwd` contém **outros usuários**. O Linux trata qualquer entidade que possa executar processos e ter permissões como um “usuário”.

Lembre-se: **usuários existem no sistema principalmente para executar processos com diferentes permissões**. Às vezes, queremos executar processos com permissões pré-determinadas. Por exemplo, o usuário `daemon` é usado para processos do tipo daemon.

Por exemplo:

`bin` → usado historicamente para gerenciar programas básicos do sistema.
`sys` → ligado a funções do sistema e serviços antigos.
`games` → usado para rodar jogos sem dar acesso desnecessário a outros arquivos.
`www-data` → usado por servidores web como o Apache ou Nginx para que, se o servidor for comprometido, o invasor tenha acesso limitado.

Também vale notar que você pode editar o arquivo `/etc/passwd` manualmente se quiser adicionar usuários ou modificar informações, usando a ferramenta `vipw`.  
Entretanto, esse tipo de tarefa é melhor ser feita com as ferramentas que veremos mais adiante, como `useradd` e `userdel`.
