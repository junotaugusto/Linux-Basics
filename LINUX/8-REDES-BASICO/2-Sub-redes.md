# Subnetting (Sub-redes)

O **subnetting** é a técnica de dividir uma rede maior em **sub-redes menores**.  
Essas divisões tornam a rede **mais organizada, eficiente e segura**, além de reduzir congestionamentos, pois limitam o tráfego de broadcast dentro de cada sub-rede.

---

## Máscara de Sub-rede

A **máscara de sub-rede** define quais bits de um endereço IP pertencem à parte da **rede** e quais pertencem à parte do **host**.  

Exemplo: um **IP 192.168.10.8** com máscara **255.255.255.0** indica que:

- **192.168.10** → parte da rede (fixa, não muda).  
- **8** → parte do host (pode variar de 1 até 254).  

Assim, temos **254 endereços de host disponíveis** (de 192.168.10.1 até 192.168.10.254).  
O **.0** é reservado como **network address** e o **.255** como **broadcast**.

### Representação em Binário

- IP: 192.168.1.10 → 11000000.10101000.00000001.00001010  
- Máscara: 255.255.255.0 (/24) → 11111111.11111111.11111111.00000000  

- Os **1** da máscara representam a **rede**.  
- Os **0** da máscara representam o **host**.  

Neste caso: **24 bits para rede** e **8 bits para host**.

---

## CIDR Notation (/24, /26, etc.)

O **CIDR (Classless Inter-Domain Routing)** é uma forma simplificada de representar máscaras de sub-rede.  
Ele indica **quantos bits, a partir da esquerda, são usados para a rede**.

### Exemplos

- **/24**  
  - Máscara: 255.255.255.0  
  - 24 bits para rede, 8 bits para host  
  - 2^8 = 256 endereços, sendo 254 para hosts  

- **/26**  
  - Máscara: 255.255.255.192  
  - 26 bits para rede, 6 bits para host  
  - 2^6 = 64 endereços, sendo 62 para hosts  

- **/27**  
  - Máscara: 255.255.255.224  
  - 27 bits para rede, 5 bits para host  
  - 2^5 = 32 endereços, sendo 30 para hosts  

### Por que isso é útil?

Imagine que uma empresa tem uma rede **/24 (254 hosts disponíveis)**, mas um setor precisa de apenas **23 computadores** a mais. Em vez de desperdiçar uma rede inteira com mais um octeto, o administrador pode criar uma sub-rede **/27**, que fornece **30 endereços para hosts**, atendendo à necessidade de forma mais eficiente.

Primeiro, vê-se quantos hosts são necessários. No caso: 23 dispositivos. Mas como precisamos sempre reservar 2 endereços (um para Network Address e outro para Broadcast Address), a conta mínima é: 23 + 2 = 25 endereços.

Aplicamos a fórmula do número de hosts em uma sub-rede: Número de hosts = (2^n) - 2. Onde `n` é a quantidade de bits de host. Portanto, com 5 bits de host → (2^5) - 2 = 32 - 2 = 30 hosts ✅

- Com 4 bits de host → (2^4) - 2 = 16 - 2 = 14 hosts ❌ (não serve, porque precisamos de pelo menos 25). Logo, **precisamos de 5 bits para host**. Um endereço IPv4 tem 32 bits no total. Se 5 bits são para host, 32 - 5 = 27 bits para a rede, ou seja, a máscara ficaria 255.255.255.224.

### Importante

Quanto **maior** o número depois da barra (`/`), **mais bits são usados para a rede** → **menos hosts ficam disponíveis**.  
Quanto **menor** o número depois da barra (`/`), **menos bits para a rede** → **mais hosts disponíveis**.

---

## Número de Hosts em uma Sub-rede

A fórmula é:
`Número de hosts = (2^n) - 2`

- `n` = quantidade de bits para host  
- Subtrai-se 2 porque:
  - 1 endereço é o **network address**  
  - 1 endereço é o **broadcast address**  

### Exemplos

- /24 → 8 bits para host → 2^8 = 256 → 256 - 2 = **254 hosts**  
- /26 → 6 bits para host → 2^6 = 64 → 64 - 2 = **62 hosts**  
- /27 → 5 bits para host → 2^5 = 32 → 32 - 2 = **30 hosts**

---

## Network Address

É o **primeiro endereço** de uma sub-rede.  
Ele identifica a própria rede e **não pode ser atribuído a um host**.

Exemplo:  
- Sub-rede: 192.168.1.0/24  
- **Network Address:** 192.168.1.0  

---

## Broadcast Address

É o **último endereço** de uma sub-rede.  
Ele serve para enviar mensagens para **todos os hosts daquela rede**.

Exemplo:  
- Sub-rede: 192.168.1.0/24  
- **Broadcast Address:** 192.168.1.255  

---

## Resumindo

- **Subnetting:** divide redes grandes em menores, otimizando endereços.  
- **Máscara de sub-rede:** define parte da rede e parte do host.  
- **CIDR (/24, /26, /27):** indica quantos bits são da rede.  
- **Hosts:** calculados com (2^n) - 2.  
- **Network Address:** primeiro IP da rede.  
- **Broadcast Address:** último IP da rede.  

> Subnetting é essencial para otimizar redes, reduzir congestionamentos e melhorar segurança e controle administrativo.
