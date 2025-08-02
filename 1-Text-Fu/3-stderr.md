## 3. stderr (Erro Padrão)

Vamos tentar algo um pouco diferente agora: listar o conteúdo de um diretório que não existe no seu sistema e redirecionar a saída para o arquivo `peanuts.txt` novamente.

```bash
$ ls /fake/directory > peanuts.txt
```

O que você deve ver é:

```
ls: cannot access /fake/directory: No such file or directory
```

Agora você deve estar pensando: essa mensagem não deveria ter sido enviada para o arquivo? Na verdade, há outro fluxo de entrada/saída envolvido aqui chamado **erro padrão** (*stderr*). 

Por padrão, o `stderr` envia sua saída para a tela também, mas é um fluxo completamente diferente do `stdout`. Portanto, você precisa redirecionar essa saída de uma forma diferente.

Infelizmente, o redirecionamento não é tão simples quanto usar `<` ou `>`, mas é bem parecido. Precisaremos usar **descritores de arquivos**. Um descritor de arquivo é um número não-negativo usado para acessar um arquivo ou fluxo. Vamos nos aprofundar nisso mais adiante, mas por enquanto saiba que os descritores para `stdin`, `stdout` e `stderr` são 0, 1 e 2, respectivamente.

Agora, se quisermos redirecionar o `stderr` para um arquivo, podemos fazer assim:

```bash
$ ls /fake/directory 2> peanuts.txt
```

Você deve ver apenas as mensagens de erro no arquivo `peanuts.txt`.

E se eu quiser ver tanto o `stderr` quanto o `stdout` no arquivo `peanuts.txt`? É possível fazer isso também usando descritores de arquivos:

```bash
$ ls /fake/directory > peanuts.txt 2>&1
```

Esse comando envia o resultado de `ls /fake/directory` para o arquivo `peanuts.txt` e, em seguida, redireciona o `stderr` para o mesmo destino do `stdout` com `2>&1`. 

A **ordem das operações** aqui importa: `2>&1` envia o `stderr` para onde quer que o `stdout` esteja apontando. Neste caso, o `stdout` está apontando para o arquivo, então `stderr` também será enviado para o mesmo arquivo. Assim, se você abrir o `peanuts.txt`, verá tanto o `stdout` quanto o `stderr`. No nosso caso, o comando acima gera apenas `stderr`.

Existe uma forma mais curta de redirecionar ambos `stdout` e `stderr` para um arquivo:

```bash
$ ls /fake/directory &> peanuts.txt
```

Agora, e se eu não quiser nenhuma dessas mensagens e quiser **descartar** completamente o `stderr`? Você pode redirecionar a saída para um arquivo especial chamado `/dev/null`, e isso fará com que qualquer entrada seja descartada.

```bash
$ ls /fake/directory 2> /dev/null
```
