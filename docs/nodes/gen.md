# GEN — Geradores Procedurais

Sessão do catálogo técnico com **12 nodes**. Cor da categoria na interface: `#10B981`.

Exemplo real da interface: ![exemplo](../assets/exemplos/gen.png)

| Node | Slug | Entradas | Saídas | Uso | Usado em |
|---|---|---|---|---|---|
| **Noise** | `noise` | Coord (vector) | Value (scalar), Color (color) | Some 10–20% de Noise a padrões geométricos para quebrar a regularidade. | Receitas #01, #02, #04, #07, #11, #13, #16, #23; Blueprints #01, #02, #04, #07, #11, #13, #16, #23 |
| **Voronoi** | `voronoi` | Coord (vector) | Value (scalar), Color (color), Distância (scalar) | Combine com Height Blend para preencher cavidades primeiro (Receita #02). | Receitas #02, #07, #12; Blueprints #02, #03, #07, #12 |
| **Brick** | `brick` | Coord (vector) | Value (scalar), ID (scalar) | A saída ID gera variação individual por peça (Receita #05). | Receitas #01, #03, #04, #05; Blueprints #01, #03, #04, #05, #14 |
| **Dots** | `dots` | Coord (vector) | Value (scalar) | Base para halftone, telas e micro-relevo de tecido. | Receitas #10, #14; Blueprints #10, #14 |
| **Checker** | `checker` | Coord (vector) | Color (color) | Ferramenta de diagnóstico: qualquer distorção de UV fica imediatamente visível. | Receitas #14; Blueprints #14 |
| **Gradient** | `gradient` | Coord (vector) | Value (scalar) | Máscaras de posição e fades de iluminação em NPR. | — |
| **Wave** | `wave` | Coord (vector), Fase (scalar) | Value (scalar) | Time ➔ Mapping ➔ Wave para bandeiras e superfícies animadas (Receita #15). | Receitas #17, #26; Blueprints #17, #26 |
| **White Noise** | `white-noise` | — | Value (scalar) | Grão de filme, dithering e sementes aleatórias por instância. | — |
| **Truchet** | `truchet` | Coord (vector) | Value (scalar) | Labirintos, circuitos e padrões decorativos sem emendas. | — |
| **Caustics** | `caustics` | Coord (vector), Escala (scalar) | Value (scalar), Color (color) | Superfícies de água e fundo de piscina; anime via Time no domínio. | — |
| **Cells** | `cells` | Coord (vector) | Value (scalar), Color (color) | Pedras, escamas e placas; varie a cor por célula com Color Ramp. | — |
| **Stripes** | `stripes` | Coord (vector) | Value (scalar) | Madeira e tecido listrado; anime via Mapping com Time. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)