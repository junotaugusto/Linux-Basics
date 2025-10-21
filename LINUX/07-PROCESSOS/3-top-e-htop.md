# Comandos `top` e `htop`

No Linux, os comandos `top` e `htop` são usados para **monitorar em tempo real os processos e o uso de recursos do sistema**, como CPU, memória e swap. Eles ajudam a identificar processos que estão consumindo muitos recursos ou problemas de desempenho.

---

## `top`

- **Descrição:** comando nativo do Linux que exibe uma lista dinâmica dos processos ativos, atualizada a cada poucos segundos.
- **Principais informações mostradas:**
  - `PID`: identificador do processo
  - `USER`: usuário dono do processo
  - `PR`: prioridade do processo
  - `NI`: valor de “nice” (prioridade ajustável pelo usuário)
  - `VIRT, RES, SHR`: consumo de memória virtual, residente e compartilhada
  - `S`: estado do processo (R=Running, S=Sleeping, Z=Zombie, etc.)
  - `%CPU e %MEM`: uso de CPU e memória
  - `TIME+`: tempo de CPU consumido
  - `COMMAND`: comando ou programa executado
- **Comandos dentro do `top`:**
  - `P` → ordenar por uso de CPU
  - `M` → ordenar por uso de memória
  - `k` → finalizar processo pelo PID
  - `q` → sair do `top`

> É nativo, leve e funcional, mas a interface é simples e não interativa com mouse.

---

## `htop`

- **Descrição:** versão mais avançada e interativa do `top`, geralmente precisa ser instalada (`sudo apt install htop` no Debian/Ubuntu).
- **Principais diferenças em relação ao `top`:**
  - Interface colorida e mais amigável
  - Permite **navegação interativa com teclado e mouse**
  - Facilita ordenar, filtrar e buscar processos
  - Mostra barras gráficas de CPU, memória e swap
  - Permite **matar, renice e gerenciar processos** diretamente com teclas de atalho
- **Principais teclas:**
  - `F6` → escolher a coluna para ordenar
  - `F9` → matar processo selecionado
  - `F10` → sair do `htop`

> Em resumo, `htop` é uma versão mais visual e amigável do `top`, com funcionalidades extras para gerenciamento de processos.

---

## Conclusão

- Use **`top`** se quiser algo rápido e disponível em qualquer sistema Linux sem instalar nada.
- Use **`htop`** se preferir uma visualização mais clara, interativa e colorida dos processos e recursos do sistema.
