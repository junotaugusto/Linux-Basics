# Comando Traceroute

O **traceroute** é uma ferramenta de diagnóstico de rede usada para rastrear o caminho que os pacotes percorrem até um destino. Ele mostra todos os **saltos** (routers) intermediários entre o computador de origem e o destino, ajudando a identificar problemas de conectividade ou lentidão em pontos específicos da rede.

## Sintaxe Básica
```bash
traceroute [opções] destino
```
- `destino`: Pode ser um endereço IP ou um nome de domínio.

**Exemplo:**
traceroute 8.8.8.8
traceroute google.com

**OBS:** No Windows, o comando equivalente é `tracert`.

## Como Funciona
1. O traceroute envia pacotes **UDP ou ICMP** (dependendo do sistema) com TTL inicial igual a 1.
2. Cada roteador que recebe o pacote decrementa o TTL em 1.
3. Quando o TTL chega a 0, o roteador envia uma mensagem ICMP “Time Exceeded” de volta para o remetente.
4. O traceroute aumenta o TTL gradualmente, descobrindo cada salto até chegar ao destino.
5. Para cada salto, ele mede o tempo de ida e volta (**RTT**).

## Saída do Traceroute
Uma saída típica se parece com isto:
```bash
traceroute to google.com (142.250.72.14), 30 hops max, 60 byte packets
1 192.168.1.1 1.123 ms 0.987 ms 1.056 ms
2 10.10.0.1 10.234 ms 10.198 ms 10.221 ms
3 142.250.72.14 12.345 ms 12.210 ms 12.299 ms
```

- **Coluna 1**: número do salto (hop)  
- **Coluna 2**: IP ou hostname do roteador  
- **Colunas 3-5**: tempos de ida e volta (RTT) para cada tentativa  

Se aparecer `* * *`, significa que não houve resposta do roteador nesse salto.

## Principais Opções

| Opção           | Função |
|-----------------|--------|
| `-m N`          | Define o TTL máximo (máximo de saltos) |
| `-n`            | Mostra apenas IPs, sem tentar resolver nomes |
| `-p porta`      | Define a porta inicial para os pacotes UDP |
| `-q N`          | Número de pacotes enviados por salto (default 3) |
| `-w tempo`      | Timeout para resposta em segundos |
| `-I`            | Usa ICMP Echo em vez de UDP (similar ao ping) |

**Exemplo com opções:**
```bash
traceroute -n -m 20 google.com
```
- Mostra até 20 saltos e exibe apenas os IPs, sem nomes.

## Usos Comuns
- Descobrir a rota que os pacotes percorrem até um servidor
- Identificar onde há lentidão ou falhas na rede
- Diagnosticar problemas de roteamento ou perda de pacotes
- Verificar se um host é acessível através da rede

## Observações

- Alguns roteadores podem bloquear pacotes ICMP, fazendo com que alguns saltos não respondam (`* * *`), mesmo que a rede esteja funcionando.
- O traceroute mostra **apenas o caminho**, não testa portas ou serviços.
- É útil para administradores de rede e para diagnóstico de problemas de internet.

