# UTI — Utilitários & Lógica

Sessão do catálogo técnico com **9 nodes**. Cor da categoria na interface: `#F472B6`.

Exemplo real da interface: ![exemplo](../assets/exemplos/uti.png)

| Node | Slug | Entradas | Saídas | Especificações Técnicas | Uso | Usado em |
|---|---|---|---|---|---|---|
| **Math** | `math` | A (scalar), B (scalar) | Value (scalar) | Add/sub/mul/div/sine/power/… com clamp opcional; custo mínimo por operação. Encadeie sem medo, mas nomeie cada node para legibilidade. | O canivete do grafo: encadeie vários para construir sinais complexos. | Receitas #01, #10, #11, #14, #15, #20, #21; Blueprints #01, #10, #11, #14, #15, #20, #21 |
| **Step** | `step` | In (scalar), Limite (scalar) | Value (scalar) | Edge 0–1 (padrão 0.5), saída binária 0/1 sem anti-aliasing — siga com Smoothstep ou Blur para borda suave. | Converta picos de áudio em gatilhos limpos (Receita #21). | Receitas #18; Blueprints #18 |
| **Smoothstep** | `smoothstep` | In (scalar) | Value (scalar) | Interpolação Hermite entre 0 e 1, edge padrão 0.5. Custo mínimo; substitui o Step em quase todo caso visual. | Versão orgânica do Step para transições sem serrilhado. | Receitas #09, #19, #20; Blueprints #09, #19, #20 |
| **Clamp** | `clamp` | In (scalar) | Value (scalar) | Limita a Min/Max ajustáveis (padrão 0–1) com custo zero. Hábito obrigatório após Multiply/Divide antes de máscaras. | Sempre clamp saídas de Multiply antes de usar como máscara. | Receitas #16; Blueprints #16 |
| **Curve** | `curve` | Fac (scalar) | Value (scalar) | Bézier 0–1 com pontos livres e avaliação por lookup; controle artístico de falloffs, mais expressivo que Levels. | Controle artístico fino de falloffs e animações por vida. | — |
| **Object Info** | `object-info` | — | Position (vector), Scale (vector), ID (scalar) | Position e Scale (vetores) + ID estável por objeto (hash do id). Atualiza por objeto, não por pixel. | Variação por objeto: alimente ID em Hue Shift ou offset de Noise. | Receitas #21; Blueprints #21 |
| **Instance Info** | `instance-info` | — | Id (scalar), Aleatório (scalar), Escala (scalar) | Id, Aleatório e Escala por instância do Scatter (todos escalares); só existe dentro do domínio de instâncias. | Variação individual em florestas e multidões espalhadas. | Receitas #25; Blueprints #25 |
| **Switch** | `switch` | A (color), B (color), Condição (scalar) | Saída (color) | Condição ≥ 0.5 escolhe A ou B; ambos os lados são avaliados (sem branch real na GPU) — custo do caminho mais caro. | Alterne materiais/estados em tempo real (UI interativa). | — |
| **Reroute** | `reroute` | In (scalar) | Out (scalar) | Pass-through puro: sem custo e sem conversão, preserva o tipo do pino conectado. Use para organizar cabos longos. | Aceita qualquer tipo de pino; use para evitar cruzamentos longos de cabos. | — |

---

[← Voltar ao manual](../../index.html) · [Catálogo completo](catalogo.md)