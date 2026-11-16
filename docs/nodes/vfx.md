# VFX — Partículas & VFX

Sessão do catálogo técnico com **9 nodes**. Cor da categoria na interface: `#EF4444`.

Exemplo real da interface: ![exemplo](../assets/exemplos/vfx.png)

| Node | Slug | Entradas | Saídas | Especificações Técnicas | Uso | Usado em |
|---|---|---|---|---|---|---|
| **Emitter** | `emitter` | — | Partículas (inst) | Taxa (partículas/s), vida útil, velocidade inicial e origem com Seed estável; fonte do sistema, sem entradas. | Início de todo sistema VFX (Receitas #27–30). | Receitas #27, #29; Blueprints #27, #29 |
| **Particle** | `particle` | Partículas (inst) | Idade (scalar), Posição (vector), Velocidade (vector) | Estado somente leitura: Idade 0–1, Position e Velocity; alimente os nodes over-Life a partir daqui. | Age 0–1 sincroniza Size/Color over Life e Fade (par canônico). | Receitas #27, #28, #29; Blueprints #27, #28, #29 |
| **Turbulence** | `turbulence` | Posição (vector), Escala (scalar) | Posição (vector) | Curl noise com escala e strength, animado via Time; agita sem explodir trajetórias. Custo médio por partícula. | Brasas e poeira errática (Receita #30). | Receitas #27, #30; Blueprints #27, #30 |
| **Size over Life** | `size-over-life` | Idade (scalar) | Tamanho (scalar) | Curva tamanho × idade; normalize com Remap para garantir um tamanho mínimo visível. Barato. | Nascimento pequeno ➔ pico ➔ fade; use Remap para um mínimo visível. | Receitas #28; Blueprints #28 |
| **Color over Life** | `color-over-life` | Idade (scalar) | Cor (color) | Gradiente cor × idade (fogo: branco→laranja→vermelho→fumaça). Barato. | Fogo: branco ➔ laranja ➔ vermelho ➔ fumaça. | Receitas #27; Blueprints #27 |
| **Fade** | `fade` | Idade (scalar) | Opacidade (scalar) | Opacidade com curvas de entrada e saída; mantenha sempre um fade-out ativo para evitar pops. | Evite pops: sempre fade-out suave antes da morte da partícula. | Receitas #27, #29; Blueprints #27, #29 |
| **Sprite** | `sprite` | Cor (color), Opacidade (scalar) | Visual (inst) | Billboard por partícula com Cor/Opacidade e saída Visual (inst); use textura suave para fumaça e brasas. | Fumaça, brasas e detritos com textura suave. | Receitas #27, #28; Blueprints #27, #28 |
| **Simulation** | `simulation` | Position (vector), Velocity (vector), Idade (scalar) | Position (vector), Velocity (vector), Idade (scalar) | Integra o estado por delta time com entradas e saídas simétricas (Position/Velocity/Idade) para encadear forças; use um Simulation por sistema. | Núcleo do loop VFX: Emitter ➔ Simulation ➔ Color over Life ➔ VFX Output. | — |
| **Field** | `field` | Position (vector) | Field (vector) | Amostra força/direção numa Position; a saída vetorial está pronta para somar na Velocity do Simulation. | Combine com Simulation para vento, gravidade localizada e redemoinhos. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)