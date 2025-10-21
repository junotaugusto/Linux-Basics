# Systemd

O **systemd** é um sistema de inicialização (init system) e gerenciador de serviços para sistemas operacionais Linux. Ele substitui sistemas mais antigos, como o **SysVinit** e o **Upstart**, trazendo uma abordagem moderna, eficiente e mais consistente para gerenciar o boot do sistema, serviços e processos em execução.

## O que é o systemd

- É responsável pelo **boot do sistema**, iniciando serviços essenciais e montando sistemas de arquivos.
- Funciona como um **gerenciador de serviços**, monitorando e controlando processos em segundo plano.
- Utiliza **unidades (units)** para definir serviços, sockets, dispositivos, montagens e timers.
- Integra funções de inicialização, gerenciamento de serviços, log e auditoria em um único sistema.

---

## Pontos-chave do systemd

1. **Inicialização paralela**  
   - Inicia serviços em paralelo sempre que possível, reduzindo o tempo de boot.
   
2. **Unidades (Units)**  
   - Cada recurso gerenciado pelo systemd é representado como uma unidade. Exemplos:  
     - `service` → serviços (ex: nginx.service)  
     - `socket` → sockets de comunicação  
     - `mount` → pontos de montagem  
     - `target` → grupos de unidades para atingir estados específicos (como runlevels)
   
3. **Dependências explícitas**  
   - Permite definir dependências entre serviços, garantindo que um serviço só inicie após outro estar pronto.
   
4. **Controle de processos**  
   - Utiliza **cgroups** para organizar e monitorar processos, controlando recursos de CPU, memória e I/O.
   
5. **Logs centralizados (journald)**  
   - Coleta logs de todos os serviços de forma centralizada, permitindo fácil análise e monitoramento.

6. **Timers e agendamentos**  
   - Substitui o uso do `cron` com timers integrados, oferecendo maior precisão e flexibilidade.

---

## Benefícios do systemd

- **Boot mais rápido**: inicialização paralela e otimização de dependências reduzem o tempo de boot.  
- **Gestão unificada**: combina init, gerenciamento de serviços e logging em um único sistema.  
- **Controle avançado de processos**: cgroups permitem limitar recursos e evitar que um serviço consuma tudo.  
- **Monitoramento eficiente**: fácil verificação do status de serviços (`systemctl status`) e logs (`journalctl`).  
- **Automação e agendamento simplificados**: timers substituem crons complexos e scripts manuais.  
- **Consistência entre distribuições**: amplamente adotado em diversas distribuições modernas (Debian, Ubuntu, Fedora, CentOS).

---

## Comandos úteis

- `systemctl start <serviço>` → Inicia um serviço.  
- `systemctl stop <serviço>` → Para um serviço.  
- `systemctl restart <serviço>` → Reinicia um serviço.  
- `systemctl enable <serviço>` → Habilita para iniciar no boot.  
- `systemctl disable <serviço>` → Desabilita o serviço no boot.  
- `systemctl status <serviço>` → Mostra o status de um serviço.  
- `journalctl -xe` → Exibe logs detalhados do sistema e serviços.

---

O **systemd** é, portanto, uma ferramenta poderosa que moderniza a forma como o Linux gerencia serviços e processos, trazendo **eficiência, controle e confiabilidade** ao sistema.
