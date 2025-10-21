# Shell

## O que é Shell?
O **Shell** é uma interface baseada em texto que permite ao usuário interagir com o sistema operacional. Ele serve como uma camada entre o usuário e o Kernel, recebendo comandos, interpretando-os e retornando os resultados.  

Embora pareça que estamos nos comunicando diretamente com o Kernel, na verdade o Shell atua como um tradutor, repassando as instruções e exibindo a resposta.

---

## Como o Shell funciona?
O funcionamento do Shell pode ser entendido em quatro etapas principais:

1. **User Input** – O usuário digita um comando no terminal.  
2. **Command Parsing** – O Shell interpreta e analisa o comando digitado.  
3. **Command Execution** – O Shell encaminha o comando para o Kernel, que executa a ação necessária.  
4. **Output Display** – O resultado da execução é exibido de volta ao usuário no terminal.  

---

## Automação com Shell Script
O Shell permite a criação de **scripts**, que nada mais são do que arquivos de texto contendo uma sequência de comandos pré-definidos.  
Esses scripts automatizam tarefas repetitivas, como verificação de arquivos de log, backups, monitoramento de recursos e muito mais.  

Exemplo prático: verificar em um log a ocorrência de determinado texto e emitir um alerta.

---

## Por que usar Shell Scripts?
- **Eficiência e consistência** – Automatiza tarefas para reduzir erros humanos.  
- **Flexibilidade** – Pode ser adaptado a diferentes cenários.  
- **Automação** – Executa atividades de forma autônoma.  
- **Otimização de tempo** – Economiza tempo em processos manuais.  
- **Escalabilidade** – Útil em ambientes com múltiplos servidores e usuários.  

---

## Exemplo de Shell Script

Aqui está um script simples que verifica se há a palavra "ERROR" em um arquivo de log:

```bash
#!/bin/bash
# Script simples para verificar erros em um arquivo de log

LOGFILE="/var/log/syslog"

if grep -q "ERROR" "$LOGFILE"; then
    echo "⚠️ Atenção: Erros encontrados em $LOGFILE"
else
    echo "✅ Nenhum erro encontrado em $LOGFILE"
fi
```
**Como usar:**
1 - Salve o conteúdo em um arquivo, por exemplo check_log.sh.
2 - Dê permissão de execução.
```bash
chmod +x check_log.sh
```
3 - Execute o script:
```bash
./check_log.sh
```
4 - Caso o arquivo em questão precise de permissão para poder ler, execute o script com sudo.
