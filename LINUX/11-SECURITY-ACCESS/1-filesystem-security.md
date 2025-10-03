# Segurança de Acesso e do Filesystem

## chroot: Alterando o Diretório Raiz

### 1. O que `chroot` quer dizer e o que ele faz?

O nome **`chroot`** é uma abreviação de *"change root"*, que significa **"alterar a raiz"**.

O comando `chroot` é uma operação que altera o diretório raiz (`/`) da visão de um processo e de todos os seus processos filhos. 

Em outras palavras, para um programa que está rodando dentro de um ambiente `chroot`, o diretório que definimos como a "nova raiz" passa a ser o topo da hierarquia de arquivos. 

Ele simplesmente não consegue "ver" ou acessar qualquer arquivo ou diretório que esteja "acima" dessa nova raiz.

Isso nos leva diretamente ao conceito de "chroot jail".

### 2. O Conceito de `chroot jail` (Jaula chroot)

Uma **`chroot jail`** (jaula chroot) é o ambiente isolado que criamos com o `chroot`. A analogia da "jaula" ou "prisão" é perfeita:

Imagine que você está em uma sala. Ao aplicar o `chroot`, a porta pela qual você entrou desaparece e as paredes se tornam intransponíveis. Para você, aquela sala se torna o universo inteiro. Você só pode interagir com os objetos e ferramentas que já estavam dentro da sala com você.

Da mesma forma, um processo "preso" em uma `chroot jail` não pode acessar `/etc/passwd` do sistema real, nem o `/home` dos outros usuários, pois, do ponto de vista dele, esses caminhos simplesmente não existem.

### 3. Por que usar o `chroot`? (Casos de Uso)

Entender seus casos de uso é a melhor maneira de compreender sua utilidade.

#### a) Segurança

Este é o uso mais clássico. Se um serviço que está exposto à internet (como um servidor FTP ou um servidor web antigo) for comprometido, um atacante poderia, em teoria, ganhar acesso ao sistema inteiro.

Ao rodar esse serviço dentro de uma `chroot jail`, o dano potencial é drasticamente limitado. Se o atacante explorar uma vulnerabilidade no servidor FTP, ele só terá acesso aos arquivos que estão *dentro da jaula*. Ele não conseguirá acessar arquivos críticos do sistema real, pois eles estão fora do seu diretório raiz visível.

#### b) Desenvolvimento e Testes

Desenvolvedores podem criar ambientes `chroot` para testar aplicações em um ambiente "limpo" e controlado. Por exemplo, eles podem montar uma jaula contendo apenas as bibliotecas e dependências de uma versão específica do sistema (ex: Ubuntu 18.04) para garantir que a aplicação funcione corretamente nesse ambiente, sem precisar de uma máquina virtual inteira ou de alterar o sistema hospedeiro.

#### c) Recuperação de Sistemas

Este é um dos usos mais importantes para administradores de sistema. Imagine que o seu Linux não inicia mais porque o bootloader (GRUB) foi corrompido ou uma atualização quebrou arquivos críticos.

O procedimento de recuperação é:
1.  Iniciar o computador usando um Live CD/USB de uma distribuição Linux.
2.  Montar o disco rígido do sistema quebrado em um diretório (ex: `/mnt/meu_sistema_quebrado`).
3.  Usar o `chroot` para "entrar" nesse sistema montado: `sudo chroot /mnt/meu_sistema_quebrado`.

A partir desse momento, o seu terminal no Live CD passa a operar como se estivesse rodando diretamente no sistema quebrado. Você pode executar comandos como `grub-install` ou `apt-get upgrade` para consertar o sistema, pois todos os caminhos (`/boot`, `/etc`, etc.) serão os do sistema original.

### 4. Comandos e Uso Prático com `chroot`

Usar o `chroot` exige um preparo. Como o processo fica "preso", ele precisa de todas as suas ferramentas e dependências *dentro* da jaula.

#### Sintaxe Básica
```bash
# Sintaxe: chroot /caminho/para/nova/raiz [COMANDO_A_EXECUTAR]
sudo chroot /caminho/para/nova/raiz
```
Se nenhum comando for especificado, ele tentará executar `/bin/bash` por padrão.

#### Exemplo: Criando uma Jaula Simples

1.  **Criar o diretório da jaula:**
    ```bash
    sudo mkdir /minha_jaula
    ```

2.  **Copiar os binários essenciais para dentro da jaula:**
    Um shell é inútil sem comandos. Vamos copiar o `bash` (o shell) e o `ls` (para listar arquivos).
    ```bash
    # Criar a estrutura de diretórios dentro da jaula
    sudo mkdir -p /minha_jaula/bin

    # Copiar os binários
    sudo cp /bin/bash /minha_jaula/bin/
    sudo cp /bin/ls /minha_jaula/bin/
    ```

3.  **Copiar as bibliotecas (dependências):**
    Binários como `bash` e `ls` dependem de bibliotecas compartilhadas (`.so` files). Sem elas, eles não funcionam. O comando `ldd` nos diz quais são as dependências.
    ```bash
    # Verificar as dependências do bash
    ldd /bin/bash
    ```
    Você precisará copiar cada uma dessas bibliotecas listadas para dentro da estrutura correspondente na jaula (ex: `/minha_jaula/lib/` e `/minha_jaula/lib64/`). Este é o passo mais trabalhoso.

4.  **Entrar na jaula:**
    ```bash
    sudo chroot /minha_jaula
    ```
    Se tudo foi feito corretamente, seu prompt mudará, e se você executar `ls /`, verá apenas o conteúdo de `/minha_jaula`. Tentar acessar `../../` não o levará para fora da jaula.

> **Nota:** `chroot` não é uma ferramenta de segurança infalível. Um processo rodando com privilégios de `root` dentro da jaula pode, em certas condições, encontrar maneiras de "escapar". Para um isolamento mais robusto, tecnologias modernas como **Containers (Docker, LXC)** e **Namespaces** são recomendadas.