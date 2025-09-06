# Autenticação de Usuário e sudo


No Linux, a autenticação de usuários é um processo central para o controle de acesso ao sistema. Um dos arquivos mais importantes para isso é o **/etc/passwd**, que guarda informações essenciais sobre cada usuário.  

Cada linha do **/etc/passwd** corresponde a um usuário e contém vários campos separados por dois pontos `:`. Apesar do nome, **não há senhas neste arquivo**, apenas informações sobre contas de usuário. As senhas ou seus hashes ficam em outro arquivo, geralmente **/etc/shadow**.  

---

## O Arquivo /etc/passwd

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

## O Arquivo /etc/shadow

O arquivo **/etc/shadow** é responsável por armazenar informações sensíveis de autenticação, incluindo **senhas criptografadas** e dados relacionados ao gerenciamento de senhas dos usuários.  

Ele é mais seguro que o **/etc/passwd**, pois **pode ser lido apenas pelo usuário root** ou por usuários que têm permissões administrativas configuradas, geralmente através do `sudo` (lista dos sudoers).  

Cada linha do arquivo corresponde a um usuário e contém campos separados por dois pontos `:`:
**usuario:senha:ultimo_alteracao:min:max:aviso:inativo:expiracao:reservado**

- **usuario** → Nome do usuário, igual ao que aparece no `/etc/passwd`.
- **senha** → Senha criptografada do usuário. Se for `*` ou `!`, significa que o login com senha está desabilitado.
- **ultimo_alteracao** → Data da última alteração de senha, contada em dias desde 1º de janeiro de 1970.
- **min** → Número mínimo de dias entre alterações de senha.
- **max** → Número máximo de dias que a senha pode ser usada antes de expirar.
- **aviso** → Número de dias antes da expiração que o usuário começará a receber avisos.
- **inativo** → Número de dias após a expiração da senha que a conta será desativada.
- **expiracao** → Data em que a conta expirará (contada em dias desde 1º de janeiro de 1970).
- **reservado** → Campo reservado para uso futuro.

---

### Lista de sudoers

A **lista de sudoers** é o conjunto de usuários e grupos que têm permissão para executar comandos como root usando o `sudo`. Ela é definida no arquivo **/etc/sudoers** ou em arquivos dentro de **/etc/sudoers.d/**.  

Usuários incluídos nessa lista podem realizar tarefas administrativas sem precisar fazer login diretamente como root, mantendo a segurança e o controle sobre ações privilegiadas.

O **sudo** é um comando que permite que usuários comuns executem comandos com privilégios de **root** ou outro usuário. Para que um usuário utilize `sudo`, ele deve estar configurado no arquivo **/etc/sudoers** ou em arquivos incluídos dentro de **/etc/sudoers.d**.  

O uso do sudo garante que o sistema continue seguro, permitindo tarefas administrativas apenas para usuários autorizados, enquanto mantém a operação diária limitada a contas normais.
