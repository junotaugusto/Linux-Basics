# SysVinit

## O que é o SysVinit?
O **SysVinit** é um sistema de inicialização tradicional utilizado em distribuições Linux mais antigas, derivado do Unix System V.  
Ele é responsável por iniciar e parar os processos do sistema durante o boot e também quando o sistema muda de estado (runlevel).  

Apesar de ter sido substituído em muitas distribuições modernas pelo **systemd**, o SysVinit ainda é importante para entender como funcionava a inicialização clássica do Linux.

## Como o SysVinit funciona?

- **Initialization Scripts (Scripts de Inicialização):**  
  Esses scripts, localizados no diretório `/etc/init.d`, são responsáveis por iniciar e parar serviços do sistema.

- **Runlevels (Níveis de Execução):**  
  O SysVinit define diferentes runlevels, cada um representando um estado específico do sistema.  
  - Por exemplo:
    - **Runlevel 0:** estado de desligamento (halt).  
    - **Runlevel 1:** modo de usuário único (single-user mode).  
    - **Runlevel 5:** modo multiusuário com interface gráfica (default na maioria dos sistemas).  

- **Boot Process (Processo de Inicialização):**  
  Durante o boot, o SysVinit transita por diferentes runlevels, começando de um nível baixo e avançando até os mais altos.  
  - À medida que percorre cada runlevel, ele executa os scripts de inicialização correspondentes.

- **Algumas desvantagens**
    - Pode ser lento.
    - Complexidade para ser montado.
    - Paralelismo limitado, ou seja, apenas inicia dispositivos de forma sequenciada, o que pode ser ineficiente. 
