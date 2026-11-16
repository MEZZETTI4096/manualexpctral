# VFX — Partículas & VFX

Sessão do catálogo técnico com **9 nodes**. Cor da categoria na interface: `#EF4444`.

Exemplo real da interface: ![exemplo](../assets/exemplos/vfx.png)

| Node | Slug | Entradas | Saídas | Especificações Técnicas | Uso | Usado em |
|---|---|---|---|---|---|---|
| **Emitter** | `emitter` | Seed (scalar) | Origin (vector), Direction (vector) | Entrada Seed para variação estável; saídas Origin e Direction alimentam o Motion. Fonte de todo sistema VFX. | Início de todo sistema VFX (Receitas #27–30). | Receitas #27, #29; Blueprints #27, #29 |
| **Particle** | `particle` | — | Age (scalar), Time (scalar), Seed (scalar), Random (vector) | Estado somente leitura: Age 0–1, Time, Seed e Random (vetor); alimente os nodes over-Life a partir daqui. | Age 0–1 sincroniza Size/Color over Life e Fade (par canônico). | Receitas #27, #28, #29; Blueprints #27, #28, #29 |
| **Turbulence** | `turbulence` | Position (vector), Strength (scalar) | Position (vector), Velocity (vector) | Curl noise com escala e strength, animado via Time; agita sem explodir trajetórias. Custo médio por partícula. | Brasas e poeira errática (Receita #30). | Receitas #27, #30; Blueprints #27, #30 |
| **Size over Life** | `size-over-life` | Age 0-1 (scalar) | Size (scalar) | Curva tamanho × idade; normalize com Remap para garantir um tamanho mínimo visível. Barato. | Nascimento pequeno ➔ pico ➔ fade; use Remap para um mínimo visível. | Receitas #28; Blueprints #28 |
| **Color over Life** | `color-over-life` | Age 0-1 (scalar) | Color (color) | Gradiente cor × idade (fogo: branco→laranja→vermelho→fumaça). Barato. | Fogo: branco ➔ laranja ➔ vermelho ➔ fumaça. | Receitas #27; Blueprints #27 |
| **Fade** | `fade` | Age 0-1 (scalar) | Opacity (scalar) | Opacidade com curvas de entrada e saída; mantenha sempre um fade-out ativo para evitar pops. | Evite pops: sempre fade-out suave antes da morte da partícula. | Receitas #27, #29; Blueprints #27, #29 |
| **Sprite** | `sprite` | Mask (scalar) | Visual (scalar) | Billboard por partícula: entrada Mask (escalar) e saída Visual para o VFX Output; use textura suave para fumaça e brasas. | Fumaça, brasas e detritos com textura suave. | Receitas #27, #28; Blueprints #27, #28 |
| **Simulation** | `simulation` | Position (vector), Velocity (vector), Age (scalar) | Position (vector), Velocity (vector), Age (scalar) | Integra o estado por delta time com entradas e saídas simétricas (Position/Velocity/Age) para encadear forças; use um Simulation por sistema. | Núcleo do loop VFX: Emitter ➔ Simulation ➔ Color over Life ➔ VFX Output. | — |
| **Field** | `field` | Position (vector) | Field (vector) | Amostra força/direção numa Position; a saída vetorial está pronta para somar na Velocity do Simulation. | Combine com Simulation para vento, gravidade localizada e redemoinhos. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)