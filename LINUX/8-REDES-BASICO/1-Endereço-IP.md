# Endereçamento de IP

O **endereçamento IP** é o sistema que identifica dispositivos em uma rede, permitindo que computadores, servidores e outros equipamentos se comuniquem entre si. Cada dispositivo em uma rede TCP/IP precisa ter um endereço único.

## Tipos de Endereço IP

Existem duas versões principais:

1. **IPv4**
   - Formato: 32 bits, geralmente escrito como quatro números decimais separados por pontos.
   - Exemplo: 192.168.0.1
   - Cada número varia de 0 a 255.
   - Possui aproximadamente 4,3 bilhões de endereços possíveis.

2. **IPv6**
   - Formato: 128 bits, escrito como oito grupos de quatro dígitos hexadecimais separados por dois pontos.
   - Exemplo: 2001:0db8:85a3:0000:0000:8a2e:0370:7334
   - Criado para suportar o crescimento da internet e resolver a escassez de endereços IPv4.

## Componentes de um Endereço IPv4

Um endereço IPv4 é composto por duas partes:

1. **Identificador da rede (Network ID):** define a rede à qual o dispositivo pertence.
2. **Identificador do host (Host ID):** identifica o dispositivo específico dentro dessa rede.

### Máscara de Sub-rede

A **máscara de sub-rede** define qual parte do endereço é da rede e qual é do host.

- Exemplo: 192.168.1.10/24  
  - /24 significa que os primeiros 24 bits são da rede.
  - Os últimos 8 bits são para identificar hosts na rede.

## Classes de Endereços IPv4 (históricas)

As classes ajudam a organizar o endereçamento em redes:

- **Classe A:** 1.0.0.0 – 126.255.255.255  
  - Redes grandes, muitos hosts.  
- **Classe B:** 128.0.0.0 – 191.255.255.255  
  - Redes médias.  
- **Classe C:** 192.0.0.0 – 223.255.255.255  
  - Redes pequenas, poucos hosts.  
- **Classe D:** 224.0.0.0 – 239.255.255.255  
  - Multicast.  
- **Classe E:** 240.0.0.0 – 255.255.255.255  
  - Reservada para uso futuro ou experimental.

## Tipos de Endereço IP

- **IP Público:** acessível pela internet, único globalmente.
- **IP Privado:** usado em redes internas, não roteável pela internet. Exemplos de faixas privadas:
  - 10.0.0.0 – 10.255.255.255
  - 172.16.0.0 – 172.31.255.255
  - 192.168.0.0 – 192.168.255.255

- **IP Estático:** fixo, não muda.
- **IP Dinâmico:** atribuído automaticamente por um servidor DHCP, pode mudar.

## Diferença entre IP e MAC

- **IP:** endereço lógico, pode mudar, usado para roteamento.
- **MAC:** endereço físico da placa de rede, único e fixo.
