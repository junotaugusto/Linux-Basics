# Comandos de Manipulação e Análise de Texto

## grep
O comando **grep** é utilizado para realizar buscas em arquivos de texto.  
Ele procura padrões definidos pelo usuário, que podem ser palavras ou expressões regulares, e retorna as linhas que correspondem ao critério. É muito usado para localizar rapidamente informações em arquivos grandes, como logs de sistema.  

A sintaxe básica é:  
(grep 'padrão' arquivo)  

Exemplo:  

```bash
grep "error" syslog.txt
```
→ mostra todas as linhas do arquivo que contêm a palavra "error".  

### Flags mais usadas:
- (-i) → ignora maiúsculas e minúsculas.  
- (-r) → busca recursivamente dentro de um diretório.  
- (-v) → mostra apenas linhas que **não** correspondem ao padrão.  

Também podemos usar `grep` em conjunto com outros comandos via pipe (`|`):  

```bash
cat syslog.txt | grep "error")  
```

---

## sort
O comando **sort** organiza linhas de texto de acordo com uma ordem definida.  
Por padrão, ele realiza a ordenação alfabética, mas pode também inverter a ordem ou ordenar numericamente. É útil para organizar listas, resultados de buscas e saídas de outros comandos.  

Sintaxe:  
(sort [opções] arquivo)  

Por padrão, a ordem é alfabética (A → Z).  

### Flags mais usadas:
- (-r) → inverte a ordem.  
- (-n) → organiza de forma numérica.  

Exemplos:  
```bash
sort nomes.txt  
sort -r nomes.txt  
sort -n numeros.txt 
```

👉 Podemos combinar `grep` com `sort`. Exemplo:  

```bash
cat syslog.txt | grep "error" | sort
```

E ainda redirecionar para outro arquivo:  

```bash
cat syslog.txt | grep "error" | sort > erros.txt  
```

---

## cut
O comando **cut** extrai partes específicas de cada linha de um arquivo de texto. Ele trabalha geralmente com delimitadores e campos, permitindo selecionar colunas específicas em arquivos estruturados. É muito usado para manipular arquivos em formato de tabela ou arquivos de configuração.

Exemplos:  

```bash
cut -d ":" -f1 /etc/passwd
```
→ Mostra apenas a primeira coluna (nomes de usuários) do arquivo `/etc/passwd`, usando ":" como delimitador.  

Principais opções:  
- (-d) → define o delimitador.  
- (-f) → seleciona o(s) campo(s).  

---

## sed
O **sed** (stream editor) é uma ferramenta voltada para edição e transformação de texto de forma automatizada. Ele permite substituir, deletar, inserir ou modificar conteúdos dentro de arquivos, sem abrir um editor de texto tradicional. Pode atuar de forma temporária, exibindo apenas no terminal, ou aplicar mudanças diretamente no arquivo.  

Exemplo básico:  

```bash
sed 's/error/ERRO/' syslog.txt
```

→ Substitui a palavra "error" por "ERRO" em todas as ocorrências, mostrando no terminal.  

### Flag importante:
- (-i) → faz a modificação diretamente no arquivo (in-place).  

Exemplo:  

```bash
sed -i 's/error/ERRO/' syslog.txt   
```
→ Altera o arquivo `syslog.txt` diretamente.

---

## awk
O **awk** é uma linguagem de processamento de texto poderosa, projetada para analisar dados estruturados em colunas. Ele permite realizar filtragens, cálculos, impressões condicionais e até gerar relatórios personalizados. É bastante utilizado para análise de arquivos de log e manipulação de grandes volumes de dados.  

Exemplo básico:  

```bash
awk '{print $1}' syslog.txt 
```
→ Mostra apenas a primeira coluna do arquivo.  

Mais exemplos:  
(awk '{print $1, $3}' syslog.txt) → mostra a primeira e a terceira coluna.  
(awk '/error/ {print $0}' syslog.txt) → mostra apenas as linhas que contêm "error".  

👉 O `awk` é especialmente útil para relatórios e filtragens em logs.  

---
