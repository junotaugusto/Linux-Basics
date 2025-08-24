# Userspace

- **Userspace é o ambiente onde as aplicações em nível de usuário são executadas.**  
  Ou seja, é onde rodam programas como navegadores, editores de texto, players de música, terminais e praticamente tudo o que o usuário interage no dia a dia. Esses programas não têm acesso direto ao hardware, mas sim usam chamadas ao sistema para pedir serviços ao kernel.  

- **É um espaço separado do kernel, fornecendo um ambiente isolado para que as aplicações rodem sem interagir diretamente com o hardware.**  
  Isso significa que, em vez de um programa mexer diretamente na memória, no disco rígido ou na placa de vídeo, ele pede ao kernel para realizar essas operações. Essa camada de separação evita que erros ou falhas em um programa comprometam todo o sistema.  

- **Essa separação é crucial para a estabilidade e segurança do sistema.**  
  Graças a essa divisão, mesmo que um aplicativo trave ou tenha comportamento malicioso, o kernel continua funcionando e protege os outros processos. Assim, o sistema não desmorona por causa de um único erro, e ainda garante que usuários comuns não possam acessar recursos críticos sem permissão.  

## Características Principais

- **Isolation (Isolamento):**  
  Os processos em *userspace* são isolados uns dos outros e também do kernel.  
  ➝ Isso significa que se um processo falhar, ele não compromete os demais nem o funcionamento do sistema inteiro.

- **User-Level Programs (Programas de Nível de Usuário):**  
  O *userspace* contém uma grande variedade de aplicações, como editores de texto, navegadores, jogos e utilitários de sistema.  
  ➝ Em outras palavras, tudo que o usuário executa diretamente (sem ser parte interna do kernel) roda no *userspace*.

- **Limited Privileges (Privilégios Limitados):**  
  Os processos do *userspace* possuem permissões limitadas.  
  ➝ Eles não podem acessar diretamente o hardware nem modificar configurações críticas do sistema. Isso protege o sistema de falhas e de usos maliciosos.

  ## Mecanismos de Comunicação

### 1. **System Calls (Chamadas de Sistema)**
- São a principal forma de comunicação entre o *userspace* e o kernel.
- Uma *system call* é uma função especial que permite que um programa no *userspace* solicite ao kernel que realize uma tarefa (ex.: abrir um arquivo, alocar memória, enviar dados pela rede).
- Exemplo:  
  - `open()` → abre um arquivo.  
  - `read()` → lê dados do arquivo.  
  - `write()` → escreve dados em um arquivo.  
  - `fork()` → cria um novo processo.  

➡️ O programa não acessa o hardware diretamente. Ele pede ao kernel, que faz o trabalho de forma segura.

---

### 2. **Bibliotecas de Sistema**
- Normalmente, o programador não chama as *system calls* diretamente.
- As linguagens utilizam bibliotecas que funcionam como uma **camada intermediária** entre o programa e o kernel.
- Exemplo:  
  - A biblioteca **glibc** no Linux fornece funções como `printf()` ou `fopen()`, que internamente usam *system calls*.

---

### 3. **Drivers e Módulos**
- O kernel possui **drivers** que traduzem as solicitações vindas do *userspace* em comandos específicos para o hardware.
- O *userspace* não fala diretamente com a placa de vídeo, disco ou rede — ele pede ao kernel (através de drivers) que faça isso.

---

### 4. **Interprocess Communication (IPC)**
- Além de pedir serviços ao kernel, os processos em *userspace* também precisam se comunicar entre si.
- O kernel oferece mecanismos de IPC para isso:
  - **Pipes** → canal de comunicação entre processos.  
  - **Sockets** → comunicação em rede ou local.  
  - **Shared Memory (Memória Compartilhada)** → vários processos acessam a mesma área de memória.  
  - **Signals** → mensagens simples enviadas a processos (ex.: `kill -9` envia um sinal para encerrar um processo).

---

## Resumo

- **Userspace → Kernel:** Programas pedem serviços via *system calls*.  
- **Kernel → Hardware:** O kernel traduz essas solicitações em operações reais no hardware.  
- **Segurança:** O userspace não acessa o hardware diretamente, evitando falhas catastróficas.  
- **Bibliotecas:** Simplificam o uso de chamadas de sistema.  
- **IPC:** Permite a comunicação entre processos em *userspace*, mediada pelo kernel.  

➡️ Em resumo: o *userspace* pede, o **kernel decide** e o **hardware executa**.