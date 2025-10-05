# Listas de Controle de Acesso (Access Control Lists - ACL)

## 1. O que são ACLs e por que usá-las?

No modelo padrão de permissões do Linux, cada arquivo é governado por apenas três entidades: um **Dono**, um **Grupo** e os **Outros**. Isso é simples e eficaz para a maioria dos casos, mas pode ser muito rígido.

**Imagine o seguinte problema:**
Você tem um diretório `/srv/dados/relatorios` que pertence ao usuário `pedro` e ao grupo `financeiro`.
* O `pedro` (dono) precisa de acesso total.
* O time `financeiro` (grupo) precisa de acesso total.
* Ninguém mais (`outros`) pode ter acesso. A permissão é `770` (`rwxrwx---`).

Agora, seu chefe pede que o `joao`, do time de marketing, tenha acesso de **apenas leitura** a esse diretório para consultar um relatório específico. Como você faz isso?
* Você não pode mudar o dono.
* Você não quer adicionar o `joao` ao grupo `financeiro`, pois isso lhe daria acesso de escrita e acesso a outros arquivos do grupo.
* Você não pode dar permissão para "outros", pois isso liberaria o acesso para todo o sistema.

É para resolver exatamente este tipo de exceção que as **Access Control Lists (ACLs)** existem.

Pense no modelo padrão como tendo chaves para "Dono", "Família" e "Público". A ACL é como uma **lista de convidados VIP na porta**, permitindo que você adicione nomes específicos (`joao`) e lhes dê permissões personalizadas, sem mexer nas regras principais.

## 2. Verificando o Suporte a ACLs

Antes de usar, é preciso garantir que seu sistema está pronto.

1.  **Instalar as ferramentas:** O pacote `acl` contém os comandos `getfacl` e `setfacl`.
```bash
    sudo apt update
    sudo apt install acl
```

2.  **Verificar o sistema de arquivos:** Sistemas de arquivos modernos como `ext4` e `xfs` geralmente já vêm com o suporte a ACLs ativado por padrão na montagem.

## 3. Como as ACLs Funcionam

Quando um arquivo ou diretório possui uma ACL, você notará um sinal de `+` no final da string de permissões ao usar o comando `ls -l`.

`drwxrwx---+ 2 pedro financeiro 4096 out  4 22:10 relatorios`

Esse `+` é o seu indicador visual de que, além das permissões base, existem regras extras de ACL que você pode ver com o comando `getfacl`.

## 4. Entradas ACL (ACL Entries) e seus Tipos

O comando `getfacl` mostra todas as regras de permissão para um arquivo. A saída dele nos revela os diferentes tipos de entradas.

**Exemplo de saída de `getfacl relatorios/`:**
```
# file: relatorios/
# owner: pedro
# group: financeiro
user::rwx
user:joao:r-x
group::rwx
group:auditoria:r--
mask::rwx
other::---
```

Vamos decifrar cada tipo de entrada:

* **`user::rwx` (Dono):** Define as permissões do usuário dono (`pedro`). É o equivalente direto da porção "dono" do `chmod`.

* **`user:joao:r-x` (Usuário Nomeado):** **Esta é a essência da ACL.** É a nossa "entrada VIP". Aqui, estamos dando ao usuário específico `joao` as permissões de leitura (`r`) e execução (`x`), mesmo que ele não seja o dono nem pertença ao grupo `financeiro`.

* **`group::rwx` (Grupo Dono):** Define as permissões do grupo dono (`financeiro`). Equivalente à porção "grupo" do `chmod`.

* **`group:auditoria:r--` (Grupo Nomeado):** Semelhante ao usuário nomeado, permite conceder permissões a um grupo inteiro (`auditoria`) que não é o grupo principal do arquivo.

* **`mask::rwx` (Máscara):** A máscara é um filtro de segurança. Ela define as **permissões máximas** que qualquer entrada extra (usuários nomeados, grupos nomeados) pode ter. Por exemplo, se a `mask` fosse `r--`, mesmo que a entrada `user:joao:r-x` exista, a permissão efetiva do João seria apenas de leitura (`r--`), pois a máscara bloqueia a permissão de execução.

* **`other::---` (Outros):** As permissões para todos os outros. Equivalente à porção "outros" do `chmod`.

## 5. Comandos Essenciais: `getfacl` e `setfacl`

* **`getfacl` (Ver as ACLs):**
```bash
    # Ver as ACLs de um arquivo ou diretório
    getfacl nome_do_arquivo
```

* **`setfacl` (Definir as ACLs):**
    Este é o comando para modificar as permissões.

   * **Modificar/Adicionar (`-m`):**
```bash
        # Dar ao usuário 'joao' permissão de leitura e execução (r-x) no diretório 'relatorios'
        setfacl -m u:joao:rx relatorios/

        # Dar ao grupo 'auditoria' permissão de apenas leitura (r)
        setfacl -m g:auditoria:r relatorios/
```

   * **Remover uma entrada específica (`-x`):**
```bash
        # Remove a regra específica para o usuário 'joao'
        setfacl -x u:joao relatorios/
```

   * **Remover todas as ACLs (`-b`):**
        Remove todas as entradas extras, revertendo para o modelo de permissões padrão (Dono, Grupo, Outros).
```bash
        setfacl -b relatorios/
```

   * **ACLs Padrão (Default):**
        Uma funcionalidade extremamente útil para diretórios. Uma ACL padrão (`-d`) faz com que **qualquer novo arquivo ou pasta criado dentro do diretório herde automaticamente aquela ACL**.
```bash
        # Define que qualquer novo item criado em 'relatorios' dará automaticamente
        # permissão de leitura e escrita para o usuário 'joao'.
        setfacl -d -m u:joao:rw relatorios/
```