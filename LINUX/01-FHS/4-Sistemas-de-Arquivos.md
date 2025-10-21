# Tipos de Sistemas de Arquivos (Filesystem) Comuns

Um sistema de arquivos (filesystem) é a forma como o sistema operacional organiza e gerencia os dados em um dispositivo de armazenamento. Cada sistema de arquivos possui suas características, vantagens e limitações.  

## ext4 (Fourth Extended Filesystem)
- **Journaling**: mantém um diário (journal) de mudanças, ajudando a evitar corrupção de dados em caso de falhas inesperadas.  
- **Large File Support**: suporta arquivos individuais de até **16 terabytes**.  
- **Large Filesystem Support**: suporta sistemas de arquivos de até **1 exabyte**.  
- **Enhanced Performance**: possui técnicas como *delayed allocation* e *multiblock allocation*, que melhoram a performance de escrita.  
- **Extensibilidade**: evolução direta do ext3, com retrocompatibilidade.  
- **Uso comum**: é o padrão em muitas distribuições Linux modernas.  

## XFS
- **Alta performance**: especialmente bom em manipular arquivos muito grandes.  
- **Journaling avançado**: permite recuperação rápida após falhas.  
- **Desempenho paralelo**: muito eficiente em sistemas com múltiplos processadores.  
- **Limitações**: não lida tão bem com um grande número de arquivos pequenos em comparação ao ext4.  
- **Uso comum**: frequentemente utilizado em servidores e ambientes que lidam com grandes volumes de dados.  

## NTFS (New Technology File System)
- **Desenvolvido pela Microsoft**: usado principalmente em sistemas Windows.  
- **Journaling**: possui registro de transações.  
- **Controle de permissões**: ACLs (Access Control Lists) permitem controle granular de acesso.  
- **Compressão e criptografia**: oferece suporte nativo a recursos como EFS (Encrypting File System).  
- **Compatibilidade**: Linux pode ler e escrever em NTFS usando o driver `ntfs-3g`.  

## FAT32 (File Allocation Table 32)
- **Compatibilidade universal**: funciona em praticamente todos os sistemas operacionais (Windows, Linux, macOS, câmeras, consoles, etc).  
- **Limite de tamanho de arquivo**: suporta arquivos de no máximo **4 GB**.  
- **Limite de partição**: até **2 TB**.  
- **Sem journaling**: mais vulnerável à corrupção de dados após falhas.  
- **Uso comum**: pendrives, cartões de memória e dispositivos que precisam ser compatíveis com vários sistemas.  

---
