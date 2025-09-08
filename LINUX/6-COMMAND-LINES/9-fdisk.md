# fdisk (Fixed Disk)

O **fdisk** é uma ferramenta poderosa de linha de comando usada para **criar, modificar e excluir partições** em dispositivos de armazenamento. Ele é um dos utilitários clássicos do Linux para gerenciamento de discos, permitindo configurar como o sistema operacional vai organizar e acessar os dados dentro de um dispositivo.

---

## Uso Básico

### Abrindo um Disco para Particionamento
```bash
sudo fdisk /dev/sda
```
Esse comando abre o disco `/dev/sda` para edição de partições.
`/dev/sda` → representa o primeiro disco rígido identificado pelo sistema.
`/dev/sdb`, `/dev/sdc` → seriam outros discos, como HDs adicionais, SSDs ou até pendrives conectados.

⚠️ É importante substituir /dev/sda pelo dispositivo correto do seu sistema, caso contrário você pode alterar o disco errado.

# Comandos do `fdisk`

O `fdisk` é uma ferramenta de linha de comando usada para **criar, modificar e excluir partições** em dispositivos de armazenamento. Quando você o executa, ele entra em um **modo interativo** no qual você digita letras que correspondem a ações.

Para executá-lo, digite o disco que quer realizar as alterações. Por exemplo o sda.
```bash
sudo fdisk /dev/sda
```
Ele irá abrir o menu:

### Comando `m`
Mostra o **menu de ajuda** com todos os comandos disponíveis.

### Comando `p`
Exibe a **tabela de partições** do disco selecionado.
Isso mostra:
- Número das partições (`/dev/sda1`, `/dev/sda2`, etc.).
- Tipo de partição (Linux, EFI, swap, etc.).
- Tamanho e setores usados.

### Comando `n`
Cria uma **nova partição**.
Passos típicos:
1. Escolher **primária (p)** ou **estendida (e)**.  
2. Número da partição (1 a 4).  
3. Setor inicial e final (ou tamanho, como `+2G`).  

### Comando `d`
Apaga uma partição existente.
⚠️ Remove todos os dados da partição escolhida.

### Comando `t`
Altera o **tipo de partição**.
Exemplos:
- `83` → Linux filesystem.  
- `82` → Linux swap.  
- `07` → NTFS.  
- `ef` → EFI System.  

### Comando `w`
Grava as mudanças feitas no disco e **sai**.
⚠️ Alterações não podem ser desfeitas após este comando.

### Comando `q`
Sai do `fdisk` **sem salvar** alterações.

### Outros Comandos Úteis
- `v` → Verifica erros na tabela de partições.  
- `x` → Funções avançadas.  
- `g` → Cria nova tabela de partições GPT.  
- `o` → Cria nova tabela de partições MBR.  

### Fluxo de Uso Comum
1. `m` → ajuda.  
2. `p` → listar partições.  
3. `n` → criar partição.  
4. `t` → definir tipo.  
5. `w` → salvar e sair.  

---

## Exemplo Prático

bash





