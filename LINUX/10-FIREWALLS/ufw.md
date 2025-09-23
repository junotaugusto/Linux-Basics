# UFW (Uncomplicated Firewall)

## 1. O que é o UFW?

O **UFW (Uncomplicated Firewall)** é uma interface de gerenciamento de firewall projetada para ser intuitiva e fácil de usar. Ele atua como um "front-end" para o `iptables`, a ferramenta de firewall padrão do kernel Linux, que é extremamente poderosa, mas também bastante complexa.

O principal objetivo do UFW é simplificar o processo de configuração de um firewall, sendo a escolha padrão em distribuições como o Ubuntu e seus derivados (Linux Mint, Pop!_OS, etc.) por sua simplicidade e eficácia.

## 2. Comandos Essenciais

A seguir, estão os comandos mais comuns para administrar o UFW no dia a dia.

### Ativando e Desativando o Firewall

Para que suas regras tenham efeito, o firewall precisa estar ativo.

* **Ativar o UFW:**
```bash
    sudo ufw enable
```
    > **Atenção:** Ao ativar o UFW pela primeira vez, especialmente em um servidor remoto, certifique-se de que você já possui uma regra que libere o acesso SSH (`sudo ufw allow ssh`), caso contrário, sua conexão será cortada.

* **Desativar o UFW:**
```bash
    sudo ufw disable
```

### Verificando o Status

Este é o comando que você mais usará para verificar as regras ativas e o estado geral do firewall.

* **Verificar o status simples:**
```bash
    sudo ufw status
```
    > Para informações mais específicas, utilize o seguinte comando:
```bash
sudo ufw status verbose
```

* **Verificar o status com as regras numeradas (útil para deletar regras):**
```bash
    sudo ufw status numbered
```

### Gerenciando Regras (allow e deny)

A lógica principal do firewall é definir políticas padrão (geralmente negar tudo que entra) e abrir portas específicas para os serviços necessários.

* **Permitir (allow) uma porta:**
```bash
    # Permitir tráfego na porta 443 usando o protocolo TCP
    sudo ufw allow 443/tcp
```

* **Permitir (allow) um serviço pelo nome:**
    O UFW conhece os portos padrão de vários serviços comuns.
```bash
    # Permitir tráfego SSH (equivale a 'ufw allow 22/tcp')
    sudo ufw allow ssh

    # Permitir tráfego HTTP (equivale a 'ufw allow 80/tcp')
    sudo ufw allow http
```

* **Permitir acesso por meio de um endereço IP confiável:**
Ao trabalhar com o UFW, você também pode especificar endereços IP. Por exemplo, se quiser permitir conexões de um endereço IP específico, como um endereço IP de trabalho ou domicílio de 192.168.5.35, você precisa especificar `from`, então o endereço IP:
```bash
sudo ufw allow from 192.168.5.35

#Ou por uma porta específica apenas em:
sudo ufw allow from 192.168.5.35 to any port 22
```

* **Negar (deny) uma porta:**
```bash
    # Negar explicitamente o tráfego na porta 25 usando o protocolo UDP
    sudo ufw deny 25/udp
```

### Deletando Regras

Para remover uma regra que não é mais necessária, a forma mais fácil é listá-las com números e depois deletar pelo número correspondente.

1.  **Liste as regras numeradas:**
```bash
    sudo ufw status numbered
```
2.  **Delete a regra pelo seu número:**
```bash
    # Exemplo: deletando a regra de número 3
    sudo ufw delete 3
```

### Gerenciando Logs (Logging)

Os logs são úteis para monitorar tentativas de acesso e depurar problemas de conexão.

* **Ativar os logs:**
```bash
    sudo ufw logging on
```

* **Desativar os logs:**
```bash
    sudo ufw logging off
```
Os logs geralmente são armazenados em `/var/log/ufw.log`.

## 3. Informações Finais e Boas Práticas

* **Política Padrão:** Uma prática de segurança recomendada é negar todo o tráfego de entrada por padrão e permitir todo o tráfego de saída. Você pode definir isso com os seguintes comandos:
```bash
    sudo ufw default deny incoming
    sudo ufw default allow outgoing
```
    > Depois disso, você só precisa adicionar regras de `allow` para os serviços que deseja expor publicamente (como SSH, HTTP, etc.).

* **Resetar o Firewall:** Se precisar apagar todas as regras e voltar às configurações de fábrica, use o comando `reset`.
```bash
    sudo ufw reset
```

O UFW é uma ferramenta poderosa para proteger seu sistema sem a complexidade do `iptables`. Dominar esses comandos essenciais já proporciona um excelente nível de segurança para a maioria dos casos de uso.
