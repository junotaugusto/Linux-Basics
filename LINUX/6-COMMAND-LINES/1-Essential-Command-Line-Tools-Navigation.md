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

# Resumo
- Use (whoami) para saber o usuário atual e (hostname) para saber o nome da máquina.  
- (pwd), (cd) e (ls) são a base da navegação no Linux.  
- Comandos como (touch), (mkdir), (cp), (mv), (rm), (zip), (tar) permitem gerenciar arquivos e diretórios.  
- Sempre confira as opções (-h, --help) para aprender mais sobre cada comando.
