# FHS (Filesystem Hierarchy Standard)

## Direrório `Root (/)`

- O diretório `/` (root) é o **diretório de nível mais alto** do sistema.
- Todos os outros diretórios do FHS estão dentro de `/`. Eles são organizados de forma **hierárquica**.
- Subdiretórios podem conter outros subdiretórios, todos sempre dentro de `/`.
- O dono do diretório `/` é o **usuário root**, que possui controle total sobre ele.
- A organização das estruturas e o conteúdo desses diretórios são **cruciais para a estabilidade e a segurança** do sistema. Por isso, todo cuidado aqui é pouco.
- Muitos pacotes de software são instalados em diretórios específicos dentro de `/`.
- Administradores de sistema (sysadmins) trabalham diretamente com a hierarquia de diretórios para manter e configurar o sistema.

### Informações complementares

- O **FHS (Filesystem Hierarchy Standard)** é um padrão que define como os diretórios devem ser organizados em sistemas do tipo Unix/Linux, garantindo **consistência entre diferentes distribuições**.
- Alguns diretórios principais:
  - `/bin` → binários essenciais do sistema.
  - `/etc` → arquivos de configuração.
  - `/home` → diretórios pessoais dos usuários.
  - `/root` → diretório pessoal do usuário root.
  - `/var` → arquivos variáveis (logs, spool, cache).
  - `/tmp` → arquivos temporários.
- Nem todas as distribuições seguem o FHS **de forma 100% idêntica**, mas a grande maioria mantém a estrutura básica para compatibilidade.

## Diretório `/bin`

- Contém os **binários executáveis essenciais** para o funcionamento do sistema.
- É usado principalmente durante o **processo de boot** e em **single-user mode**.
- Geralmente é **acessível a todos os usuários**.
- Os comandos dentro de `/bin` são fundamentais para operações básicas de gerenciamento de arquivos e navegação no sistema.

### Exemplos de comandos comuns em `/bin`

- `ls` → lista arquivos e diretórios.
- `cat` → concatena e mostra o conteúdo de arquivos.
- `cp` → copia arquivos e diretórios.
- `mv` → move ou renomeia arquivos e diretórios.
- `rm` → remove arquivos e diretórios.

### Evolução do diretório `/bin`

- **Antigamente**:  
  O diretório `/bin` armazenava apenas os **binários essenciais** para inicializar o sistema e permitir que ele fosse usado mesmo em modo de recuperação (single-user mode). 
   
  Já o diretório `/usr/bin` continha outros binários considerados "não essenciais", ou seja, programas adicionais para o uso cotidiano.  

  Isso acontecia porque o diretório `/usr` podia estar em **outra partição**, que não era montada imediatamente durante o boot. Dessa forma, o sistema precisava garantir que os comandos básicos estivessem sempre disponíveis em `/bin`, mesmo sem acesso ao `/usr`.

- **Hoje em dia**:  
  Em muitas distribuições modernas (Debian, Ubuntu, Fedora, entre outras), houve uma **unificação de diretórios**.  
  - O conteúdo de `/bin`, `/sbin`, `/lib` e `/lib64` foi movido para dentro de `/usr`.  
  - Para manter a compatibilidade com softwares antigos, foram criados **links simbólicos**:  
    - `/bin` → `/usr/bin`  
    - `/sbin` → `/usr/sbin`  
    - `/lib` → `/usr/lib`  

- **Por que essa mudança aconteceu?**  
  - Simplificação da estrutura do sistema de arquivos.  
  - Facilitar o gerenciamento e empacotamento de softwares.  
  - Reduzir redundâncias (já que havia duplicação de comandos entre `/bin` e `/usr/bin`).  

- **Conceito histórico**:  
  Apesar dessa mudança técnica, o conceito de `/bin` como “local dos binários essenciais” continua sendo ensinado, pois faz parte do **FHS** e ajuda a entender a evolução da organização dos diretórios no Linux.
