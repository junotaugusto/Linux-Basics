# Comando grep

O comando `grep` é possivelmente o comando de processamento de texto mais comum que você usará. Ele permite procurar dentro de arquivos por caracteres que correspondam a um determinado padrão.  

Por exemplo, se você quiser saber se um arquivo contém uma palavra específica ou se uma determinada string está presente, não precisará verificar manualmente cada linha — basta usar `grep`.  

Usando nosso arquivo `sample.txt` como exemplo:  

```
grep fox sample.txt
```

Isso fará com que `grep` localize a palavra `fox` dentro de `sample.txt`.  

Você também pode pesquisar ignorando maiúsculas e minúsculas com a flag `-i`:  

```
grep -i somepattern somefile
```

Para tornar o uso do `grep` ainda mais flexível, você pode combiná-lo com outros comandos usando o operador `|` (pipe):  

```
env | grep -i User
```

Assim, é possível filtrar a saída de outros comandos.  

O `grep` também suporta expressões regulares, permitindo buscas mais avançadas. Por exemplo:  

```
ls /somedir | grep '.txt$'
```

Esse comando retornará todos os arquivos terminados com `.txt` no diretório `somedir`.  
