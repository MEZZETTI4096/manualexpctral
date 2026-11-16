# OUT — Saídas & Render

Sessão do catálogo técnico com **3 nodes**. Cor da categoria na interface: `#94A3B8`.


| Node | Slug | Entradas | Saídas | Especificações Técnicas | Uso | Usado em |
|---|---|---|---|---|---|---|
| **Material Output** | `material-output` | Base Color (color), Roughness (scalar), Metallic (scalar), Normal (vector), Height (scalar), Emissive (color), Occlusion (scalar), Clearcoat (scalar), Clearcoat Rough (scalar), Sheen (color), Transmission (scalar), IOR (scalar), Opacity (scalar), Anisotropy (scalar) | — | Terminal com 14 entradas: Base Color, Roughness, Metallic, Normal, Height, Emissive, Occlusion, Clearcoat, Clearcoat Rough, Sheen, Transmission, IOR, Opacity e Anisotropy; valores fora da faixa são clampados. Um por pipeline de material. | Todo caminho de material termina aqui (usado em 19 receitas). | Receitas #01, #02, #03, #04, #05, #06, #07, #08, #09, #10, #11, #12, #15, #16, #17, #18, #19, #20, #21, #25; Blueprints #01, #02, #03, #04, #05, #06, #07, #08, #09, #10, #11, #12, #15, #16, #17, #18, #19, #20, #21, #25 |
| **Geometry Output** | `geometry-output` | Geometria (geo), Instâncias (inst) | — | Terminal GEO: recebe a Geometria final e as Instâncias do Scatter. Um por pipeline de geometria. | Fim do fluxo [GEO]; sem saídas à direita (node terminal). | Receitas #23, #24, #26; Blueprints #23, #24, #26 |
| **VFX Output** | `vfx-output` | Position (vector), Color (color), Size (scalar), Opacity (scalar), Sprite (scalar) | — | Terminal VFX: Position, Color, Size, Opacity e Sprite; conecte Turbulence/Motion em Position para movimento. | Fim do fluxo VFX; conecte Turbulence em Position para movimento. | Receitas #27, #28, #29, #30; Blueprints #27, #28, #29, #30 |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)