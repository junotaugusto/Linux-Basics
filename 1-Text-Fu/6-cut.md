## 6. Comando `cut`

Vamos aprender alguns comandos úteis para processar texto. Antes de começar, vamos criar um arquivo com o qual trabalharemos. Copie e cole o seguinte comando no terminal. Depois de colar, adicione uma TAB entre as palavras `lazy` e `dog` (use `Ctrl+v` seguido de `TAB` para inserir uma TAB literal):

```bash
echo 'The quick brown; fox jumps over the lazy  dog' > sample.txt
```

O primeiro comando que vamos aprender é o `cut`. Ele serve para extrair partes específicas de texto de um arquivo.

### Extrair conteúdo por número de caracteres

```bash
cut -c 5 sample.txt
```

Este comando exibe o 5º caractere de cada linha do arquivo. No exemplo acima, a saída será:

```
q
```

**Nota:** o espaço também conta como caractere.

### Extrair conteúdo por campo (field)

```bash
cut -f 2 sample.txt
```

A flag `-f` (field/campo) permite cortar o texto com base em campos. Por padrão, o `cut` usa TABs como delimitadores, ou seja, tudo o que está separado por TABs é considerado um campo diferente. Como adicionamos uma TAB entre `lazy` e `dog`, a saída será:

```
dog
```

### Extrair conteúdo por campo com delimitador personalizado

Você também pode usar um delimitador personalizado com a flag `-d` (delimiter):

```bash
cut -f 1 -d ";" sample.txt
```

Nesse caso, mudamos o delimitador padrão (TAB) para o ponto e vírgula `;`. Como estamos extraindo o primeiro campo (`-f 1`), a saída será:

```
The quick brown
```

Ou seja, tudo o que aparece antes do ponto e vírgula na linha.

Essas opções do comando `cut` são muito úteis para manipular e extrair informações específicas de arquivos de texto estruturados.
