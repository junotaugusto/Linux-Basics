# 3. Process Details

Antes de entrarmos em aplicações práticas de processos, precisamos primeiro entender **o que eles são e como funcionam**. Essa parte pode ser um pouco confusa, já que vamos entrar em detalhes mais técnicos, então sinta-se à vontade para voltar a essa lição mais tarde se quiser.

Um **processo**, como mencionamos antes, é um **programa em execução** no sistema. Mais precisamente, é o **sistema alocando memória, CPU e I/O** para fazer o programa rodar.  

> **Comentário:** Um processo não é apenas o arquivo do programa em disco, mas a instância ativa dele na memória com todos os recursos que ele usa.

Um processo é, portanto, **uma instância de um programa em execução**. Exemplo prático: abra **três janelas de terminal**.  
- Nas duas primeiras, rode o comando `cat` sem opções (o `cat` vai ficar aberto esperando entrada pelo stdin).  
- Na terceira janela, rode:
```bash
ps aux | grep cat
```
Você verá dois processos cat, mesmo que estejam chamando o mesmo programa.
O kernel é responsável por gerenciar os processos. Quando você executa um programa:
**1** - O kernel carrega o código do programa na memória
**2** - Determina e aloca os recursos necessários
**3** - Mantém controle sobre cada processo, sabendo:
    - O status do processo
    - Os recursos que o processo está usando e recebendo
    - O proprietário do processo
    - O tratamento de sinais (signal handling) — veremos mais adiante
    - E basicamente tudo sobre o processo

Todos os processos estão “disputando” recursos do sistema, e é função do kernel garantir que cada processo receba a quantidade adequada de recursos, conforme sua demanda. Quando um processo termina, os recursos que ele estava usando são liberados para outros processos.

**Comentário:** É como um gerente de recursos que distribui memória, CPU e tempo de I/O entre todos os processos do sistema.