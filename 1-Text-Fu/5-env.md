## 5. env (Variáveis de Ambiente)

Execute o seguinte comando:

```bash
$ echo $HOME
```

Você deverá ver o caminho para o seu diretório pessoal (home). No meu caso, aparece algo como `/home/seunome`.

E este comando?

```bash
$ echo $USER
```

Você verá o seu nome de usuário!

De onde vêm essas informações? Elas vêm das suas variáveis de ambiente. Você pode visualizá-las digitando:

```bash
$ env
```

Esse comando mostra uma grande quantidade de informações sobre as variáveis de ambiente que estão definidas no momento. Essas variáveis contêm informações úteis que o shell e outros processos podem utilizar.

Aqui está um exemplo simples:

```
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/bin
PWD=/home/user
USER=pete
```

Uma variável particularmente importante é a variável `PATH`. Você pode acessar essas variáveis colocando um `$` antes do nome da variável, assim:

```bash
$ echo $PATH
```

Isso retorna uma lista de caminhos separados por dois-pontos, que o sistema utiliza para procurar por comandos quando você os executa. 

Por exemplo, se você baixar e instalar um pacote manualmente da internet e colocá-lo em um diretório não padrão, e tentar executar com `$ coolcommand`, o terminal pode dizer "command not found". Isso é frustrante, já que você vê o binário na pasta e sabe que ele existe.

O que acontece é que a variável `$PATH` não está configurada para procurar naquele diretório específico, então o sistema não encontra o comando.

Se você tiver vários binários que deseja executar a partir desse diretório, basta modificar a variável `PATH` para incluir esse diretório.

## Entendendo melhor o PATH e execução de programas no Linux

O `PATH` é uma variável de ambiente que contém uma lista de diretórios onde o sistema procura por programas executáveis quando você digita um comando no terminal. 

Essa variável é essencial para o funcionamento do Linux, pois permite que você execute comandos sem precisar digitar o *caminho completo* até o arquivo executável.

Os diretórios padrão no `PATH` geralmente incluem locais como `/bin`, `/usr/bin`, `/usr/local/bin`, entre outros. No entanto, você pode adicionar outros diretórios ao `PATH` se desejar executar programas ou scripts localizados em pastas não padrão.

Por exemplo, se você criar um script ou programa em uma pasta personalizada, precisará adicionar essa pasta ao `PATH` para poder executar o programa de qualquer lugar no terminal, apenas digitando o nome do programa.

### Exemplo prático

Primeiro, crie uma pasta nova na área de trabalho chamada `MeuPrograma`:

```bash
cd ~/Desktop
mkdir MeuPrograma
cd MeuPrograma
```

Dentro dessa pasta, crie um arquivo chamado `ola.sh` com o seguinte conteúdo:

```bash
#!/bin/bash
echo "Olá, desenvolvedor! Esse é seu programa executável."
```

Salve o arquivo e dê permissão de execução com o comando:

```bash
chmod +x ola.sh
```

Agora, dentro da pasta `MeuPrograma`, execute o programa com:

```bash
./ola.sh
```

Você verá a mensagem:

```
Olá, desenvolvedor! Esse é seu programa executável.
```

Se você voltar para a pasta `Desktop` e tentar executar apenas `ola.sh`, receberá uma mensagem de *comando não encontrado*, porque a pasta `MeuPrograma` não está no `PATH` e o terminal não sabe onde encontrar o programa.

Para permitir que o sistema encontre o programa em `MeuPrograma` de qualquer lugar, adicione essa pasta ao `PATH` temporariamente com o comando:

```bash
export PATH=$PATH:$HOME/Desktop/MeuPrograma
```

Agora, mesmo estando em outra pasta, você pode executar `ola.sh` diretamente e verá a mensagem normalmente.

Se quiser tornar essa alteração permanente, adicione a linha

```bash
export PATH=$PATH:$HOME/Desktop/MeuPrograma
```

no final do arquivo `~/.bashrc` (ou `~/.zshrc` se usar zsh), salve e depois recarregue o arquivo com:

```bash
source ~/.bashrc
```

Assim, o sistema sempre reconhecerá os programas dentro da pasta `MeuPrograma`, e você poderá executá-los de qualquer diretório sem problemas.

Esse exemplo ajuda a entender que o `PATH` é uma maneira de dizer ao sistema onde procurar por executáveis, facilitando a execução dos seus programas e comandos personalizados.

