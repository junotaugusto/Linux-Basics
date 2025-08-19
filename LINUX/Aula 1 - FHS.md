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

## Diretório `/sbin`

- Contém **binários executáveis usados principalmente para administração do sistema**.  
- Normalmente, esses comandos exigem **privilégios de root**, pois envolvem alterações críticas que afetam o funcionamento do sistema operacional.  
- São usados por **administradores de sistema (sysadmins)** em tarefas como inicialização, desligamento, reparo de discos e gerenciamento de partições.  

### Exemplos de comandos comuns em `/sbin`

- `fdisk` → manipula tabelas de partição em discos.  
- `fsck` → verifica e repara sistemas de arquivos.  
- `init` → processo inicial que dá início à inicialização do sistema (nas distribuições modernas, muitas vezes substituído por `systemd`).  
- `reboot` → reinicia o sistema.  
- `shutdown` → desliga ou reinicia o sistema de forma controlada.  

### Informações complementares

- **Usuário comum vs root**:  
  - Usuários comuns geralmente **não têm permissão** para executar diretamente esses comandos.  
  - Eles podem, no entanto, usar ferramentas como `sudo`, que significa **super user do (superusuário faz)**  para executar determinadas tarefas administrativas.  

- **Mudança em distribuições modernas**:  
  Assim como aconteceu com `/bin`, muitas distribuições modernas **unificaram** o `/sbin` dentro de `/usr/sbin`.  
  - `/sbin` → link simbólico para `/usr/sbin`.  

- **Diferença histórica entre `/bin` e `/sbin`**:  
  - `/bin` → comandos essenciais usados tanto por usuários comuns quanto pelo sistema.  
  - `/sbin` → comandos essenciais voltados para **administração e manutenção do sistema**.  

## Diretório `/etc`

- Contém **arquivos de configuração** do sistema operacional e de diversos serviços e aplicativos.  
- Pode ser considerado o **“Control Center”** do sistema, já que praticamente toda a configuração do Linux é feita através de arquivos de texto localizados nesse diretório.  
- O conteúdo do `/etc` pode variar de acordo com a **distribuição do Linux** utilizada e com os **softwares instalados**.  

### Características importantes

- Todos os arquivos em `/etc` são, em geral, **arquivos de texto simples**.  
- Podem ser editados com qualquer editor de texto (como `nano`, `vim` ou `gedit`).  
- A edição desses arquivos normalmente requer privilégios de **root**.  

### Exemplos de arquivos e diretórios em `/etc`

- `/etc/passwd` → informações básicas sobre usuários do sistema.  
- `/etc/shadow` → senhas (criptografadas) dos usuários.  
- `/etc/group` → informações sobre grupos de usuários.  
- `/etc/fstab` → lista de sistemas de arquivos a serem montados na inicialização.  
- `/etc/hosts` → mapeamento de endereços IP para nomes de host.  
- `/etc/hostname` → nome do host (computador) no sistema.  
- `/etc/network/` → configuração de rede (dependendo da distro).  
- `/etc/ssh/` → configurações do servidor SSH.
- `/etc/resolv.conf`→ configurações do DNS.


### Informações complementares

- A **estrutura do `/etc`** é um dos pontos mais sensíveis do Linux.  
  - Configurações incorretas podem comprometer a inicialização, a segurança ou a conectividade da máquina.  
- Muitos serviços (como Apache, Nginx, MySQL, SSH, etc.) armazenam suas configurações em subdiretórios dentro de `/etc`.  
- Uma boa prática é **fazer backup de arquivos de configuração antes de editá-los**, para poder restaurar caso algo dê errado.  

### Subdiretórios e arquivos importantes dentro de `/etc`

O diretório `/etc` contém não apenas arquivos, mas também subdiretórios específicos para cada serviço instalado no sistema. Alguns exemplos importantes:

#### `/etc/apache2`

- Contém os arquivos de configuração do **servidor web Apache**.  
- Permite configurar virtual hosts, módulos, diretivas de segurança, logs e muito mais.  
- Arquivos relevantes:
  - `apache2.conf` → configuração principal do Apache.
  - `sites-available/` e `sites-enabled/` → configuração de sites virtual hosts.
  - `mods-available/` e `mods-enabled/` → configuração de módulos do Apache.

#### `/etc/nginx`

- Contém os arquivos de configuração do **servidor web Nginx**.  
- Permite definir servidores virtuais, redirecionamentos, caches e regras de segurança.  
- Arquivos relevantes:
  - `nginx.conf` → configuração principal do Nginx.
  - `sites-available/` e `sites-enabled/` → configuração de sites virtuais (como no Apache).

#### `/etc/mysql/my.cnf`

- Arquivo de configuração principal do **MySQL** (ou MariaDB em algumas distros).  
- Define parâmetros como portas de conexão, diretórios de dados, buffers de memória, logs e permissões.  
- Pode ser dividido em seções `[client]`, `[mysqld]`, `[mysqld_safe]` para diferentes componentes do MySQL.

#### `/etc/postgresql/postgresql.conf`

- Arquivo de configuração principal do **PostgreSQL**.  
- Controla parâmetros de desempenho, autenticação, logs, conexão e replicação.  
- É possível ajustá-lo para otimizar o banco de dados de acordo com a carga de trabalho.

#### `/etc/ssh/sshd_config`

- Arquivo de configuração do **servidor SSH** (`sshd`).  
- Permite definir:
  - Portas de conexão.
  - Métodos de autenticação.
  - Controles de acesso de usuários.
  - Configurações de segurança como desabilitar login de root remoto.

