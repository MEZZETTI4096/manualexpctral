# Receitas & Combinações Úteis — 30 Fluxos (Vol. 2)

Cadeias completas de encadeamento organizadas em 6 domínios técnicos, com mapeamento exato de pinos e dicas de calibração.

## 1. Materiais PBR & Superfícies (01–07)

### #01 — Desgaste Metálico em Quinas (Edge Wear PBR)

`Materiais PBR & Superfícies` · **Intermediário** · [GEN] [FIL] [COL] [OUT]

**Cadeia de encadeamento:**

1. **Brick + Noise** — OUT: Value _(escalar)_
2. **Math [Add]** — IN: A / B · OUT: Value _(escalar)_
3. **Edge Wear** — IN: Height · OUT: Value _(escalar)_
4. **Mix + Invert** — IN: Fac / In · OUT: Color _(cor)_
5. **Material Output** — IN: Base Color & Roughness _(cor)_

**Utilidade técnica:** Detecta automaticamente as quinas convexas do relevo combinado para revelar metal brilhante e polido nas bordas expostas, mantendo a pintura fosca nas superfícies planas.

**Calibração & ajuste fino:** Use Invert na saída de Edge Wear antes de ligar em Roughness para que as quinas desgastadas fiquem mais lisas (menor rugosidade) que a tinta.

### #02 — Acúmulo Realista de Neve, Areia ou Musgo (Height Blend)

`Materiais PBR & Superfícies` · **Intermediário** · [GEN] [COL] [VEC] [OUT]

**Cadeia de encadeamento:**

1. **Voronoi (Pedra) + Noise (Neve)** — OUT: Value _(escalar)_
2. **Height Blend** — IN: Base / Blend / Height · OUT: Out & Height _(cor)_
3. **Bump** — IN: Height · OUT: Normal _(vetor)_
4. **Material Output** — IN: Base Color & Normal _(cor)_

**Utilidade técnica:** Diferente de uma mistura linear comum, o Height Blend compara a altura física de dois materiais para preencher primeiro frestas e cavidades profundas antes de cobrir o topo das pedras.

**Calibração & ajuste fino:** Anime ou ajuste o deslocamento de altura do material B para controlar o volume acumulado de neve ou areia.

### #03 — Sombreamento de Cavidades & Sujeira (Micro-AO)

`Materiais PBR & Superfícies` · **Essencial** · [GEN] [FIL] [COL] [OUT]

**Cadeia de encadeamento:**

1. **Brick** — OUT: Value _(escalar)_
2. **Height AO** — IN: Height · OUT: Value _(escalar)_
3. **Levels** — IN: In · OUT: Color _(cor)_
4. **Blend [Multiply]** — IN: Blend · OUT: Color _(cor)_
5. **Material Output** — IN: Base Color & Occlusion _(escalar)_

**Utilidade técnica:** Calcula oclusão de ambiente procedural diretamente a partir do mapa de altura, escurecendo rejuntes e cavidades sem depender de texturas pré-assadas.

**Calibração & ajuste fino:** Conecte o mesmo sinal de Height AO tanto em Blend [Multiply] na cor base quanto no pino Occlusion do Material Output.

### #04 — Alvenaria Orgânica com Tijolos Quebrados (Slope Blur)

`Materiais PBR & Superfícies` · **Intermediário** · [GEN] [FIL] [VEC] [OUT]

**Cadeia de encadeamento:**

1. **Brick (In) + Noise (Slope)** — OUT: Value _(escalar)_
2. **Slope Blur** — IN: In / Slope · OUT: Color _(cor)_
3. **Bump** — IN: Height · OUT: Normal _(vetor)_
4. **Material Output** — IN: Normal _(vetor)_

**Utilidade técnica:** Quebra a perfeição geométrica das linhas retas do node Brick empurrando seus contornos ao longo das inclinações de um ruído, criando tijolos lascados e pedras naturais.

**Calibração & ajuste fino:** Ajuste a escala do Noise conectado em Slope para alternar entre lascas finas de alta frequência ou deformações amplas.

### #05 — Variação Individual por Peça / Ladrilho (Brick ID)

