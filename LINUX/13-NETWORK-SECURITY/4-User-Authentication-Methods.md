# User Authentication Methods

A autenticação é o processo de verificar a identidade de um usuário antes de conceder-lhe acesso a um sistema. No Linux, existem vários métodos para isso, sendo os mais comuns a autenticação por senha e por chave pública.

## 1. Autenticação Baseada em Senha (Password-Based Authentication)

Este é o método padrão e mais familiar. O usuário possui um nome de usuário e uma senha secreta. Para acessar, ele fornece ambos, e o sistema verifica se a senha corresponde à que está armazenada (de forma criptografada) para aquele usuário.

### Melhorando a Segurança: Autenticação Multi-Fator (MFA)

Embora seja o padrão, a autenticação por senha sozinha é vulnerável a ataques de adivinhação, força bruta e phishing. Para mitigar isso, a prática de segurança moderna é adicionar a **Autenticação Multi-Fator (MFA)**, também conhecida como Autenticação de Dois Fatores (2FA).

MFA reduz significativamente o acesso não autorizado ao exigir que o usuário prove sua identidade com **pelo menos dois** dos três tipos de fatores:

1.  **Algo que você sabe:** A senha ou um PIN.
2.  **Algo que você tem:** Um token físico, um celular (recebendo um código SMS ou usando um app como Google Authenticator).
3.  **Algo que você é:** Biometria (impressão digital, reconhecimento facial).

**Como funciona na prática:** Mesmo que um atacante roube sua senha (fator 1), ele não conseguirá fazer login sem ter acesso físico ao seu celular (fator 2). O sistema geralmente requisita o segundo fator em situações de maior risco, como ao detectar um login de um novo dispositivo, uma nova localização geográfica, ou após o cache e os cookies do navegador serem limpos.

## 2. Autenticação por Chave Pública (Public Key Authentication)

A autenticação por chave pública é um método drasticamente **mais seguro** e conveniente do que o uso de senhas para conexões remotas, como o SSH.

Este método envolve o uso de um par de chaves criptográficas:

* **Chave Privada (`id_rsa`):** É o seu segredo. Ela fica armazenada de forma segura na sua máquina local (seu computador) e **nunca, jamais, deve ser compartilhada**. Pense nela como a chave física da sua casa.
* **Chave Pública (`id_rsa.pub`):** É o seu cadeado. Ela pode ser compartilhada livremente e é instalada nos servidores aos quais você deseja acessar. Pense nela como um cadeado que você instala na porta da sua casa na praia.

**Como funciona a "mágica"?**
Quando você tenta se conectar a um servidor, ele vê sua chave pública (o cadeado) e envia um desafio aleatório para você. Apenas a sua chave privada correspondente (a única chave que abre aquele cadeado) consegue resolver esse desafio corretamente. 

Ao resolver, você prova ao servidor que é realmente você, e o acesso é concedido, tudo sem que a senha ou qualquer segredo precise viajar pela rede.

### Vantagens Principais:

* **Resistência a Ataques de Força Bruta:** Atacantes podem tentar adivinhar senhas, mas é computacionalmente impossível adivinhar uma chave privada, que é extremamente longa e complexa. Desativar a autenticação por senha e usar apenas chaves torna ataques de força bruta inúteis.
* **Logins Automatizados (sem senha):** É ideal para scripts e automação. Você não precisa armazenar senhas em texto plano em seus scripts.
* **Segurança Aumentada:** Sua chave privada (o segredo) nunca sai da sua máquina.

> **Login com senha apenas uma vez?** A sua chave privada pode ser protegida por uma "passphrase" (uma senha longa). Ao iniciar sua sessão de trabalho, você digita essa passphrase uma vez para "destrancar" a chave privada, que fica disponível para uso (geralmente gerenciada por um programa chamado `ssh-agent`). Enquanto sua sessão estiver ativa, você pode se conectar a quantos servidores quiser sem digitar a passphrase novamente.

## 3. Guia Prático: Configurando a Autenticação por Chave Pública

### Passo 1: Gerar o Par de Chaves com `ssh-keygen`

Este comando cria o par de chaves na sua máquina local.

```bash
# Execute este comando no terminal da sua máquina local (ex: seu Mac ou notebook com Linux)
ssh-keygen
```
O programa fará algumas perguntas:
* `Enter file in which to save the key...`: Pressione Enter para aceitar o local padrão (`~/.ssh/id_rsa`).
* `Enter passphrase...`: **Recomendado!** Digite uma senha forte. Isso protege sua chave privada caso seu computador seja roubado. Você pode deixar em branco, mas é menos seguro.

Ao final, dois arquivos serão criados no seu diretório `~/.ssh/`: `id_rsa` (sua chave privada) e `id_rsa.pub` (sua chave pública).

### Passo 2: Copiar a Chave Pública para o Servidor com `ssh-copy-id`

Este é o método mais fácil e seguro para instalar sua chave pública no servidor.

```bash
# Sintaxe: ssh-copy-id usuario@servidor
ssh-copy-id joao@192.168.1.10
```
**O que este comando faz automaticamente:**
1.  Ele se conecta ao servidor usando sua senha (esta é a última vez que você a usará).
2.  Copia o conteúdo da sua chave pública (`~/.ssh/id_rsa.pub`).
3.  Adiciona a chave ao final do arquivo `~/.ssh/authorized_keys` no servidor.
4.  Define as permissões corretas para o diretório `~/.ssh` (700) e o arquivo `authorized_keys` (600), o que é crucial para a segurança.

### Passo 3: Conectar-se ao Servidor com `ssh user@server`

Agora vem o teste final. Tente se conectar ao servidor novamente.

```bash
ssh joao@192.168.1.10
```
Se tudo deu certo, você será conectado **instantaneamente**, sem que o servidor peça sua senha. Se você definiu uma passphrase para sua chave, seu computador local pode pedi-la para "destrancar" a chave privada antes de usá-la.