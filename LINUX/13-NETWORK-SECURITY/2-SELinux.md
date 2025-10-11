# SELinux (Security-Enhanced Linux)

## 1. O que é e como funciona o SELinux?

**SELinux (Security-Enhanced Linux)** é um módulo de segurança avançado para o kernel do Linux que implementa uma arquitetura de **Controle de Acesso Mandatório (MAC - Mandatory Access Control)**.

Para entender o que isso significa, é crucial diferenciar do modelo que vimos até agora:

* **DAC (Discretionary Access Control - Controle de Acesso Discricionário):** Este é o modelo de permissões padrão do Linux (`chmod`, `chown`, ACLs). Nesse modelo, o **dono** de um arquivo tem a **discrição** (o poder) de mudar suas permissões. O superusuário `root` pode ignorar todas essas permissões e acessar qualquer coisa.

* **MAC (Mandatory Access Control - Controle de Acesso Mandatório):** Este é o modelo do SELinux. Aqui, o acesso é ditado por uma **política de segurança central e mandatória**, que é carregada no kernel. Nem o dono de um arquivo, nem mesmo o `root`, pode realizar uma ação que viole essa política.

Pense na diferença entre a segurança da sua casa (DAC) e a de uma base militar de alta segurança (MAC). Na sua casa, você (o dono) decide quem entra. Na base militar, não importa se você é um general (`root`); se a política central diz que você não pode entrar em uma sala específica, você será bloqueado.

O SELinux foi originalmente desenvolvido pela Agência de Segurança Nacional dos EUA (NSA) com o objetivo principal de limitar o dano de um ataque de "escalonamento de privilégios". 

Se um serviço (como um servidor web) for comprometido, mesmo que o invasor consiga privilégios de `root`, o SELinux o impedirá de realizar ações fora do que é estritamente permitido para aquele serviço pela política.

## 2. Segurança Através de Políticas

O SELinux funciona com base em **rótulos (labels)**, também conhecidos como **contextos de segurança**. Tudo no sistema — processos, arquivos, diretórios, portas de rede — possui um rótulo SELinux.

A **política de segurança** do SELinux é um conjunto massivo de regras que define como os rótulos podem interagir entre si.

O fluxo de decisão funciona assim:
1.  Um **sujeito** (ex: o processo do servidor Apache) tenta realizar uma ação em um **objeto** (ex: o arquivo `/var/www/html/index.html`).
2.  Antes da permissão DAC ser verificada, o Kernel pergunta ao módulo SELinux: "Essa ação é permitida?".
3.  O SELinux verifica o rótulo do processo Apache (ex: `httpd_t`) e o rótulo do arquivo `index.html` (ex: `httpd_sys_content_t`).
4.  Ele consulta a política carregada na memória para ver se existe uma regra que permita a um sujeito `httpd_t` ler (`read`) um objeto `httpd_sys_content_t`.
5.  Se a regra existir, a ação é permitida (e só então as permissões DAC são checadas). Se não existir, a ação é **bloqueada** e um alerta é registrado no log de auditoria (geralmente em `/var/log/audit/audit.log`).

## 3. Modos de Operação

O SELinux pode operar em três modos distintos, que você pode gerenciar para diagnóstico e produção.

1.  **Enforcing (Impositivo):**
    Este é o modo padrão e o mais seguro. A política de segurança do SELinux é totalmente **ativa e aplicada**. Qualquer ação que viole a política será **bloqueada** e registrada no log.

2.  **Permissive (Permissivo):**
    Este modo é usado principalmente para testes e solução de problemas. A política do SELinux **não é aplicada** (nada é bloqueado), mas as ações que *teriam sido* bloqueadas no modo Enforcing **são registradas** no log. É uma forma de ver o que o SELinux faria sem quebrar o funcionamento do sistema.

3.  **Disabled (Desativado):**
    O módulo SELinux é completamente desativado no kernel. Nenhuma política é carregada e nada é registrado. Para reativar o SELinux a partir deste modo, uma reinicialização do sistema é necessária.

## 4. Alguns Comandos Essenciais

Gerenciar o SELinux geralmente envolve verificar o estado, mudar modos e corrigir contextos.

* **Verificar o Status do SELinux:**
    O comando principal para obter um relatório completo do estado atual.
```bash
    sestatus
```
    Ele mostrará o modo atual, a política carregada, etc.

* **Verificar o Modo Atual Rapidamente:**
```bash
    getenforce
```
    Retornará `Enforcing`, `Permissive`, ou `Disabled`.

* **Mudar o Modo de Operação (Temporariamente):**
    Esta mudança não sobrevive a uma reinicialização.
```bash
    # Coloca em modo Enforcing (1 = Enforcing)
    sudo setenforce 1

    # Coloca em modo Permissive (0 = Permissive)
    sudo setenforce 0
```

* **Mudar o Modo de Operação (Permanentemente):**
    Para que a mudança persista após o boot, você deve editar o arquivo de configuração.
```bash
    # Edite o arquivo /etc/selinux/config
    sudo nano /etc/selinux/config
```
    Altere a linha `SELINUX=enforcing` para `SELINUX=permissive` ou `SELINUX=disabled`. Salve o arquivo. (Uma reinicialização é necessária para desativar ou reativar a partir do estado desativado).

* **Visualizar os Contextos (Rótulos):**
```bash
    # Ver o contexto de arquivos e diretórios (note o -Z maiúsculo)
    ls -Z

    # Ver o contexto de processos em execução
    ps auxZ
```

* **Restaurar o Contexto Padrão de um Arquivo:**
    Este é um comando de manutenção crucial. Se você moveu (`mv`) um arquivo para um diretório de servidor web, ele pode manter o contexto errado. `restorecon` corrige isso.
```bash
    # Restaura o contexto de segurança padrão do arquivo index.html
    sudo restorecon -v /var/www/html/index.html

    # Restaura o contexto de todo o diretório web de forma recursiva (-R)
    sudo restorecon -vR /var/www/html
```