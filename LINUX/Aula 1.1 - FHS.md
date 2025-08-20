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

## Diretório `/usr`

- O diretório `/usr` armazena **programas, bibliotecas, documentação e outros arquivos de suporte** para os usuários e para o sistema.  
- Historicamente, `/usr` era considerado “Unix System Resources” e continha programas que não eram essenciais para o boot (diferente de `/bin` e `/sbin`).  
- Hoje, em muitas distribuições modernas, há **unificação de diretórios** (ex.: `/bin` → `/usr/bin`), mas o conceito original ainda é mantido para fins de organização e compatibilidade.

### Diretórios chave dentro de `/usr`

- `/usr/bin` → contém binários executáveis disponíveis para **todos os usuários** (a maioria dos programas comuns do sistema está aqui).  
- `/usr/sbin` → contém binários administrativos do sistema. Normalmente requer privilégios de root para execução.  
- `/usr/lib` → contém **bibliotecas compartilhadas** necessárias para os programas em `/usr/bin` e `/usr/sbin`.  
- `/usr/local` → usado para software instalado **fora do sistema de pacotes da distribuição**.  
  - Muito útil para programas compilados manualmente.  
- `/usr/share` → contém arquivos **compartilhados e independentes de arquitetura**, como documentação, ícones, manuais, arquivos de configuração padrão.  
- `/usr/src` → contém **código-fonte** de programas e do kernel (em algumas distros, usado para desenvolvimento e compilação).

### Por que `/usr` é importante?

- **Execução de programas**: `/usr/bin` e `/usr/sbin` são essenciais para rodar a maioria dos comandos e serviços.  
- **Compartilhamento de bibliotecas**: `/usr/lib` garante eficiência ao permitir que vários programas utilizem as mesmas bibliotecas.  
- **Instalação de software**: muitos pacotes de software são instalados dentro de `/usr`, mantendo a organização do sistema.  
- **Documentação do sistema**: `/usr/share/doc` contém manuais, licenças e guias de programas instalados.  

### Pontos chave

- **Read-Only**: Em ambientes corporativos ou de produção, `/usr` pode ser montado como **somente leitura** (read-only), já que não deve ser alterado constantemente.  
- **Package Management**: O conteúdo de `/usr` geralmente é gerenciado pelo sistema de pacotes da distribuição (apt, yum/dnf, pacman, etc.).  
- **User Access**: Programas em `/usr/bin` podem ser executados por todos os usuários, mas arquivos administrativos em `/usr/sbin` normalmente exigem privilégios elevados.  

## Diretório `/opt`

O diretório `/opt` é utilizado para armazenar **pacotes de software adicionais** que não fazem parte do sistema base. Ele foi projetado para instalação de softwares **opcionais**, normalmente provenientes de **terceiros** ou fora do ciclo padrão de pacotes da distribuição.

---

### Por que utilizar?

- **Organização** → Mantém softwares que não fazem parte do sistema base em um local separado, facilitando manutenção e remoção.  
- **Isolamento** → Evita conflitos entre pacotes e bibliotecas de softwares diferentes.  
- **Flexibilidade** → Permite instalação manual ou via scripts sem interferir no restante do sistema.  

---

### Estrutura típica em `/opt`

Quando um software é instalado em `/opt`, geralmente cria um diretório próprio com o nome do pacote.  Exemplo: se você instalar o **MySQL Data Server**, ele pode criar:  
/opt/mysql/
├── bin/ (executáveis)
├── lib/ (bibliotecas)
├── etc/ (configurações do software)
├── data/ (arquivos e bases de dados)
└── doc/ (documentação)


Assim, tudo relacionado ao software fica **contido em um único diretório**, facilitando migração ou remoção.

### Pontos-chave

- **Permissão e posse** → Dependem do software; alguns exigem privilégios de root para instalação.  
- **Gerenciamento de pacotes** →  
  - Softwares instalados via **gerenciador de pacotes** (APT, DNF, etc.) normalmente não usam `/opt`.  
  - Softwares de terceiros ou instalados **manualmente** (ex.: download de tar.gz, binários proprietários, jogos, IDEs) costumam ficar em `/opt`.  
- **Configuração** → Alguns softwares armazenam seus arquivos de configuração em `/opt`, outros seguem o padrão e utilizam `/etc`.  
- **Limpeza** → Ao remover um software instalado em `/opt`, é responsabilidade do administrador excluir todos os arquivos/diretórios associados.  

---

## Observações importantes

- `/opt` é **menos usado em distribuições modernas** quando comparado a `/usr/local`.  
- A diferença é:  
  - `/usr/local` → software **compilado/instalado pelo administrador** a partir do código-fonte.  
  - `/opt` → software de **terceiros**, geralmente distribuído como pacote fechado ou pré-compilado.  

## Diretório `/dev`

- **Um virtual filesystem** que representa dispositivos de hardware em forma de arquivos.  
- Permite que o sistema operacional interaja com os hardwares usando **operações padrão de arquivos** (abrir, ler, escrever, fechar).  

