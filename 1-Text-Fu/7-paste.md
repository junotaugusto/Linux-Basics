# Comando `paste`

O comando `paste` é usado para **mesclar linhas de um arquivo**, semelhante ao `cat`, mas ao invés de exibir as linhas em sequência, ele **as combina horizontalmente**, ou seja, na mesma linha.

Vamos criar um arquivo chamado `sample2.txt` com o seguinte conteúdo:

```
The
quick
brown
fox
```

### Combinando as linhas com o `paste`

Podemos combinar todas essas linhas em uma única linha com o comando:

```bash
paste -s sample2.txt
```

- O `-s` (de "serial") diz para o `paste` combinar as linhas **uma após a outra, na mesma linha**, em vez de combiná-las por colunas.
- Por padrão, o delimitador usado será um **TAB**. Assim, o resultado será:

```
The    quick    brown    fox
```

(Os espaços representam os TABs aqui.)

### Mudando o delimitador

Se quisermos usar um **espaço simples** ao invés de TAB, podemos usar a opção `-d` (delimiter):

```bash
paste -d ' ' -s sample2.txt
```

Agora, o resultado será:

```
The quick brown fox
```

Esse comando é muito útil quando você quer transformar linhas em colunas ou juntar conteúdo em uma só linha com um separador personalizado.
