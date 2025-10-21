# Essential Command Line & Navigation

Neste capítulo vamos explorar comandos essenciais do Linux relacionados a **informações do sistema**, **navegação no terminal** e **gerenciamento de arquivos e diretórios**. É importante lembrar que os comandos no Linux são **case-sensitive** (diferenciam maiúsculas de minúsculas).

## 1. Comandos com Informações do Sistema

### whoami
Exibe o **usuário atual** logado no sistema.

```bash
whoami
```
Exemplo de saída:  
(antonio)

---

### uname
Mostra informações sobre o sistema.

```bash
(uname)
```

Exemplo de saída:  
(Linux)

Opções comuns:  
- (uname -a) → mostra todas as informações (kernel, hostname, versão, arquitetura, etc.)  
- (uname -r) → mostra apenas a versão do kernel  
- (uname -m) → mostra a arquitetura da máquina  

---

### hostname
Mostra ou define o **nome da máquina** (host).

```bash
(hostname)
```

Exemplo de saída:  
(debian-pc)

Opções úteis:  
- (hostname -i) → mostra o endereço IP associado ao host  
- (hostname -a) → mostra o nome alias (apelido) do host  
- (hostname -A) → mostra todos os nomes FQDN (Fully Qualified Domain Names) atribuídos  

---

### Diferença entre whoami e hostname
- (whoami) → mostra **quem é o usuário atual**.  
- (hostname) → mostra **qual é a máquina** em que o usuário está logado.  

## 2. Comandos de Navegação

### pwd (Print Working Directory)
Mostra o **caminho completo do diretório atual**.

```bash
pwd
```
Saída:  
(/home/junot/Documents)

---

### cd (Change Directory)
Usado para navegar entre diretórios.

```bash
cd /home/junot/Documents
```

Opções comuns:  
- (cd ..) → volta um diretório  
- (cd ~) → vai para o diretório home do usuário  
- (cd -) → volta para o último diretório acessado  

---

### ls (List)
Lista o conteúdo do diretório.

```bash
ls
```

Opções úteis:  
- (ls -l) → mostra detalhes (permissões, dono, tamanho, data)  
- (ls -a) → mostra arquivos ocultos  
- (ls -lh) → mostra detalhes com tamanhos legíveis (KB, MB, GB)  
- (ls -R) → lista recursivamente subdiretórios  

---

## 3. Comandos de Gerenciamento de Arquivos e Diretórios

### touch
Cria um arquivo vazio ou atualiza a data de modificação de um arquivo existente.

```bash
touch arquivo.txt
```

Opções:  
- (touch -c) → não cria o arquivo se ele não existir  
- (touch -t 202308261200 arquivo.txt) → define data/hora específicas  

---

### mkdir
Cria diretórios.

```bash
mkdir projetos
```

Opções:  
- (mkdir -p pasta1/pasta2/pasta3) → cria toda a hierarquia de pastas de uma vez  

---

### cp
Copia arquivos ou diretórios.

```bash
cp arquivo.txt copia.txt
```

Opções:  
- (cp -r pasta destino/) → copia diretórios recursivamente  
- (cp -i arquivo.txt destino/) → pede confirmação antes de sobrescrever  

---

### mv
Move ou renomeia arquivos/diretórios.

```bash
mv arquivo.txt pasta/  
mv arquivo.txt novo_nome.txt
```
---

### rm
Remove arquivos.

```bash
rm arquivo.txt
```

Opções:  
- (rm -i arquivo.txt) → pede confirmação  
- (rm -r pasta/) → remove diretórios recursivamente  
- (rm -rf pasta/) → remove diretórios e arquivos **sem pedir confirmação** (perigoso!)  

---

### rmdir
Remove diretórios vazios.

```bash
rmdir pasta_vazia
```

---

### file
Mostra o tipo de um arquivo.

```bash
file arquivo.txt
```

Exemplo de saída:  
(arquivo.txt: ASCII text)

---

### zip
Compacta arquivos em formato `.zip`.

```bash
zip arquivos.zip arquivo1.txt arquivo2.txt
```

Opções:  
- (zip -r arquivos.zip pasta/) → compacta recursivamente  

---

### unzip
Extrai arquivos `.zip`.

```bash
unzip arquivos.zip
```

Opções:  
- (unzip arquivos.zip -d destino/) → extrai em um diretório específico  

---

### tar
Compacta e descompacta arquivos no formato `.tar`.

```bash
tar -cvf arquivos.tar arquivo1.txt arquivo2.txt
```

