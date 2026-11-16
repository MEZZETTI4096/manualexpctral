# INP — Inputs & Fontes de Dados

Sessão do catálogo técnico com **10 nodes**. Cor da categoria na interface: `#38BDF8`.

Exemplo real da interface: ![exemplo](../assets/exemplos/inp.png)

| Node | Slug | Entradas | Saídas | Especificações Técnicas | Uso | Usado em |
|---|---|---|---|---|---|---|
| **Image Texture** | `image-texture` | — | Color (color), Alpha (scalar) | Sem entradas; expõe canais R/G/B/A. Padrão: sRGB para cor, Linear para dados (ORM). Suporta PNG/JPG/EXR — prefira EXR para HDR. O custo cresce com a resolução; use mipmaps. | Padrão para mapas ORM: R = Occlusion, G = Roughness, B = Metalness (Receita #06). | Receitas #06, #08, #13; Blueprints #06, #08, #13 |
| **Audio Input** | `audio-input` | — | Spectrum (scalar), Level (scalar), Beat (scalar) | Atualiza a cada frame de áudio (~60 Hz). Spectrum: bandas 0–1; Level: RMS; Beat: pulso 0/1 no transiente. Sem buffer histórico — estabilize com Smoothstep. | Base para reatividade sonora: calibre picos com Step/Smoothstep (Receita #21). | Receitas #18, #19, #30; Blueprints #18, #19, #30 |
| **Time** | `time` | — | Segundos (scalar), Normalizado (scalar) | Segundos corridos (float crescente) e ciclo normalizado 0.0–1.0. A precisão do float decai após horas — reinicie o ciclo para loops longos. | Combine com Math [Sine] e Remap para pulsações e ondas contínuas. | Receitas #13, #15, #26; Blueprints #13, #15, #26 |
| **Pointer** | `pointer` | — | UV (vector), Down (scalar) | UV do cursor em 0–1 e Down 0/1. Só atualiza com interação e sem suavização nativa — passe por Smoothstep/Lerp para movimento orgânico. | Compare UV do cursor com UV do node para máscaras interativas (Receita #20). | Receitas #20; Blueprints #20 |
| **Data Input** | `data-input` | — | Valor (scalar) | Lê colunas T/U externas como escalares 0–1, sem interpolação nativa; normalize com Remap. Atualiza quando a fonte muda. | Ideal para dashboards e visualizações dirigidas por dados. | Receitas #22; Blueprints #22 |
| **Viewport** | `viewport` | — | Aspect (vector), Resolução (vector) | Aspect (x, y) e Resolução em pixels; estático por frame. Multiplique padrões pelo aspect para evitar esticamento em telas não quadradas. | Corrija distorções de padrões em telas não quadradas (Receita #19). | Receitas #14; Blueprints #14 |
| **Camera** | `camera` | Resolution (vector), Division (scalar), FOV (scalar), Near (scalar), Far (scalar) | Posição (vector) | Projeção com FOV padrão 60°, Near 0.1 e Far 100. A saída entrega a posição/transform da câmera no mundo; Division controla as fatias do frustum (tiling). | Alimente a posição da câmera em Vector Math/Fresnel para efeitos dependentes da visão. | — |
| **Mesh Map** | `mesh-map` | Position (vector), UV (vector) | Value (scalar) | Amostra mapas assados (curvatura, AO, espessura) por vértice/UV, valores 0–1. A resolução do bake da malha limita o detalhe. | Use curvatura como máscara de desgaste e AO para sujar cavidades sem bake externo. | — |
| **Color** | `color` | — | Cor (color) | Constante RGBA 0–1 com color picker e custo de amostragem zero. Use como parâmetro exposto em grupos em vez de digitar valores node a node. | Defina cores base e parâmetros de Blend/Mix sem depender de texturas externas. | — |
| **Value** | `value` | Valor (scalar) | Valor (scalar) | Slider escalar (padrão 0.5, faixa ajustável); repassa o valor conectado se houver cabo. Custo zero — ideal para expor parâmetros. | Exponha controles (intensidade, mix, limiar) sem editar o grafo. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)