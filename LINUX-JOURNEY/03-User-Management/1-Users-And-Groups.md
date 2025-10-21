# 1. Usuários e Grupos

Em qualquer sistema operacional tradicional, existem usuários e grupos. Eles existem unicamente para controle de acesso e permissões. 

Ao executar um processo, ele será executado como o dono desse processo, seja ele Jane ou Bob. O acesso e a propriedade de arquivos também dependem de permissões. Você não iria querer que Jane visse os documentos de Bob e vice-versa.

Cada usuário possui seu próprio diretório pessoal onde seus arquivos específicos ficam armazenados, geralmente localizado em `/home/username`, mas isso pode variar em diferentes distribuições.

O sistema usa IDs de usuário (UID) para gerenciar usuários. Nomes de usuário são a forma amigável de associar um usuário à sua identificação, mas o sistema identifica os usuários pelo seu UID. 

O sistema também usa grupos para gerenciar permissões. Grupos são apenas conjuntos de usuários com permissões definidas por aquele grupo e são identificados pelo sistema com seu ID de grupo (GID).

No Linux, além dos usuários humanos normais, existem também usuários adicionais. Às vezes, esses usuários são *daemons* do sistema que executam processos continuamente para manter o sistema funcionando. 

Um dos usuários mais importantes é o **root** ou superusuário. O root é o usuário mais poderoso do sistema: pode acessar qualquer arquivo e iniciar ou encerrar qualquer processo. Por esse motivo, operar como root o tempo todo pode ser perigoso, pois você poderia remover arquivos críticos do sistema. 

cFelizmente, se o acesso root for necessário e um usuário tiver permissão para tal, ele pode executar um comando como root usando o comando `sudo`. O comando `sudo` (*superuser do*) é usado para executar um comando com privilégios de root. Mais adiante veremos em detalhes como um usuário obtém acesso root.

Experimente visualizar um arquivo protegido como `/etc/shadow`:

```
$ cat /etc/shadow
```

Note que você receberá um erro de "permissão negada". Veja as permissões com:

```
$ ls -la /etc/shadow
```

```
-rw-r----- 1 root shadow 1134 Dec 1 11:45 /etc/shadow
```

Ainda não abordamos permissões, mas o que está acontecendo aqui é que o root é o dono do arquivo, e você precisará de acesso root ou fazer parte do grupo `shadow` para ler o conteúdo. Agora execute o comando com `sudo`:

```
$ sudo cat /etc/shadow
```

Agora você poderá ver o conteúdo do arquivo!