Explicando as opções:  
- c → create (criar arquivo tar)  
- v → verbose (mostrar processo no terminal)  
- f → file (especifica o nome do arquivo)  

Exemplo de extração:  

```bash
tar -xvf arquivos.tar
```
Para arquivos compactados com gzip:  

```bash
tar -czvf arquivos.tar.gz pasta/  
tar -xzvf arquivos.tar.gz  
```
---

### Redirecionamento de Saída: `>`
O operador `>` é usado para **redirecionar a saída de um comando para um arquivo**. Se o arquivo não existir, ele será criado. Se já existir, o conteúdo será substituído.

```bash
echo "File Content" > new-archive.txt)  
```
Isso cria (ou sobrescreve) o arquivo `new-archive.txt` com o texto "File Content".

---

### Acrescentar Saída: `>>`
O operador `>>` também redireciona a saída, mas **acrescenta (append)** ao final do arquivo, sem apagar o conteúdo já existente.

```bash
echo "Nova linha" >> new-archive.txt)  
```
Isso adiciona "Nova linha" no final do arquivo `new-archive.txt`.

---

### Executar em Segundo Plano: `&`
O operador `&` executa um comando em segundo plano, permitindo que o terminal continue sendo usado sem esperar o processo terminar.

```bash
firefox & 
```
Isso abre o navegador Firefox em segundo plano.

---

### Executar Condicionalmente: `&&`
O operador `&&` executa o segundo comando **apenas se o primeiro for bem-sucedido** (ou seja, se o retorno for 0).

```bash
mkdir teste && cd teste
```

Aqui, o diretório `teste` é criado e, se der certo, o terminal entra nele.

---

## Visualizar Arquivo: `cat`
O comando `cat` exibe o conteúdo de um arquivo diretamente no terminal.

```bash
cat new-archive.txt
```

---

### Visualizar Começo e Final: `head` e `tail`
- `head` mostra as primeiras linhas de um arquivo (por padrão, 10).  

```bash
head new-archive.txt)  
```

- `tail` mostra as últimas linhas de um arquivo (por padrão, 10).  

```bash
tail new-archive.txt
```

Também é possível especificar quantas linhas mostrar:  

```bash
head -n 5 new-archive.txt) 
```
→ mostra as 5 primeiras linhas.  

```bash
tail -n 20 new-archive.txt
```
→ mostra as 20 últimas linhas.

---

### Leitura Paginada: `less` e `more`
- `more` mostra o conteúdo de um arquivo **página por página**. Você navega com espaço (avançar) e `q` para sair.  

```bash
more new-archive.txt
```

- `less` é mais avançado, permitindo rolar para frente e para trás.  

```bash
less new-archive.txt
```
---

## Buscar Arquivos: `find`
O comando `find` procura arquivos e diretórios em uma árvore de diretórios, com base em critérios como nome, tamanho, tipo, etc.

```bash
find /home -name "new-archive.txt"
```

Isso busca o arquivo `new-archive.txt` dentro da pasta `/home`.

```bash
find /var/log -type f -size +10M  
```

Isso procura arquivos maiores que 10 MB dentro de `/var/log`. 

Vale lembrar que o comando `find` pede um **caminho**, seguido de **opções e expressões de teste**.  
A sintaxe geral é:  
(find [path] [options] [expression])  

Nos exemplos acima:  
- Caminho: `/home` ou `/var/log`  
- Opção: `-name` ou `-size`  
- Expressão: `"new-archive.txt"` ou `+10M` 

---

### Buscar Arquivos no Banco de Dados: `locate`

O comando `locate` pesquisa arquivos rapidamente em um **banco de dados indexado** do sistema. Esse banco de dados precisa estar atualizado (com o comando `updatedb`), senão os resultados podem não refletir mudanças recentes no sistema de arquivos.  

```bash
locate new-archive.txt)  
```
Isso procura todas as ocorrências do arquivo `new-archive.txt` no banco de dados.  

```bash
located *.txt)  
```

Isso lista todos os arquivos com extensão `.txt` que estejam indexados.  

A sintaxe básica é:  
(locate [pattern])  

### Diferença entre `find` e `locate`
- `find` percorre os diretórios **em tempo real**, garantindo resultados atuais, mas pode ser mais lento.  
- `locate` usa um banco de dados pré-construído, sendo muito mais rápido, mas pode mostrar resultados desatualizados.  

Exemplo prático:  
- Se você criar um arquivo agora (echo "teste" > exemplo.txt) e rodar `locate exemplo.txt`, pode ser que ele **não apareça** até que você rode (updatedb).  
- Já com `find`, o arquivo aparece imediatamente.  

