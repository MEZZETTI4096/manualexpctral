# manualexpctral

manual de nodes e suas interações

## 📖 Manual Prism (online)

O manual unificado está publicado no GitHub Pages:

**https://mezzetti4096.github.io/manualexpctral/**

Um único arquivo navegável com 6 seções: Visão Geral (com guia rápido "Como ler as fichas": cores de pinos, conversões e tags) · Catálogo Técnico (90 nodes em 9 sessões, 1 por categoria) · Anatomia & Coerção · Mapa de Caminhos · 30 Receitas (utilidade & calibração) · 30 Fluxos (frames com as portas reais de cada node).

Atalhos: `Ctrl+K` ou `/` abre a busca global (150+ entradas indexadas: 90 nodes + 60 receitas/blueprints) · `Exportar PDF (tudo)` gera o manual completo em PDF.

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

- **Vol. 1 — Catálogo de Nodes:** 90 nodes em 9 categorias ([INP], [GEN], [COL], [FIL], [VEC], [UTI], [GEO], [VFX], [OUT]), com entradas/saídas tipadas pelas 4 cores reais da UI (🟠 escalar `#FF9F1C` · 🔵 vetor `#06B6D4` · 🟣 cor `#A855F7` · 🟢 geometria/instâncias `#2DD4BF`).
- **Vol. 2 — Arquitetura & Mapa de Caminhos:** anatomia do node, regras de coerção entre portas, pares canônicos de encadeamento e 30 receitas práticas em 6 blocos temáticos.
- **Vol. 3 — Fluxos (Blueprints):** os mesmos 30 padrões apresentados como frames com as portas reais de cada node (portas conectadas destacadas), conexão label a label entre etapas e parâmetros internos de calibração, com filtros por bloco e complexidade.
