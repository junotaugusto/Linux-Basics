# Comando `ip` – Ferramenta de Configuração de Rede

O comando **ip** é a ferramenta moderna para gerenciar e configurar interfaces de rede em sistemas Linux, substituindo o antigo `ifconfig`. Ele permite visualizar informações, configurar endereços IP, rotas e status das interfaces.

---

## 1. Visualizar Interfaces de Rede
Para listar todas as interfaces de rede ativas e suas configurações:

```bash
ip addr show  
```

### Exemplo de saída:
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
inet 127.0.0.1/8 scope host lo

2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
link/ether 00:11:22:33:44:55 brd ff:ff:ff:ff:ff:ff
inet 192.168.1.100/24 brd 192.168.1.255 scope global eth0

- **lo** → interface de loopback (127.0.0.1).  
- **eth0** → interface Ethernet.  
- **inet 192.168.1.100/24** → endereço IPv4 com máscara de sub-rede.  
- **brd 192.168.1.255** → endereço de broadcast.  

---

## 2. Atribuir um Endereço IP
Podemos configurar manualmente um IP em uma interface:
```bash  
sudo ip addr add 192.168.1.100/24 dev eth0  
```

### Explicação:
- **sudo** → executa como administrador.  
- **ip addr add** → adiciona um endereço IP.  
- **192.168.1.100/24** → endereço IP e máscara de sub-rede (255.255.255.0).  
- **dev eth0** → especifica a interface de rede.  

---

## 3. Remover um Endereço IP
Se for necessário retirar um IP manualmente configurado:
```bash
sudo ip addr del 192.168.1.100/24 dev eth0  
```

---

## 4. Ativar ou Desativar uma Interface
- Ativar interface:  
```bash  
sudo ip link set eth0 up  
```
- Desativar interface:  
```bash  
sudo ip link set eth0 down  
```

---

## 5. Ver Rotas da Tabela de Roteamento
Para visualizar a tabela de roteamento atual:

```bash  
ip route show  
```

### Exemplo:
default via 192.168.1.1 dev eth0
192.168.1.0/24 dev eth0 proto kernel scope link src 192.168.1.100

- **default via 192.168.1.1** → gateway padrão.  
- **192.168.1.0/24 dev eth0** → rede local conectada na interface `eth0`.  

---

## Resumindo

- `ip addr show` → mostra interfaces e endereços.  
- `ip addr add/del` → adiciona ou remove IPs.  
- `ip link set up/down` → ativa ou desativa interfaces.  
- `ip route show` → exibe rotas da rede.  

O comando `ip` é essencial para configuração e troubleshooting de redes no Linux, sendo a forma mais atual de gerenciar interfaces.