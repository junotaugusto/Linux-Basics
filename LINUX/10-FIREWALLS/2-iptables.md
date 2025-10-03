# iptables

## 1. O que é o iptables?

O **`iptables`** é um programa de linha de comando que permite a um administrador de sistemas configurar as regras de firewall do kernel Linux. 

Ele atua como uma interface direta para a estrutura `Netfilter`, que é responsável por **filtrar pacotes** de rede, fazer NAT (Network Address Translation) e realizar outras manipulações de pacotes.

Diferente de ferramentas como o `ufw`, o `iptables` é considerado de "baixo nível", oferecendo um controle extremamente granular e poderoso, mas com uma curva de aprendizado maior.

## 2. Como o iptables Funciona?

Para entender o `iptables`, é crucial conhecer sua estrutura, que é baseada em três conceitos principais: **Tables (Tabelas)**, **Chains (Correntes)** e **Rules (Regras)**.

A lógica é a seguinte: quando um pacote de rede chega ou sai da máquina, ele atravessa uma série de "correntes" (Chains). Em cada corrente, existem "regras" (Rules) que o pacote é comparado. 

Se o pacote corresponder a uma regra, uma ação (Target) é executada (ex: aceitar, descartar). Essas correntes estão organizadas dentro de "tabelas" (Tables) de acordo com sua finalidade.

### a) Tables (Tabelas)

Existem várias tabelas, mas as três principais são:

1.  **`filter`**: É a tabela padrão e a mais utilizada. Sua função é filtrar pacotes, decidindo se eles devem ser permitidos ou bloqueados.

2.  **`nat`** (Network Address Translation): Usada para alterar os endereços de origem ou destino dos pacotes. É aqui que se configura o compartilhamento de conexão com a internet (masquerading), por exemplo.

3.  **`mangle`**: Utilizada para realizar modificações especializadas nos pacotes de rede, como alterar o campo "Type of Service" (ToS).

### b) Chains (Correntes)

As Chains são sequências de regras que são verificadas em ordem. A tabela `filter` (padrão) possui três Chains principais:

1.  **`INPUT`**: Processa pacotes cujo destino final é o próprio sistema (ex: uma conexão SSH chegando no seu servidor). 
2.  **`OUTPUT`**: Processa pacotes que são gerados pelo seu sistema e estão saindo para a rede (ex: uma requisição do seu servidor para um site externo).
3.  **`FORWARD`**: Processa pacotes que estão apenas passando pelo seu sistema, sendo roteados para outro destino. Isso é comum em roteadores ou gateways.

### c) Rules (Regras) e Targets (Alvos)

Cada regra em uma Chain especifica critérios para um pacote (ex: "é do IP `192.168.1.100`?", "está usando o protocolo TCP e a porta 22?"). Se um pacote corresponde aos critérios, a regra define um **Target**, que é a ação a ser tomada.

Os Targets mais comuns são:

* **`ACCEPT`**: Permite a passagem do pacote.
* **`DROP`**: Descarta o pacote silenciosamente. O remetente não recebe nenhuma resposta.
* **`REJECT`**: Descarta o pacote, mas envia uma mensagem de erro ao remetente.
* **`LOG`**: Registra as informações do pacote em um log do sistema. A verificação continua na próxima regra.

## 3. Comandos Essenciais e Exemplos

> **Aviso:** Os comandos `iptables` geralmente exigem privilégios de root (`sudo`).

### Gerenciamento Básico

* **Listar todas as regras (da tabela `filter`):**
```bash
    sudo iptables -L -v
    # -L: Listar regras
    # -v: Modo verbose (mais detalhes)
```

* **Listar regras com números de linha:**
```bash
    sudo iptables -L --line-numbers
```

* **Definir a Política Padrão (Default Policy):**
    Esta é a ação a ser tomada se um pacote não corresponder a nenhuma regra. Uma boa prática de segurança é negar tudo e liberar apenas o necessário.
```bash
    # Define que todo pacote de entrada será descartado por padrão
    sudo iptables -P INPUT DROP
```

* **Apagar (Flush) todas as regras de uma Chain:**
```bash
    # Remove todas as regras da chain INPUT
    sudo iptables -F INPUT
```

### Criando Regras

A opção `-A` é usada para adicionar (Append) uma nova regra ao final de uma Chain.

* **Permitir tráfego de loopback (essencial para o sistema):**
```bash
    # -i lo: especifica a interface de rede 'loopback'
    sudo iptables -A INPUT -i lo -j ACCEPT
```

* **Permitir conexões SSH de entrada:**
```bash
    # -p tcp: protocolo TCP
    # --dport 22: porta de destino 22
    sudo iptables -A INPUT -p tcp --dport 22 -j ACCEPT
```

* **Bloquear um endereço de IP específico:**
```bash
    # -s 192.0.2.51: source (origem) do IP especificado
    sudo iptables -A INPUT -s 192.0.2.51 -j DROP
```

* **Permitir tráfego de conexões já estabelecidas:**
    Esta é uma regra crucial para permitir que o sistema receba respostas de conexões que ele mesmo iniciou.
```bash
    # -m conntrack: usa o módulo de "connection tracking"
    # --ctstate: verifica o estado da conexão
    sudo iptables -A INPUT -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
```

## 4. Persistência das Regras

As regras do `iptables` são voláteis e **são perdidas quando o sistema é reiniciado**. Para torná-las permanentes, você precisa usar um pacote auxiliar. Em sistemas baseados em Debian/Ubuntu, o mais comum é o `iptables-persistent`.

```bash
# Instalar o pacote
sudo apt-get install iptables-persistent

# Salvar as regras atuais
sudo netfilter-persistent save
```