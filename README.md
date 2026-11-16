# manualexpctral

manual de nodes e suas interações

## 📖 Manual Prism (online)

O manual unificado está publicado no GitHub Pages:

**https://mezzetti4096.github.io/manualexpctral/**

Um único arquivo navegável com 7 seções: Visão Geral (com guia rápido de cores de pinos e tags) · Catálogo Parte 1 (50 nodes) · Catálogo Parte 2 (40 nodes) · Anatomia & Coerção · Mapa de Caminhos · 30 Receitas · 30 Blueprints Aprimorados.

Atalhos: `Ctrl+K` ou `/` abre a busca global (140 itens indexados) · `Exportar PDF (tudo)` gera o manual completo em PDF.

## 📂 Estrutura do repositório

| Caminho | Conteúdo |
|---|---|
| `index.html` | **Manual Prism unificado** (Vols. 1–3) — versão publicada no Pages |
| `manual_prism_unificado.html` | Mesmo arquivo com nome explícito |
| `assets/exemplos/` | Screenshots reais da interface Prism (1 por categoria: inp, gen, col, fil, vec, uti, geo, vfx) |
| `docs/README.md` | Índice da documentação por tópicos |
| `docs/nodes/` | Catálogo em 9 sessões — 1 arquivo por categoria (`inp.md`, `gen.md`, …, `out.md`) + índice (`catalogo.md`) |
| `docs/receitas/` | Vol. 2 em texto: 30 receitas com cadeias, utilidade e calibração |
| `docs/blueprints/` | Vol. 3 em texto: 30 blueprints aprimorados com parâmetros recomendados |
| `docs/arquitetura/` | Vol. 2 em texto: zonas do node, regras de coerção e pares canônicos |
| `volumes/` | Volumes originais (2 e 3) como páginas standalone de referência |

## 🗂 Os 3 volumes

- **Vol. 1 — Catálogo de Nodes:** 90 nodes em 9 categorias ([INP], [GEN], [COL], [FIL], [VEC], [UTI], [GEO], [VFX], [OUT]), com entradas/saídas tipadas por cor (🟠 escalar · 🔵 vetor · 🟣 cor · 🟢 geometria · 🟩 instâncias).
- **Vol. 2 — Arquitetura & Mapa de Caminhos:** anatomia do node, regras de coerção entre portas, pares canônicos de encadeamento e 30 receitas práticas em 6 blocos temáticos.
- **Vol. 3 — Catálogo Aprimorado:** os mesmos 30 padrões com resumo, topologia detalhada e parâmetros internos de calibração, com filtros por bloco e complexidade.
