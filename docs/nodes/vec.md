# VEC — Vetores & UV

Sessão do catálogo técnico com **9 nodes**. Cor da categoria na interface: `#00BBF9`.

Exemplo real da interface: ![exemplo](../assets/exemplos/vec.png)

| Node | Slug | Entradas | Saídas | Uso | Usado em |
|---|---|---|---|---|---|
| **UV** | `uv` | — | UV (vector) | Ponto de partida de quase todo padrão procedural (par canônico com Mapping). | Receitas #14, #17, #18, #20; Blueprints #14, #17, #18, #20 |
| **Mapping** | `mapping` | UV (vector) | UV (vector) | Defina escala/rotação ANTES de amostrar qualquer padrão (par canônico). | Receitas #10, #13, #26; Blueprints #10, #13, #26 |
| **Separate RGB** | `separate-rgb` | Cor (color) | R (scalar), G (scalar), B (scalar) | Desempacote mapas ORM canal a canal (Receita #06). | Receitas #06; Blueprints #06 |
| **Combine XYZ** | `combine-xyz` | X (scalar), Y (scalar), Z (scalar) | Vetor (vector) | Reconstrua vetores após processar cada eixo separadamente. | — |
| **Vector Math** | `vector-math` | A (vector), B (vector) | Vetor (vector), Valor (scalar) | Distance ➔ Smoothstep é o par canônico de proximidade (Receita #20). | — |
| **Remap** | `remap` | In (scalar) | Value (scalar) | Normalize sinais: [-1..1 ➔ 0..1] antes de alimentar um Color Ramp. | Receitas #15, #22; Blueprints #15, #22 |
| **Fresnel** | `fresnel` | Normal (vector), Visão (vector) | Value (scalar) | Rim light, iridescência e contornos em NPR (Receita #11). | Receitas #09, #11; Blueprints #09, #11 |
| **Position** | `position` | — | Posição (vector) | Gradientes espaciais 3D e domínios de ruído em geometria. | Receitas #07; Blueprints #07 |
| **Normal** | `normal` | — | Normal (vector) | Combine com Dot e Fresnel para sombreamento customizado. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)