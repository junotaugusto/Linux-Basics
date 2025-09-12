# **NMCLI – NetworkManager Command Line Interface**

O **nmcli** é uma ferramenta de linha de comando usada para **gerenciar conexões de rede** e **configurações de interfaces** em sistemas Linux que utilizam o **NetworkManager**. 

Ele permite configurar conexões de rede, Wi-Fi, VLANs, endereços IP, DNS e muito mais, sem a necessidade de interfaces gráficas.

---

## **Principais funcionalidades**
- Configurar interfaces de rede (ativar/desativar).
- Criar, editar e remover conexões.
- Definir endereços IP, gateway e DNS.
- Conectar-se a redes Wi-Fi.
- Exibir status e detalhes das conexões de rede.
- Automatizar configurações via scripts.

---

## **Comandos básicos**

### 1. **Verificar status geral da rede**
```bash
nmcli general status
```
Mostra o estado geral do NetworkManager.

### 2. **Listar dispositivos de rede**
```bash
nmcli device status
```
Exibe os dispositivos de rede (interfaces) e seus estados:
- `connected` → dispositivo conectado.
- `disconnected` → dispositivo disponível, mas não conectado.
- `unmanaged` → dispositivo não controlado pelo NetworkManager.

### 3. **Listar conexões configuradas**
```bash
nmcli connection show
```
Mostra as conexões ativas. Mostra detalhes como o nome da conexão, o UUID (Universally Unique Identifier), tipo e o dispositivo.

### 4. **Ativar ou desativar uma conexão**
- Ativar:
```bash
nmcli connection up nome-da-conexao
```
- Desativar:
```bash
nmcli connection down nome-da-conexao
```

### 5. **Ativar ou desativar um dispositivo**
- Ativar:
```bash
nmcli device connect eth0
```
- Desativar:
```bash
nmcli device disconnect eth0
```

### 6. **Configurar IP estático**
Exemplo: definir IP manualmente em `eth0`.
```bash
nmcli connection modify eth0 ipv4.addresses 192.168.1.50/24 ipv4.gateway 192.168.1.1 ipv4.dns 8.8.8.8 ipv4.method manual
```
Depois, reativar a conexão:
```bash
nmcli connection down eth0 && nmcli connection up eth0
```

### 7. **Configurar DHCP**
```bash
nmcli connection modify eth0 ipv4.method auto
```

### 8. **Conectar a uma rede Wi-Fi**
```bash
nmcli device wifi connect "NomeDaRede" password "senha"
```

### 9. **Listar redes Wi-Fi disponíveis**
```bash
nmcli device wifi list
```

## **Exemplo prático**
1. Verificar dispositivos:
```bash
nmcli device status
```
2. Conectar-se a uma rede Wi-Fi chamada `MinhaRede`:
```bash
nmcli device wifi connect "MinhaRede" password "12345678"
```
3. Conferir IP obtido:
```bash
nmcli device show wlan0
```

## **Vantagens do NMCLI**
- Não depende de interface gráfica.
- Permite automação de configurações.
- Útil para servidores sem GUI.
- Funciona de forma integrada ao **NetworkManager**.

---

## **Resumo**
O `nmcli` é uma ferramenta poderosa para gerenciar conexões de rede via terminal. Ele permite tanto operações simples (como listar dispositivos e conexões) quanto configurações avançadas (endereços IP estáticos, múltiplos DNS, VLANs, Wi-Fi corporativo, etc.), sendo indispensável em ambientes de servidores Linux.
