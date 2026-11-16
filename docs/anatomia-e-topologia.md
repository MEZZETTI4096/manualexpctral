# Anatomia do Node, Coerção de Portas & Mapa de Caminhos (Vol. 2)

## Anatomia — as 4 zonas do node

### 1. Cabeçalho & Tag de Categoria

`IDENTIFICAÇÃO` — Exibe o nome funcional do operador à esquerda e o código de 3 letras da categoria à direita ([INP], [GEN], [COL], [FIL], [VEC], [UTI], [GEO], [VFX], [OUT]). A barra superior colorida indica o domínio.

> **Dica:** Use a tag [CAT] para localizar rapidamente qualquer node no menu de busca ou no Volume 1.

### 2. Display Interno & Preview em Tempo Real

`TELEMETRIA VISUAL` — Mostra uma miniatura em tempo real da textura/gradiente gerado, o wireframe de vértices (em [GEO]) ou o valor escalar/vetorial atual avaliado pelo node.

> **Dica:** Permite diagnosticar máscaras ou valores estourados sem precisar conectar cada node na saída final.

### 3. Portas de Entrada (Inputs — Esquerda)

`RECEPTORES DE SINAL` — Recebem dados vindos de nodes anteriores. A cor do círculo indica o tipo esperado: Laranja (Escalar), Ciano (Vetor), Roxo (Cor), Turquesa (Geometria) e Menta (Instâncias).

> **Dica:** Quando desconectados, os inputs assumem o valor padrão configurado nos parâmetros internos do node.

### 4. Portas de Saída (Outputs — Direita)

`EMISSORES DE SINAL` — Exportam os resultados calculados pelo node. Uma única porta de saída pode se ramificar (Fan-Out) para alimentar múltiplos nodes simultaneamente.

> **Dica:** Nodes terminais ([OUT] Material Output, Geometry Output e VFX Output) não possuem saídas à direita.

## Pares Canônicos de Encadeamento

| De | Para | Por quê |
|---|---|---|
| UV / Mapping (UV 🔵) | Noise / Image Texture (Coord/UV 🔵) | Define escala, rotação e deslocamento espacial antes de amostrar qualquer padrão ou textura. |
| Noise / Voronoi (Value 🟠) | Color Ramp (Fac 🟠) | Converte mapas procedurais em escala de cinza para paletas cromáticas complexas. |
| Brick / Noise (Value 🟠) | Bump / Height AO / Edge Wear (Height 🟠) | Transforma mapas de altura em normais 3D, sombras de cavidade e máscaras de desgaste. |
| Edge Wear / Histogram Scan (Value 🟠) | Mix / Blend (Fac / Mask 🟠) | Atua como máscara de controle para mesclar dois materiais ou camadas de cor. |
| Time (Value 🟠) | Math [Sine/Multiply] ➔ Remap (In 🟠) | Gera ciclos contínuos normalizados (0.0 a 1.0) para pulsações luminosas e ondas. |
| Audio Input (Spectrum/Beat 🟠) | Step / Smoothstep (In 🟠) | Calibra picos sonoros em gatilhos limpos para deformação geométrica ou emissão. |
| Primitive / Deform (Geometria 🟢) | Scatter (Superfície/Instância 🟢) | Encadeamento base para criar terrenos e espalhar milhares de instâncias sobre eles. |
| Particle (Age 0-1 🟠) | Size / Color over Life & Fade (Age 0-1 🟠) | Sincroniza escala, evolução de cor e transparência ao longo da vida de cada partícula. |

## Regras de Coerção entre Portas

| Conexão | Status | Comportamento |
|---|---|---|
| escalar → escalar | COMPATÍVEL DIRETO (1:1) | Transferência numérica direta sem perda ou conversão. |
| escalar → cor | COERÇÃO AUTOMÁTICA (AUTO-CAST) | O valor escalar X é replicado nos canais RGB como tom de cinza (X, X, X, 1.0). |
| escalar → vetor | COERÇÃO AUTOMÁTICA (AUTO-CAST) | O valor escalar X preenche todos os eixos do vetor (X, X, X). |
| vetor → vetor | COMPATÍVEL DIRETO (1:1) | Transferência vetorial direta (Vec2 ou Vec3). |
| vetor → escalar | EXTRAÇÃO DE CANAL (X) | Apenas o primeiro componente (eixo X / U) do vetor é lido pela entrada escalar. |
| vetor → cor | MAPEAMENTO ESPACIAL (XYZ → RGB) | Os eixos X, Y e Z são interpretados diretamente como canais Vermelho, Verde e Azul. |
| cor → cor | COMPATÍVEL DIRETO (1:1) | Transferência cromática completa RGBA. |
| cor → escalar | CONVERSÃO POR LUMINÂNCIA | O motor calcula automaticamente a luminância ponderada em escala de cinza (0.0 a 1.0). |
| cor → vetor | CONVERSÃO (RGB → XYZ) | Os canais R, G e B alimentam os componentes X, Y e Z do vetor. |
| geometria → geometria | COMPATÍVEL DIRETO (MESH) | Fluxo de malha poligonal válido dentro do pipeline [GEO]. |
| instância → instância | COMPATÍVEL DIRETO (INSTÂNCIAS) | Coleção de instâncias conectada diretamente ao Geometry Output. |

Qualquer combinação não listada (ex.: geometria → escalar) é **incompatível sem conversor**.