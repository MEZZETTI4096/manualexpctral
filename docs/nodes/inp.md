# INP — Inputs & Fontes de Dados

Sessão do catálogo técnico com **6 nodes**. Cor da categoria na interface: `#38BDF8`.

Exemplo real da interface: ![exemplo](../assets/exemplos/inp.png)

| Node | Slug | Entradas | Saídas | Uso | Usado em |
|---|---|---|---|---|---|
| **Image Texture** | `image-texture` | — | Color (color), Alpha (scalar) | Padrão para mapas ORM: R = Occlusion, G = Roughness, B = Metalness (Receita #06). | Receitas #06, #08, #13; Blueprints #06, #08, #13 |
| **Audio Input** | `audio-input` | — | Spectrum (scalar), Level (scalar), Beat (scalar) | Base para reatividade sonora: calibre picos com Step/Smoothstep (Receita #21). | Receitas #18, #19, #30; Blueprints #18, #19, #30 |
| **Time** | `time` | — | Segundos (scalar), Normalizado (scalar) | Combine com Math [Sine] e Remap para pulsações e ondas contínuas. | Receitas #13, #15, #26; Blueprints #13, #15, #26 |
| **Pointer** | `pointer` | — | UV (vector), Down (scalar) | Compare UV do cursor com UV do node para máscaras interativas (Receita #20). | Receitas #20; Blueprints #20 |
| **Data Input** | `data-input` | — | Valor (scalar) | Ideal para dashboards e visualizações dirigidas por dados. | Receitas #22; Blueprints #22 |
| **Viewport** | `viewport` | — | Aspect (vector), Resolução (vector) | Corrija distorções de padrões em telas não quadradas (Receita #19). | Receitas #14; Blueprints #14 |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)