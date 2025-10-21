## 2. stdin (Entrada Padrão)

Na lição anterior, aprendemos que temos diferentes fluxos de saída padrão (stdout) que podemos usar, como um arquivo ou a tela. 

Pois bem, também existem diferentes fluxos de entrada padrão (stdin) que podemos utilizar. Sabemos que temos entrada padrão vinda de dispositivos como o teclado, mas também podemos usar arquivos, a saída de outros processos e o terminal. Vamos ver um exemplo.

Vamos usar o arquivo `peanuts.txt` da lição anterior para este exemplo — lembre-se de que ele continha o texto *Hello World*.

```bash
$ cat < peanuts.txt > banana.txt
```

Assim como usamos `>` para redirecionar a saída padrão (stdout), podemos usar `<` para redirecionar a entrada padrão (stdin).

Normalmente, no comando `cat`, você passa um arquivo para ele e esse arquivo se torna a entrada padrão. Neste caso, redirecionamos `peanuts.txt` para ser a nossa entrada padrão. Em seguida, a saída do comando `cat peanuts.txt`, que seria *Hello World*, é redirecionada para outro arquivo chamado `banana.txt`.
