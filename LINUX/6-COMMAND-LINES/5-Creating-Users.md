# Criando e Gerenciando Usuários

## Criando um Usuário
- O comando básico para criar um usuário é **useradd** ou **adduser** dependendo da distro que você estiver utilizando. 

Exemplo:
```bash
sudo useradd Silvio 
```
- Lembrando que o `useradd` cria uma nova conta adicionando entradas em `/etc/passwd` e `/etc/shadow`; se o nome já existir, o comando falha. 
- Note que useradd é uma ferramenta de baixo nível: por padrão não cria o diretório home a menos que você use `-m`. 
- Em distribuições Debian/Ubuntu existe o `adduser`, que é um wrapper mais amigável (ele cria o home, pede senha etc.). Você precisa de privilégios de root (ou sudo) para rodar ambos.

## Adicionando uma Senha ao Usuário
- Para adicionais outros detalhes ao usuário como, por exemplo, uma senha:
```bash
passwd Joao
```
- A senha que você inserir será adicionada ao usuário.

## Adicionando um Home Directory ao Usuário
- O diretório casa é uma pasta particular do seu usuário. 
- Por padrão, quando criamos um *diretório casa* para um usuário, ele será criado em (/home). Por exemplo, se queremos criar um diretório casa para o usuário João:
```bash
sudo useradd -m Joao
```
- Imediatamente ele irá criar um diretório casa em (/home/Joao).
- Caso você queira criar este diretório em outro lugar que não seja o padrão do Linux, você utiliza a flag "-d", como no exemplo abaixo:
```bash
sudo useradd -m -d /home/users/Joao Joao
```
- Além disso, você pode **alterar o home directory** de um usuário já existente. Digamos que o home directory de Joao é `/home/users/Joao` e você quer alterar para `/home/users/adm/Joao`. O comando para isso é:
```bash
sudo usermod -d /home/users/adm/Joao -m Joao
```
- Vale lembrar que o `usermod` não recebe dois caminhos; o `-d` define o novo diretório home e o `-m` apenas manda mover os arquivos do **home antigo** para o novo.

## Especificando o Shell ao Usuário
- No Linux, quando se fala que o comando especifica um “login shell”, significa que você está definindo qual programa de terminal será iniciado automaticamente quando o usuário fizer login no sistema.
```bash
sudo adduser -s /bin/bash username
```
- `-s /bin/bash` especifica o shell que será usado pelo usuário.
- `/bin/bash`é o Bash, o shell padrão mais comum no Linux.
- Sem definir o shell, o Linux poderia usar o shell padrão do sistema, que nem sempre é o que você deseja.

## Adicionando o Usuário a um Grupo Específico
- Grupos no Linux são coleções de contas usadas para organizar usuários com necessidades de acesso semelhantes, ou seja, ao invés de dar permissão usuário por usuário, você atribui permissões a um grupo (por exemplo, acesso a uma pasta, execução de um recurso ou entrada em regras do sudo).

- Você adiciona ou remove usuários de determinado grupo, o que torna a administração mais simples e segura — arquivos e processos têm dono e grupo, e as permissões de grupo determinam o que qualquer membro daquele grupo pode fazer.

- **Grupo Primário** - Cada usuário tem um só. Ele é definido em `/etc/passwd`. Normalmente, quando você cria um usuário, o sistema cria um grupo com o mesmo nome e o torna primário. Todos os arquivos que o usuário cria vêm com esse grupo primário.

- **Grupos Suplementares** - São adicionais. Servem para dar permissões extras em pastas ou recursos sem mudar o grupo primário. Um usuário pode pertencer a vários grupos suplementares.

- **IMPORTANTE** - Quando você roda o comando `getent group`, você percebe que, por padrão, o Linux possui muitos grupos diferentes, sem você ter criado nada. 
- Isso ocorre porque quando você instala o Linux, muitos serviços e programas precisam rodar com permissões específicas. Para não rodar tudo como `root` (o que seria muito inseguro), o sistema cria usuários e grupos especiais só para eles.
- Alguns grupos são usados para controlar recursos do hardware, como `audio` ou `video`, outros servem para definir permissões de administração, como `sudo`. 

- Para criar um grupo novo, o comando é:
```bash
sudo addgroup Nome_Do_Grupo
```

- Já para atribuir um usuário ao grupo, o comando é:
```bash
sudo useradd -G developers,admins Joao
```
- Irá criar um novo usuário chamado `Joao`.
- Irá atribuir a ele os grupos suplementares `developers` e `admins`, caso esses grupos já existam. Caso contrário, dará erro.
- Lembrando que a flag `-G` irá atribuir o usuário a **grupos suplementares**. Para atribuir o usuário a **grupos primários**, utilize a flag `-g`.

- Para atribuir um grupo a um usuário já existente, o comando é um pouco diferente:
```bash
sudo usermod -G developers,admins Joao
```
- Ao invés de utilizar `useradd` onde ele irá criar um usuário novo, utilize `usermod` para ele atribuir os grupos ao usuário já existente.
- **Um detalhe importante:** quando você usa `usermod -G`, ele **substitui todos os grupos suplementares anteriores**. Se quiser só adicionar sem remover os que já existiam, precisa usar -aG (append). No caso, seria:
```bash
sudo usermod -aG developers,admins Joao
```
