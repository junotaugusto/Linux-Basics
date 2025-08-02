# stdout (Saída Padrão)

Até agora, já nos familiarizamos com alguns comandos e suas saídas, o que nos leva ao nosso próximo assunto: fluxos de E/S (entrada/saída). Vamos executar o seguinte comando e discutir como isso funciona.

```bash
$ echo Hello World > peanuts.txt
```

O que acabou de acontecer? Bem, verifique o diretório onde você executou esse comando e, veja só, você deverá ver um arquivo chamado `peanuts.txt`. 

Olhe dentro desse arquivo e deverá ver o texto *"Hello World"*. Muitas coisas aconteceram em um único comando, então vamos dividi-lo.

Primeiro, vamos analisar a primeira parte:

```bash
$ echo Hello World
```

Sabemos que isso imprime *"Hello World"* na tela, mas como? Processos usam fluxos de E/S para receber **entrada** e retornar **saída**. Por padrão, o comando `echo` recebe a entrada (entrada padrão ou `stdin`) do teclado e retorna a saída (saída padrão ou `stdout`) para a tela. 

É por isso que, quando você digita `echo Hello World` no seu shell, você vê *"Hello World"* na tela. No entanto, a **redireção de E/S** nos permite mudar esse comportamento padrão, dando-nos maior flexibilidade com arquivos.

Vamos prosseguir para a próxima parte do comando:

```
>
```

O `>` é um operador de redirecionamento que nos permite alterar para onde a saída padrão vai. Ele nos permite enviar a saída do `echo Hello World` para um arquivo em vez da tela. 

Se o arquivo ainda não existir, ele será criado. No entanto, **se já existir, ele será sobrescrito** (você pode adicionar uma flag do shell para evitar isso, dependendo do shell que estiver usando).

E é basicamente assim que funciona a redireção do `stdout`!

Bem, digamos que eu não queira sobrescrever meu `peanuts.txt`. Felizmente, existe um operador de redirecionamento para isso também, o `>>`:

```bash
$ echo Hello World >> peanuts.txt
```

Isso irá adicionar "Hello World" ao final do arquivo `peanuts.txt`. Se o arquivo ainda não existir, ele será criado da mesma forma que com o redirecionador `>`!
