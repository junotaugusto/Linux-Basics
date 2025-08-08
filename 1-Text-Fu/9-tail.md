# Comando tail

O comando `tail` é similar ao comando `head`, mas ao invés de mostrar o início de um arquivo, ele exibe as últimas linhas. Por padrão, `tail` mostra as últimas 10 linhas de um arquivo.

Exemplo:

```
tail /var/log/syslog
```

Isso mostra as últimas 10 linhas do arquivo `/var/log/syslog`.

Você também pode alterar a quantidade de linhas exibidas com a flag `-n` (number):

```
tail -n 10 /var/log/syslog
```

Outra opção muito útil é a flag `-f` (follow). Essa flag faz com que o `tail` continue exibindo em tempo real as novas linhas adicionadas ao final do arquivo conforme ele cresce:

```
tail -f /var/log/syslog
```

Enquanto o sistema estiver funcionando e registrando eventos, o arquivo `/var/log/syslog` continuará sendo atualizado. Com `tail -f`, você pode observar essas mudanças ao vivo, o que é muito útil para monitoramento de logs em tempo real.
