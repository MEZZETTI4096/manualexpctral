# FIL — Filtros & Convolução

Sessão do catálogo técnico com **9 nodes**. Cor da categoria na interface: `#F59E0B`.

Exemplo real da interface: ![exemplo](../assets/exemplos/fil.png)

| Node | Slug | Entradas | Saídas | Uso | Usado em |
|---|---|---|---|---|---|
| **Blur** | `blur` | Entrada (color), Raio (scalar) | Color (color) | Suavize máscaras serrilhadas antes de usar como Fac. | Receitas #12; Blueprints #12 |
| **Slope Blur** | `slope-blur` | In (color), Slope (scalar) | Color (color) | Erosão e lascas: Brick + Noise em Slope (Receita #04). | Receitas #04; Blueprints #04 |
| **Directional Warp** | `directional-warp` | Entrada (color), Ângulo (scalar), Intensidade (scalar) | Color (color) | Fluxos direcionais: vento, cabelo, água (Receita #14). | Receitas #13, #17; Blueprints #13, #17 |
| **Edge Wear** | `edge-wear` | Height (scalar) | Value (scalar) | Desgaste metálico PBR (Receita #01); inverta para Roughness. | Receitas #01; Blueprints #01 |
| **Height AO** | `height-ao` | Height (scalar) | Value (scalar) | Escureça cavidades e conecte também em Occlusion do Material Output (Receita #03). | Receitas #03; Blueprints #03 |
| **Bump** | `bump` | Height (scalar) | Normal (vector) | Conecte sempre a Height combinada para manter continuidade das normais. | Receitas #02, #04; Blueprints #02, #04 |
| **Normal Map** | `normal-map` | Height (scalar) | Normal (vector) | Prefira ao Bump quando o material for exportado para outros motores. | Receitas #12; Blueprints #12 |
| **Sobel Normal** | `sobel-normal` | Height (scalar) | Normal (vector) | Detalhe de micro-relevo em textos, tecidos e gravações. | Receitas #12; Blueprints #12 |
| **Sharpen** | `sharpen` | Entrada (color), Intensidade (scalar) | Color (color) | Recupere definição após Blurs intensos ou upscales. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)