`Materiais PBR & Superfícies` · **Essencial** · [GEN] [COL] [OUT]

**Cadeia de encadeamento:**

1. **Brick** — OUT: ID _(escalar)_
2. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
3. **Blend [Overlay]** — IN: Blend · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade técnica:** Aproveita o identificador numérico único (ID) gerado por cada tijolo individual para atribuir variações sutis de tonalidade e queima entre peças vizinhas.

**Calibração & ajuste fino:** Mantenha as paradas do Color Ramp próximas em luminância e use baixa opacidade (Mask) no Blend para um realismo sutil.

### #06 — Desempacotamento de Mapas ORM (Channel-Packed PBR)

`Materiais PBR & Superfícies` · **Essencial** · [INP] [VEC] [OUT]

**Cadeia de encadeamento:**

1. **Image Texture (ORM)** — OUT: Color _(cor)_
2. **Separate RGB** — IN: Color · OUT: R, G, B _(escalar)_
3. **Material Output** — IN: Occlusion (R), Roughness (G), Metallic (B) _(escalar)_

**Utilidade técnica:** Otimiza memória de vídeo lendo um único arquivo RGB onde cada canal carrega uma propriedade física distinta do shader PBR.

**Calibração & ajuste fino:** Padrão da indústria: R = Ambient Occlusion, G = Roughness, B = Metalness.

### #07 — Textura Triplanar / Sem Costuras UV (World-Space)

`Materiais PBR & Superfícies` · **Essencial** · [VEC] [GEN] [COL] [OUT]

**Cadeia de encadeamento:**

1. **Position** — OUT: Position _(vetor)_
2. **Noise / Voronoi** — IN: Coord · OUT: Value _(escalar)_
3. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade técnica:** Avalia geradores procedurais no espaço 3D contínuo (Position) em vez de coordenadas UV 2D, eliminando emendas visíveis em terrenos e malhas complexas.

**Calibração & ajuste fino:** Multiplique Position por um Value antes de entrar em Coord para controlar a densidade global do padrão no mundo.

## 2. Estilização & Retro NPR (08–12)

### #08 — Cel-Shading / Faixas Tonais Retro 64-Bit

`Estilização & Retro NPR` · **Essencial** · [INP] [COL] [OUT]

**Cadeia de encadeamento:**

1. **Image Texture** — OUT: Color _(cor)_
2. **Posterize** — IN: In · OUT: Color _(cor)_
3. **Gradient Map 4** — IN: In · OUT: Out _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade técnica:** Quantiza gradientes contínuos em degraus tonais rígidos e remapeia os 4 níveis resultantes para uma paleta fechada estilo pixel art ou console retro.

**Calibração & ajuste fino:** Configure Posterize para 4 níveis para alinhar perfeitamente cada faixa tonal com as 4 paradas do Gradient Map 4.

### #09 — Contorno Mágico / Rim Light (Fresnel + Smoothstep)

`Estilização & Retro NPR` · **Essencial** · [VEC] [UTI] [COL] [OUT]

**Cadeia de encadeamento:**

1. **Fresnel** — OUT: Value _(escalar)_
2. **Smoothstep** — IN: In · OUT: Value _(escalar)_
3. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
4. **Material Output** — IN: Emissive _(cor)_

**Utilidade técnica:** Isola apenas os ângulos rasantes da silhueta do objeto em relação à câmera para criar auras holográficas, escudos de energia ou contornos estilizados.

**Calibração & ajuste fino:** Aproxime Edge0 e Edge1 no Smoothstep (ex: 0.65 e 0.85) para criar um contorno fino e intenso na borda do modelo.

### #10 — Retícula de Quadrinhos / Halftone Dinâmico

`Estilização & Retro NPR` · **Avançado** · [VEC] [GEN] [COL] [UTI] [OUT]

**Cadeia de encadeamento:**

1. **Mapping ➔ Dots (Value) + Luminance (Value)** — OUT: Value _(escalar)_
2. **Math [Greater Than]** — IN: A / B · OUT: Value _(escalar)_
3. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade técnica:** Compara a grade procedural de pontos (Dots) com o brilho percebido (Luminance) de uma imagem para gerar retículas estilizadas estilo impressão em quadrinhos.

