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
Benefícios dos Boot Targets

`Flexibilidade: fácil mudar o comportamento do boot entre linha de comando e interface gráfica.`

`Segurança: permite inicializar em modos de recuperação (rescue/emergency).`

`Controle: possibilita alternar dinamicamente entre estados do sistema sem reiniciar.`

`Clareza: substitui os antigos runlevels por nomes mais descritivos.`