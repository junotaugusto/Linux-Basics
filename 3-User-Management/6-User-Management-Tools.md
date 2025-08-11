# 6. Ferramentas de Gerenciamento de Usuários

A maioria dos ambientes empresariais utiliza sistemas de gerenciamento para administrar usuários, contas e senhas. No entanto, em um computador individual, existem comandos úteis para gerenciar usuários.

## Adicionando Usuários

Você pode usar os comandos **adduser** ou **useradd**. O comando **adduser** possui mais recursos úteis, como a criação do diretório home, entre outros. Existem arquivos de configuração para a adição de novos usuários que podem ser personalizados dependendo do que você deseja alocar para um usuário padrão.

```bash
$ sudo useradd bob
```
O comando acima cria uma entrada para o usuário bob no arquivo /etc/passwd, configura os grupos padrão e adiciona uma entrada no arquivo /etc/shadow.

## Removendo Usuários
Para remover um usuário, você pode usar o comando userdel.
```bash
$ sudo userdel bob
```
Esse comando basicamente tenta desfazer as alterações feitas pelo useradd.

## Alterando Senhas
```bash
$ passwd bob
```
Esse comando permite alterar a senha do próprio usuário ou de outro usuário (se você estiver como root).
