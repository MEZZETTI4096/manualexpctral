# GEN — Geradores Procedurais

Sessão do catálogo técnico com **12 nodes**. Cor da categoria na interface: `#10B981`.

Exemplo real da interface: ![exemplo](../assets/exemplos/gen.png)

| Node | Slug | Entradas | Saídas | Especificações Técnicas | Uso | Usado em |
|---|---|---|---|---|---|---|
| **Noise** | `noise` | Coord (vector) | Value (scalar), Color (color) | Fractal FBM: 4 octaves e escala 5.0 por padrão, saída ~0–1 centrada em 0.5. Cada octave dobra o custo — 3 a 5 cobrem a maioria dos casos. | Some 10–20% de Noise a padrões geométricos para quebrar a regularidade. | Receitas #01, #02, #04, #07, #11, #13, #16, #23; Blueprints #01, #02, #04, #07, #11, #13, #16, #23 |
| **Voronoi** | `voronoi` | Coord (vector) | Value (scalar), Color (color), Distância (scalar) | Distância ao ponto mais próximo, saída ~0–1; 1–4 feature points por célula e aleatoriedade 0–1 (padrão 1). Mais caro que Noise — evite octaves altas. | Combine com Height Blend para preencher cavidades primeiro (Receita #02). | Receitas #02, #07, #12; Blueprints #02, #03, #07, #12 |
| **Brick** | `brick` | Coord (vector) | Value (scalar), ID (scalar) | Padrões Running/Stack com juntes ~0.04 e offset de linha 0.5 por padrão. Saída Value + ID por tijolo. Avaliação analítica por pixel — barato. | A saída ID gera variação individual por peça (Receita #05). | Receitas #01, #03, #04, #05; Blueprints #01, #03, #04, #05, #14 |
| **Dots** | `dots` | Coord (vector) | Value (scalar) | Disco central por célula com raio 0–0.5 (padrão 0.35) e borda suavizada. Muito barato; base de halftone e micro-relevo. | Base para halftone, telas e micro-relevo de tecido. | Receitas #10, #14; Blueprints #10, #14 |
| **Checker** | `checker` | Coord (vector) | Color (color) | Binário 0/1 por paridade de célula; escala via Coord e custo desprezível. Use apenas como diagnóstico de UV. | Ferramenta de diagnóstico: qualquer distorção de UV fica imediatamente visível. | Receitas #14; Blueprints #14 |
| **Gradient** | `gradient` | Coord (vector) | Value (scalar) | Linear/radial/diamante entre P0 e P1, saída 0–1 com clamp nas extremidades. Barato; combine com Step para bandas duras. | Máscaras de posição e fades de iluminação em NPR. | — |
| **Wave** | `wave` | Coord (vector), Fase (scalar) | Value (scalar) | Sine/Tri/Square com fase 0–1 animável por Time; saída 0–1 (ou −1–1 em modo raw). Custo mínimo. | Time ➔ Mapping ➔ Wave para bandeiras e superfícies animadas (Receita #15). | Receitas #17, #26; Blueprints #17, #26 |
| **White Noise** | `white-noise` | — | Value (scalar) | Hash por pixel sem coerência espacial, saída 0–1 uniforme e sem parâmetros de escala. Baratíssimo; semente por instância via Object Info. | Grão de filme, dithering e sementes aleatórias por instância. | — |
| **Truchet** | `truchet` | Coord (vector) | Value (scalar) | Azulejos com arcos/linhas rotacionados por hash, formando caminhos contínuos; a escala controla o tamanho do mosaico. Custo baixo-médio. | Labirintos, circuitos e padrões decorativos sem emendas. | — |
| **Caustics** | `caustics` | Coord (vector), Escala (scalar) | Value (scalar), Color (color) | Refração animada com escala padrão ~5 e velocidade via Time. Mais caro que Noise puro — reserve para superfícies de destaque. | Superfícies de água e fundo de piscina; anime via Time no domínio. | — |
| **Cells** | `cells` | Coord (vector) | Value (scalar), Color (color) | Voronoi de bordas duras com ID por célula; Value 0–1 e Color por célula. Use o ID com Color Ramp para variação por peça. Custo médio. | Pedras, escamas e placas; varie a cor por célula com Color Ramp. | — |
| **Stripes** | `stripes` | Coord (vector) | Value (scalar) | Faixas com largura 0–1 (padrão 0.5) e direção controlada via Mapping; bordas suaves opcionais. Barato. | Madeira e tecido listrado; anime via Mapping com Time. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)