# Comando sort

O comando `sort` é útil para ordenar linhas de um arquivo.

Por exemplo, dado o arquivo `file1.txt` com o conteúdo:

```
dog
cow
cat
elephant
bird
```

Se você executar:

```
sort file1.txt
```

O resultado será:

```
bird
cat
cow
dog
elephant
```

Você também pode ordenar em ordem inversa usando a flag `-r`:

```
sort -r file1.txt
```

O resultado será:

```
elephant
dog
cow
cat
bird
```

Além disso, é possível ordenar por valor numérico com a flag `-n`:

```
sort -n file1.txt
```

No exemplo acima, como o arquivo contém palavras e não números, a ordenação numérica não faz sentido e o resultado será igual ao ordenado alfabeticamente.
