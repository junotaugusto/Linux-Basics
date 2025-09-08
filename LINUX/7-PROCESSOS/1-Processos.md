# O que é um Processo

No contexto de **sistemas operacionais**, um **processo** é uma **instância de um programa em execução**. Em outras palavras, quando você executa um programa no computador, ele deixa de ser apenas um arquivo armazenado no disco e passa a existir como um processo ativo na memória do sistema.

## Características de um Processo

Um processo possui diversas informações que o sistema operacional utiliza para gerenciá-lo. Algumas são:

- **Identificador do processo (PID):** número único usado pelo sistema para identificar o processo.
- **Identificador do processo pai (PPID):** é o identificador do processo pai que criou o processo atual. 
- **Estado do processo:** indica se ele está pronto, em execução ou aguardando algum evento.

## Estados de um Processo

Um processo pode estar em diferentes estados durante sua execução:

1. **Novo:** processo foi criado, mas ainda não está pronto para executar.
2. **Pronto (Ready):** processo aguardando para ser executado pela CPU.
3. **Em execução (Running):** processo atualmente sendo executado pela CPU.
4. **Bloqueado (Waiting/Blocked):** processo aguardando algum evento, como a entrada de dados do usuário.
5. **Finalizado (Terminated):** processo terminou sua execução e está aguardando limpeza de recursos.

# O que é um Daemon

No contexto de **sistemas operacionais**, um **daemon** é um **processo em segundo plano** que é executado continuamente, geralmente iniciando junto com o sistema, e que **fornece serviços ou executa tarefas sem interação direta do usuário**.

## Características de Daemons

- **Execução em segundo plano:** não possuem interface gráfica ou terminal.
- **Início automático:** muitos daemons iniciam durante o boot do sistema.
- **Serviços contínuos:** ficam rodando aguardando eventos ou requisições, como acesso à rede ou tarefas agendadas.
- **Associados a serviços específicos:** por exemplo:
  - `sshd` → permite conexões SSH.
  - `cron` → executa tarefas agendadas.
  - `httpd` ou `nginx` → servidor web.
  - `systemd` → gerencia outros processos e serviços no Linux moderno.

Normalmente termina com o sulfixo `d` como `sshd` ou `crond`.

## Diferença entre processo comum e daemon

- **Processo comum:** geralmente iniciado por um usuário e pode ter interação direta.
- **Daemon:** iniciado pelo sistema ou outro processo e opera silenciosamente em segundo plano.

# Serviços

Em sistemas operacionais, **serviços** são programas ou processos que **executam tarefas específicas em segundo plano** e fornecem funcionalidades essenciais para o sistema ou para outros aplicativos. Eles são semelhantes aos **daemons**, especialmente em sistemas Unix/Linux.

Na verdade **um serviço é uma funcionalidade do sistema que pode ser fornecida por um ou mais daemons em segundo plano**. Por exemplo, o serviço `httpd` disponibiliza o servidor web Apache, cujo daemon é o processo que efetivamente roda essa funcionalidade

## Características dos Serviços

- **Execução contínua:** geralmente rodam durante todo o tempo em que o sistema está ativo.
- **Sem interface direta:** não exigem interação constante do usuário.
- **Iniciados automaticamente ou manualmente:** podem ser configurados para iniciar junto com o sistema ou quando solicitados.
- **Fornecem funções essenciais:** podem incluir redes, impressão, banco de dados, monitoramento de segurança, entre outros.

## Exemplos de Serviços

- **Linux/Unix:**
  - `sshd` → serviço de acesso remoto via SSH.
  - `cron` → serviço de agendamento de tarefas.
  - `nginx` ou `httpd` → serviços de servidor web.
  
- **Windows:**
  - `Windows Update` → atualizações automáticas do sistema.
  - `Print Spooler` → gerencia impressoras e filas de impressão.
  - `Windows Defender` → proteção em tempo real contra malware.

## Diferença entre Daemons e Serviços

- No **Linux/Unix**, um daemon é um tipo de serviço.
- No **Windows**, os serviços são a forma padrão de processos em segundo plano que fornecem funcionalidades contínuas ao sistema.

> Em resumo, **serviços são processos que rodam em segundo plano para manter funcionalidades essenciais do sistema ou disponibilizar recursos para outros programas**.

