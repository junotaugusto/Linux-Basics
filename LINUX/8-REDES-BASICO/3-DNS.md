# DNS (Domain Name System)

O **DNS (Domain Name System)** é um sistema hierárquico e distribuído que traduz **nomes de domínio legíveis por humanos** (como `www.google.com`) em **endereços IP** (como `142.250.190.132`), que são usados pelos computadores para se comunicar na rede.

---

## Por que o DNS é importante?

- Facilita a navegação na internet: é mais fácil lembrar `www.exemplo.com` do que `192.168.1.100`.  
- Centraliza e organiza os nomes de domínio de forma global e hierárquica.  
- Permite que um mesmo servidor tenha vários nomes associados (aliases).  
- Suporta balanceamento de carga e redundância através de múltiplos registros.

---

## Como funciona a resolução DNS?

1. O usuário digita `www.exemplo.com` no navegador.  
2. O sistema consulta o **resolver local** (geralmente configurado pelo provedor de internet ou roteador).  
3. Se não houver cache no seu navegador, o resolver envia uma consulta a servidores **DNS raiz**.  
4. A partir daí, a consulta percorre a hierarquia:
   - **Servidor raiz** → indica o servidor responsável pelo TLD (`.com`, `.org`, `.br`, etc.).  
   - **Servidor TLD** → indica o servidor autoritativo para `exemplo.com`.  
   - **Servidor autoritativo** → fornece o endereço IP do host solicitado (`www.exemplo.com`).  
5. O navegador então se conecta ao IP retornado.

---

## Estrutura hierárquica do DNS

- **Servidores raiz (Root Servers):** nível mais alto da hierarquia.  
- **TLD (Top Level Domain):** `.com`, `.org`, `.net`, `.br`, etc.  
- **Domínios de segundo nível:** `exemplo.com`, `openai.org`, etc.  
- **Subdomínios:** `www.exemplo.com`, `mail.exemplo.com`.

---

## Tipos de Registros DNS

- **A:** associa um domínio a um endereço IPv4.  
- **AAAA:** associa um domínio a um endereço IPv6.  
- **CNAME:** cria um alias, apontando um domínio para outro.  
- **MX:** define servidores de e-mail do domínio.  
- **NS:** indica os servidores autoritativos do domínio.  
- **PTR:** usado em consultas reversas (IP → nome de domínio).  
- **TXT:** permite armazenar informações arbitrárias, como SPF/DKIM.

---

## Exemplo prático

Para o domínio `www.exemplo.com`, os registros poderiam ser:

- A → `192.168.1.50`  
- CNAME → `site.exemplo.com`  
- MX → `mail.exemplo.com`  
- NS → `ns1.exemplo.com`, `ns2.exemplo.com`

---

## Cache DNS

O DNS utiliza cache para acelerar consultas. Isso acontece em:
- O próprio sistema operacional.  
- O navegador do usuário.  
- O resolver do provedor de internet.  

O tempo de permanência no cache é definido pelo **TTL (Time To Live)** do registro DNS.

---

## Resumindo

- O **DNS traduz nomes de domínio em endereços IP**.  
- Funciona de forma **hierárquica e distribuída**.  
- Utiliza **registros DNS** para indicar serviços, IPs, e-mails e aliases.  
- **Cache** melhora desempenho, mas pode causar problemas se registros forem alterados antes do TTL expirar.  

> Sem o DNS, a internet seria navegada apenas por endereços numéricos, tornando-a muito menos prática para os usuários.

---

## Exemplo de DNS Server

# Como funciona a resolução de nomes no DNS

![alt text](<Captura de Tela 2023-12-05 às 13.55.40.png>)

A imagem ilustra o processo que ocorre quando um usuário tenta acessar o endereço **self.repair.apple.com**. Esse processo é chamado de **resolução recursiva de nomes** e envolve diversos servidores DNS até que se chegue ao endereço IP correto (ou uma resposta negativa).

---

## Passo a passo da resolução

1. **Verificação local**
   - O computador do usuário (cliente) verifica primeiro no **cache DNS local** e no **arquivo hosts** se já possui o endereço de `self.repair.apple.com`.
   - Se não encontrar, a consulta é enviada ao **servidor DNS local** (geralmente fornecido pelo roteador ou provedor de internet).

2. **Servidor DNS local**
   - O servidor DNS local recebe a requisição e, se não tiver a resposta em cache, começa a buscar perguntando a outros servidores na internet.

3. **Consulta ao Root Server**
   - O DNS local pergunta a um **Root Server**: "Onde está `self.repair.apple.com`?"
   - O Root Server responde: "Não sei exatamente, mas sei quem cuida do `.com`. Pergunte a ele."

4. **Consulta ao servidor TLD (.com)**
   - O DNS local envia a pergunta ao servidor responsável pelos domínios `.com`.
   - Resposta: "Não sei o `self.repair.apple.com`, mas sei quem cuida de `apple.com`. Pergunte para ele."

5. **Consulta ao servidor autoritativo de apple.com**
   - O DNS local pergunta: "Onde está `self.repair.apple.com`?"
   - O servidor de `apple.com` responde: "Não tenho esse subdomínio, mas sei quem cuida de `repair.apple.com`."

6. **Consulta ao servidor autoritativo de repair.apple.com**
   - O DNS local pergunta: "Onde está `self.repair.apple.com`?"
   - Esse servidor é o responsável por esse nível do domínio. Ele responde:
     - Caso exista: fornece o **endereço IP** do servidor.
     - Caso não exista: responde **NXDOMAIN** ("Não existe esse domínio").

7. **Resposta ao cliente**
   - O DNS local recebe a resposta final e repassa ao computador do usuário.
   - O cliente agora pode se conectar diretamente ao endereço IP correspondente.

---

## Representação resumida do fluxo

1. Cliente → Cache/hosts  
2. Cliente → DNS Local  
3. DNS Local → Root Server (.com?)  
4. DNS Local → Servidor TLD `.com` (apple.com?)  
5. DNS Local → Servidor autoritativo `apple.com` (repair.apple.com?)  
6. DNS Local → Servidor autoritativo `repair.apple.com` (self.repair.apple.com?)  
7. Servidor autoritativo responde com IP ou erro  
8. DNS Local → Cliente (resposta final)  

---

## Pontos importantes

- O **Root Server** só sabe quem gerencia cada domínio de topo (.com, .org, .net, etc.).  
- O **TLD Server** sabe quem gerencia o domínio principal (apple.com).  
- O **Servidor autoritativo** tem a informação definitiva sobre os registros do domínio.  
- O **DNS local** armazena (cacheia) as respostas para acelerar futuras consultas.  
- Caso o domínio não exista, o servidor autoritativo retorna **NXDOMAIN**.  

---

📌 **Resumo:**  
O DNS funciona como uma cadeia hierárquica de servidores, indo do mais geral (Root) ao mais específico (autoritativo do subdomínio), até encontrar o endereço IP ou confirmar que ele não existe.
