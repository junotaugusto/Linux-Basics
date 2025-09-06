# Permissões de Arquivos no Linux

No Linux, **permissões** definem quem pode acessar ou modificar arquivos e diretórios. Entender como funcionam é essencial para administração de sistemas e segurança.

---

## 1. Ownership (Propriedade)

Cada arquivo ou diretório possui dois donos principais:

- **Usuário (owner):** o dono principal do arquivo.
- **Grupo (group):** um grupo de usuários que também pode ter permissões sobre ele.

Além disso, existe a categoria **outros (others)**, que representa todos os demais usuários do sistema.

Exemplo:

```bash
-rw-r----- 1 joao developers 1234 set 05 10:00 arquivo.txt
```
-> joao → dono do arquivo
-> developers → grupo do arquivo
-> others → todos os outros usuários

## 2. Tipos de Permissão

Existem **três tipos** de permissões que podem ser aplicadas a usuários, grupos e outros:

`r (read / leitura)`: permite ler o arquivo ou listar os conteúdos de um diretório.
`w (write / escrita)`: permite modificar o arquivo ou criar/excluir arquivos dentro de um diretório.
`x (execute / execução)`: permite executar o arquivo como programa ou entrar no diretório.

## 3. Estrutura de Permissões

Quando usamos ls -l, vemos algo assim:
```bash
-rwxr-x---
```
**Quebrando:**
O primeiro caractere indica o tipo de arquivo:
- → arquivo normal
d → diretório
l → link simbólico

Os próximos três (rwx) são as permissões do dono.
Os três seguintes (r-x) são as permissões do grupo.
Os últimos (---) são as permissões de outros usuários.

No exemplo acima:
`Dono` → pode ler, escrever e executar
`Grupo` → pode ler e executar
`Outros` → não tem permissão

## 4. Diferença de Permissões em Arquivos e Diretórios

Permissão	         Arquivo	             Diretório
r	                 Ler conteúdo	         Listar arquivos dentro do diretório
w	                 Modificar conteúdo	     Criar, renomear ou apagar arquivos dentro do diretório
x	                 Executar arquivo	     Entrar no diretório (cd) e acessar arquivos pelo nome

⚠️ Exemplo: `drwx------` → somente o dono pode listar, criar, apagar e acessar arquivos dentro do diretório; grupo e outros não têm nenhum acesso.

## 5. Alterando as Permissões

No Linux, cada arquivo e diretório possui permissões que definem quem pode **ler**, **escrever** ou **executar** aquele arquivo. As permissões podem ser alteradas de duas formas: **simbólica** e **numérica**.

---

### Forma Simbólica

Para alterar permissões de forma simbólica, utiliza-se o comando `chmod`. Por exemplo, para transformar um arquivo `.sh` em executável:
```bash
chmod u+x arquivo.sh
```
- O `u+x` significa:
- - `u`- Usuário dono.
- - `+`- Adicionar permissão.
- - `x`- Permissão de execução.

Se você quiser que todos (usuário, grupo e outros) possam executar o arquivo, pode fazer:
```bash
chmod +x arquivo.sh
```
**Nota: As permissões simbólicas podem combinar outras letras:**
- r → leitura (read)
- w → escrita (write)
- x → execução (execute)

E os alvos podem ser:
- u → usuário dono
- g → grupo
- o → outros
- a → todos (u+g+o)

### Forma Numérica

Outra forma de definir permissões é usando números, também com chmod. Por exemplo:
```bash
chmod 755 arquivo
```
Cada número representa permissões para usuário, grupo e outros, respectivamente.
As permissões são somadas da seguinte forma:
- r (read) = 4
- w (write) = 2
- x (execute) = 1
Assim:
- 7 = 4 + 2 + 1 = leitura + escrita + execução
- 5 = 4 + 0 + 1 = leitura + execução
- 0 = nenhuma permissão

No exemplo `chmod 755` arquivo:
- 7 → usuário dono pode ler, escrever e executar
- 5 → grupo pode ler e executar
- 5 → outros podem ler e executar

## 6. Mudando a Propriedade

### CHOWN
Podemos também alterar o dono de um arquivo com o comando `chown`. Por exemplo:
```bash
sudo chown joao arquivo.txt
```
Isso faz com que o usuário `joao` se torne o dono do arquivo arquivo.txt. O chown também permite alterar simultaneamente o grupo do arquivo, usando a sintaxe:
```bash
sudo chown joao:desenvolvimento arquivo.txt
```
Neste caso, o dono do arquivo será joao e o grupo será desenvolvimento.

### CHGRP

Já o comando chgrp serve especificamente para alterar apenas o grupo de um arquivo ou diretório. Por exemplo:
```bash
chgrp marketing arquivo.txt
```
Isso muda o grupo associado ao arquivo para marketing, permitindo que todos os membros desse grupo apliquem as permissões de grupo definidas.

Esses comandos são essenciais para gerenciamento de acesso em sistemas multiusuário, pois permitem controlar quem pode ler, escrever ou executar arquivos com base na propriedade de usuário e grupo, aumentando a organização e a segurança em ambientes Linux.