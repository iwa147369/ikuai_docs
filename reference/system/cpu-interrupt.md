# CPU Interrupt Control

**Source:** https://www.ikuai8.com/support/ymgn/lyym/xtsz/2020-07-31-07-00-43/cpu.html

## I. Overview

CPU Interrupt Control manages CPU frequency scaling and the distribution of network interrupt handling across CPU cores.

---

## II. CPU Frequency Scaling Modes

| Mode | Description |
|---|---|
| Performance | Runs at maximum frequency under full load |
| Conservative | Lower frequency with gradual adjustments; more energy-efficient |
| Powersave | Runs at minimum frequency; lowest power consumption |
| Ondemand | Default mode; automatically adjusts frequency based on load |
| Schedutil | Faster and more precise frequency control with better efficiency |

---

## III. Interrupt Types

**Hardware Interrupts** — Asynchronous signals from peripheral hardware to the CPU. They require an interrupt controller and are processed faster than software interrupts. They can be masked via CPU flags.

**Software Interrupts** — Signals from software programs to the kernel, typically triggered by hardware interrupt handlers or process schedulers. They cannot be masked.

---

## IV. Recommended Configuration

- Enable **soft interrupts** on both LAN and WAN ports to distribute load across cores.
- If a specific CPU core is overloaded, disable its soft interrupt to shift work to other cores.
- When manually assigning a network card to a specific CPU, first disable that CPU's **hard interrupt** for that card.
- Assign **later CPU IDs** to high-traffic LAN ports and **earlier CPU IDs** to WAN ports.
