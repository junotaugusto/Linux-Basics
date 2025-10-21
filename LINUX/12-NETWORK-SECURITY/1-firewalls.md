# Network Security: Manutenção de um Firewall

## 1. Introdução ao Firewall

Um firewall é uma barreira de segurança digital que monitora e controla o tráfego de rede que entra e sai de um sistema ou de uma rede. Pense nele como um segurança ou porteiro na porta de entrada do seu servidor.

A principal característica de um firewall é que ele não toma decisões por conta própria. Sua eficácia depende inteiramente das **"regras"** que nós, como administradores, estabelecemos. 

Ele analisa cada "pacote" de dados que tenta passar e o compara com a lista de regras. Se o pacote corresponder a uma regra, a ação definida (permitir ou bloquear) é executada. Se não corresponder a nenhuma regra, a política padrão (geralmente "bloquear tudo") é aplicada.

No Linux, as duas ferramentas mais comuns para gerenciar o firewall do kernel (Netfilter) são o `UFW` e o `iptables`.

## 2. UFW (Uncomplicated Firewall) - A Camada Amigável

O UFW foi projetado para ser uma interface simples e intuitiva para o `iptables`. Ele é ideal para cenários comuns e para quem está começando.

### Comandos Essenciais do UFW

* **Ativar e Desativar:**
```bash
    # Ativa o firewall e o faz iniciar com o sistema
    sudo ufw enable

    # Desativa o firewall
    sudo ufw disable
```

* **Verificar o Status:**
```bash
    # Mostra o status e as regras ativas
    sudo ufw status verbose
```

* **Permitir Tráfego (Allow):**
```bash
    # Permite tráfego SSH (na porta 22)
    sudo ufw allow ssh

    # Permite tráfego web na porta 80/tcp
    sudo ufw allow 80/tcp
```

* **Negar Tráfego (Deny):**
```bash
    # Bloqueia explicitamente o tráfego na porta de email 25/tcp
    sudo ufw deny 25/tcp
```

* **Permitir um IP Específico a uma Porta Específica:**
    Esta é uma regra muito comum para reforçar a segurança, por exemplo, permitindo que apenas o IP do seu escritório acesse a porta SSH do servidor.
```bash
    # Sintaxe: ufw allow from [ip] to any port [porta]
    
    # Exemplo: Permitir que o IP 203.0.113.54 se conecte à porta SSH (22)
    sudo ufw allow from 203.0.113.54 to any port 22
```

## 3. iptables - O Controle Granular

O `iptables` é a ferramenta de "baixo nível" que conversa diretamente com o Netfilter no kernel do Linux. É imensamente mais poderoso e flexível que o UFW, mas também mais complexo. Ele organiza as regras em **Tabelas** (ex: `filter`, `nat`) e **Correntes** (ex: `INPUT`, `OUTPUT`, `FORWARD`).

### Alguns Comandos com `iptables`

* **Listar todas as regras da corrente INPUT:**
```bash
    sudo iptables -L INPUT -v
```

* **Bloquear todo o tráfego de entrada por padrão (Política Padrão):**
```bash
    sudo iptables -P INPUT DROP
```

* **Permitir tráfego de conexões já estabelecidas (Regra Essencial):**
```bash
    sudo iptables -A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
```

## 4. Desvendando Comandos `iptables` em Detalhes

### a) Analisando: `sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT`

Esta é uma das regras mais comuns: permitir conexões SSH de entrada.

* `sudo`: Executa o comando com privilégios de administrador.
* `iptables`: O programa que estamos usando.
* `-A INPUT`: **A**diciona (`Append`) esta regra ao final da corrente `INPUT`. A corrente `INPUT` lida com todo o tráfego cujo destino final é o nosso próprio servidor.
* `-p tcp`: Especifica o **p**rotocolo a ser correspondido. Neste caso, `tcp`.
* `--dport 22`: Condição de correspondência. `dport` significa "destination port" (porta de destino). A regra só se aplicará a pacotes destinados à porta `22`.
* `-j ACCEPT`: A ação a ser tomada. `-j` significa "jump" (pular). Se todas as condições anteriores forem verdadeiras, pule para o alvo `ACCEPT` (Aceitar), que permite a passagem do pacote.

**Conclusão:** "Adicione uma regra à corrente de tráfego de entrada que ACEITA pacotes do protocolo TCP destinados à porta 22."

### b) Analisando: `sudo iptables -A INPUT -p tcp --dport 80 -j DROP`

Esta regra bloqueia conexões de entrada para um servidor web. A lógica é a mesma da anterior, mudando apenas a porta e a ação final.

* `--dport 80`: A condição agora é a porta de destino `80` (padrão para tráfego web HTTP).
* `-j DROP`: A ação final. Se as condições forem verdadeiras, pule para o alvo `DROP` (Descartar). O alvo `DROP` descarta o pacote silenciosamente, sem enviar nenhuma resposta ao remetente.

**Conclusão:** "Adicione uma regra à corrente de tráfego de entrada que DESCARTA silenciosamente pacotes do protocolo TCP destinados à porta 80."

## 5. Salvando as Regras do `iptables`

Por padrão, as regras do `iptables` são voláteis, ou seja, **são perdidas quando o sistema é reiniciado**. Para torná-las permanentes, você precisa salvá-las.

### Método 1: `iptables-save` (O Clássico)

Você pode salvar o estado atual das regras em um arquivo e depois restaurá-las.

```bash
# Salva as regras atuais no arquivo /etc/iptables/rules.v4
sudo iptables-save > /etc/iptables/rules.v4

# Para restaurar as regras a partir do arquivo
sudo iptables-restore < /etc/iptables/rules.v4
```
Com este método, você precisaria configurar um script para executar o `iptables-restore` a cada inicialização do sistema.

### Método 2: `iptables-persistent` (O Moderno - Recomendado)

Em sistemas baseados em Debian/Ubuntu, este pacote automatiza o processo.

```bash
# Instalar o pacote
sudo apt install iptables-persistent

# Durante a instalação, ele perguntará se você deseja salvar as regras atuais. Diga 'Sim'.

# Se você modificar as regras DEPOIS da instalação e quiser salvá-las, use:
sudo netfilter-persistent save
```
Este pacote cria um serviço que é executado automaticamente durante o boot, carregando as últimas regras que foram salvas.