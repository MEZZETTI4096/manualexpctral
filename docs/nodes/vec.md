# VEC — Vetores & UV

Sessão do catálogo técnico com **9 nodes**. Cor da categoria na interface: `#00BBF9`.

Exemplo real da interface: ![exemplo](../assets/exemplos/vec.png)

| Node | Slug | Entradas | Saídas | Especificações Técnicas | Uso | Usado em |
|---|---|---|---|---|---|---|
| **UV** | `uv` | — | UV (vector) | Coordenadas 0–1 do canal ativo (objeto/tela), custo zero. Passe sempre por Mapping antes de amostrar padrões. | Ponto de partida de quase todo padrão procedural (par canônico com Mapping). | Receitas #14, #17, #18, #20; Blueprints #14, #17, #18, #20 |
| **Mapping** | `mapping` | UV (vector) | UV (vector) | Scale/Rotation/Translation em ordem fixa (S→R→T), padrão identidade. Barato; anime Translation via Time para deslocar padrões. | Defina escala/rotação ANTES de amostrar qualquer padrão (par canônico). | Receitas #10, #13, #26; Blueprints #10, #13, #26 |
| **Separate RGB** | `separate-rgb` | Cor (color) | R (scalar), G (scalar), B (scalar) | Decomposição em 3 escalares 0–1 por swizzle — custo zero. Porta de entrada para mapas empacotados (ORM). | Desempacote mapas ORM canal a canal (Receita #06). | Receitas #06; Blueprints #06 |
| **Combine XYZ** | `combine-xyz` | X (scalar), Y (scalar), Z (scalar) | Vetor (vector) | Monta um Vec3 a partir de 3 escalares independentes; custo zero. Reconstrua vetores após processar eixos isolados. | Reconstrua vetores após processar cada eixo separadamente. | — |
| **Vector Math** | `vector-math` | A (vector), B (vector) | Vetor (vector), Valor (scalar) | Add/sub/dot/cross/normalize/distance com saída dupla Vetor+Valor (dot/distance). Custo mínimo. | Distance ➔ Smoothstep é o par canônico de proximidade (Receita #20). | — |
| **Remap** | `remap` | In (scalar) | Value (scalar) | From/To lineares com clamp opcional; padrão [−1..1]→[0..1]. Barato e essencial antes de Color Ramp. | Normalize sinais: [-1..1 ➔ 0..1] antes de alimentar um Color Ramp. | Receitas #15, #22; Blueprints #15, #22 |
| **Fresnel** | `fresnel` | Normal (vector), Visão (vector) | Value (scalar) | IOR 0–2 (padrão ~1.45), saída 0–1 com bordas acesas. Barato; base de rim light e iridescência. | Rim light, iridescência e contornos em NPR (Receita #11). | Receitas #09, #11; Blueprints #09, #11 |
| **Position** | `position` | — | Posição (vector) | Espaço objeto/mundo/mesh selecionável; Vec3 sem normalizar. Base para gradientes 3D e domínios de ruído. | Gradientes espaciais 3D e domínios de ruído em geometria. | Receitas #07; Blueprints #07 |
| **Normal** | `normal` | — | Normal (vector) | Normal de superfície já normalizada no espaço escolhido; reflete Bump/Normal Map aplicados antes na cadeia. | Combine com Dot e Fresnel para sombreamento customizado. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)