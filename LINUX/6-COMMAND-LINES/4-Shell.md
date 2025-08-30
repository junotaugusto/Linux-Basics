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