# INP — Inputs & Fontes de Dados

Sessão do catálogo técnico com **10 nodes**. Cor da categoria na interface: `#38BDF8`.

Exemplo real da interface: ![exemplo](../assets/exemplos/inp.png)

| Node | Slug | Entradas | Saídas | Especificações Técnicas | Uso | Usado em |
|---|---|---|---|---|---|---|
| **Image Texture** | `image-texture` | UV (vector) | Color (color), Alpha (scalar) | Expõe canais R/G/B/A com entrada UV para amostragem customizada. Padrão: sRGB para cor, Linear para dados (ORM). Suporta PNG/JPG/EXR — prefira EXR para HDR. O custo cresce com a resolução; use mipmaps. | Padrão para mapas ORM: R = Occlusion, G = Roughness, B = Metalness (Receita #06). | Receitas #06, #08, #13; Blueprints #06, #08, #13 |
| **Audio Input** | `audio-input` | — | Level (scalar), Bass (scalar), Mid (scalar), Treble (scalar), Peak (scalar), Beat (scalar), Spectrum (scalar) | Atualiza a cada frame de áudio (~60 Hz). Level: RMS; Bass/Mid/Treble: bandas 0–1; Peak: pico instantâneo; Beat: pulso 0/1 no transiente; Spectrum: bandas completas. Sem buffer histórico — estabilize com Smoothstep. | Base para reatividade sonora: calibre picos com Step/Smoothstep (Receita #21). | Receitas #18, #19, #30; Blueprints #18, #19, #30 |
| **Time** | `time` | — | Value (scalar) | Valor de tempo contínuo em segundos (float crescente); a precisão decai após horas — reinicie o ciclo para loops longos. | Combine com Math [Sine] e Remap para pulsações e ondas contínuas. | Receitas #13, #15, #26; Blueprints #13, #15, #26 |
| **Pointer** | `pointer` | — | UV (vector), Down (scalar) | UV do cursor em 0–1 e Down 0/1. Só atualiza com interação e sem suavização nativa — passe por Smoothstep/Lerp para movimento orgânico. | Compare UV do cursor com UV do node para máscaras interativas (Receita #20). | Receitas #20; Blueprints #20 |
| **Data Input** | `data-input` | T (scalar), U (scalar) | Value (scalar), Count (scalar) | Lê colunas T/U externas como escalares 0–1, sem interpolação nativa; normalize com Remap. Atualiza quando a fonte muda. | Ideal para dashboards e visualizações dirigidas por dados. | Receitas #22; Blueprints #22 |
| **Viewport** | `viewport` | — | Aspect (scalar), Resolution (vector) | Aspect (escalar) e Resolution em pixels (vetor); estático por frame. Multiplique padrões pelo aspect para evitar esticamento em telas não quadradas. | Corrija distorções de padrões em telas não quadradas (Receita #19). | Receitas #14; Blueprints #14 |
| **Camera** | `camera` | — | Position (vector), Direction (vector), FOV (scalar), Near (scalar), Far (scalar) | Saídas Position e Direction (vetores) + FOV (padrão 60°), Near 0.1 e Far 100 (escalares); acompanha a câmera ativa da cena. | Alimente a posição da câmera em Vector Math/Fresnel para efeitos dependentes da visão. | — |
| **Mesh Map** | `mesh-map` | Position (vector), UV (vector) | Value (scalar) | Amostra mapas assados (curvatura, AO, espessura) por vértice/UV, valores 0–1. A resolução do bake da malha limita o detalhe. | Use curvatura como máscara de desgaste e AO para sujar cavidades sem bake externo. | — |
| **Color** | `color` | — | Color (color) | Constante RGBA 0–1 com color picker e custo de amostragem zero. Use como parâmetro exposto em grupos em vez de digitar valores node a node. | Defina cores base e parâmetros de Blend/Mix sem depender de texturas externas. | — |
| **Value** | `value` | Value (scalar) | Value (scalar) | Slider escalar (padrão 0.5, faixa ajustável); repassa o valor conectado se houver cabo. Custo zero — ideal para expor parâmetros. | Exponha controles (intensidade, mix, limiar) sem editar o grafo. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)