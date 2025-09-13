# Comando Netstat

O **netstat** (network statistics) é uma ferramenta usada para exibir informações detalhadas sobre conexões de rede, tabelas de roteamento e estatísticas de interfaces de rede.  

Ele é útil para administradores e analistas de rede verificarem **quais conexões estão ativas, quais portas estão em uso e por quais processos**.

## Sintaxe Básica
```bash
netstat [opções]
```

---

## Principais Opções

| Opção       | Função |
|-------------|--------|
| `-a`        | Mostra todas as conexões e portas de escuta |
| `-n`        | Mostra endereços e portas em formato numérico (sem resolver nomes) |
| `-t`        | Mostra conexões TCP |
| `-u`        | Mostra conexões UDP |
| `-l`        | Mostra apenas portas em escuta (listening) |
| `-p`        | Mostra o **PID** e o programa que está usando a conexão |
| `-r`        | Mostra a tabela de roteamento |
| `-i`        | Mostra estatísticas das interfaces de rede |
| `-s`        | Mostra estatísticas por protocolo |

---

## Exemplos Práticos

### 1. Ver conexões TCP ativas
```bash
netstat -at
```
### 2. Ver conexões UDP ativas
```bash
netstat -au
```
### 3. Ver todas as conexões em formato numérico
```bash
netstat -an
```
### 4. Ver portas em escuta e seus processos
```bash
netstat -tulnp
```
Saída típica:
```bash
Proto Recv-Q Send-Q Local Address Foreign Address State PID/Program name
tcp 0 0 0.0.0.0:22 0.0.0.0:* LISTEN 875/sshd
udp 0 0 0.0.0.0:68 0.0.0.0:* 567/dhclient
```

## Usos Comuns
- Listar quais portas estão abertas no sistema
- Descobrir qual processo está ocupando uma porta
- Monitorar conexões estabelecidas e em espera
- Verificar a tabela de roteamento do host
- Obter estatísticas detalhadas sobre tráfego de rede

## Observações Importantes
- Em muitas distribuições modernas (como Debian, Ubuntu, CentOS), o `netstat` não vem mais instalado por padrão, pois foi **substituído pelo `ss`**.  
- O `ss` é considerado mais rápido e fornece informações mais detalhadas, mas a lógica de uso é semelhante.  
- Mesmo assim, o `netstat` continua muito usado em tutoriais e ambientes legados.

# Comando `ss` no Linux

O comando `ss` (socket statistics) é uma ferramenta moderna que substitui o `netstat` em muitas distribuições Linux, oferecendo informações sobre sockets de rede de forma **mais rápida, detalhada e eficiente**. Ele é amplamente utilizado para monitorar conexões TCP, UDP, sockets Unix e estatísticas de tráfego.

## Diferenças principais entre `ss` e `netstat`
- **Velocidade**: `ss` é muito mais rápido, pois acessa diretamente os dados do kernel sem precisar percorrer arquivos em `/proc`.
- **Detalhamento**: oferece mais informações sobre cada conexão (como timers TCP).
- **Disponibilidade**: em algumas distribuições modernas, `netstat` nem vem instalado, mas `ss` já está presente por padrão.

## Uso básico

- Listar todas as conexões abertas:
```bash
ss -a
```
- Mostrar apenas conexões TCP:
```bash
ss -t
```
- Mostrar apenas conexões UDP:
```bash
ss -u
```
- Mostrar apenas sockets de domínio Unix:
```bash
ss -x
```

## Informações de estado da conexão
- Conexões estabelecidas:
```bash
ss -t state established
```
- Conexões em espera (listening):
```bash
ss -ltn
```
- Conexões fechadas ou encerradas:
```bash
ss -t state closed
```

## Opções úteis
- Mostrar estatísticas resumidas:
```bash
ss -s
```
- Mostrar nome do processo usando o socket:
```bash
ss -p
```
- Mostrar conexões em determinada porta (ex.: 80):
```bash
ss -tln sport = :80
```
- Filtrar por endereço IP:
```bash
ss -tn dst 8.8.8.8
```

## Exemplos práticos
1. Ver todas as conexões TCP ativas e seus processos:
```bash
ss -tup
```
2. Ver quais portas estão abertas para escuta:
```bash
ss -lnt
```
3. Estatísticas gerais de sockets no sistema:
```bash
ss -s
```

## Conclusão
Enquanto o `netstat` ainda pode ser usado em alguns sistemas, o **`ss` é a ferramenta recomendada** atualmente para monitorar conexões de rede no Linux. Ele é mais rápido, mais detalhado e já vem instalado por padrão na maioria das distribuições.  

Para administrar redes ou realizar perícias digitais, aprender a usar `ss` é essencial, pois fornece informações cruciais sobre **quem está conectado, em qual porta e em qual estado**.
