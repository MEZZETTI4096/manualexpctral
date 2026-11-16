# COL — Cor & Composição

Sessão do catálogo técnico com **19 nodes**. Cor da categoria na interface: `#9B5DE5`.

Exemplo real da interface: ![exemplo](../assets/exemplos/col.png)

| Node | Slug | Entradas | Saídas | Especificações Técnicas | Uso | Usado em |
|---|---|---|---|---|---|---|
| **Color Ramp** | `color-ramp` | Fac (scalar) | Color (color) | Interpolação Linear/Constant/B-Spline entre paradas; Fac 0–1. O custo cresce com o número de paradas — 2 a 6 bastam. | O conversor universal: Noise/Voronoi ➔ Color Ramp é um par canônico. | Receitas #05, #07, #09, #10, #17, #18, #22, #25; Blueprints #05, #07, #09, #10, #17, #18, #22, #25 |
| **Blend** | `blend` | Base (color), Blend (color), Mask (scalar) | Color (color) | Modos Multiply/Overlay/Screen/Add… com opacidade por Mask 0–1. Operação por pixel barata; modos com pow (Overlay) custam um pouco mais. | Camadas de sujeira e variação controladas por máscara (Receita #03). | Receitas #03, #05; Blueprints #03, #05 |
| **Mix** | `mix` | A (color), B (color), Fac (scalar) | Color (color) | Lerp A↔B por Fac 0–1 (padrão 0.5). O mix mais barato do grafo — prefira ao Blend quando não precisar de modo de mesclagem. | Combine com Invert para trocar material exposto/base (Receita #01). | Receitas #01; Blueprints #01 |
| **Invert** | `invert` | In (color) | Color (color) | 1−x por canal preservando alpha, sem parâmetros e custo zero. Combine com Clamp para evitar negativos em entradas HDR. | Em Edge Wear, inverta antes de Roughness para metal liso nas quinas. | Receitas #01; Blueprints #01 |
| **Levels** | `levels` | In (color) | Color (color) | Black/White points e gamma (padrão 0–1 com gamma 1). Recompressão linear e barata; encadeie no máximo 2–3 para evitar banding. | Endureça máscaras: comprima o branco para manter áreas expostas em 1.0. | Receitas #03; Blueprints #03 |
| **Histogram Scan** | `histogram-scan` | In (color) | Value (scalar) | Threshold + contraste sobre o histograma, com posição 0–1 e suavização de borda. Transforma altura em máscara nítida. Custo baixo. | Transforme mapas de altura em máscaras precisas de desgaste. | Receitas #16; Blueprints #16 |
| **Hue Shift** | `hue-shift` | In (color), Hue (scalar) | Color (color) | Rotação de matiz de −180° a +180° (padrão 0), preservando S/L. Barato; evite empilhar vários shifts — some os ângulos. | Variação de cor por objeto via Object Info (ID). | Receitas #21; Blueprints #21 |
| **Posterize** | `posterize` | In (color), Passos (scalar) | Color (color) | Quantiza cada canal em 2–256 passos (padrão ~5). Banding intencional e custo mínimo. | Estilo cel-shading e dithering retro (Bloco NPR). | Receitas #08; Blueprints #08 |
| **Gradient Map** | `gradient-map` | In (scalar) | Out (color) | Paleta fixa de N cores indexada pela luminância (Fac 0–1), sem paradas editáveis. Barato. | Paletas limitadas (duotone/tritone) para estilização NPR. | — |
| **Luminance** | `luminance` | In (color) | Value (scalar) | Peso Rec.709 (0.2126/0.7152/0.0722), saída 0–1 com clamp acima de 1. Custo zero; porta de entrada padrão para alturas derivadas de cor. | Extraia altura de texturas coloridas para Bump/Deform. | Receitas #10; Blueprints #10 |
| **Curves** | `curves` | In (color) | Color (color) | Bézier editável ponto a ponto por canal, resposta não destrutiva em 0–1. Avaliação por lookup — barato mesmo com muitos pontos. | Contraste fino de máscaras sem empilhar múltiplos Levels. | — |
| **Spectral Dispersion** | `spectral-dispersion` | Thickness (scalar), Intensidade (scalar) | Color (color) | Separa comprimentos de onda com ângulo e intensidade 0–1 (padrão sutil, ~0.3); 3 amostras de espectro por pixel — custo médio. | Efeitos holográficos e de bolha de sabão (Receita #12). | Receitas #11; Blueprints #11 |
| **Height Blend** | `height-blend` | Base (color), Blend (color), Height (scalar) | Out (color), Height (scalar) | Compara as alturas dos dois materiais e resolve a mistura (cavidades primeiro). A saída dupla Color+Height mantém o relevo coerente. Custo baixo-médio. | Preencha cavidades antes do desgaste; devolve também a altura mesclada (Receita #02). | Receitas #02; Blueprints #02 |
| **Highlights/Midtones** | `highlights-midtones` | Image (color), Mask (scalar) | Image (color) | Ganho de ±1 aplicado separadamente a highlights e midtones, com Mask opcional. Opera em luma/HSV — barato. | Corrija exposição e temperatura das áreas claras sem afetar as sombras. | — |
| **Ratio** | `ratio` | A (scalar), B (scalar) | Out (scalar) | Out = A/(A+B) com proteção contra divisão por zero (retorna 0.5); use entradas ≥ 0. Custo mínimo. | Normalize misturas de dois sinais mantendo o balanço dentro de 0–1. | — |
| **Saturation** | `saturation` | In (color), Saturation (scalar) | Color (color) | Fator 0–2 (0 = cinza, 1 = original, 2 = dobrado), padrão 1; lerp em luma. Barato. | Dessature máscaras auxiliares ou intensifique cores em estilização. | — |
| **Specular Displacement** | `specular-displacement` | Displacement (scalar), Specular (color) | Displacement (scalar) | Modula o displacement pela energia especular, escala 0–1; mantém micro-relevo onde o material brilha. Custo depende do mapa de spec. | Micro-relevo em materiais molhados e metálicos; combine com Bump. | — |
| **Gradient Map 2** | `gradient-map-2` | In (scalar) | Out (color) | Duotone fixo: lerp entre 2 cores por Fac 0–1, sem paradas editáveis. O mais barato dos Gradient Maps. | Estilização de alto contraste com paleta reduzida (Bloco NPR). | — |
| **Gradient Map 4** | `gradient-map-4` | In (scalar) | Out (color) | Paleta quantizada de 4 cores por faixa de Fac (0–0.25/0.25–0.5/…), sem interpolação entre faixas em modo Step. Barato. | Paletas quantizadas para cel-shading e pôsteres (Receita #08). | Receitas #08; Blueprints #08 |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)