**Calibração & ajuste fino:** Rotacione o Mapping em 45 graus para obter o ângulo clássico de retícula tipográfica.

### #11 — Iridescência Óptica / Bolha de Sabão e Óleo

`Estilização & Retro NPR` · **Intermediário** · [VEC] [GEN] [UTI] [COL] [OUT]

**Cadeia de encadeamento:**

1. **Fresnel (Value) + Noise (Value)** — OUT: Value _(escalar)_
2. **Math [Add]** — IN: A / B · OUT: Value _(escalar)_
3. **Spectral Dispersion** — IN: Thickness · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color & Clearcoat _(cor)_

**Utilidade técnica:** Simula interferência de filme fino variando a espessura óptica conforme o ângulo da câmera e um ruído orgânico, produzindo reflexos arco-íris dinâmicos.

**Calibração & ajuste fino:** Combine com Roughness baixo (0.05) e Clearcoat em 1.0 para simular vidro dicroico ou películas líquidas.

### #12 — Conversão de Altura para Normal Map RGB (Sobel)

`Estilização & Retro NPR` · **Intermediário** · [GEN] [FIL] [VEC] [OUT]

**Cadeia de encadeamento:**

1. **Voronoi** — OUT: Value _(escalar)_
2. **Blur** — IN: In · OUT: Color _(cor)_
3. **Sobel Normal** — IN: Height · OUT: Normal Map _(cor)_
4. **Normal Map** — IN: Color · OUT: Normal _(vetor)_
5. **Material Output** — IN: Normal _(vetor)_

**Utilidade técnica:** Gera uma textura RGB de Normal Map via operador Sobel antes da decodificação, permitindo mesclar mapas normais usando nodes da categoria [COL].

**Calibração & ajuste fino:** Passar pelo Blur antes do Sobel Normal suaviza degraus de quantização e cria chanfros redondos nas células.

## 3. UV, Distorção & Animação (13–17)

### #13 — Superfície de Água Ondulante / Distorção de Calor

`UV, Distorção & Animação` · **Intermediário** · [UTI] [VEC] [GEN] [INP]

**Cadeia de encadeamento:**

1. **Time ➔ Mapping** — OUT: UV _(vetor)_
2. **Noise** — IN: Coord · OUT: Value _(escalar)_
3. **Directional Warp** — IN: Map (+ UV) · OUT: Color _(vetor)_
4. **Image Texture** — IN: UV · OUT: Color _(cor)_

**Utilidade técnica:** Desloca continuamente um campo de ruído ao longo do tempo para deformar as coordenadas UV de qualquer textura, simulando refração líquida ou ondas de calor.

**Calibração & ajuste fino:** Mantenha a intensidade do Directional Warp baixa (0.02 a 0.08) para evitar esticamento excessivo dos pixels.

### #14 — Correção de Proporção de Tela (Aspect Ratio Fix)

`UV, Distorção & Animação` · **Essencial** · [VEC] [INP] [UTI] [GEN]

**Cadeia de encadeamento:**

1. **UV (UV) + Viewport (Aspect)** — OUT: Vector/Scalar _(vetor)_
2. **Math [Multiply]** — IN: A / B · OUT: Value _(escalar)_
3. **Dots / Checker** — IN: Coord · OUT: Value _(escalar)_

**Utilidade técnica:** Compensa a razão de aspecto da janela atual sobre as coordenadas UV para impedir que círculos, pontos e grades fiquem ovalados em telas widescreen ou mobile.

**Calibração & ajuste fino:** Essencial em shaders 2D de tela cheia e interfaces interativas.

### #15 — Pulso Rítmico Normalizado (Senoide Calibrada)

`UV, Distorção & Animação` · **Essencial** · [UTI] [OUT]

**Cadeia de encadeamento:**

1. **Time** — OUT: Value _(escalar)_
2. **Math [Sine]** — IN: A · OUT: Value _(escalar)_
3. **Remap [-1..1 → 0..1]** — IN: In · OUT: Value _(escalar)_
4. **Material Output** — IN: Emissive _(cor)_

