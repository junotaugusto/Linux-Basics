# Mounting a File System no Linux

## O que é montar (mount)?
No Linux (e em outros sistemas Unix-like), **montar um sistema de arquivos (mounting a file system)** significa **tornar um dispositivo de armazenamento acessível** dentro da árvore de diretórios do sistema operacional.

Ou seja, quando você conecta um HD, SSD, pendrive ou até uma partição, ele só poderá ser usado depois de ser **montado** em um ponto do sistema chamado **ponto de montagem** (*mount point*).

## Por que montar?

Porque o hardware sozinho não basta — ele só fornece blocos de dados (0s e 1s). O sistema de arquivos traduz esses blocos em arquivos/pastas organizados.

A montagem é o passo que diz ao sistema operacional:
*"Use esse sistema de arquivos (ext4/FAT32/NTFS/etc) que está nesse dispositivo, e anexe-o aqui nesse diretório para que o usuário consiga acessar os arquivos."*

## Como funciona
- O Linux tem uma **árvore única de diretórios**, que começa no `/` (raiz).
- Dispositivos extras (pendrives, HDs, ISOs, partições, etc.) não aparecem automaticamente em um drive separado, como no Windows (`C:\`, `D:\`) ou MacOS.
- Em vez disso, eles são "anexados" (*mounted*) em um **diretório específico** dentro da árvore.

Exemplo:
- Um pendrive pode ser montado em `/mnt/usb` ou `/media/user/pendrive`.
- Depois de montado, você acessa os arquivos indo até esse diretório.

## Comando básico `mount`

Quando você conecta um pendrive, HD externo ou cria uma nova partição, o Linux cria um device file dentro de `/dev`. Esses nomes seguem um padrão:

Discos SATA/SCSI/USB comuns → sda, sdb, sdc...
- sda1, sda2 = partições do disco sda
- sdb1 = primeira partição do segundo disco (pode ser seu pendrive)

**Como descobrir qual é o seu dispositivo recém-plugado:**

O comando `lsblk` lista os discos e partições em árvore. A saída normalmente é:
sda      100G
├─sda1   512M
├─sda2   30G  /
└─sda3   70G  /home
sdb      32G
└─sdb1   32G

Nesse caso, sdb1 seria o seu pendrive. Até porque, a primeira partição se chama `sda`, depois vem o `sdb`, `sdc` e assim por diante.

### Outros comandos
`dmesg | tail -20` → mostra as últimas mensagens do kernel, incluindo quando um novo dispositivo foi detectado.
`sudo fdisk -l` → lista os discos e partições com detalhes.

### Montando o dispositivo
O comando para montar um sistema de arquivos é:
```bash
sudo mount /dev/nome_do_dispositivo mount/point
```
- O nome do dispositivo pode ser descoberto utilizando o comando `lsblk`conforme descrito acima.
- Depois, defina o caminho do ponto de montagem. **É comum criar um diretório vazio para ser o ponto de montagem.** Por exemplo, com o comando `mkdir /mnt/usb`.

Um exemplo prático seria:
```bash
sudo mount /dev/sdb1 /mnt/usb
```
`/dev/sdb1` → dispositivo físico (partição do pendrive).
`/mnt/usb` → diretório onde os arquivos ficarão acessíveis.

Agora, os arquivos do pendrive estarão disponíveis dentro de `/mnt/usb`.

## Montagem automática (fstab)

Se você quiser que o dispositivo seja montado automaticamente em cada inicialização, precisa editar o arquivo `/etc/fstab`.

Exemplo de entrada no fstab:
```bash
/dev/sdb1   /mnt/usb   ext4   defaults   0   0
```