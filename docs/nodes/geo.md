# GEO — Geometria Procedural

Sessão do catálogo técnico com **10 nodes**. Cor da categoria na interface: `#00F5D4`.

Exemplo real da interface: ![exemplo](../assets/exemplos/geo.png)

| Node | Slug | Entradas | Saídas | Uso | Usado em |
|---|---|---|---|---|---|
| **Primitive** | `primitive` | — | Geometria (geo) | Início de todo pipeline [GEO]; plano + Noise = terreno (Receita #23). | Receitas #23, #24; Blueprints #23, #24 |
| **Deform** | `deform` | Geometria (geo), Height (scalar) | Geometria (geo) | Terrenos e ondulações: height procedural direto na malha. | Receitas #19, #22, #23, #24, #26; Blueprints #19, #22, #23, #24, #26 |
| **Scatter** | `scatter` | Superfície (geo), Instância (geo), Densidade (scalar) | Instâncias (inst) | Par canônico Primitive ➔ Scatter; use Noise na densidade (Receita #24). | Receitas #24; Blueprints #24 |
| **Attractor** | `attractor` | Geometria (geo), Ponto (vector), Força (scalar) | Geometria (geo) | Interação do cursor com a malha (Bloco Interação). | Receitas #29; Blueprints #29 |
| **Vortex** | `vortex` | Geometria (geo), Eixo (vector), Força (scalar) | Geometria (geo) | Redemoinhos e espirais em VFX e geometria. | Receitas #28; Blueprints #28 |
| **Mirror** | `mirror` | Geometria (geo) | Geometria (geo) | Simetria rápida para personagens e props. | — |
| **Subdivide** | `subdivide` | Geometria (geo), Nível (scalar) | Geometria (geo) | Subdivida ANTES de Deform/Displace para evitar facetas. | — |
| **Array** | `array` | Geometria (geo), Contagem (scalar) | Instâncias (inst) | Colunas, grades e coroas de objetos. | — |
| **Displace** | `displace` | Geometria (geo), Height (scalar), Escala (scalar) | Geometria (geo) | Relevo real (não falso como Bump); combine com Subdivide. | — |
| **Delete** | `delete` | Geometria (geo), Taglist (scalar) | Geometria (geo) | Delete por tag antes do Scatter; combine com Instance Info (Id). | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)