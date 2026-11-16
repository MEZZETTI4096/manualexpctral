# OUT — Saídas & Render

Sessão do catálogo técnico com **3 nodes**. Cor da categoria na interface: `#94A3B8`.


| Node | Slug | Entradas | Saídas | Uso | Usado em |
|---|---|---|---|---|---|
| **Material Output** | `material-output` | Base Color (color), Roughness (scalar), Metalness (scalar), Normal (vector), Occlusion (scalar), Emissive (color) | — | Todo caminho de material termina aqui (usado em 19 receitas). | Receitas #01, #02, #03, #04, #05, #06, #07, #08, #09, #10, #11, #12, #15, #16, #17, #18, #19, #20, #21, #25; Blueprints #01, #02, #03, #04, #05, #06, #07, #08, #09, #10, #11, #12, #15, #16, #17, #18, #19, #20, #21, #25 |
| **Geometry Output** | `geometry-output` | Geometria (geo) | — | Fim do fluxo [GEO]; sem saídas à direita (node terminal). | Receitas #23, #24, #26; Blueprints #23, #24, #26 |
| **VFX Output** | `vfx-output` | Posição (vector), Tamanho (scalar), Opacidade (scalar), Sprite (inst) | — | Fim do fluxo VFX; conecte Turbulence em Position para movimento. | Receitas #27, #28, #29, #30; Blueprints #27, #28, #29, #30 |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)