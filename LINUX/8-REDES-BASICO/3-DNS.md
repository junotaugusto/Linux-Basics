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
