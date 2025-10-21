# Segurança em Atualizações

As atualizações de sistema não trazem apenas correções funcionais, mas também são essenciais para a segurança. Três pontos principais são:

**Vulnerability Patches (Correções de Vulnerabilidades):**  
Softwares frequentemente possuem falhas que podem ser exploradas por atacantes. As atualizações corrigem essas falhas rapidamente, reduzindo a chance de ataques.

**Improved Security Features (Recursos de Segurança Aprimorados):**  
Além de correções, as atualizações podem adicionar novas funcionalidades e mecanismos de proteção que reforçam a postura de segurança do sistema.

**Dependency Updates (Atualizações de Dependências):**  
Muitos programas dependem de bibliotecas externas. Atualizar essas dependências garante que todas estejam seguras, minimizando o risco de exploração.

---

## Comandos no Linux

### CentOS/RHEL (yum/dnf)

```bash
# Atualizar a lista de pacotes
sudo yum check-update

# Atualizar pacotes específicos
sudo yum update nome-do-pacote

# Atualizar todos os pacotes do sistema
sudo yum update -y

# Atualizar apenas patches de segurança (quando disponível)
sudo yum update --security -y
```
### Debian/Ubuntu

```bash
# Atualizar lista de pacotes
sudo apt update

# Atualizar todos os pacotes instalados
sudo apt upgrade -y

# Atualização completa, incluindo pacotes que mudam dependências
sudo apt full-upgrade -y

# Atualizar apenas pacotes de segurança
sudo apt install unattended-upgrades
sudo unattended-upgrades
```
## Stability

Manter o sistema estável é fundamental para garantir uma boa experiência de uso, evitando falhas e melhorando o desempenho. As atualizações de software desempenham um papel central nisso, trazendo correções, melhorias e garantindo compatibilidade contínua.

### 🔹 Bug Fixes
As atualizações frequentemente incluem correções para **erros e falhas** que podem fazer com que aplicativos travem ou se comportem de maneira inesperada.  
Manter os pacotes atualizados garante uma experiência mais fluida e confiável.

### 🔹 Performance Enhancements
Atualizações regulares podem **otimizar o desempenho** do sistema, fazendo com que ele rode de forma mais eficiente e responsiva.  
Isso garante melhor aproveitamento dos recursos de hardware e software.

### 🔹 Compatibility
Com o lançamento de novas versões de softwares, é importante que haja **compatibilidade** entre aplicações e componentes do sistema.  
As atualizações mantêm essa harmonia, evitando conflitos e assegurando um funcionamento contínuo e sem interrupções.



