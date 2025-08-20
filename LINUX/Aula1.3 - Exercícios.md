1. Qual é a função do diretório `/` no Linux? 

*R: O diretório / é a raiz do sistema Linux. Ele é o ponto de partida da hierarquia de diretórios e contém todos os outros diretórios e arquivos do sistema.*

2. Onde ficam armazenados os arquivos de configuração do sistema?
*R: Os arquivos de configuração do sistemas ficam no diretório **/etc**.*

3. Qual a diferença entre `/bin` e `/sbin`?
*R: Ambos abrigam arquivos binários. O diretório /bin guarda programas essenciais que qualquer usuário pode usar. Já /sbin contém programas voltados para administração do sistema, normalmente usados pelo root.*

4. Para que serve o diretório `/usr`?
*R: O diretório /usr guarda a maioria dos programas e bibliotecas do sistema, além de documentação. É como um “pacote” de recursos adicionais ao núcleo do Linux.*

5. Qual é a função de `/usr/local` em comparação a `/usr/bin`?
*R: /usr/bin contém programas instalados pela distribuição e disponíveis para todos. Já /usr/local é usado para programas instalados manualmente, fora do gerenciador de pacotes.*

6. Onde são armazenados os arquivos de log do sistema?
*R: /var/log*  

7. Qual é a diferença entre `/tmp` e `/var/tmp`?
*R: O diretório /tmp contém arquivos de curta duração, que são "apagados" em um reboot, por exemplo. Já os arquivos em /var/tmp também são temporários, mas persistem entre reinicializações do sistema, como logs temporários de uma instalação que pode demorar dias ou caches de compilação (como quando você compila um software grande e o processo pode continuar depois de reiniciar).*

8. Qual diretório contém os diretórios pessoais dos usuários?
*R: /home* 

9. Qual é a função do diretório `/root`?
*R: É o diretório pessoal do usuário root*

10. Onde ficam os arquivos necessários para a inicialização do sistema?
*R: Os arquivos necessários para iniciar o sistema ficam em /boot, como o kernel e o carregador de inicialização (bootloader).*

11. Para que serve o diretório `/mnt`?
*R: É usado como ponto de montagem temporário para sistemas de arquivos, por exemplo, montar manualmente uma outra partição ou um ISO.*  

12. Onde geralmente são montados dispositivos removíveis como pen drives?
*R: Os dispositivos de hardware aparecem em /dev, mas quando montados, geralmente vão para /media (montagem automática) ou /mnt (se feito manualmente).*

13. Qual a função do diretório `/proc`?
*R: É um sistema de arquivos virtual que mostra informações em tempo real sobre processos e também sobre o kernel (ex.: memória, CPU, parâmetros do sistema).*

14. Qual é a diferença entre `/proc` e `/sys`?
*R: Enquanto o /proc exibe processos do sistema, o /sys, além de exibir dispositivos e kernel modules. Assim, o /proc fornece informações sobre processos e parâmetros do kernel em execução e o /sys fornece uma visão mais estruturada dos dispositivos de hardware e do kernel, permitindo até configuração dinâmica de alguns deles.*

15. Para que serve o diretório `/srv`?
*R: É usado para armazenar dados servidos por serviços de rede, como arquivos de um servidor web (/srv/www) ou servidor FTP.*

16. Onde estão localizadas as bibliotecas essenciais do sistema?
*R: Ficam em /lib, /lib32, /lib64 (dependendo da arquitetura).*  

17. Qual a função do diretório `/dev`?
*R: Ele representa dispositivos de hardware em forma de arquivos, permitindo que o kernel e programas interajam com o hardware.*

18. O que pode ser encontrado dentro de `/run`?
*R: Contém arquivos de runtime do sistema desde o boot. Exemplos: PID de processos em execução, sockets, informações temporárias de serviços e usuários logados. Diferente de /tmp, é sempre limpo a cada reinicialização.*

19. Em qual diretório ficaria a configuração do servidor SSH?
*R: /etc/ssh.*

20. Por que `/boot` pode estar em uma partição separada?
*R: Para facilitar a recuperação do sistema, ou seja, para garantir que os arquivos essenciais de inicialização (kernel, initramfs, carregador de boot) fiquem acessíveis mesmo que o restante do sistema esteja corrompido ou em outro formato de partição não reconhecido pelo bootloader. Isso facilita recuperação e aumenta a confiabilidade do boot.*