**Utilidade técnica:** Converte a saída negativa/positiva de uma onda senoidal (-1.0 a +1.0) para a faixa segura de [0.0, 1.0], criando pulsações luminosas suaves e cíclicas.

**Calibração & ajuste fino:** Multiplique Time antes do Sine para acelerar ou desacelerar a frequência da pulsação.

### #16 — Erosão / Dissolve Orgânico com Histogram Scan

`UV, Distorção & Animação` · **Intermediário** · [GEN] [FIL] [UTI] [OUT]

**Cadeia de encadeamento:**

1. **Noise** — OUT: Value _(escalar)_
2. **Histogram Scan** — IN: In · OUT: Value _(escalar)_
3. **Clamp** — IN: In · OUT: Value _(escalar)_
4. **Material Output** — IN: Opacity _(escalar)_

**Utilidade técnica:** Varre progressivamente a faixa tonal de um ruído para fazer objetos surgirem ou se dissolverem organicamente (efeito teletransporte ou queima).

**Calibração & ajuste fino:** Use o histograma invertido em um Smoothstep estreito para extrair uma borda brilhante incandescente exatamente na linha de queima.

### #17 — Madeira Procedural com Veios Orgânicos

`UV, Distorção & Animação` · **Intermediário** · [VEC] [GEN] [COL] [OUT]

**Cadeia de encadeamento:**

1. **UV ➔ Directional Warp (+ Noise)** — OUT: Color _(vetor)_
2. **Wave** — IN: Coord · OUT: Value _(escalar)_
3. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade técnica:** Deforma o espaço UV com ruído antes de gerar ondas periódicas, transformando listras retas em anéis concêntricos e veios naturais de madeira.

**Calibração & ajuste fino:** Estique a escala Y no Mapping antes do Wave para alongar os veios no sentido das tábuas.

## 4. Áudio, Cursor & Dados (18–22)

### #18 — Visualizador de Espectro de Áudio (Spectrum Bars)

`Áudio, Cursor & Dados` · **Intermediário** · [VEC] [INP] [UTI] [COL] [OUT]

**Cadeia de encadeamento:**

1. **UV** — OUT: UV _(vetor)_
2. **Audio Input** — OUT: Spectrum _(escalar)_
3. **Step** — IN: In · OUT: Value _(escalar)_
4. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
5. **Material Output** — IN: Emissive _(cor)_

**Utilidade técnica:** Amostra a magnitude de cada banda de frequência ao longo do eixo horizontal da tela (UV.x), desenhando barras luminosas reativas em tempo real.

**Calibração & ajuste fino:** Compare UV.y com Spectrum usando Math [Less Than] para desenhar barras verticais sólidas de baixo para cima.

### #19 — Batida Musical Pulsando Geometria e Luz (Beat Trigger)

`Áudio, Cursor & Dados` · **Essencial** · [INP] [UTI] [GEO] [OUT]

**Cadeia de encadeamento:**

1. **Audio Input** — OUT: Beat & Bass _(escalar)_
2. **Smoothstep** — IN: In · OUT: Value _(escalar)_
3. **Deform (Height) + Material Output (Emissive)** — IN: Height / Emissive _(escalar)_

**Utilidade técnica:** Sincroniza deformações físicas da malha 3D e picos de brilho emissivo exatamente com os graves e batidas detectadas na música.

**Calibração & ajuste fino:** Use Smoothstep para amaciar a queda do pulso Beat e evitar trepidações bruscas.

### #20 — Pincel / Halo Interativo com o Cursor (Pointer Tracking)

`Áudio, Cursor & Dados` · **Avançado** · [VEC] [INP] [UTI] [OUT]

**Cadeia de encadeamento:**

1. **UV (UV) vs Pointer (UV)** — OUT: Vector _(vetor)_
2. **Math [Distance] ➔ Smoothstep** — IN: A / B · OUT: Value _(escalar)_
3. **Math [Multiply] (+ Pointer Down)** — IN: A / B · OUT: Value _(escalar)_
4. **Material Output** — IN: Emissive _(cor)_

