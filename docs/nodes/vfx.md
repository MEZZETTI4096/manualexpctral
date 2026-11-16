# VFX — Partículas & VFX

Sessão do catálogo técnico com **9 nodes**. Cor da categoria na interface: `#EF4444`.

Exemplo real da interface: ![exemplo](../assets/exemplos/vfx.png)

| Node | Slug | Entradas | Saídas | Uso | Usado em |
|---|---|---|---|---|---|
| **Emitter** | `emitter` | — | Partículas (inst) | Início de todo sistema VFX (Receitas #27–30). | Receitas #27, #29; Blueprints #27, #29 |
| **Particle** | `particle` | Partículas (inst) | Idade (scalar), Posição (vector), Velocidade (vector) | Age 0–1 sincroniza Size/Color over Life e Fade (par canônico). | Receitas #27, #28, #29; Blueprints #27, #28, #29 |
| **Turbulence** | `turbulence` | Posição (vector), Escala (scalar) | Posição (vector) | Brasas e poeira errática (Receita #30). | Receitas #27, #30; Blueprints #27, #30 |
| **Size over Life** | `size-over-life` | Idade (scalar) | Tamanho (scalar) | Nascimento pequeno ➔ pico ➔ fade; use Remap para um mínimo visível. | Receitas #28; Blueprints #28 |
| **Color over Life** | `color-over-life` | Idade (scalar) | Cor (color) | Fogo: branco ➔ laranja ➔ vermelho ➔ fumaça. | Receitas #27; Blueprints #27 |
| **Fade** | `fade` | Idade (scalar) | Opacidade (scalar) | Evite pops: sempre fade-out suave antes da morte da partícula. | Receitas #27, #29; Blueprints #27, #29 |
| **Sprite** | `sprite` | Cor (color), Opacidade (scalar) | Visual (inst) | Fumaça, brasas e detritos com textura suave. | Receitas #27, #28; Blueprints #27, #28 |
| **Simulation** | `simulation` | Position (vector), Velocity (vector), Idade (scalar) | Position (vector), Velocity (vector), Idade (scalar) | Núcleo do loop VFX: Emitter ➔ Simulation ➔ Color over Life ➔ VFX Output. | — |
| **Field** | `field` | Position (vector) | Field (vector) | Combine com Simulation para vento, gravidade localizada e redemoinhos. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)