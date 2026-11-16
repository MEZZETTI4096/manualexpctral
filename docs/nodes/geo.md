# GEO — Geometria Procedural

Sessão do catálogo técnico com **10 nodes**. Cor da categoria na interface: `#00F5D4`.

Exemplo real da interface: ![exemplo](../assets/exemplos/geo.png)

| Node | Slug | Entradas | Saídas | Especificações Técnicas | Uso | Usado em |
|---|---|---|---|---|---|---|
| **Primitive** | `primitive` | — | Geometria (geo) | Plano/cubo/esfera/cilindro/torus com segmentos paramétricos (padrão 32); a contagem de vértices aparece no próprio node. | Início de todo pipeline [GEO]; plano + Noise = terreno (Receita #23). | Receitas #23, #24; Blueprints #23, #24 |
| **Deform** | `deform` | Geometria (geo), Height (scalar) | Geometria (geo) | Desloca vértices por Height/campo com intensidade 0–1+; requer malha refinada — aplique Subdivide antes. | Terrenos e ondulações: height procedural direto na malha. | Receitas #19, #22, #23, #24, #26; Blueprints #19, #22, #23, #24, #26 |
| **Scatter** | `scatter` | Superfície (geo), Instância (geo), Densidade (scalar) | Instâncias (inst) | Distribuição com densidade 0–10k+ e Seed estável; saída Instance Array consumida por Geometry Output. Custo linear com o número de instâncias. | Par canônico Primitive ➔ Scatter; use Noise na densidade (Receita #24). | Receitas #24; Blueprints #24 |
| **Attractor** | `attractor` | Geometria (geo), Ponto (vector), Força (scalar) | Geometria (geo) | Ponto + força ± (atrai/repulsa) com falloff por distância; interativo via Pointer. Custo por vértice. | Interação do cursor com a malha (Bloco Interação). Na variante VFX: entradas Position/Age 0-1 e saída Position. | Receitas #29; Blueprints #29 |
| **Vortex** | `vortex` | Geometria (geo), Eixo (vector), Força (scalar) | Geometria (geo) | Eixo + força tangencial com falloff; bom para redemoinhos. Combine com Attractor para sucção espiral. | Redemoinhos e espirais em VFX e geometria. Na variante VFX: entradas Position/Time (s) e saída Position. | Receitas #28; Blueprints #28 |
| **Mirror** | `mirror` | Geometria (geo) | Geometria (geo) | Espelha em X/Y/Z com merge opcional no plano de corte; dobra os vértices — aplique antes de simulações pesadas. | Simetria rápida para personagens e props. | — |
| **Subdivide** | `subdivide` | Geometria (geo), Nível (scalar) | Geometria (geo) | Nível 0–4 tipicamente, com custo exponencial (×4 faces por nível). Subdivida antes de Deform/Displace. | Subdivida ANTES de Deform/Displace para evitar facetas. | — |
| **Array** | `array` | Geometria (geo), Contagem (scalar) | Instâncias (inst) | Contagem e offset linear/radial com saída Instance Array; prefira ao Scatter quando o padrão for regular. | Colunas, grades e coroas de objetos. | — |
| **Displace** | `displace` | Geometria (geo), Height (scalar), Escala (scalar) | Geometria (geo) | Desloca vértices ao longo da normal por Height × Escala; relevo real que exige Subdivide — mais caro que Bump. | Relevo real (não falso como Bump); combine com Subdivide. | — |
| **Delete** | `delete` | Geometria (geo), Offset (vector), Height (scalar) | Geometria (geo) | Recorta a malha por Height com Offset, mantendo a malha válida; combine com Instance Info (Id) para remoção seletiva. | Recorte por altura antes do Scatter; combine com Instance Info (Id). | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)