# Tabela Resumida dos Diretórios do Linux

| Diretório  | Função Principal                                                                 |
|------------|----------------------------------------------------------------------------------|
| `/`        | Raiz do sistema de arquivos, ponto inicial de todos os diretórios.               |
| `/bin`     | Programas essenciais do sistema, disponíveis para todos os usuários.             |
| `/sbin`    | Programas administrativos e de manutenção do sistema.                           |
| `/usr`     | Programas, bibliotecas e arquivos de uso geral do sistema.                      |
| `/usr/bin` | Programas e utilitários para todos os usuários.                                 |
| `/usr/sbin`| Programas administrativos não essenciais.                                       |
| `/usr/local` | Programas instalados manualmente pelo administrador.                          |
| `/etc`     | Arquivos de configuração do sistema.                                            |
| `/etc/apache2` | Configurações do servidor Apache.                                           |
| `/etc/nginx`   | Configurações do servidor Nginx.                                            |
| `/etc/mysql/my.cnf` | Arquivo de configuração principal do MySQL.                            |
| `/etc/postgresql/postgresql.conf` | Arquivo de configuração do PostgreSQL.                   |
| `/etc/ssh/sshd_config` | Configuração do servidor SSH.                                       |
| `/var`     | Dados variáveis que mudam frequentemente (logs, cache, filas).                  |
| `/var/log` | Arquivos de log do sistema e serviços.                                          |
| `/var/mail`| Caixas de e-mail dos usuários locais.                                           |
| `/var/spool` | Dados em filas, como impressoras e e-mails pendentes.                         |
| `/var/tmp` | Arquivos temporários que podem persistir após reboot.                           |
| `/tmp`     | Arquivos temporários de curta duração (limpos a cada reboot).                   |
| `/home`    | Diretórios pessoais dos usuários.                                               |
| `/root`    | Diretório pessoal do usuário root (administrador).                              |
| `/boot`    | Arquivos necessários para inicialização do sistema (kernel, GRUB, initramfs).   |
| `/mnt`     | Ponto de montagem temporário de sistemas de arquivos.                           |
| `/media`   | Ponto de montagem automático de mídias removíveis (USB, CD, DVD).               |
| `/proc`    | Sistema de arquivos virtual com informações do kernel e processos em tempo real.|
| `/srv`     | Dados servidos por serviços de rede (web, ftp, etc.).                           |
| `/sys`     | Sistema de arquivos virtual com informações sobre dispositivos e drivers.       |
| `/lib`     | Bibliotecas essenciais para o sistema.                                          |
| `/lib64`   | Bibliotecas de 64 bits em sistemas compatíveis.                                 |
| `/opt`     | Softwares opcionais de terceiros.                                               |
| `/dev`     | Arquivos de dispositivos do sistema (discos, terminais, etc.).                  |
| `/run`     | Informações voláteis em tempo de execução (processos, sockets, etc.).           |

---

# Observações Importantes
- Diretórios como `/proc` e `/sys` **não ocupam espaço em disco**: são sistemas virtuais gerados pelo kernel.  
- `/etc` é considerado o **coração da configuração** do Linux.  
- `/var` é um dos diretórios que mais cresce em uso, especialmente por armazenar **logs**.  
- `/boot` pode estar em uma **partição separada** em sistemas críticos.  