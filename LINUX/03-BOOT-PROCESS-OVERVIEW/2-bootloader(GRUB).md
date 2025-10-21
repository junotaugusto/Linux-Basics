# GRUB (Grand Unified Bootloader)

O **GRUB** é um dos *bootloaders* mais utilizados em distribuições Linux. Ele atua como intermediário entre o firmware da máquina (BIOS ou UEFI) e o sistema operacional, sendo responsável por carregar corretamente o kernel escolhido durante o processo de inicialização.

## O que é o GRUB?

- **GRUB (Grand Unified Bootloader)**  
    - Um *bootloader* popular usado em muitas distribuições Linux.  
    - É o software que assume o controle do sistema depois que o **BIOS ou UEFI** conclui seu processo inicial de boot.  
    - Em essência, o GRUB é o intermediário entre o hardware e o sistema operacional.  
    - Ele garante que o sistema operacional correto seja carregado e oferece uma forma amigável para o usuário escolher entre diferentes opções de boot.  

O GRUB funciona justamente como um **"menu de seleção de sistemas operacionais"**.

Se você tem mais de um sistema instalado (exemplo: macOS + Kali Linux no seu caso, ou Windows + Linux em outros cenários), o GRUB aparece na tela e **permite que você escolha qual sistema quer carregar**.

👉 Além disso, ele também pode:

- Oferecer opções avançadas de inicialização (como iniciar com outro kernel ou em modo de recuperação).

- É **flexível** aceitando diferentes sistemas operacionais, tornando-se versátil para configurações de dual-boot ou multi-boot.

- Permite customização do menu, mudanças no cronômetro ou opções de boot padrão por meio de arquivos de configuração. 

- Pode ser configurado com opções de boot seguro, se prevenindo de ataques maliciosos.

- Permitir que você passe parâmetros extras para o kernel (útil em testes, troubleshooting ou para configurações específicas).

- Até mesmo carregar sistemas que não sejam Linux, como o Windows, desde que esteja configurado.

## Em resumo

O GRUB é uma peça essencial no processo de inicialização, permitindo que o usuário tenha controle sobre qual sistema iniciar (no caso de *dual boot*), além de fornecer opções adicionais de depuração e configuração para o kernel.

### Dual-Boot

- **Detecção de Sistemas Operacionais:**  
  Quando você instala um novo sistema operacional ao lado de um já existente, o instalador geralmente modifica a configuração do GRUB para incluir o novo SO como uma opção de boot.

- **Criação do Menu de Boot:**  
  O GRUB gera um menu de inicialização, exibindo uma lista dos sistemas operacionais disponíveis.

- **Seleção pelo Usuário:**  
  Ao iniciar o computador, você pode escolher o sistema operacional desejado a partir do menu.

- **Carregamento do Sistema Operacional Selecionado:**  
  O GRUB carrega o kernel do sistema operacional selecionado e o disco RAM inicial (*initramfs*) para a memória.

- **Transferência de Controle:**  
  Uma vez que o kernel e o *initramfs* são carregados, o GRUB transfere o controle para o kernel, que então inicializa o restante do sistema operacional.