**Utilidade técnica:** Calcula a distância entre cada pixel e o cursor do mouse/toque, acendendo um halo interativo apenas enquanto o botão está pressionado (Down = 1.0).

**Calibração & ajuste fino:** Conecte Pointer (Position) em Directional Warp (Map) para criar ondas que se deslocam ao arrastar o dedo.

### #21 — Variação Automática por Objeto na Cena (Object ID)

`Áudio, Cursor & Dados` · **Essencial** · [INP] [UTI] [COL] [OUT]

**Cadeia de encadeamento:**

1. **Object Info** — OUT: ID _(escalar)_
2. **Math [Multiply]** — IN: A · OUT: Value _(escalar)_
3. **Hue Shift** — IN: In · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade técnica:** Usa o identificador numérico único de cada objeto na cena para rotacionar sua matiz automaticamente, evitando repetição visual ao reutilizar materiais.

**Calibração & ajuste fino:** Multiplique ID por uma fração irracional (ex: 0.37) para espalhar bem as cores entre objetos consecutivos.

### #22 — Visualização de Gráficos Guiada por Planilha (Data)

`Áudio, Cursor & Dados` · **Intermediário** · [INP] [UTI] [GEO] [COL]

**Cadeia de encadeamento:**

1. **Data (T / Coluna U)** — OUT: Value _(escalar)_
2. **Remap** — IN: In · OUT: Value _(escalar)_
3. **Deform (Height) + Color Ramp (Fac)** — IN: Height / Fac _(escalar)_

**Utilidade técnica:** Conecta tabelas externas diretamente à elevação e cor de malhas 3D, permitindo criar gráficos dinâmicos e animações orientadas por dados.

**Calibração & ajuste fino:** Use a saída Count do node Data para normalizar o índice T entre 0.0 e 1.0.

## 5. Geometria Procedural (23–26)

### #23 — Terreno Procedural Esculpido (Primitive + Deform)

`Geometria Procedural` · **Essencial** · [GEO] [GEN]

**Cadeia de encadeamento:**

1. **Primitive (Plano) + Noise (Value)** — OUT: Geo / Scalar _(geometria)_
2. **Deform** — IN: Geometria / Height · OUT: Geometria _(geometria)_
3. **Geometry Output** — IN: Geometria _(geometria)_

**Utilidade técnica:** Transforma uma malha plana subdividida em relevo montanhoso contínuo deslocando fisicamente seus vértices através de um campo de ruído.

**Calibração & ajuste fino:** Aumente a densidade de vértices no Primitive para capturar detalhes finos do ruído sem serrilhado poligonal.

### #24 — Ecossistema / Floresta com Clareiras Naturais (Scatter)

`Geometria Procedural` · **Intermediário** · [GEO] [GEN]

**Cadeia de encadeamento:**

1. **Deform (Terreno) + Primitive (Árvore)** — OUT: Geometria _(geometria)_
2. **Scatter (+ Noise em Densidade)** — IN: Superfície / Instância / Densidade · OUT: Instâncias _(instância)_
3. **Geometry Output** — IN: Geometria & Instâncias _(instância)_

**Utilidade técnica:** Espalha milhares de cópias de um objeto sobre um terreno usando um ruído escalar para modular onde a vegetação nasce densa e onde surgem clareiras.

**Calibração & ajuste fino:** Passe o Noise por um Histogram Scan antes de ligar em Densidade para definir clareiras com bordas mais nítidas.

### #25 — Colorização Aleatória de Instâncias (Instance Info)

`Geometria Procedural` · **Essencial** · [GEO] [COL] [OUT]

**Cadeia de encadeamento:**

1. **Instance Info** — OUT: Aleatório _(escalar)_
2. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
3. **Material Output** — IN: Base Color _(cor)_

**Utilidade técnica:** Lê a semente aleatória individual (0.0 a 1.0) de cada cópia gerada pelo Scatter para variar cores de folhas, pedras ou cristais sem duplicar geometria.

**Calibração & ajuste fino:** Funciona em conjunto com qualquer malha instanciada via Scatter.

### #26 — Deformação Ondulante Animada em Malha

