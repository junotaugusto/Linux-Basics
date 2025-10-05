# Guia de Referência: Permissões (Permissions) e Propriedade (Ownership)

## 1. A Filosofia: Quem pode fazer O Quê e Onde

Como você bem observou, a segurança no Linux se resume a um sistema de regras que controla o acesso. Cada arquivo e diretório no sistema tem um "dono" e pertence a um "grupo", e para cada um desses níveis, há um conjunto de permissões.

Isso é governado por três categorias principais que definem a relação de um usuário com um arquivo:

1.  **Dono (User/Owner):** É o proprietário do arquivo. Por padrão, o usuário que cria um arquivo se torna seu dono. O dono geralmente tem o maior nível de controle sobre ele.

2.  **Grupo (Group):** Todo arquivo pertence a um grupo. Grupos são conjuntos de usuários. Isso permite que você dê permissões a um "time" inteiro de uma só vez, em vez de dar permissão para cada usuário individualmente.

3.  **Outros (Others):** Representa todo o resto do mundo. Qualquer usuário que não seja o Dono e não pertença ao Grupo do arquivo se encaixa nesta categoria. É o nível de permissão mais "público".

É importante entender que um mesmo usuário pode ser **Dono** de um arquivo, membro do **Grupo** de outro, e um **"Outro"** para um terceiro arquivo. A categoria em que você se encaixa depende do arquivo específico que você está tentando acessar.

## 2. Os Três Níveis de Permissão

Para cada uma das três categorias (Dono, Grupo, Outros), existem três tipos de permissão que podem ser concedidas ou negadas.

| Permissão | Símbolo | Valor Numérico | Significado para **ARQUIVOS** | Significado para **DIRETÓRIOS** |
| :--- | :--- | :--- | :--- | :--- |
| **Leitura** | `r` | **4** | Permite ler o conteúdo do arquivo. | Permite **listar** o conteúdo do diretório (ver os nomes dos arquivos). |
| **Escrita** | `w` | **2** | Permite alterar ou apagar o conteúdo do arquivo. | Permite **criar, apagar e renomear** arquivos dentro do diretório. |
| **Execução**| `x` | **1** | Permite executar o arquivo (se for um programa ou script). | Permite **entrar** no diretório (usar `cd` para acessá-lo). |

## 3. Lendo a Linha de Permissões (`-rwxr-xr-x`)

O comando `ls -l` exibe as permissões como uma sequência de 10 caracteres. Vamos decifrar o exemplo `-rwxr-xr-x`:

`[ - ] [ rwx ] [ r-x ] [ r-x ]`

1.  **Primeiro Caractere (Tipo):**
    * `-`: Arquivo comum.
    * `d`: Diretório.
    * `l`: Link simbólico.

2.  **Primeiro Trio (Permissões do DONO):**
    * `rwx`: O dono pode ler, escrever e executar.

3.  **Segundo Trio (Permissões do GRUPO):**
    * `r-x`: Membros do grupo podem ler e executar, mas **não** podem escrever.

4.  **Terceiro Trio (Permissões de OUTROS):**
    * `r-x`: Outros usuários também podem ler e executar, mas **não** podem escrever.

## 4. Modificando Permissões com `chmod`

O comando `chmod` (change mode) é a ferramenta para alterar essas permissões. Normalmente, requer `sudo` se você não for o dono do arquivo.

### a) Modo Simbólico (com letras)

Este modo é mais intuitivo e usa letras para representar as mudanças.

**Sintaxe:** `chmod [quem] [ação] [permissão] nome_do_arquivo`

* **Quem:**
    * `u` (user, o dono)
    * `g` (group, o grupo)
    * `o` (others, outros)
    * `a` (all, todos os três)
* **Ação:**
    * `+` (adiciona uma permissão)
    * `-` (remove uma permissão)
    * `=` (define a permissão exatamente como especificado)
* **Permissão:**
    * `r`, `w`, `x`

**Exemplo:** `chmod u+rwx,g+rx,o+rx script.sh`
* Para o **Dono (`u`)**, adiciona (`+`) as permissões `rwx`.
* Para o **Grupo (`g`)**, adiciona (`+`) as permissões `rx`.
* Para **Outros (`o`)**, adiciona (`+`) as permissões `rx`.

> **Pergunta:** Isso funciona para diretórios ou links?
> **Resposta:**
> * **Diretórios:** Sim, funciona exatamente da mesma forma. O que muda é o significado das permissões `rwx`, conforme a tabela acima.
> * **Links Simbólicos:** Por padrão, usar `chmod` em um link simbólico **altera as permissões do arquivo ou diretório para o qual o link aponta**, não as permissões do link em si.

### b) Modo Numérico (Octal)

Este modo usa a soma dos valores numéricos (`r=4`, `w=2`, `x=1`) para definir as permissões de forma rápida.

**Exemplo:** `sudo chmod 755 /home/Usuario`
* **Primeiro número (`7` para o Dono):** `4 + 2 + 1` = `rwx` (controle total).
* **Segundo número (`5` para o Grupo):** `4 + 1` = `r-x` (leitura e execução).
* **Terceiro número (`5` para Outros):** `4 + 1` = `r-x` (leitura e execução).

## 5. Modificando a Propriedade com `chown`

O comando `chown` (change owner) é usado para mudar o dono e/ou o grupo de um arquivo ou diretório.

### Sintaxe e Exemplos:

* **Mudar apenas o dono:**
```bash
    sudo chown novodono nome_do_arquivo
```

* **Mudar o dono e o grupo de uma só vez:**
```bash
    sudo chown novodono:novogrupo nome_do_arquivo
```

* **Mudar apenas o grupo:**
(O comando `chgrp` também existe para isso)
```bash
    sudo chown :novogrupo nome_do_arquivo
```

* **Mudar recursivamente para um diretório inteiro:**
A opção `-R` (recursiva) aplica a mudança ao diretório e a **tudo** que estiver dentro dele.
```bash
    sudo chown -R usuario:grupo /caminho/para/o/diretorio
```