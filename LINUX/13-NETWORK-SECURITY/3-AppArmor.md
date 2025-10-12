# AppArmor (Application Armor)

## 1. O que é e como funciona o AppArmor?

**AppArmor (Application Armor)** é, assim como o SELinux, um módulo de segurança do kernel que implementa o **Controle de Acesso Mandatório (MAC)**. Ele foi projetado para ser mais simples e fácil de administrar que o SELinux, sendo a escolha padrão em distribuições como Ubuntu, Debian e seus derivados.

A principal diferença filosófica entre AppArmor e SELinux está em como eles identificam os sujeitos e objetos:

* **SELinux:** Usa **rótulos (labels)** em *todos* os arquivos e processos do sistema. A segurança é baseada em como esses rótulos podem interagir.
* **AppArmor:** É baseado em **caminhos de arquivo (path-based)**. Em vez de rotular tudo, o AppArmor associa perfis de segurança diretamente a um programa executável específico (ex: `/usr/sbin/nginx`).

Pense no AppArmor como um segurança particular contratado para vigiar um único programa. Esse segurança recebe uma lista de regras (o **perfil**) que diz o que aquele programa específico pode ou não fazer: quais arquivos ele pode ler, em quais pode escrever, se pode acessar a rede, etc. Se o programa tentar fazer algo que não está na sua lista de permissões, o AppArmor o bloqueia.

## 2. Segurança Através de Perfis (Profiles)

O coração do AppArmor são os **perfis**. Um perfil é um arquivo de texto simples que define as regras de segurança para um único executável. Esses perfis são armazenados no diretório `/etc/apparmor.d/`.

Um perfil contém uma lista de regras que especificam os recursos que o programa pode acessar.

**Exemplo de regras dentro de um perfil:**
* `owner /home/jota/documentos/ r,`: Permite que o programa leia (`r`) arquivos no diretório `/home/jota/documentos/` se o processo estiver rodando como o usuário `jota`.
* `/var/log/nginx/access.log w,`: Permite que o programa escreva (`w`) no arquivo de log específico.
* `network tcp,`: Permite que o programa use a rede com o protocolo TCP.
* `/usr/bin/php-fpm ix,`: Permite que o programa execute (`ix`) outro programa (`php-fpm`) de forma que o novo programa herde o perfil.

Se uma ação não estiver explicitamente permitida no perfil, ela será negada por padrão.

## 3. Modos de Operação

Assim como o SELinux, o AppArmor tem modos de operação para cada perfil, permitindo testes e produção.

1.  **Enforce Mode (Impositivo):**
    Este é o modo de produção. O perfil está ativo e o AppArmor **bloqueará** qualquer ação do programa que viole as regras definidas. As violações também são registradas nos logs do sistema (geralmente em `/var/log/audit/audit.log` ou `/var/log/syslog`).

2.  **Complain Mode (Modo de Reclamação):**
    Este é o modo de aprendizado ou depuração. O AppArmor **não bloqueia** nenhuma ação, mas ele **registra nos logs** todas as ações que *teriam sido* bloqueadas se o perfil estivesse em modo *enforce*. É extremamente útil para desenvolver ou ajustar um perfil sem quebrar a funcionalidade da aplicação.

3.  **Unloaded/Disabled (Descarregado/Desativado):**
    Um perfil pode ser completamente descarregado da memória do kernel. Nesse caso, o AppArmor não monitora o programa correspondente de forma alguma.

## 4. Alguns Comandos Essenciais

Gerenciar o AppArmor envolve verificar o status dos perfis e alternar seus modos. Os comandos geralmente usam o prefixo `aa-` (de AppArmor).

* **Verificar o Status do AppArmor:**
    Este é o comando mais importante. Ele mostra quais perfis estão carregados, em qual modo eles estão e quais processos estão sendo confinados.
    ```bash
    # A versão mais nova e recomendada
    sudo aa-status

    # A versão mais antiga, ainda muito comum
    sudo apparmor_status
    ```

* **Colocar um Perfil em Complain Mode:**
    Útil quando um programa está se comportando de forma estranha e você suspeita que o AppArmor o está bloqueando.
    ```bash
    # Sintaxe: sudo aa-complain /caminho/para/o/executavel
    sudo aa-complain /usr/sbin/nginx
    ```

* **Colocar um Perfil em Enforce Mode:**
    O inverso do comando anterior, usado para reativar a proteção após os testes.
    ```bash
    # Sintaxe: sudo aa-enforce /caminho/para/o/executavel
    sudo aa-enforce /usr/sbin/nginx
    ```

* **Gerar um Novo Perfil (Modo de Aprendizagem):**
    O AppArmor possui ferramentas interativas que ajudam a criar um perfil do zero.
    ```bash
    # 1. Coloca um programa sem perfil em modo complain
    sudo aa-genprof /caminho/para/novo/programa

    # 2. Em outro terminal, use o programa normalmente para gerar eventos de log.

    # 3. Volte ao primeiro terminal e pressione 's' (scan). O aa-genprof
    #    lerá os logs e perguntará a você, para cada ação, se deseja
    #    permiti-la (Allow), negá-la (Deny) ou ignorá-la (Ignore).
    ```

* **Recarregar Todos os Perfis:**
    Se você editou um arquivo de perfil manualmente, precisa recarregá-lo.
    ```bash
    sudo systemctl reload apparmor
    ```