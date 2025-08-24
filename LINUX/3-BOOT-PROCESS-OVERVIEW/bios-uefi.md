# Processo de Boot

O **processo de boot** é a sequência de etapas que ocorre desde o momento em que o computador é ligado até o carregamento completo do sistema operacional. Ele envolve a inicialização do hardware e a preparação do ambiente para que o sistema possa funcionar.

---

## BIOS vs UEFI

- **BIOS (Basic Input/Output System)**
  - Criado nos anos 80, é o firmware tradicional usado em computadores mais antigos.
  - Suporta discos até **2 TB** e tabela de partição **MBR (Master Boot Record)**.
  - Interface simples, geralmente em modo texto.
  - Funciona em modo de **16 bits**, o que limita a velocidade de inicialização e recursos.
  - Executa o **POST (Power-On Self Test)** para checar o hardware.

- **UEFI (Unified Extensible Firmware Interface)**
  - Substitui o BIOS em computadores modernos.
  - Suporta discos maiores que **2 TB** e usa a tabela de partição **GPT (GUID Partition Table)**.
  - Interface mais amigável, muitas vezes com suporte a mouse e modo gráfico.
  - Funciona em **32 ou 64 bits**, garantindo inicialização mais rápida e com mais funcionalidades.
  - Possui recursos avançados, como **Secure Boot**, que evita a execução de softwares maliciosos no processo de inicialização.

---

## Funções Principais do BIOS (aplicáveis também no UEFI)

- **Power-On Self-Test (POST):**
  - Realiza testes para verificar se os componentes de hardware estão funcionando corretamente.
  - Emite sinais sonoros (beeps) que indicam erros detectados.

- **Hardware Initialization:**
  - Inicializa componentes essenciais como teclado, mouse, memória e discos.

- **Boot Loader:**
  - Localiza e carrega o **boot loader** do sistema operacional (ex: GRUB, Windows Boot Manager), que por sua vez carrega o sistema.

- **Basic Input/Output Services:**
  - Fornece serviços básicos de entrada e saída para o sistema operacional, como leitura do teclado, uso do mouse e exibição de informações na tela.

- **UEFI:**
  - Unified Extensible Firmware Interface.  
  - É uma interface de firmware moderna projetada para substituir o BIOS tradicional.  
  - O UEFI oferece um processo de inicialização mais flexível, rápido e seguro em comparação com seu antecessor.  
