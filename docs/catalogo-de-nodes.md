# Catálogo Técnico — 73 Nodes (Vol. 1)

Referência dos 73 nodes mapeados nas 9 categorias funcionais da Prism.
A cor do pino indica o tipo de sinal: 🟠 escalar · 🔵 vetor · 🟣 cor · 🟢 geometria · 🟩 instâncias.

## [INP] Inputs & Fontes de Dados (6)

| Node | Entradas (esquerda) | Saídas (direita) | Uso prático |
|---|---|---|---|
| **Image Texture** | — | Color _(cor)_, Alpha _(escalar)_ | Padrão para mapas ORM: R = Occlusion, G = Roughness, B = Metalness (Receita #06). |
| **Audio Input** | — | Spectrum _(escalar)_, Level _(escalar)_, Beat _(escalar)_ | Base para reatividade sonora: calibre picos com Step/Smoothstep (Receita #21). |
| **Time** | — | Segundos _(escalar)_, Normalizado _(escalar)_ | Combine com Math [Sine] e Remap para pulsações e ondas contínuas. |
| **Pointer** | — | UV _(vetor)_, Down _(escalar)_ | Compare UV do cursor com UV do node para máscaras interativas (Receita #20). |
| **Data Input** | — | Valor _(escalar)_ | Ideal para dashboards e visualizações dirigidas por dados. |
| **Viewport** | — | Aspect _(vetor)_, Resolução _(vetor)_ | Corrija distorções de padrões em telas não quadradas (Receita #19). |

### Image Texture · `image-texture`

Carrega um arquivo de imagem (PNG/JPG/EXR) e expõe seus canais para o grafo.

### Audio Input · `audio-input`

Captura o áudio do ambiente em tempo real e o traduz em sinais numéricos.

### Time · `time`

Relógio do grafo: segundos corridos e ciclo normalizado 0.0–1.0.

### Pointer · `pointer`

Posição do cursor na viewport e estado de clique.

### Data Input · `data-input`

Lê colunas de dados externos (T, U) e as expõe como valores numéricos.

### Viewport · `viewport`

Dimensões da tela: proporção (aspect) e resolução em pixels.

## [GEN] Geradores Procedurais (10)

| Node | Entradas (esquerda) | Saídas (direita) | Uso prático |
|---|---|---|---|
| **Noise** | Coord _(vetor)_ | Value _(escalar)_, Color _(cor)_ | Some 10–20% de Noise a padrões geométricos para quebrar a regularidade. |
| **Voronoi** | Coord _(vetor)_ | Value _(escalar)_, Color _(cor)_, Distância _(escalar)_ | Combine com Height Blend para preencher cavidades primeiro (Receita #02). |
| **Brick** | Coord _(vetor)_ | Value _(escalar)_, ID _(escalar)_ | A saída ID gera variação individual por peça (Receita #05). |
| **Dots** | Coord _(vetor)_ | Value _(escalar)_ | Base para halftone, telas e micro-relevo de tecido. |
| **Checker** | Coord _(vetor)_ | Color _(cor)_ | Ferramenta de diagnóstico: qualquer distorção de UV fica imediatamente visível. |
| **Gradient** | Coord _(vetor)_ | Value _(escalar)_ | Máscaras de posição e fades de iluminação em NPR. |
| **Wave** | Coord _(vetor)_, Fase _(escalar)_ | Value _(escalar)_ | Time ➔ Mapping ➔ Wave para bandeiras e superfícies animadas (Receita #15). |
| **White Noise** | — | Value _(escalar)_ | Grão de filme, dithering e sementes aleatórias por instância. |
| **Truchet** | Coord _(vetor)_ | Value _(escalar)_ | Labirintos, circuitos e padrões decorativos sem emendas. |
| **Caustics** | Coord _(vetor)_, Escala _(escalar)_ | Value _(escalar)_, Color _(cor)_ | Superfícies de água e fundo de piscina; anime via Time no domínio. |

### Noise · `noise`

Ruído procedural fractal clássico, base de quase toda variação orgânica.

### Voronoi · `voronoi`

Células orgânicas com pontos de crescimento; ótimo para pedra, pele e solo.

### Brick · `brick`

Grade de tijolos/ladrilhos paramétrica com juntes e deslocamento de linhas.

### Dots · `dots`

Grade de pontos circulares com espaçamento e raio ajustáveis.

### Checker · `checker`

Xadrez binário para testar UVs e escala de textura.

### Gradient · `gradient`

Gradiente linear, radial ou diamante entre dois pontos do espaço.

### Wave · `wave`

Ondas senoidal, triangular e quadrada, animáveis por fase.

### White Noise · `white-noise`

Aleatoriedade pura por pixel, sem coerência espacial.

### Truchet · `truchet`

Mosaico de azulejos rotacionados aleatoriamente que formam caminhos contínuos.

### Caustics · `caustics`

Padrão de luz refratada em água, procedural e animável.

## [COL] Cor & Composição (12)

| Node | Entradas (esquerda) | Saídas (direita) | Uso prático |
|---|---|---|---|
| **Color Ramp** | Fac _(escalar)_ | Color _(cor)_ | O conversor universal: Noise/Voronoi ➔ Color Ramp é um par canônico. |
| **Blend** | Base _(cor)_, Blend _(cor)_, Mask _(escalar)_ | Color _(cor)_ | Camadas de sujeira e variação controladas por máscara (Receita #03). |
| **Mix** | A _(cor)_, B _(cor)_, Fac _(escalar)_ | Color _(cor)_ | Combine com Invert para trocar material exposto/base (Receita #01). |
| **Invert** | Entrada _(cor)_ | Color _(cor)_ | Em Edge Wear, inverta antes de Roughness para metal liso nas quinas. |
| **Levels** | Entrada _(cor)_ | Color _(cor)_ | Endureça máscaras: comprima o branco para manter áreas expostas em 1.0. |
| **Histogram Scan** | Value _(escalar)_ | Value _(escalar)_ | Transforme mapas de altura em máscaras precisas de desgaste. |
| **Hue Shift** | Cor _(cor)_, Deslocamento _(escalar)_ | Color _(cor)_ | Variação de cor por objeto via Object Info (Random). |
| **Posterize** | Entrada _(cor)_, Passos _(escalar)_ | Color _(cor)_ | Estilo cel-shading e dithering retro (Bloco NPR). |
| **Gradient Map** | Value _(escalar)_ | Color _(cor)_ | Paletas limitadas (duotone/tritone) para estilização NPR. |
| **Luminance** | Cor _(cor)_ | Value _(escalar)_ | Extraia altura de texturas coloridas para Bump/Deform. |
| **Curves** | Entrada _(cor)_ | Color _(cor)_ | Contraste fino de máscaras sem empilhar múltiplos Levels. |
| **Spectral Dispersion** | Ângulo _(escalar)_, Intensidade _(escalar)_ | Color _(cor)_ | Efeitos holográficos e de bolha de sabão (Receita #12). |

### Color Ramp · `color-ramp`

Converte um valor 0–1 em paleta de cores com paradas editáveis.

### Blend · `blend`

Mescla duas cores com modos (Multiply, Overlay, Screen, Add…).

### Mix · `mix`

Mistura linear A↔B controlada pelo fator Fac.

### Invert · `invert`

Inverte valores (1−x) ou gera a cor complementar.

### Levels · `levels`

Recomprime tons com pontos de preto e branco remapeáveis.

### Histogram Scan · `histogram-scan`

Isola uma faixa de tons como máscara com suavização de borda.

### Hue Shift · `hue-shift`

Rotaciona o matiz mantendo saturação e luminosidade.

### Posterize · `posterize`

Reduz o número de níveis de tom, criando degraus discretos.

### Gradient Map · `gradient-map`

Mapeia a luminância para uma paleta fixa de N cores.

### Luminance · `luminance`

Converte cor em escala de cinza ponderada (0.0–1.0).

### Curves · `curves`

Curva de resposta editável ponto a ponto sobre qualquer sinal.

### Spectral Dispersion · `spectral-dispersion`

Separa a luz por comprimento de onda, gerando iridescência.

## [FIL] Filtros & Convolução (9)

| Node | Entradas (esquerda) | Saídas (direita) | Uso prático |
|---|---|---|---|
| **Blur** | Entrada _(cor)_, Raio _(escalar)_ | Color _(cor)_ | Suavize máscaras serrilhadas antes de usar como Fac. |
| **Slope Blur** | In _(cor)_, Slope _(escalar)_ | Color _(cor)_ | Erosão e lascas: Brick + Noise em Slope (Receita #04). |
| **Directional Warp** | Entrada _(cor)_, Ângulo _(escalar)_, Intensidade _(escalar)_ | Color _(cor)_ | Fluxos direcionais: vento, cabelo, água (Receita #14). |
| **Edge Wear** | Height _(escalar)_ | Value _(escalar)_ | Desgaste metálico PBR (Receita #01); inverta para Roughness. |
| **Height AO** | Height _(escalar)_ | Value _(escalar)_ | Escureça cavidades e conecte também em Occlusion do Material Output (Receita #03). |
| **Bump** | Height _(escalar)_ | Normal _(vetor)_ | Conecte sempre a Height combinada para manter continuidade das normais. |
| **Normal Map** | Height _(escalar)_ | Normal _(vetor)_ | Prefira ao Bump quando o material for exportado para outros motores. |
| **Sobel Normal** | Height _(escalar)_ | Normal _(vetor)_ | Detalhe de micro-relevo em textos, tecidos e gravações. |
| **Sharpen** | Entrada _(cor)_, Intensidade _(escalar)_ | Color _(cor)_ | Recupere definição após Blurs intensos ou upscales. |

### Blur · `blur`

Suavização gaussiana/box com raio ajustável.

### Slope Blur · `slope-blur`

Desloca pixels ao longo do gradiente de um segundo ruído.

### Directional Warp · `directional-warp`

Distorce a imagem numa direção específica com intensidade animável.

### Edge Wear · `edge-wear`

Detecta quinas convexas do relevo e gera máscara de desgaste.

### Height AO · `height-ao`

Oclusão de ambiente derivada do mapa de altura, sem baking.

### Bump · `bump`

Converte altura em perturbação de normais (relevo falso, barato).

### Normal Map · `normal-map`

Gera mapa de normais tangent-space a partir de altura ou arquivo.

### Sobel Normal · `sobel-normal`

Convolução de Sobel para extrair normais nítidas de alta frequência.

### Sharpen · `sharpen`

Realça bordas e detalhes por máscara de nitidez (unsharp mask).

## [VEC] Vetores & UV (9)

| Node | Entradas (esquerda) | Saídas (direita) | Uso prático |
|---|---|---|---|
| **UV** | — | UV _(vetor)_ | Ponto de partida de quase todo padrão procedural (par canônico com Mapping). |
| **Mapping** | UV _(vetor)_ | UV _(vetor)_ | Defina escala/rotação ANTES de amostrar qualquer padrão (par canônico). |
| **Separate RGB** | Cor _(cor)_ | R _(escalar)_, G _(escalar)_, B _(escalar)_ | Desempacote mapas ORM canal a canal (Receita #06). |
| **Combine XYZ** | X _(escalar)_, Y _(escalar)_, Z _(escalar)_ | Vetor _(vetor)_ | Reconstrua vetores após processar cada eixo separadamente. |
| **Vector Math** | A _(vetor)_, B _(vetor)_ | Vetor _(vetor)_, Valor _(escalar)_ | Distance ➔ Smoothstep é o par canônico de proximidade (Receita #20). |
| **Remap** | In _(escalar)_ | Value _(escalar)_ | Normalize sinais: [-1..1 ➔ 0..1] antes de alimentar um Color Ramp. |
| **Fresnel** | Normal _(vetor)_, Visão _(vetor)_ | Value _(escalar)_ | Rim light, iridescência e contornos em NPR (Receita #11). |
| **Position** | — | Posição _(vetor)_ | Gradientes espaciais 3D e domínios de ruído em geometria. |
| **Normal** | — | Normal _(vetor)_ | Combine com Dot e Fresnel para sombreamento customizado. |

### UV · `uv`

Coordenadas de textura 0–1 do objeto ou da tela.

### Mapping · `mapping`

Aplica escala, rotação e translação às coordenadas.

### Separate RGB · `separate-rgb`

Decompõe uma cor nos canais R, G e B escalares.

### Combine XYZ · `combine-xyz`

Monta um vetor a partir de três escalares independentes.

### Vector Math · `vector-math`

Operações vetoriais: add, sub, dot, cross, normalize, distance.

### Remap · `remap`

Remapeia um intervalo de entrada para outro de saída (linear).

### Fresnel · `fresnel`

Intensidade do ângulo de visão: bordas acesas, frente apagada.

### Position · `position`

Posição do ponto no espaço do objeto ou do mundo.

### Normal · `normal`

Vetor normal da superfície no ponto avaliado.

## [UTI] Utilitários & Lógica (8)

| Node | Entradas (esquerda) | Saídas (direita) | Uso prático |
|---|---|---|---|
| **Math** | A _(escalar)_, B _(escalar)_ | Value _(escalar)_ | O canivete do grafo: encadeie vários para construir sinais complexos. |
| **Step** | In _(escalar)_, Limite _(escalar)_ | Value _(escalar)_ | Converta picos de áudio em gatilhos limpos (Receita #21). |
| **Smoothstep** | In _(escalar)_ | Value _(escalar)_ | Versão orgânica do Step para transições sem serrilhado. |
| **Clamp** | In _(escalar)_ | Value _(escalar)_ | Sempre clamp saídas de Multiply antes de usar como máscara. |
| **Curve** | Fac _(escalar)_ | Value _(escalar)_ | Controle artístico fino de falloffs e animações por vida. |
| **Object Info** | — | Posição _(vetor)_, Random _(escalar)_ | Variação por objeto: alimente Random em Hue Shift ou offset de Noise. |
| **Instance Info** | — | Idade _(escalar)_, Random _(escalar)_ | Variação individual em florestas e multidões espalhadas. |
| **Switch** | A _(cor)_, B _(cor)_, Condição _(escalar)_ | Saída _(cor)_ | Alterne materiais/estados em tempo real (UI interativa). |

### Math · `math`

Operações aritméticas e funções: add, multiply, sine, power, distance…

### Step · `step`

Degrau binário: 0 abaixo do limite, 1 acima.

### Smoothstep · `smoothstep`

Degrau suavizado com interpolação Hermite nas bordas.

### Clamp · `clamp`

Limita o sinal a um intervalo mínimo/máximo.

### Curve · `curve`

Curva de resposta editável (bézier) sobre um sinal 0–1.

### Object Info · `object-info`

Dados do objeto: posição, rotação, escala e random estável.

### Instance Info · `instance-info`

Dados de cada instância no Scatter: idade, transform e random.

### Switch · `switch`

Escolhe entre duas entradas com base em uma condição.

## [GEO] Geometria Procedural (9)

| Node | Entradas (esquerda) | Saídas (direita) | Uso prático |
|---|---|---|---|
| **Primitive** | — | Geometria _(geometria)_ | Início de todo pipeline [GEO]; plano + Noise = terreno (Receita #23). |
| **Deform** | Geometria _(geometria)_, Height _(escalar)_ | Geometria _(geometria)_ | Terrenos e ondulações: height procedural direto na malha. |
| **Scatter** | Superfície _(geometria)_, Instância _(geometria)_, Densidade _(escalar)_ | Instâncias _(instância)_ | Par canônico Primitive ➔ Scatter; use Noise na densidade (Receita #24). |
| **Attractor** | Geometria _(geometria)_, Ponto _(vetor)_, Força _(escalar)_ | Geometria _(geometria)_ | Interação do cursor com a malha (Bloco Interação). |
| **Vortex** | Geometria _(geometria)_, Eixo _(vetor)_, Força _(escalar)_ | Geometria _(geometria)_ | Redemoinhos e espirais em VFX e geometria. |
| **Mirror** | Geometria _(geometria)_ | Geometria _(geometria)_ | Simetria rápida para personagens e props. |
| **Subdivide** | Geometria _(geometria)_, Nível _(escalar)_ | Geometria _(geometria)_ | Subdivida ANTES de Deform/Displace para evitar facetas. |
| **Array** | Geometria _(geometria)_, Contagem _(escalar)_ | Instâncias _(instância)_ | Colunas, grades e coroas de objetos. |
| **Displace** | Geometria _(geometria)_, Height _(escalar)_, Escala _(escalar)_ | Geometria _(geometria)_ | Relevo real (não falso como Bump); combine com Subdivide. |

### Primitive · `primitive`

Malhas base paramétricas: plano, cubo, esfera, cilindro, torus.

### Deform · `deform`

Deforma a geometria usando um mapa de altura ou campo vetorial.

### Scatter · `scatter`

Espalha instâncias sobre uma superfície com densidade controlável.

### Attractor · `attractor`

Puxa ou empurra vértices e partículas em direção a um ponto.

### Vortex · `vortex`

Gira vértices/partículas ao redor de um eixo com falloff.

### Mirror · `mirror`

Duplica e espelha a geometria em um eixo.

### Subdivide · `subdivide`

Refina a malha dividindo faces, habilitando deformações suaves.

### Array · `array`

Replica a geometria em grade linear ou radial.

### Displace · `displace`

Desloca vértices ao longo da normal por um mapa de altura.

## [VFX] Partículas & VFX (7)

| Node | Entradas (esquerda) | Saídas (direita) | Uso prático |
|---|---|---|---|
| **Emitter** | — | Partículas _(instância)_ | Início de todo sistema VFX (Receitas #27–30). |
| **Particle** | Partículas _(instância)_ | Idade _(escalar)_, Posição _(vetor)_, Velocidade _(vetor)_ | Age 0–1 sincroniza Size/Color over Life e Fade (par canônico). |
| **Turbulence** | Posição _(vetor)_, Escala _(escalar)_ | Posição _(vetor)_ | Brasas e poeira errática (Receita #30). |
| **Size over Life** | Idade _(escalar)_ | Tamanho _(escalar)_ | Nascimento pequeno ➔ pico ➔ fade; use Remap para um mínimo visível. |
| **Color over Life** | Idade _(escalar)_ | Cor _(cor)_ | Fogo: branco ➔ laranja ➔ vermelho ➔ fumaça. |
| **Fade** | Idade _(escalar)_ | Opacidade _(escalar)_ | Evite pops: sempre fade-out suave antes da morte da partícula. |
| **Sprite** | Cor _(cor)_, Opacidade _(escalar)_ | Visual _(instância)_ | Fumaça, brasas e detritos com textura suave. |

### Emitter · `emitter`

Fonte de partículas: taxa, vida útil, velocidade inicial e origem.

### Particle · `particle`

Estado de cada partícula: idade 0–1, posição e velocidade.

### Turbulence · `turbulence`

Campo de ruído que agita posições de partículas e vértices.

### Size over Life · `size-over-life`

Curva de tamanho ao longo da vida da partícula.

### Color over Life · `color-over-life`

Gradiente de cor ao longo da vida da partícula.

### Fade · `fade`

Opacidade da partícula com curvas de entrada e saída.

### Sprite · `sprite`

Billboard texturizado renderizado por partícula.

## [OUT] Saídas & Render (3)

| Node | Entradas (esquerda) | Saídas (direita) | Uso prático |
|---|---|---|---|
| **Material Output** | Base Color _(cor)_, Roughness _(escalar)_, Metalness _(escalar)_, Normal _(vetor)_, Occlusion _(escalar)_, Emissive _(cor)_ | — | Todo caminho de material termina aqui (usado em 19 receitas). |
| **Geometry Output** | Geometria _(geometria)_ | — | Fim do fluxo [GEO]; sem saídas à direita (node terminal). |
| **VFX Output** | Posição _(vetor)_, Tamanho _(escalar)_, Opacidade _(escalar)_, Sprite _(instância)_ | — | Fim do fluxo VFX; conecte Turbulence em Position para movimento. |

### Material Output · `material-output`

Terminal do pipeline de material: define o shader final da superfície.

### Geometry Output · `geometry-output`

Terminal do pipeline de geometria: malha final para render.

### VFX Output · `vfx-output`

Terminal do pipeline de partículas: posição, tamanho, opacity e sprite.
