# Autenticação de Usuário e sudo

No Linux, a autenticação de usuários é um processo central para o controle de acesso ao sistema. Um dos arquivos mais importantes para isso é o **/etc/passwd**, que guarda informações essenciais sobre cada usuário.  

Cada linha do **/etc/passwd** corresponde a um usuário e contém vários campos separados por dois pontos `:`. Apesar do nome, **não há senhas neste arquivo**, apenas informações sobre contas de usuário. As senhas ou seus hashes ficam em outro arquivo, geralmente **/etc/shadow**.  

A estrutura de cada linha no `/etc/passwd` é a seguinte:
**usuario:senha:UID:GID:comentario:diretorio_home:shell**
- **usuario** → Nome do usuário que será usado para login no sistema.
- **senha** → Normalmente é um `x` ou `*`, indicando que a senha está armazenada no arquivo `/etc/shadow`.
- **UID (User ID)** → Número único que identifica o usuário no sistema. Usuário root geralmente tem UID 0.
- **GID (Group ID)** → Número do grupo principal ao qual o usuário pertence.
- **comentario** → Campo opcional usado para informações adicionais sobre o usuário, como nome completo.
- **diretorio_home** → Caminho para o diretório home do usuário.
- **shell** → Programa que será iniciado quando o usuário fizer login, geralmente uma shell como `/bin/bash`.

---

O **sudo** é um comando que permite que usuários comuns executem comandos com privilégios de **root** ou outro usuário. Para que um usuário utilize `sudo`, ele deve estar configurado no arquivo **/etc/sudoers** ou em arquivos incluídos dentro de **/etc/sudoers.d**.  

O uso do sudo garante que o sistema continue seguro, permitindo tarefas administrativas apenas para usuários autorizados, enquanto mantém a operação diária limitada a contas normais.
