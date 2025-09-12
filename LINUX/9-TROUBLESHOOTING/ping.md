# Comando Ping

O **ping** é uma ferramenta de rede usada para testar a conectividade entre computadores em uma rede. Ele envia pacotes **ICMP (Internet Control Message Protocol) Echo Request** para o destino e espera receber respostas (**Echo Reply**). É útil para diagnosticar problemas de rede e medir tempos de resposta.

## Sintaxe Básica
```bash
ping [opções] destino
```
- `destino`: Pode ser um endereço IP ou um nome de domínio.

**Exemplo:**
```bash
ping 8.8.8.8
ping google.com
```

## Funcionamento
1. O comando envia um pacote ICMP Echo Request para o destino.
2. O destino responde com um pacote ICMP Echo Reply.
3. O ping calcula o tempo de ida e volta (**RTT – Round Trip Time**) e mostra se houve perda de pacotes.

## Saída do Ping
Uma saída típica do ping se parece com isto:
```bash
PING google.com (142.250.72.14) 56(84) bytes of data.
64 bytes from iad23s63-in-f14.1e100.net (142.250.72.14): icmp_seq=1 ttl=115 time=12.3 ms
64 bytes from iad23s63-in-f14.1e100.net (142.250.72.14): icmp_seq=2 ttl=115 time=11.8 ms
```
- **icmp_seq**: número sequencial do pacote enviado  
- **ttl**: "Time To Live", indica o número máximo de saltos que o pacote pode percorrer  
- **time**: tempo em milissegundos que o pacote levou para ir e voltar  

No final, o ping mostra estatísticas como:

- Número de pacotes enviados e recebidos
- Percentual de perda de pacotes
- Tempo mínimo, máximo e médio de resposta

## Principais Opções
| Opção         | Função |
|---------------|--------|
| `-c N`        | Envia apenas N pacotes e encerra |
| `-i N`        | Intervalo de N segundos entre envios |
| `-t N`        | Define o valor de TTL |
| `-s N`        | Define o tamanho do pacote em bytes |
| `-4`          | Força uso de IPv4 |
| `-6`          | Força uso de IPv6 |

**Exemplo com opções:**
```bash
ping -c 5 -i 2 google.com
```
Envia 5 pacotes para `google.com` com intervalo de 2 segundos entre eles.

## Usos Comuns
- Verificar se um host está ativo
- Medir latência da rede
- Diagnosticar perda de pacotes
- Testar conectividade com um servidor ou site específico

## Observações

- Alguns hosts podem bloquear pacotes ICMP, fazendo o ping falhar mesmo que o host esteja online.
- O ping não testa portas TCP ou UDP; para isso, ferramentas como `telnet`, `nc` ou `nmap` são mais adequadas.



