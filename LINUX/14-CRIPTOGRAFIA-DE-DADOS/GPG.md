# Criptografia de Dados com GPG

## 1. O que é o GPG (GNU Privacy Guard)?

**GPG (GNU Privacy Guard)** é uma implementação de software livre do padrão **OpenPGP**, uma ferramenta que garante a segurança de comunicações e dados. Seu principal objetivo é fornecer privacidade e autenticidade usando criptografia.

Você pode usar o GPG para:
* **Criptografar arquivos:** Tornar o conteúdo de um arquivo ilegível para qualquer pessoa que não seja o destinatário pretendido.
* **Assinar digitalmente arquivos:** Provar que um arquivo veio de você e que não foi modificado no caminho.

O GPG é a ferramenta que coloca em prática os conceitos de criptografia assimétrica no seu terminal.

## 2. O Conceito: Criptografia Assimétrica

Para entender o GPG, é crucial entender a **criptografia assimétrica**, também conhecida como criptografia de chave pública/privada.

Este método utiliza um par de chaves matematicamente ligadas para cada usuário:

* **Chave Privada:** Este é o seu segredo mais bem guardado. Ela fica armazenada de forma segura no seu computador (protegida por uma senha forte) e **nunca** deve ser compartilhada. 

A chave privada é a única capaz de **descriptografar** mensagens e **assinar digitalmente** (provar que você é você).

* **Chave Pública:** Este é o seu "cadeado" digital. Você pode (e deve) compartilhá-la livremente com qualquer pessoa. Outras pessoas usarão sua chave pública para **criptografar** mensagens que só você poderá ler.

## 3. Como o GPG Funciona na Prática

Vamos focar no caso de uso da criptografia de dados:

**Cenário:** Alice quer enviar um arquivo secreto (`relatorio.txt`) para Bruno.

1.  **Troca de Chaves:** Primeiro, Bruno envia sua **chave pública** para Alice. Alice a importa para seu "chaveiro" GPG.

2.  **Alice Criptografa (Encrypt):** Alice usa o GPG e a **chave pública de Bruno** para criptografar o arquivo.
    * `gpg --encrypt --recipient "Bruno" relatorio.txt`

3.  O GPG gera um novo arquivo, `relatorio.txt.gpg`, que está completamente ilegível.

4.  **Transferência:** Alice envia o arquivo `relatorio.txt.gpg` para Bruno. Isso pode ser feito por e-mail, pendrive, ou qualquer outro meio, pois o arquivo está seguro. Se um hacker interceptar o arquivo, ele verá apenas dados embaralhados.

5.  **Bruno Descriptografa (Decrypt):** Bruno recebe o arquivo e usa o GPG com sua **chave privada** (que só ele possui) para descriptografá-lo.
    * `gpg --decrypt relatorio.txt.gpg > relatorio_decifrado.txt`

6.  O GPG pede a senha da chave privada de Bruno. Ele a digita e o GPG gera o arquivo original `relatorio_decifrado.txt`.

Isso garante que **apenas o destinatário correto (Bruno)**, o único que possui a chave privada correspondente, pode ler a mensagem criptografada.

## 4. Comandos Essenciais do GPG

Aqui estão os comandos básicos para começar a usar o GPG:

* **Gerar seu próprio par de chaves:**
    Este é o primeiro passo. O GPG fará uma série de perguntas (tipo de chave, tamanho, data de validade, seu nome, e-mail e uma senha forte para proteger sua chave privada).
```bash
    gpg --full-gen-key
```

* **Listar as chaves públicas no seu chaveiro:**
    Mostra as chaves que você possui e as chaves públicas de outras pessoas que você importou.
```bash
    gpg --list-keys
```

* **Listar suas chaves privadas:**
```bash
    gpg --list-secret-keys
```

* **Exportar sua chave pública para compartilhar:**
    Isso cria um arquivo de texto (`.asc`) com sua chave pública, que você pode enviar para seus contatos.
```bash
    # Substitua "Seu Nome" pelo nome ou e-mail da sua chave
    gpg --export -a "Seu Nome" > minha_chave_publica.asc
```

* **Importar a chave pública de alguém:**
```bash
    gpg --import chave_do_bruno.asc
```

* **Criptografar um arquivo (para um destinatário):**
```bash
    # Você deve ter a chave pública do destinatário importada
    gpg --encrypt --recipient "email@destinatario.com" arquivo_secreto.txt
```

* **Descriptografar um arquivo:**
    O GPG automaticamente usará a chave privada correta do seu chaveiro.
```bash
    # O GPG pedirá a senha da sua chave privada
    gpg --decrypt arquivo_secreto.txt.gpg
    
    # Para salvar a saída em um novo arquivo:
    gpg --output arquivo_decifrado.txt --decrypt arquivo_secreto.txt.gpg
```