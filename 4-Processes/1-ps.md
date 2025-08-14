# 1. ps (Processos)

Processos são os programas que estão sendo executados na sua máquina. Eles são gerenciados pelo kernel, e cada processo possui um ID associado chamado **Process ID (PID)**. Esse PID é atribuído na ordem em que os processos são criados.

> **Comentário:** O PID é único no momento da execução, mas pode ser reutilizado depois que um processo termina.

## Comando PS
Execute o comando `ps` para ver uma lista de processos em execução:

```bash
$ ps
```
Saída de exemplo:
```bash
PID TTY STAT TIME CMD
41230 pts/4 Ss 00:00:00 bash
51224 pts/4 R+ 00:00:00 ps
```
Isso mostra um snapshot rápido dos processos atuais:

- **PID:** Identificador do processo  
- **TTY:** Terminal de controle associado ao processo (vamos ver isso em detalhes mais tarde)  
- **STAT:** Código de status do processo  
- **TIME:** Tempo total de uso de CPU  
- **CMD:** Nome do executável/comando  

Se você olhar a página de manual (`man`) do comando `ps`, verá que existem várias opções que podem ser passadas, e elas variam dependendo do estilo que você quer usar: **BSD**, **GNU** ou **Unix**.  
Na prática, o estilo **BSD** é mais popular, então vamos usar esse.

> **Comentário:** A principal diferença entre os estilos é a quantidade de traços (`-`) e os flags que acompanham.

```bash
$ ps aux
```
- **a** → Mostra todos os processos em execução, incluindo os de outros usuários.  
- **u** → Mostra mais detalhes sobre os processos.  
- **x** → Lista todos os processos que não têm um TTY associado (ex.: processos de daemon iniciados com o sistema).  
  - Esses programas aparecem com `?` no campo TTY.  

Agora você verá muito mais campos. Não é necessário decorar todos neste momento, pois veremos novamente em um curso mais avançado sobre processos:

- **USER:** Usuário efetivo (aquele cujos privilégios estão sendo usados)  
- **PID:** Identificador do processo  
- **%CPU:** Tempo de CPU usado dividido pelo tempo em que o processo está em execução  
- **%MEM:** Proporção do uso de memória física pelo processo  
- **VSZ:** Uso de memória virtual de todo o processo  
- **RSS:** Resident Set Size, a parte da memória física utilizada pelo processo que não foi trocada para o swap  
- **TTY:** Terminal de controle associado  
- **STAT:** Código de status do processo  
- **START:** Hora de início do processo  
- **TIME:** Tempo total de uso de CPU  
- **COMMAND:** Nome do executável/comando  

O comando `ps` pode gerar uma saída um pouco poluída. Por enquanto, os campos mais importantes para observar são **PID**, **STAT** e **COMMAND**.

## Comando TOP
Outro comando muito útil é o `top`.  
O `top` fornece informações **em tempo real** sobre os processos, ao contrário do `ps`, que mostra apenas um snapshot. Por padrão, a tela é atualizada a cada 10 segundos.

> **Comentário:** O `top` é excelente para identificar processos que estão consumindo mais recursos do sistema.

