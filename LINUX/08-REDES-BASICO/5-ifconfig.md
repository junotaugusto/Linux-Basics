# Comando ifconfig – Interface Configuration

O **ifconfig** (interface configuration) é uma ferramenta de linha de comando utilizada em sistemas baseados em Unix, como Linux e macOS, para **configurar e visualizar interfaces de rede**.  

Embora tenha sido substituído em distribuições modernas pelo comando **ip**, o `ifconfig` ainda é muito utilizado e aparece com frequência em cursos, tutoriais e manuais.

---

## Para que serve o ifconfig?

- **Visualizar interfaces de rede**: mostra todas as placas de rede conectadas (físicas ou virtuais).  
- **Configurar endereços IP**: atribui manualmente IPs a interfaces.  
- **Ativar ou desativar interfaces**: permite colocar uma placa de rede em funcionamento ou desligá-la.  
- **Exibir informações da interface**: como máscara de sub-rede, endereço MAC, broadcast e status da conexão.  

---

## O que aparece no ifconfig?

Quando digitamos apenas:
```bash
ifconfig
```
A saída pode mostrar algo assim:

eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST> mtu 1500
inet 192.168.1.100 netmask 255.255.255.0 broadcast 192.168.1.255
ether 08:00:27:1a:2b:3c txqueuelen 1000 (Ethernet)

### Explicando os elementos:
- **eth0** → nome da interface de rede (pode ser `eth1`, `wlan0`, etc.).  
- **flags** → status da interface (ex: UP = ativa, RUNNING = em uso).  
- **mtu 1500** → *Maximum Transmission Unit*, tamanho máximo de pacote que pode ser transmitido.  
- **inet 192.168.1.100** → endereço IPv4 atribuído à interface.  
- **netmask 255.255.255.0** → máscara de sub-rede.  
- **broadcast 192.168.1.255** → endereço de broadcast da rede.  
- **ether 08:00:27:1a:2b:3c** → endereço físico da interface (MAC Address).  

---

## Exemplos de uso

### 1. Mostrar todas as interfaces de rede
(ifconfig)

### 2. Ativar uma interface
(ifconfig eth0 up)

### 3. Desativar uma interface
(ifconfig eth0 down)

### 4. Atribuir um IP manualmente
(ifconfig eth0 192.168.1.50 netmask 255.255.255.0)

### 5. Alterar o endereço MAC
(ifconfig eth0 hw ether 00:11:22:33:44:55)

---

## Observação importante

- Em distribuições Linux modernas, o comando **ifconfig** foi substituído por ferramentas da suíte `iproute2`, principalmente o comando **ip**.  
- Exemplo equivalente ao `ifconfig`:
  (ip addr show)
