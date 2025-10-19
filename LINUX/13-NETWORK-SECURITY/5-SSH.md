# SSH (Secure Shell) Hardening

## 1. O que é o Secure Shell (SSH)?

O **Secure Shell (SSH)** é um protocolo de rede criptográfico que permite a administradores e usuários acessarem e controlarem um computador remotamente de forma segura. Ele é usado para:
* Executar comandos em um servidor remoto.
* Transferir arquivos com segurança (usando `sftp` ou `scp`).
* Encaminhar portas de rede (túneis SSH).

Ele cria um "túnel" criptografado entre o seu computador local e o servidor, garantindo que toda a comunicação (incluindo senhas e comandos) seja protegida contra espionagem na rede. Ele é o substituto moderno e seguro do antigo e inseguro protocolo `telnet`.

## 2. A Necessidade de "Endurecer" (Hardening) o SSH

Por padrão, a única barreira para acessar um servidor via SSH é um **nome de usuário e uma senha**. Em um mundo ideal, isso seria suficiente, mas no mundo real, a internet está cheia de *bots* mal-intencionados que passam o dia inteiro tentando "adivinhar" senhas em servidores.

Esse tipo de ataque, chamado de **força bruta**, tenta milhares de combinações de senhas por minuto (como `root`/`admin`, `root`/`123456`, etc.). Se a sua senha for fraca, é uma questão de tempo até que um desses bots consiga acesso.

"Endurecer" o SSH é o processo de realizar algumas configurações-chave para **mitigar ameaças potenciais** e adicionar múltiplas camadas de defesa, tornando o trabalho do atacante muito mais difícil.

## 3. O Arquivo de Configuração Principal

Quase todo o *hardening* do SSH é feito em um único arquivo de configuração no servidor:

**`/etc/ssh/sshd_config`**

Para editá-lo, você sempre precisará de privilégios de administrador:
```bash
sudo nano /etc/ssh/sshd_config
```
Depois de qualquer alteração neste arquivo, o serviço SSH precisa ser reiniciado para que as mudanças tenham efeito.

## 4. Práticas de Hardening Essenciais

A seguir, estão as configurações mais comuns e eficazes para proteger seu serviço SSH.

### a) Alterar a Porta Padrão (Port)

* **Por que?** Por padrão, o SSH roda na porta `22`. Cerca de 99% dos bots de ataque de força bruta são "burros" e miram exclusivamente na porta 22. 

Apenas mudando a porta, você se torna "invisível" para a grande maioria desses ataques automatizados. É uma forma simples e eficaz de "segurança por obscuridade".
* **Como fazer:**
    1.  Abra o arquivo `/etc/ssh/sshd_config`.
    2.  Encontre a linha que diz `#Port 22`.
    3.  Remova o `#` do início da linha (para "descomentar").
    4.  Altere o `22` para um número de porta alto e não utilizado (ex: `2222`, `49150`, etc.).
    5.  A linha deve ficar assim:
```bash
        Port 2222
```
    6.  Salve o arquivo.

### b) Desabilitar o Login do Root (PermitRootLogin)

* **Por que?** O usuário `root` é o superusuário. Se um atacante conseguir adivinhar a senha do `root`, ele ganha controle total e irrestrito do seu sistema ("Game Over"). Ao desabilitar o login do `root`, você força um ataque a ser feito em duas etapas: primeiro, o atacante precisa comprometer uma conta de usuário normal (como `jap` ou `bruno`) e, *depois*, ele precisa encontrar uma forma de "escalar privilégios" para se tornar `root`. É uma barreira de segurança crucial.
* **Como fazer:**
    1.  Abra o arquivo `/etc/ssh/sshd_config`.
    2.  Encontre a linha que diz `#PermitRootLogin prohibit-password` (ou algo similar, como `PermitRootLogin yes`).
    3.  Mude esta linha para:
        ```ini
        PermitRootLogin no
        ```
    4.  Salve o arquivo.

### c) Limitar o Acesso de Usuários (AllowUsers)

* **Por que?** Seguindo o "Princípio do Menor Privilégio", nem todo usuário criado no seu sistema precisa de acesso remoto. Se você tem um usuário de serviço (como `www-data`) ou um usuário que só deve acessar localmente, não há por que permitir que ele seja um vetor de ataque via SSH. Esta configuração cria uma "lista VIP": **somente** os usuários listados poderão tentar o login.
* **Como fazer:**
    1.  Abra o arquivo `/etc/ssh/sshd_config`.
    2.  Vá até o final do arquivo.
    3.  Adicione uma nova linha listando, separados por espaço, **apenas** os usuários que você quer permitir.
        ```ini
        # Lista apenas os usuários que podem acessar via SSH
        AllowUsers jap bruno alice
        ```
    4.  Salve o arquivo.

## 5. Aplicando as Alterações (Systemctl)

Depois de salvar suas alterações no arquivo `/etc/ssh/sshd_config`, elas **não terão efeito** até que você reinicie o serviço `sshd`.

O comando para fazer isso é:
```bash
sudo systemctl restart sshd
```
Este comando força o serviço a parar e iniciar novamente, lendo o novo arquivo de configuração.

> **⚠️ AVISO IMPORTANTE: NÃO SE TRANQUE PARA FORA!**
> Se você (1) alterou a porta e (2) está usando um firewall (como o `ufw`), você **DEVE** permitir a nova porta no firewall **ANTES** de reiniciar o SSH.
>
> **Fluxo de trabalho correto:**
> 1.  `sudo nano /etc/ssh/sshd_config` (e mudar a porta para `2222`).
> 2.  `sudo ufw allow 2222/tcp` (Avisar ao firewall para permitir a nova porta).
> 3.  `sudo systemctl restart sshd` (Reiniciar o serviço).
> 4.  Tentar se conectar em um **novo terminal** usando `ssh -p 2222 usuario@servidor` para confirmar que funciona, antes de fechar sua sessão atual.