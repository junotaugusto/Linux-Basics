# Comandos kill e pkill

No Linux, os comandos **kill** e **pkill** são usados para **enviar sinais a processos**, normalmente para **finalizá-los**, mas também para outros sinais de controle.

---

## kill

- **Descrição:** envia sinais a processos **especificando o PID (Process ID)**.
- **Sintaxe básica:**

```bash
kill [opções] <PID>
```
- **Exemplo de uso:**
```bash
kill 1234
```
> Envia o sinal padrão SIGTERM (15) ao processo de PID 1234, solicitando que ele termine de forma graciosa.

- **Principais sinais usados:**
  - SIGTERM (15) → terminar o processo de forma segura (padrão)
  - SIGKILL (9) → força a finalização imediata do processo
  - SIGHUP (1) → reiniciar o processo (usado por serviços)

- **Exemplo matando um processo à força:**

```bash
kill -9 1234
```
---

## pkill

- **Descrição:** envia sinais a processos **especificando o nome do processo**, sem precisar do PID.
- **Sintaxe básica:**

```bash
pkill [opções] <nome_do_processo>
```
- **Exemplo de uso:**

```bash
pkill firefox
```
> Envia o sinal padrão SIGTERM para todos os processos cujo nome contém "firefox".

- **Opções comuns:**
  - -9 → força a finalização (SIGKILL)
  - -u <usuário> → filtra processos de um usuário específico
  - -f → considera o nome completo do comando (path incluído)

---

## Diferenças principais

| Comando | Identificação do processo | Observações |
|---------|---------------------------|-------------|
| kill    | PID                       | Mais preciso, mas exige que você saiba o PID |
| pkill   | Nome do processo          | Mais prático para finalizar processos pelo nome, pode afetar múltiplos processos |

> Em resumo, **kill é baseado em PID**, enquanto **pkill é baseado no nome do processo**, mas ambos servem para controlar processos via sinais.
