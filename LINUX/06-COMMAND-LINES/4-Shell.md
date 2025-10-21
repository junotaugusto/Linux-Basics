# Criando um Shell Script Simples

Um **shell script** é um arquivo de texto que contém uma sequência de comandos que podem ser executados automaticamente pelo interpretador de shell (como o Bash).

---

## Passo 1 – Criar o arquivo de script
O primeiro passo é criar um arquivo com extensão `.sh` (embora a extensão não seja obrigatória, é uma boa prática para indicar que se trata de um script).  

Exemplo: 

```bash
script.sh
```

Na primeira linha do arquivo, adiciona-se o **shebang**:  
(#!/bin/bash)  

O shebang indica qual interpretador deve ser usado para executar o script.  
No caso acima, estamos dizendo ao sistema que o script será interpretado pelo **Bash**, localizado no caminho `/bin/bash`.

---

## Passo 2 – Tornar o script executável
Por padrão, um arquivo de texto recém-criado não possui permissão de execução.  
Para que o sistema entenda que ele pode ser executado como um programa, é necessário alterar suas permissões.  

Isso é feito com o comando:  

```bash
chmod +x script.sh
```

- `chmod` → comando para alterar permissões.  
- `+x` → adiciona a permissão de execução.  
- `script.sh` → é o nome do arquivo.  

Após esse passo, o script pode ser executado no terminal.  

---

## Usando Variáveis

No shell, podemos criar variáveis para armazenar informações. Um exemplo simples seria **name="LinuxGPT"**. Neste caso, chamamos essa variável no código usando **$name**.

Também é possível armazenar a saída de um comando dentro de uma variável. Um exemplo seria **data=$(date)**. Nesse caso, a variável **data** recebe o resultado do comando *date*.  

## Usando condicionais

As condicionais, basicamente utilizam as expressões *if* e *then*. Uma estrutura básica seria:

if [ "$variável" == "valor" ]; then
    echo "Condição verdadeira"
else
    echo "Condição falsa"
fi

## Tipos de Condições
Dentro dos colchetes `[ ]`, podemos usar diferentes comparações:  

- **Números**  
  - (-eq) → igual  
  - (-ne) → diferente  
  - (-gt) → maior que  
  - (-lt) → menor que  
  - (-ge) → maior ou igual  
  - (-le) → menor ou igual  

- **Strings**  
  - (=) → igual  
  - (!=) → diferente  
  - (-z) → string vazia  
  - (-n) → string não vazia  

- **Arquivos**  
  - (-e arquivo) → existe  
  - (-f arquivo) → existe e é arquivo normal  
  - (-d diretório) → existe e é diretório  
  - (-r arquivo) → tem permissão de leitura  
  - (-w arquivo) → tem permissão de escrita  
  - (-x arquivo) → tem permissão de execução  

---

📌 Em resumo:  
- `if` permite tomar decisões.  
- Podemos usar `else` para tratar alternativas.  
- `elif` permite múltiplas verificações.  
- Existem testes numéricos, de strings e de arquivos. 

## Fazendo um script
- Digite `nano script1.sh`.

Este script irá verificar se o nome digitado é o que o desenvolvedor quer.

```bash
!#/bin/bash
echo "Digite o nome correto: "
read nome

if [ $nome = "Lucas"]; then
    echo "Nome correto!"
else
    echo "Nome incorreto!"
fi    
```

---

Outro script, agora para realizar a automação de alguns serviços.

O script irá verificar se determinado arquivo existe e, caso exista, irá removê-lo.

```bash
#!/bin/bash
if [ -f "/home/user/Desktop/arquivo.txt" ]; then
    echo "O arquivo existe"
    echo "O arquivo será removido agora"
    rm -i "/home/user/Desktop/arquivo.txt"
else
    echo "O arquivo não existe"
fi
```