# Comandos expand e unexpand

Durante nossa lição sobre o comando `cut`, utilizamos o arquivo `sample.txt`, que continha um caractere TAB. 

Normalmente, TABs são visíveis como espaçamentos maiores, mas alguns editores de texto ou arquivos não mostram essa diferença de forma clara. Além disso, ter TABs em um arquivo pode não ser o tipo de espaçamento que você deseja.

Para converter TABs em espaços, usamos o comando `expand`.

```
expand sample.txt
```

O comando acima imprimirá a saída com cada TAB convertido em um grupo de espaços. Para salvar esse resultado em um novo arquivo, podemos usar redirecionamento de saída:

```
expand sample.txt > result.txt
```

O oposto de `expand` é o comando `unexpand`, que converte grupos de espaços de volta em TABs. Para isso, usamos a flag `-a`:

```
unexpand -a result.txt
```