`Geometria Procedural` · **Essencial** · [UTI] [VEC] [GEN] [GEO]

**Cadeia de encadeamento:**

1. **Time ➔ Mapping ➔ Wave** — OUT: Value _(escalar)_
2. **Deform (+ Primitive)** — IN: Height / Geometria · OUT: Geometria _(geometria)_
3. **Geometry Output** — IN: Geometria _(geometria)_

**Utilidade técnica:** Cria bandeiras tremulando, ondas oceânicas físicas ou superfícies orgânicas pulsantes diretamente nos vértices da geometria 3D.

**Calibração & ajuste fino:** Combine dois nodes Wave em direções cruzadas com Math [Add] para simular ondas marítimas naturais.

## 6. Partículas & VFX (27–30)

### #27 — Fogo / Fumaça Ascendente com Turbulência

`Partículas & VFX` · **Intermediário** · [VFX]

**Cadeia de encadeamento:**

1. **Particle ➔ Emitter ➔ Motion** — OUT: Position _(vetor)_
2. **Turbulence** — IN: Position · OUT: Position _(vetor)_
3. **Color over Life + Fade + Sprite** — OUT: Color / Opacity _(cor)_
4. **VFX Output** — IN: Position, Color, Opacity, Sprite _(vetor)_

**Utilidade técnica:** Pipeline completo de combustão onde partículas sobem a partir do emissor, ganham movimento orgânico via Turbulence, mudam de cor ao esfriar e somem suavemente.

**Calibração & ajuste fino:** Configure Color over Life de branco/amarelo (Age 0.0) para laranja vivo (0.4) e cinza escuro (1.0).

### #28 — Portal Mágico / Tornado em Espiral (Vortex)

`Partículas & VFX` · **Intermediário** · [VFX]

**Cadeia de encadeamento:**

1. **Motion (Position) + Particle (Time s)** — OUT: Vector/Scalar _(vetor)_
2. **Vortex (variante VFX)** — IN: Position / Time (s) · OUT: Position _(vetor)_
3. **Size over Life + Sprite** — OUT: Size _(escalar)_
4. **VFX Output** — IN: Position, Size, Sprite _(vetor)_

**Utilidade técnica:** Aplica força rotacional contínua ao redor de um eixo para girar partículas em redemoinho, ideal para vórtices de energia, feitiços ou tempestades.

**Calibração & ajuste fino:** Encadeie Turbulence logo após o Vortex para adicionar irregularidade orgânica às espirais.

### #29 — Absorção de Energia / Buraco Negro (Attractor)

`Partículas & VFX` · **Essencial** · [VFX]

**Cadeia de encadeamento:**

1. **Emitter (Origin) + Particle (Age 0-1)** — OUT: Vector/Scalar _(vetor)_
2. **Attractor (variante VFX)** — IN: Position / Age 0-1 · OUT: Position _(vetor)_
3. **Fade (Opacity) + VFX Output** — IN: Position / Opacity _(vetor)_

**Utilidade técnica:** Puxa partículas nascidas em uma esfera externa em direção a um ponto focal central conforme envelhecem, criando efeitos de implosão ou carregamento de poder.

**Calibração & ajuste fino:** Use Size over Life encolhendo próximo a Age 1.0 para que as partículas desapareçam ao atingir o núcleo.

### #30 — Enxame de Vaga-Lumes / Brasas Reativas ao Áudio

`Partículas & VFX` · **Avançado** · [VFX] [INP]

**Cadeia de encadeamento:**

1. **Turbulence (Position) ➔ VFX Output (Position)** — OUT: Position _(vetor)_
2. **Audio Input (Level)** — OUT: Level _(escalar)_
3. **VFX Output** — IN: Size & Opacity (+ Sprite) _(escalar)_

**Utilidade técnica:** Combina partículas flutuantes erráticas com a amplitude do áudio em tempo real para fazer com que cada brasa pulse em tamanho e brilho no ritmo da música.

**Calibração & ajuste fino:** Passe Audio Input (Level) por um Remap para definir um tamanho mínimo visível mesmo nos trechos silenciosos.
