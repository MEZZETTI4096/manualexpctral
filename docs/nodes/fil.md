# FIL — Filtros & Convolução

Sessão do catálogo técnico com **9 nodes**. Cor da categoria na interface: `#F59E0B`.

Exemplo real da interface: ![exemplo](../assets/exemplos/fil.png)

| Node | Slug | Entradas | Saídas | Especificações Técnicas | Uso | Usado em |
|---|---|---|---|---|---|---|
| **Blur** | `blur` | Entrada (color), Raio (scalar) | Color (color) | Gaussiano/box com raio 0–10+ px (padrão 2); o custo cresce com o raio — prefira 2 passes pequenos a 1 gigante. Preserve bordas com máscara. | Suavize máscaras serrilhadas antes de usar como Fac. | Receitas #12; Blueprints #12 |
| **Slope Blur** | `slope-blur` | In (color), Slope (scalar) | Color (color) | Desloca pixels ao longo do gradiente do Slope, intensidade 0–1. Custo alto (re-amostragem por pixel) — use próximo da resolução final. | Erosão e lascas: Brick + Noise em Slope (Receita #04). | Receitas #04; Blueprints #04 |
| **Directional Warp** | `directional-warp` | Entrada (color), Ângulo (scalar), Intensidade (scalar) | Color (color) | Distorce por ângulo 0–360° e intensidade, animável via Time; amostra deslocada — custo médio. | Fluxos direcionais: vento, cabelo, água (Receita #14). | Receitas #13, #17; Blueprints #13, #17 |
| **Edge Wear** | `edge-wear` | Height (scalar) | Value (scalar) | Detecta quinas convexas a partir de Height com raio de amostragem 1–4 px e contraste 0–1. Custo médio-alto — reutilize a saída em vários canais. | Desgaste metálico PBR (Receita #01); inverta para Roughness. | Receitas #01; Blueprints #01 |
| **Height AO** | `height-ao` | Height (scalar) | Value (scalar) | AO por diferença de altura local, intensidade 0–1 e raio pequeno; sem bake e mais barato que AO global. Escurece apenas cavidades. | Escureça cavidades e conecte também em Occlusion do Material Output (Receita #03). | Receitas #03; Blueprints #03 |
| **Bump** | `bump` | Height (scalar) | Normal (vector) | Derivadas de altura → perturbação de normal, strength 0–1 (padrão ~0.3). Mais barato que Normal Map; artefatos em ângulos rasos. | Conecte sempre a Height combinada para manter continuidade das normais. | Receitas #02, #04; Blueprints #02, #04 |
| **Normal Map** | `normal-map` | Height (scalar) | Normal (vector) | Conversão tangent-space com intensidade e flip Y (padrão OpenGL). Portável entre motores; custo baixo. | Prefira ao Bump quando o material for exportado para outros motores. | Receitas #12; Blueprints #12 |
| **Sobel Normal** | `sobel-normal` | Height (scalar) | Normal (vector) | Kernel Sobel 3×3 que realça alta frequência; mais nítido que Bump em detalhes finos e sensível a ruído — passe Blur antes. | Detalhe de micro-relevo em textos, tecidos e gravações. | Receitas #12; Blueprints #12 |
| **Sharpen** | `sharpen` | Entrada (color), Intensidade (scalar) | Color (color) | Unsharp mask com raio 0.5–2 px e amount 0–2 (padrão ~0.5); excesso gera halo — mantenha amount ≤ 1. | Recupere definição após Blurs intensos ou upscales. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)