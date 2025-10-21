## 4. pipe e tee

Vamos entrar agora em um pouco de "encanamento" — não literalmente, mas quase. Vamos tentar um comando:

```bash
$ ls -la /etc
```

Você deverá ver uma lista bem longa de itens — um pouco difícil de ler, na verdade. 

Em vez de redirecionar essa saída para um arquivo, não seria melhor se pudéssemos ver essa saída diretamente em outro comando, como o `less`? Pois bem, isso é possível!

```bash
$ ls -la /etc | less
```

O operador de pipe `|`, representado por uma barra vertical, permite que a saída padrão (`stdout`) de um comando seja usada como entrada padrão (`stdin`) de outro processo. 

Neste caso, pegamos o `stdout` do `ls -la /etc` e o passamos como `stdin` para o comando `less`.

O comando de pipe é extremamente útil, e continuaremos a utilizá-lo por toda a eternidade.

Agora, e se quisermos escrever a saída do nosso comando em dois lugares diferentes ao mesmo tempo? Isso é possível com o comando `tee`:

```bash
$ ls | tee peanuts.txt
```

Você verá a saída do `ls` na tela, e, se abrir o arquivo `peanuts.txt`, verá a mesma informação nele!
