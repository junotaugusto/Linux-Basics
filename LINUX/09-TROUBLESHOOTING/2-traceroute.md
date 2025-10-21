# Comando Traceroute

# Entendendo o Traceroute

O `traceroute` é uma ferramenta de diagnóstico de rede que **mostra o caminho que os pacotes percorrem até um destino**. Vamos detalhar como e por que ele funciona do jeito que funciona.

## 1. Para que serve o traceroute?
- Descobrir todos os roteadores (saltos) que existem entre o seu computador e o destino.
- Medir a latência (tempo de resposta) de cada salto.
- Identificar onde ocorrem atrasos ou perda de pacotes na rede.
- Diagnosticar problemas de roteamento ou falhas de conectividade.

Ou seja, ele ajuda a **mapear a rota e medir desempenho da rede**.

## 2. Como ele envia pacotes?
O traceroute envia **pacotes IP normais**, mas com um detalhe: o **TTL (Time To Live)** é usado de forma estratégica.

### TTL (Time To Live)
- É um valor em cada pacote IP que indica **quantos saltos ele pode percorrer**.
- Cada roteador que recebe o pacote **decrementa o TTL em 1**.
- Quando o TTL chega a 0, o pacote **não é mais encaminhado** e é descartado.
- O roteador que descarta o pacote envia uma mensagem ICMP “Time Exceeded” de volta para o remetente.

Isso é essencial: **o pacote precisa ser descartado no caminho** para que o traceroute saiba que ele chegou até aquele salto. Se não houvesse esse mecanismo, o traceroute não conseguiria identificar os roteadores intermediários até o destino.

## 3. Por que ele não mostra apenas os roteadores até o destino?
Teoricamente, poderíamos imaginar que o traceroute perguntasse a cada roteador “quem está no caminho?”. Mas a rede IP não funciona assim:
- Os roteadores **não guardam informações sobre o caminho completo** de cada pacote.
- Eles apenas **encaminham pacotes** baseado na tabela de roteamento.
- Não existe um protocolo padrão para que um pacote “peça” a lista de todos os roteadores até o destino.

Então, o **truque do traceroute** é enviar pacotes com TTL crescente:
1. TTL = 1 → atinge o primeiro roteador e é descartado → roteador responde → traceroute sabe quem é o 1º salto.
2. TTL = 2 → atinge o 2º roteador e é descartado → resposta → traceroute sabe quem é o 2º salto.
3. TTL = 3 → atinge o 3º salto e assim por diante, até chegar no destino.

Ou seja, **o descarte dos pacotes é intencional** e necessário para descobrir cada salto.

## 4. Resumo do processo
1. Envia pacote com TTL = 1 → primeiro roteador descarta → recebe ICMP → identifica o 1º salto.  
2. Envia pacote com TTL = 2 → segundo roteador descarta → recebe ICMP → identifica o 2º salto.  
3. Repete aumentando TTL até chegar no destino ou TTL máximo.  
4. Para cada salto, mede-se o tempo de ida e volta (RTT).  

## 5. Visualizando na prática
Imagine que a rota até o destino seja:
```bash
Seu PC → R1 → R2 → R3 → Destino
```
- TTL = 1 → pacote chega em R1 → descartado → ICMP de volta → traceroute registra R1.
- TTL = 2 → pacote chega em R2 → descartado → ICMP de volta → traceroute registra R2.
- TTL = 3 → pacote chega em R3 → descartado → ICMP de volta → traceroute registra R3.
- TTL = 4 → pacote chega no Destino → responde normalmente → traceroute registra Destino.

> Perceba que **os pacotes descartados não são perda real**, é só parte do mecanismo para descobrir a rota.

## 6. Conclusão
O traceroute funciona **“descartando pacotes de propósito”** para receber respostas dos roteadores intermediários, permitindo que possamos:
- Ver o caminho exato que os pacotes percorrem.
- Medir latência de cada salto.
- Detectar onde podem existir problemas de rede.

Sem esse mecanismo, o protocolo IP não permitiria descobrir a rota hop a hop.

## Sintaxe Básica
```bash
traceroute [opções] destino
```
- `destino`: Pode ser um endereço IP ou um nome de domínio.

**Exemplo:**
traceroute 8.8.8.8
traceroute google.com

**OBS:** No Windows, o comando equivalente é `tracert`.

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
- Se aparecer `* * *`, significa que não houve resposta do roteador nesse salto.

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

### E se o TTL máximo for maior que a rota real?
Exemplo: TTL máximo definido foi de 50, mas o destino está a 12 saltos.

- Os primeiros 12 pacotes vão chegar ao destino normalmente, e você verá os IPs/nomes de cada roteador.
- Depois que o destino responde, o traceroute **encerra automaticamente**.
- **Não aparecerão asteriscos** por causa do TTL maior, porque ele não precisa enviar pacotes além do destino.
- **Asteriscos só aparecem** se algum roteador no caminho **não responder**.

### E se o TTL máximo for menor que a rota real?
Exemplo: TTL máximo definido é de 5, mas o destino está a 12 saltos.

- O traceroute envia pacotes TTL = 1, 2, 3, 4, 5.
- Ele **encerra após o TTL máximo** definido, sem tentar mais.
- **Não aparecem asteriscos automaticamente** por causa do TTL menor; ele só mostra os saltos alcançados.
- **Asteriscos só aparecem** se algum desses primeiros 5 roteadores **não responder** dentro do tempo limite.
