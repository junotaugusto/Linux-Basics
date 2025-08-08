# Comandos join e split

O comando `join` permite unir múltiplos arquivos com base em um campo comum.

Por exemplo, se tivermos dois arquivos:

**file1.txt**
```
1 John
2 Jane
3 Mary
```

**file2.txt**
```
1 Doe
2 Doe
3 Sue
```

Ao executar:

```
join file1.txt file2.txt
```

O resultado será:

```
1 John Doe
2 Jane Doe
3 Mary Sue
```

A junção foi feita com base no primeiro campo de cada arquivo, que neste caso são os números 1, 2 e 3. Por padrão, o `join` usa o primeiro campo e ele precisa ter valores idênticos nos dois arquivos. Caso não estejam na mesma ordem, podemos ordenar antes.

Se tivermos arquivos assim:

**file1.txt**
```
John 1
Jane 2
Mary 3
```

**file2.txt**
```
1 Doe
2 Doe
3 Sue
```

Para unir, precisamos indicar qual campo de cada arquivo usar. Nesse caso, queremos o campo 2 do `file1.txt` e o campo 1 do `file2.txt`:

```
join -1 2 -2 1 file1.txt file2.txt
```

O resultado será:

```
1 John Doe
2 Jane Doe
3 Mary Sue
```

A opção `-1` se refere ao primeiro arquivo e `-2` ao segundo.

O comando `split` serve para dividir um arquivo em múltiplos arquivos menores:

```
split somefile
```

Por padrão, ele divide o arquivo em partes de até 1000 linhas cada. Os arquivos gerados têm nomes começando com `x` seguidos de letras.