### Informações complementares

- **Backup antes de alterar**: Antes de editar qualquer arquivo nesses diretórios, é **essencial criar uma cópia de segurança** para restaurar em caso de problemas.  
- **Reiniciar serviços**: Após alterações em arquivos de configuração de serviços (`apache2`, `nginx`, `mysql`, `postgresql`, `ssh`), geralmente é necessário **reiniciar o serviço** para que as mudanças tenham efeito. Exemplos:

```bash
sudo systemctl restart apache2
sudo systemctl restart nginx
sudo systemctl restart mysql
sudo systemctl restart postgresql
sudo systemctl restart sshd
```
## Diretório `/home`

- É o **local onde ficam as contas de usuário** do sistema Linux.  
- Serve como **localização primária para arquivos pessoais, documentos, configurações e preferências de cada usuário**.  
- Cada usuário possui um **subdiretório próprio** dentro de `/home`.  
  - Exemplo: `/home/junot` para o usuário `junot`.  

### Subdiretórios comuns dentro do diretório de cada usuário

- `Documents` → documentos do usuário.  
- `Downloads` → arquivos baixados da internet.  
- `Music` → arquivos de áudio.  
- `Pictures` → imagens e fotos.  
- `Public` → arquivos compartilhados com outros usuários.  
- `Videos` → arquivos de vídeo.  

> Observação: o conteúdo exato dos subdiretórios pode variar conforme o ambiente de desktop ou preferências do usuário.

### Permissões em `/home`

- **User Ownership (propriedade do usuário)**:  
  - Cada subdiretório é de propriedade do usuário correspondente.  
  - Apenas o dono e o root podem modificar arquivos e pastas dentro do diretório pessoal, a não ser que permissões adicionais sejam concedidas.  

- **Permissions (permissões)**:  
  - Linux usa o modelo **user/group/others** para definir permissões de leitura (`r`), escrita (`w`) e execução (`x`).  
  - Exemplo de visualização de permissões:  
    ```bash
    ls -l /home
    ```
  - Permite verificar quem pode acessar ou modificar cada pasta e arquivo.  

- **Personalização**:  
  - Cada usuário pode customizar seu ambiente dentro do `/home`, como temas, arquivos de configuração de aplicativos (`.config`) e outros ajustes pessoais.  
  - Esses arquivos de configuração geralmente ficam ocultos (começam com `.`) e são carregados automaticamente pelos aplicativos e pelo sistema.
- **Data Storage (armazenamento de dados)**:  
  - `/home` é o local principal onde os usuários armazenam seus **arquivos pessoais, documentos, mídia e configurações**.  
  - É importante gerenciar bem o espaço para evitar problemas de disco cheio.

- **Security (segurança)**:  
  - Diretórios dentro de `/home` são **protegidos contra acessos não autorizados**.  
  - Usuários comuns **não podem acessar o diretório pessoal de outros usuários** sem permissões específicas.  
  - O root, porém, pode acessar qualquer diretório.

### Boas práticas em `/home`

- **Notas importantes**:  
  - **Backup regularmente**: Faça backups frequentes dos arquivos importantes para evitar perda de dados.  
  - **File Permissions (permissões de arquivos)**: Garanta que cada arquivo e pasta tenha as permissões corretas para **proteger informações pessoais e confidenciais**.  
  - **Storage Limits (limites de armazenamento)**: Administradores podem definir limites de espaço para usuários, evitando que um único usuário consuma todo o disco.  
  - **Organization (organização)**: Mantenha o diretório pessoal bem organizado em subpastas (`Documents`, `Downloads`, `Music`, etc.) para facilitar o acesso e gerenciamento.

  ## Diretório `/var`

- O diretório `/var` armazena **dados que variam e mudam frequentemente** durante a operação do sistema.  
- Contém arquivos **dinâmicos**, como logs, arquivos temporários, mail spools e informações de estado de aplicativos.

### Diretórios chave dentro de `/var`

- `/var/log` → arquivos de log do sistema e aplicativos. **Importante para cibersegurança, troubleshooting e monitoramento do sistema.**  
- `/var/mail` → armazenagem de emails do sistema.  
- `/var/spool` → filas de impressão, e-mails e outros jobs em espera.  
- `/var/lib` → arquivos de estado de aplicativos que precisam persistir entre reinicializações.  
- `/var/tmp` → arquivos temporários que precisam persistir entre reinicializações. **Não deve ser confundido com `/tmp`**, que é para arquivos temporários de curta duração.

### Por que `/var` é importante?

- **System Health Monitoring** → logs e arquivos dinâmicos ajudam a acompanhar a saúde do sistema.  
- **Análises de segurança** → arquivos de log permitem identificar atividades suspeitas e ataques.  
- **Operações de serviços** → muitas aplicações dependem de diretórios em `/var` para funcionar corretamente.  
- **Application State** → dados de estado de aplicativos são mantidos aqui, garantindo continuidade entre reinicializações.

### Considerações importantes

- **Regular Cleanup** → manter `/var` limpo evita que o disco fique cheio.  
- **Log Rotation** → arquivos de log devem ser rotacionados para não ocuparem espaço excessivo (`logrotate`).  
- **Permissions** → apenas usuários e serviços autorizados devem ter acesso de escrita.  
- **Backup** → arquivos críticos de `/var` devem ser incluídos em políticas de backup, principalmente logs e bancos de dados de aplicativos.
