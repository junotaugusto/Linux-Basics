# Criando e Gerenciando Usuários

## Criando um Usuário
- O comando básico para criar um usuário é **useradd** ou **adduser** dependendo da distro que você estiver utilizando. 

Exemplo:
```bash
sudo useradd Silvio 
```

## Adicionando uma Senha ao Usuário
- Para adicionais outros detalhes ao usuário como, por exemplo, uma senha:
```bash
passwd Silvio
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

## Especificando o Shell ao Usuário
- No Linux, quando se fala que o comando especifica um “login shell”, significa que você está definindo qual programa de terminal será iniciado automaticamente quando o usuário fizer login no sistema.
```bash
sudo adduser -s /bin/bash username
```
- `-s /bin/bash` especifica o shell que será usado pelo usuário.
- `/bin/bash`é o Bash, o shell padrão mais comum no Linux.
- Sem definir o shell, o Linux poderia usar o shell padrão do sistema, que nem sempre é o que você deseja.
