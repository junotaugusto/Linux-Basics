# Kernel

O **kernel** é o núcleo de um sistema Linux.  
Ele atua como uma ponte entre o **hardware** (CPU, GPU, placa-mãe etc.) e as camadas de **software**, gerenciando recursos do sistema e facilitando a comunicação entre ambos.  

**Exemplo:**  
Quando você abre um arquivo no editor de texto, o software não fala diretamente com o disco rígido. Ele pede ao kernel para buscar os dados do disco. O kernel conversa com o hardware do disco, recupera os dados e os entrega ao software.

---

## Principais objetivos

### Gerenciamento de memória
- **Aloca e desaloca memória** para processos conforme necessário.
- **Page Fault Handling**: quando um processo tenta acessar uma parte da memória que não está na RAM, o kernel identifica a falha e busca os dados no disco (memória virtual ou swap).
- **Swapping**: o kernel move dados inativos da memória RAM para a área de swap no disco, liberando espaço na RAM para processos ativos.

### Gerenciamento de processos
- **Criação de processo e encerramento**: o kernel cria novos processos, atribui identificadores únicos (PIDs) e encerra quando não são mais necessários.
- **Agendamento de processos**: determina quais processos devem rodar e por quanto tempo, distribuindo o tempo de CPU de forma eficiente.
- **Troca de contexto**: alterna entre diferentes processos, mantendo seu estado e restaurando-o quando retornam à execução.  
  **Exemplo:** trocar do Google Chrome para o editor de texto e depois voltar para o Chrome, continuando de onde parou.
- **Comunicação interprocessual (IPC)**: permite que processos troquem informações e se sincronizem.  
  **Exemplo:** copiar texto de um programa e colar em outro.
- **Gerenciamento de drivers de dispositivos**: o kernel carrega e descarrega drivers, que são softwares que fazem a ponte entre o sistema e dispositivos específicos.  
  **Exemplo:** driver de uma placa de vídeo.
- **Operações de entrada/saída (I/O)**: controla o fluxo de dados entre dispositivos e memória.  
  **Exemplo:** pressionar uma tecla (entrada) e ver a letra aparecer na tela (saída).
- **Cuidados com interrupções**: responde a sinais de hardware (como disco rígido, rede ou teclado) que pedem atenção imediata.

---

## Hardware Abstraction Layer (HAL)

- O kernel fornece uma interface consistente para que softwares interajam com o hardware.
- Essa **abstração** esconde a complexidade de arquiteturas diferentes, permitindo que o mesmo software rode em várias plataformas sem grandes alterações.

---

## System Calls

As **System Calls** são os pontos de entrada que os programas usam para pedir serviços ao kernel.  
Elas funcionam como "portas oficiais" pelas quais o software pode acessar os recursos do sistema.  

**Exemplo:**  
- `read()` → um programa pede ao kernel para ler dados de um arquivo.  
- `write()` → um programa pede ao kernel para escrever dados em um arquivo.  
- `fork()` → cria um novo processo.  

Sem system calls, os programas não conseguiriam interagir com o hardware de forma segura e controlada.

---

## Segurança

O kernel implementa mecanismos de proteção contra acessos não autorizados e ataques.

- **Autenticação de usuário**: verifica identidade e permite acesso conforme privilégios.
- **Controle de acesso**: define permissões sobre arquivos e diretórios.
- **Segurança de rede**: implementa recursos como firewall e filtragem de pacotes.

Esses mecanismos garantem que apenas usuários ou processos autorizados possam acessar determinados recursos do sistema.
