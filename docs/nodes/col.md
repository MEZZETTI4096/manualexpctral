# COL — Cor & Composição

Sessão do catálogo técnico com **12 nodes**. Cor da categoria na interface: `#9B5DE5`.

Exemplo real da interface: ![exemplo](../assets/exemplos/col.png)

| Node | Slug | Entradas | Saídas | Uso | Usado em |
|---|---|---|---|---|---|
| **Color Ramp** | `color-ramp` | Fac (scalar) | Color (color) | O conversor universal: Noise/Voronoi ➔ Color Ramp é um par canônico. | Receitas #05, #07, #09, #10, #17, #18, #22, #25; Blueprints #05, #07, #09, #10, #17, #18, #22, #25 |
| **Blend** | `blend` | Base (color), Blend (color), Mask (scalar) | Color (color) | Camadas de sujeira e variação controladas por máscara (Receita #03). | Receitas #02, #03, #05; Blueprints #02, #03, #05 |
| **Mix** | `mix` | A (color), B (color), Fac (scalar) | Color (color) | Combine com Invert para trocar material exposto/base (Receita #01). | Receitas #01; Blueprints #01 |
| **Invert** | `invert` | Entrada (color) | Color (color) | Em Edge Wear, inverta antes de Roughness para metal liso nas quinas. | Receitas #01; Blueprints #01 |
| **Levels** | `levels` | Entrada (color) | Color (color) | Endureça máscaras: comprima o branco para manter áreas expostas em 1.0. | Receitas #03; Blueprints #03 |
| **Histogram Scan** | `histogram-scan` | Value (scalar) | Value (scalar) | Transforme mapas de altura em máscaras precisas de desgaste. | Receitas #16; Blueprints #16 |
| **Hue Shift** | `hue-shift` | Cor (color), Deslocamento (scalar) | Color (color) | Variação de cor por objeto via Object Info (Random). | Receitas #21; Blueprints #21 |
| **Posterize** | `posterize` | Entrada (color), Passos (scalar) | Color (color) | Estilo cel-shading e dithering retro (Bloco NPR). | Receitas #08; Blueprints #08 |
| **Gradient Map** | `gradient-map` | Value (scalar) | Color (color) | Paletas limitadas (duotone/tritone) para estilização NPR. | Receitas #08; Blueprints #08 |
| **Luminance** | `luminance` | Cor (color) | Value (scalar) | Extraia altura de texturas coloridas para Bump/Deform. | Receitas #10; Blueprints #10 |
| **Curves** | `curves` | Entrada (color) | Color (color) | Contraste fino de máscaras sem empilhar múltiplos Levels. | — |
| **Spectral Dispersion** | `spectral-dispersion` | Ângulo (scalar), Intensidade (scalar) | Color (color) | Efeitos holográficos e de bolha de sabão (Receita #12). | Receitas #11; Blueprints #11 |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)