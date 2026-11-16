# UTI — Utilitários & Lógica

Sessão do catálogo técnico com **9 nodes**. Cor da categoria na interface: `#F472B6`.

Exemplo real da interface: ![exemplo](../assets/exemplos/uti.png)

| Node | Slug | Entradas | Saídas | Uso | Usado em |
|---|---|---|---|---|---|
| **Math** | `math` | A (scalar), B (scalar) | Value (scalar) | O canivete do grafo: encadeie vários para construir sinais complexos. | Receitas #01, #10, #11, #14, #15, #20, #21; Blueprints #01, #10, #11, #14, #15, #20, #21 |
| **Step** | `step` | In (scalar), Limite (scalar) | Value (scalar) | Converta picos de áudio em gatilhos limpos (Receita #21). | Receitas #18; Blueprints #18 |
| **Smoothstep** | `smoothstep` | In (scalar) | Value (scalar) | Versão orgânica do Step para transições sem serrilhado. | Receitas #09, #19, #20; Blueprints #09, #19, #20 |
| **Clamp** | `clamp` | In (scalar) | Value (scalar) | Sempre clamp saídas de Multiply antes de usar como máscara. | Receitas #16; Blueprints #16 |
| **Curve** | `curve` | Fac (scalar) | Value (scalar) | Controle artístico fino de falloffs e animações por vida. | — |
| **Object Info** | `object-info` | — | Posição (vector), Random (scalar) | Variação por objeto: alimente Random em Hue Shift ou offset de Noise. | Receitas #21; Blueprints #21 |
| **Instance Info** | `instance-info` | — | Idade (scalar), Random (scalar) | Variação individual em florestas e multidões espalhadas. | Receitas #25; Blueprints #25 |
| **Switch** | `switch` | A (color), B (color), Condição (scalar) | Saída (color) | Alterne materiais/estados em tempo real (UI interativa). | — |
| **Reroute** | `reroute` | In (scalar) | Out (scalar) | Aceita qualquer tipo de pino; use para evitar cruzamentos longos de cabos. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)