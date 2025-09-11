# DHCP (Dynamic Host Configuration Protocol)

O **DHCP (Dynamic Host Configuration Protocol)** é um protocolo de rede usado para **atribuir dinamicamente endereços IP e outras configurações de rede** para dispositivos em uma rede, de forma **automática** e centralizada.  

Sem o DHCP, cada dispositivo teria que ser configurado manualmente, o que é inviável em redes grandes.

---

## Como o DHCP funciona

O processo de concessão de um endereço IP pelo DHCP é conhecido como **DORA**. Quando um dispositivo se conecta à uma rede, ele não possui um endereço de IP. Portanto, ele segue os seguintes passos do DORA:

1. **Discover (Descoberta)**  
   O cliente (ex: computador ou celular) envia uma mensagem de broadcast perguntando:  
   _"Existe algum servidor DHCP disponível?"_

2. **Offer (Oferta)**  
   O servidor DHCP responde oferecendo um endereço IP e outras configurações (como máscara de sub-rede, gateway e DNS).

3. **Request (Solicitação)**  
   O cliente escolhe uma das ofertas (quando há mais de um servidor) e solicita oficialmente aquele endereço IP.

4. **Acknowledge (Confirmação)**  
   O servidor confirma a atribuição, registrando o endereço como usado, e o cliente passa a utilizá-lo.

---

## Informações fornecidas pelo DHCP

Além do **endereço IP**, o servidor DHCP pode fornecer:

- **Máscara de sub-rede** → define a divisão entre rede e hosts.  
- **Gateway padrão** → rota de saída para outras redes (ex: acesso à Internet).  
- **Servidores DNS** → para resolução de nomes de domínio.  
- **Tempo de concessão (lease time)** → tempo pelo qual o endereço IP será válido.  

---

## Benefícios do DHCP

- **Automatiza** a configuração de IPs.  
- **Evita conflitos** de endereços duplicados.  
- **Escalável** → fácil gerenciamento em redes grandes.  
- **Flexível** → suporta diferentes configurações para diferentes segmentos de rede.  

---

## Exemplo do processo DORA

- Cliente envia **DHCP Discover** para `255.255.255.255`.  
- Servidor responde com **DHCP Offer** oferecendo `192.168.1.100`.  
- Cliente envia **DHCP Request** pedindo este IP.  
- Servidor confirma com **DHCP Acknowledge**.  

Agora, o cliente pode usar `192.168.1.100` até o tempo do **lease expirar**.

---

## Renovação de IP

O **DHCP Lease** é o período de tempo durante o qual um endereço IP, atribuído dinamicamente por um servidor DHCP, permanece válido para um dispositivo na rede.  

Esse conceito é importante porque garante que os endereços IP não fiquem ocupados indefinidamente, permitindo que sejam reutilizados quando não forem mais necessários.

### Como funciona
- Antes de o **lease time** expirar, o cliente envia uma requisição ao servidor para renovar o mesmo endereço IP.  
- Se o servidor permitir, o tempo é estendido sem necessidade de nova negociação completa.  
- Caso contrário, o cliente precisa iniciar novamente o processo DORA.

### Exemplo prático
1. Um cliente recebe o IP `192.168.1.50` com um lease de **24 horas**.  
2. Após cerca de **50% do tempo** (12 horas), o cliente envia um pedido de **renovação** ao servidor.  
3. O servidor confirma e estende o lease por mais 24 horas.  
4. Caso o cliente se desconecte e o lease expire, o endereço IP volta a ficar **disponível** para ser usado por outro dispositivo.  

---

## Exemplo prático no Linux

Para visualizar o endereço obtido por DHCP:
```bash
ip addr show
```
Para liberar e renovar o IP via DHCP (dependendo da distro):
```bash
dhclient -r    # libera o endereço atual  
dhclient       # solicita novo endereço  
```

---

## Diferença entre DHCP e IP Fixo

- **IP Fixo (Manual)** → cada host precisa ser configurado manualmente.  
- **DHCP (Dinâmico)** → endereços atribuídos automaticamente, reduzindo erros e tempo de configuração.  

---

## Resumo

O **DHCP é essencial em redes modernas**, permitindo que dispositivos se conectem rapidamente e sem configuração manual, garantindo eficiência, escalabilidade e redução de conflitos de IP.
