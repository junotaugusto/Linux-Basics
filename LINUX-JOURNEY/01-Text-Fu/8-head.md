# Comando head

O comando `head` é usado para exibir as primeiras linhas de um arquivo de texto. Isso é útil quando estamos lidando com arquivos grandes, como logs do sistema, e queremos visualizar apenas o início do conteúdo sem abrir tudo.

Se você rodar:

```
cat /var/log/syslog
```

Vai ver páginas e páginas de texto.

Agora, com `head`:

```
head /var/log/syslog
```

Ele vai mostrar apenas as 10 primeiras linhas (esse é o comportamento padrão do `head`).

Você pode escolher quantas linhas deseja visualizar com a flag `-n` (de number).  
Exemplo:

```
head -n 15 /var/log/syslog
```

Esse comando exibe as 15 primeiras linhas do arquivo `/var/log/syslog`.

O `head` é muito útil para inspecionar rapidamente arquivos grandes, especialmente arquivos de log, como os que ficam em `/var/log/`.
