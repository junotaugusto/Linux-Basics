# Boot Targets no Systemd

No **systemd**, os **boot targets** são conjuntos de unidades que representam **estados do sistema**.  
Eles são usados para definir e gerenciar em que modo o sistema deve inicializar (ex.: modo gráfico, multiusuário, apenas recuperação, etc.).

Os targets substituem o conceito tradicional de **runlevels** no SysVinit, oferecendo maior flexibilidade e clareza.

---

## O que são Targets?

- Um **target** é uma unidade especial do systemd, com extensão `.target`.  
- Eles agrupam outros serviços e unidades, organizando o processo de inicialização.  
- O systemd utiliza targets para decidir **quais serviços carregar** durante o boot.  
- Exemplo: o target `graphical.target` inicia tudo que é necessário para ambiente gráfico, enquanto `multi-user.target` prepara apenas ambiente de linha de comando.

---

## Principais Boot Targets

1. **default.target**  
   - Target padrão utilizado durante a inicialização.  
   - Normalmente é um link simbólico para outro target (ex.: `graphical.target` ou `multi-user.target`).  

2. **graphical.target**  
   - Inicializa todos os serviços de rede, multiusuário e também a interface gráfica.  
   - Equivalente ao antigo **runlevel 5**.

3. **multi-user.target**  
   - Inicializa serviços de rede e permite múltiplos logins, mas sem interface gráfica.  
   - Equivalente ao **runlevel 3**.

4. **rescue.target**  
   - Fornece um shell root básico com serviços mínimos carregados.  
   - Equivalente ao **runlevel 1** (modo de manutenção).

5. **emergency.target**  
   - Inicializa apenas o sistema básico, sem montar todos os sistemas de arquivos.  
   - Útil para recuperação em situações críticas.  

6. **reboot.target**  
   - Reboot do sistema.  

7. **halt.target**  
   - Interrompe (halt) o sistema sem desligar energia.  

8. **poweroff.target**  
   - Desliga completamente o sistema.  

## Comandos úteis com Targets

- **Ver o target atual**:  
```bash
systemctl get-default
```
- **Definir um novo target padrão**:
```bash
sudo systemctl set-default multi-user.target
```
- **Mudar o target em tempo de execução**:
```bash
sudo systemctl isolate graphical.target
```
- **Listar todos os targets disponíveis**:
```bash
systemctl list-unit-files --type=target
``` 
## Benefícios dos Boot Targets

**Flexibilidade:** `fácil mudar o comportamento do boot entre linha de comando e interface gráfica.`

**Segurança:** `permite inicializar em modos de recuperação (rescue/emergency).`

**Controle:** `possibilita alternar dinamicamente entre estados do sistema sem reiniciar.`

**Clareza:** `substitui os antigos runlevels por nomes mais descritivos.`

## Gerenciamento de Serviços no Systemd

No systemd, o gerenciamento de serviços é feito principalmente com o comando systemctl. Existem duas ideias que costumam gerar confusão: o controle imediato de um serviço (start e stop) e o controle de como ele se comporta durante a inicialização do sistema (enable e disable).

Quando usamos start, estamos iniciando o serviço imediatamente. Isso faz com que o serviço fique ativo apenas até o próximo reboot, sem garantir que ele volte a rodar quando a máquina for reiniciada. O stop é o oposto: ele para o serviço que está em execução, mas também não altera o comportamento no boot.

Exemplo:
```bash
sudo systemctl start nginx
sudo systemctl stop nginx
```
Já os comandos enable e disable controlam se o serviço será ou não iniciado automaticamente quando o sistema inicializar. O enable cria links simbólicos que dizem ao systemd para subir o serviço sempre no boot. 

O disable remove esses links, fazendo com que o serviço não seja carregado automaticamente, mesmo que esteja ativo no momento.
```bash
sudo systemctl enable nginx
sudo systemctl disable nginx
```
É importante perceber que enable não inicia o serviço imediatamente, apenas garante que ele suba no próximo boot. Da mesma forma, start não habilita o serviço para reinícios futuros, apenas o inicia agora. 

Se quisermos garantir que um serviço comece agora e também sempre no boot, usamos o parâmetro --now junto com enable. Assim, em um único comando, habilitamos o serviço para o futuro e já o iniciamos no presente.
```bash
sudo systemctl enable --now nginx
sudo systemctl disable --now nginx
```
Um resumo prático: start e stop lidam com o estado atual do serviço, enquanto enable e disable lidam com o comportamento do serviço no boot. 

Por exemplo, ao configurar um servidor web como nginx, podemos usar "systemctl start nginx" para rodar imediatamente, "systemctl enable nginx" para garantir que inicie em todo boot, ou "systemctl enable --now nginx" para fazer as duas coisas ao mesmo tempo.

Vale ressaltar que o start não funciona se não estiver habilitado.