### Exemplos
- **/dev/sda, /dev/sdb** → discos rígidos ou SSDs.  
- **/dev/cdrom** → unidade de CD/DVD.  
- **/dev/ttyUSB0, /dev/ttyUSB1** → portas seriais/USB.  
- **/dev/null** → "buraco negro", descarta dados escritos nele.  
- **/dev/zero** → gera uma sequência infinita de zeros (usado para testes, preenchimento de discos, etc).  

### Por que é importante?
- **Device Abstraction** → ao tratar dispositivos como arquivos, o Linux fornece uma interface **consistente** para interagir com diversos hardwares.  
- **Drivers de dispositivos** → drivers criam os arquivos em `/dev` que representam o hardware no sistema.  
- **Interação com o usuário** → usuários podem acessar e controlar dispositivos utilizando comandos como `dd`, `hdparm`, entre outros.  

### Pontos Chave
- **Criação dinâmica** → arquivos de dispositivos são criados automaticamente (via `udev`) quando plugamos algum dispositivo ou ao reiniciar o sistema.  
- **Permissões** → geralmente apenas o usuário **root** tem acesso direto aos arquivos em `/dev`.  
- **Drivers de dispositivos** → o driver correto precisa estar instalado e carregado para que o dispositivo apareça em `/dev`.  

## Diretório `/tmp`

O diretório **/tmp** é utilizado para armazenar arquivos temporários criados por programas e pelo próprio sistema.  
Seu conteúdo é **volátil** e normalmente é apagado quando o sistema reinicia ou após um período de tempo definido. É 

### Características
- **Armazenamento temporário**: usado por aplicações e processos para guardar arquivos que só são necessários durante a execução.
- **Acesso de múltiplos usuários**: é um diretório acessível por qualquer usuário do sistema.
- **Permissões especiais (Sticky Bit)**: normalmente configurado com a permissão `1777`, o que significa:
  - Todos os usuários podem **criar arquivos**.
  - Somente o **dono** do arquivo (ou o root) pode **apagá-lo**.

### Exemplos de uso
- Navegadores salvando arquivos temporários durante downloads.
- Aplicativos que criam arquivos de lock (ex.: `.X0-lock`).
- Scripts ou programas que precisam de espaço temporário para processamento de dados.

### Importância
- **Desempenho**: evita que programas precisem criar arquivos permanentes apenas para uso rápido.
- **Segurança**: o sticky bit protege arquivos de usuários contra exclusão por outros.
- **Limpeza automática**: garante que o sistema não fique acumulando lixo após reinicializações.

### Pontos chave
- O conteúdo de `/tmp` **não deve ser considerado permanente**.
- Arquivos grandes e temporários podem ser escritos aqui, mas há risco de perda após reboot.
- É um dos alvos de segurança mais monitorados, pois qualquer usuário pode gravar nele.
- Algumas distribuições configuram `/tmp` como parte da memória (tmpfs), aumentando a velocidade de acesso.

## Outros Diretórios Importantes no Linux

### Diretório `/boot`
- Contém os arquivos necessários para o **processo de inicialização** do sistema.
- Normalmente inclui:
  - Kernel do Linux (`vmlinuz`).
  - Ramdisk inicial (`initrd` ou `initramfs`).
  - Configurações do bootloader (ex.: GRUB).
- Importância:
  - Sem os arquivos do `/boot`, o sistema não consegue iniciar.
  - Em alguns sistemas, pode estar em uma **partição separada** para facilitar a recuperação.

### Diretório `/mnt`
- Usado como **ponto de montagem temporário** para sistemas de arquivos.
- Exemplo:
  - Montar um dispositivo manualmente:  
    ```bash
    mount /dev/sdb1 /mnt
    ```
- Importância:
  - Serve para acessos rápidos de dispositivos de forma temporária.
  - Montagens permanentes geralmente usam `/media` ou diretórios personalizados em `/mnt`.

### Diretório `/proc`
- É um **filesystem virtual** que expõe informações do kernel e dos processos em tempo real.
- Características:
  - Não ocupa espaço em disco (é gerado pelo kernel).
  - Exemplos:
    - `/proc/cpuinfo` → informações sobre o processador.
    - `/proc/meminfo` → informações de memória.
    - `/proc/[PID]/` → informações sobre processos específicos.
- Importância:
  - Ferramenta de **diagnóstico** e **monitoramento**.
  - Usado por comandos como `ps`, `top`, `free`, etc.

### Diretório `/srv`
- Significa **"service"**.
- Usado para armazenar dados servidos por serviços de rede.
- Exemplos:
  - `/srv/ftp` → arquivos de um servidor FTP.
  - `/srv/www` → conteúdo de um servidor web.
- Importância:
  - Ajuda a manter a organização do sistema, separando dados de serviços de outros diretórios.

### Diretório `/sys`
- Outro **filesystem virtual**, introduzido com o kernel 2.6.
- Contém informações sobre dispositivos, drivers e subsistemas do kernel.
- Diferença em relação ao `/proc`:
  - `/proc` → foco em processos e status do sistema.
  - `/sys` → foco em **dispositivos e kernel modules**.
- Exemplo:
  - `/sys/class/net/` → informações sobre interfaces de rede.
- Importância:
  - Permite que administradores e programas **interajam diretamente com dispositivos**.
  - Usado por ferramentas como `udev` para gerenciar hardware em tempo real.