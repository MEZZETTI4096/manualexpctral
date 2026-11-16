# Catálogo Aprimorado — 30 Receitas & Blueprints (Vol. 3)

Biblioteca de padrões de encadeamento prontos para produção: topologia exata de entrada/saída, parâmetros internos recomendados e utilidade técnica.

## 1. Materiais PBR & Superfícies (01–07)

### Blueprint #01 — Desgaste Metálico em Quinas (Edge Wear PBR)

`Materiais PBR & Superfícies` · **Intermediário** · [GEN] [FIL] [COL] [UTI] [OUT]

**Resumo:** Revela metal polido nas arestas expostas de objetos pintados e ajusta a rugosidade automaticamente.

**Topologia de encadeamento:**

1. **Brick + Noise** — OUT: Value _(escalar)_
2. **Math [Add]** — IN: A / B · OUT: Value _(escalar)_
3. **Edge Wear** — IN: Height · OUT: Value _(escalar)_
4. **Mix + Invert** — IN: Fac / In · OUT: Color _(cor)_
5. **Material Output** — IN: Base Color, Metallic & Roughness _(cor)_

**Utilidade & comportamento no grafo:** Calcula a curvatura convexa do relevo combinado para gerar uma máscara de desgaste físico nas quinas. Onde a tinta descasca (Value = 1.0), o metal subjacente aparece e a rugosidade cai.

**Parâmetros & calibração recomendada:**

- Math [Add]: Some 85% de Brick (Value) com 15% de Noise (Value) para quebrar quinas perfeitas.
- Edge Wear: Ajuste o raio/intensidade para isolar apenas as bordas salientes.
- Invert: Inverta a máscara antes de ligar em Roughness para tornar o metal exposto mais reflexivo.

### Blueprint #02 — Acúmulo Realista de Neve, Areia ou Musgo (Height Blend)

`Materiais PBR & Superfícies` · **Intermediário** · [GEN] [COL] [VEC] [OUT]

**Resumo:** Mistura dois materiais baseando-se em seus mapas de altura reais para preencher cavidades primeiro.

**Topologia de encadeamento:**

1. **Voronoi (Pedra) + Noise (Neve)** — OUT: Value _(escalar)_
2. **Height Blend** — IN: Base, Blend, Height · OUT: Out & Height _(cor)_
3. **Bump** — IN: Height · OUT: Normal _(vetor)_
4. **Material Output** — IN: Base Color, Normal & Roughness _(cor)_

**Utilidade & comportamento no grafo:** Ao contrário de um Mix linear que deixa a superfície semitransparente, o Height Blend compara a elevação de cada pixel, fazendo com que neve ou areia se depositem primeiro nos vãos entre as pedras.

**Parâmetros & calibração recomendada:**

- Height Blend: Use a saída Out para controlar também a transição de Roughness entre pedra úmida e neve.
- Bump: Conecte a saída Height combinada do Height Blend para manter a continuidade das normais.

### Blueprint #03 — Sombreamento de Cavidades & Sujeira (Micro-AO)

`Materiais PBR & Superfícies` · **Essencial** · [GEN] [FIL] [COL] [OUT]

**Resumo:** Gera oclusão de ambiente procedural diretamente de um mapa de altura sem baking externo.

**Topologia de encadeamento:**

1. **Brick / Voronoi** — OUT: Value _(escalar)_
2. **Height AO** — IN: Height · OUT: Value _(escalar)_
3. **Levels** — IN: In · OUT: Color _(cor)_
4. **Blend [Multiply]** — IN: Base / Blend · OUT: Color _(cor)_
5. **Material Output** — IN: Base Color & Occlusion _(escalar)_

**Utilidade & comportamento no grafo:** Escurece automaticamente frestas, rejuntes e regiões profundas cercadas por relevo alto, conferindo profundidade e peso visual imediato a qualquer superfície procedural.

**Parâmetros & calibração recomendada:**

- Levels: Comprima o ponto de branco para manter as áreas expostas em 1.0 puro.
- Material Output: Conecte o Value do Height AO também na entrada dedicada Occlusion.

### Blueprint #04 — Alvenaria Orgânica com Tijolos Quebrados (Slope Blur)

`Materiais PBR & Superfícies` · **Intermediário** · [GEN] [FIL] [VEC] [OUT]

**Resumo:** Deforma bordas geométricas seguindo as inclinações de um ruído para simular erosão e lascas.

**Topologia de encadeamento:**

1. **Brick (In) + Noise (Slope)** — OUT: Value _(escalar)_
2. **Slope Blur** — IN: In / Slope · OUT: Color _(cor)_
3. **Bump** — IN: Height · OUT: Normal _(vetor)_
4. **Material Output** — IN: Normal & Height _(vetor)_

**Utilidade & comportamento no grafo:** Empurra os pixels do padrão Brick ao longo do gradiente direcional de um Noise, destruindo o aspecto artificial de computador e criando pedras rústicas ou tijolos antigos.

**Parâmetros & calibração recomendada:**

- Noise: Use escala média-alta para simular lascas nas quinas dos tijolos.
- Slope Blur: Valores sutis preservam o rejunte enquanto desgastam apenas o contorno das peças.

### Blueprint #05 — Variação Individual por Peça / Ladrilho (Brick ID)

`Materiais PBR & Superfícies` · **Essencial** · [GEN] [COL] [OUT]

**Resumo:** Atribui variações únicas de cor e rugosidade para cada tijolo ou azulejo individualmente.

**Topologia de encadeamento:**

1. **Brick** — OUT: ID _(escalar)_
2. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
3. **Blend [Overlay]** — IN: Base / Blend · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade & comportamento no grafo:** Lê o índice exclusivo (ID) emitido por cada bloco do node Brick para mapear nuances sutis de tonalidade entre peças vizinhas.

**Parâmetros & calibração recomendada:**

- Color Ramp: Defina 3 a 4 tons próximos da cor base da argila ou pedra.
- Blend: Ajuste Mask entre 0.25 e 0.45 para evitar contraste exagerado.

### Blueprint #06 — Desempacotamento de Mapas ORM (Channel-Packed PBR)

`Materiais PBR & Superfícies` · **Essencial** · [INP] [VEC] [OUT]

**Resumo:** Extrai Occlusion, Roughness e Metalness armazenados nos canais R, G e B de uma única textura.

**Topologia de encadeamento:**

1. **Image Texture (Mapa ORM)** — OUT: Color _(cor)_
2. **Separate RGB** — IN: Color · OUT: R, G, B _(escalar)_
3. **Material Output** — IN: Occlusion (R), Roughness (G), Metallic (B) _(escalar)_

**Utilidade & comportamento no grafo:** Reduz o consumo de memória de vídeo em até 66% ao decodificar três mapas PBR em escala de cinza a partir de um único arquivo RGB.

**Parâmetros & calibração recomendada:**

- R ➔ Material Output (Occlusion)
- G ➔ Material Output (Roughness)
- B ➔ Material Output (Metalness)

### Blueprint #07 — Textura Triplanar / Sem Costuras UV (World-Space)

`Materiais PBR & Superfícies` · **Essencial** · [VEC] [GEN] [COL] [OUT]

**Resumo:** Projeta padrões procedurais usando coordenadas 3D do mundo para eliminar emendas de UV.

**Topologia de encadeamento:**

1. **Position** — OUT: Position _(vetor)_
2. **Noise / Voronoi** — IN: Coord · OUT: Value _(escalar)_
3. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade & comportamento no grafo:** Avalia os geradores procedurais diretamente no espaço tridimensional da malha (Position), garantindo continuidade perfeita mesmo em modelos sem mapeamento UV aberto.

**Parâmetros & calibração recomendada:**

- Position: Conecte diretamente na entrada Coord de Noise, Voronoi ou Cells.

## 2. Estilização & Retro NPR (08–12)

### Blueprint #08 — Cel-Shading / Faixas Tonais Retro 64-Bit

`Estilização & Retro NPR` · **Essencial** · [INP] [COL] [OUT]

**Resumo:** Quantiza gradientes em degraus rígidos e remapeia para uma paleta fechada de 4 cores.

**Topologia de encadeamento:**

1. **Image Texture** — OUT: Color _(cor)_
2. **Posterize** — IN: In · OUT: Color _(cor)_
3. **Gradient Map 4** — IN: In · OUT: Out _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade & comportamento no grafo:** Transforma texturas fotográficas ou gradientes suaves em arte estilizada com bandas tonais discretas estilo pixel art ou console 16/64-bit.

**Parâmetros & calibração recomendada:**

- Posterize: Configure para 4 níveis para alinhar exatamente cada faixa com as 4 paradas do Gradient Map 4.

### Blueprint #09 — Contorno Mágico / Rim Light (Fresnel + Smoothstep)

`Estilização & Retro NPR` · **Essencial** · [VEC] [UTI] [COL] [OUT]

**Resumo:** Isola as bordas rasantes da silhueta para criar auras emissivas e escudos de energia.

**Topologia de encadeamento:**

1. **Fresnel** — OUT: Value _(escalar)_
2. **Smoothstep** — IN: In · OUT: Value _(escalar)_
3. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
4. **Material Output** — IN: Emissive _(cor)_

**Utilidade & comportamento no grafo:** Utiliza o ângulo entre a normal da superfície e o vetor da câmera para acender apenas o perímetro externo do objeto.

**Parâmetros & calibração recomendada:**

- Smoothstep: Use faixa estreita (ex: 0.65 a 0.85) para criar um contorno nítido de energia.

### Blueprint #10 — Retícula de Quadrinhos / Halftone Dinâmico

`Estilização & Retro NPR` · **Avançado** · [VEC] [GEN] [COL] [UTI] [OUT]

**Resumo:** Converte a luminância de qualquer imagem em pontos de retícula estilizados.

**Topologia de encadeamento:**

1. **Mapping ➔ Dots (Value) + Luminance (Value)** — OUT: Value _(escalar)_
2. **Math [Greater Than]** — IN: A / B · OUT: Value _(escalar)_
3. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade & comportamento no grafo:** Compara a máscara radial de pontos (Dots) contra o brilho percebido (Luminance) da imagem original, fazendo os pontos crescerem nas sombras e encolherem nos realces.

**Parâmetros & calibração recomendada:**

- Mapping: Rotacione as coordenadas UV em 45° para reproduzir o padrão clássico de impressão.

### Blueprint #11 — Iridescência Óptica / Bolha de Sabão e Óleo

`Estilização & Retro NPR` · **Intermediário** · [VEC] [GEN] [UTI] [COL] [OUT]

**Resumo:** Simula interferência de filme fino com reflexos arco-íris variáveis pelo ângulo de visão.

**Topologia de encadeamento:**

1. **Fresnel (Value) + Noise (Value)** — OUT: Value _(escalar)_
2. **Math [Add]** — IN: A / B · OUT: Value _(escalar)_
3. **Spectral Dispersion** — IN: Thickness · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color & Clearcoat _(cor)_

**Utilidade & comportamento no grafo:** Modula a espessura óptica (Thickness) do node Spectral Dispersion usando Fresnel e ruído orgânico para criar superfícies holográficas, vidro dicroico ou manchas de óleo.

**Parâmetros & calibração recomendada:**

- Material Output: Defina Clearcoat em 1.0 e Roughness próximo de 0.05 para máximo brilho especular.

### Blueprint #12 — Conversão de Altura para Normal Map RGB (Sobel)

`Estilização & Retro NPR` · **Intermediário** · [GEN] [FIL] [VEC] [OUT]

**Resumo:** Converte mapas escalares de altura em texturas RGB de Normal Map manipuláveis.

**Topologia de encadeamento:**

1. **Voronoi** — OUT: Value _(escalar)_
2. **Blur** — IN: In · OUT: Color _(cor)_
3. **Sobel Normal** — IN: Height · OUT: Normal Map _(cor)_
4. **Normal Map** — IN: Color · OUT: Normal _(vetor)_
5. **Material Output** — IN: Normal _(vetor)_

**Utilidade & comportamento no grafo:** Permite gerar um Normal Map no formato padrão RGB (lilás/azulado) para combiná-lo com outras texturas antes de decodificá-lo para o shader.

**Parâmetros & calibração recomendada:**

- Blur: Suaviza bordas duras do Voronoi antes do filtro Sobel para produzir chanfros arredondados.

## 3. UV, Distorção & Animação (13–17)

### Blueprint #13 — Superfície de Água Ondulante / Distorção de Calor

`UV, Distorção & Animação` · **Intermediário** · [UTI] [VEC] [GEN] [INP]

**Resumo:** Anima um ruído ao longo do tempo para distorcer continuamente as coordenadas UV.

**Topologia de encadeamento:**

1. **Time ➔ Mapping** — OUT: UV _(vetor)_
2. **Noise** — IN: Coord · OUT: Value _(escalar)_
3. **Directional Warp** — IN: UV / Map · OUT: Color _(vetor)_
4. **Image Texture** — IN: UV · OUT: Color _(cor)_

**Utilidade & comportamento no grafo:** Desloca um campo de ruído no tempo e o injeta no Directional Warp para ondular qualquer textura ou padrão, simulando refração na água ou ar quente.

**Parâmetros & calibração recomendada:**

- Directional Warp: Use intensidade baixa (0.02 a 0.06) para manter a legibilidade da imagem distorcida.

### Blueprint #14 — Correção de Proporção de Tela (Aspect Ratio Fix)

`UV, Distorção & Animação` · **Essencial** · [VEC] [INP] [UTI] [GEN]

**Resumo:** Impede que formas geométricas fiquem esticadas em telas widescreen ou mobile.

**Topologia de encadeamento:**

1. **UV (UV) + Viewport (Aspect)** — OUT: Vector/Scalar _(vetor)_
2. **Math [Multiply]** — IN: A / B · OUT: Value _(escalar)_
3. **Dots / Checker / Brick** — IN: Coord · OUT: Value _(escalar)_

**Utilidade & comportamento no grafo:** Multiplica o eixo horizontal das coordenadas UV pela razão de aspecto dinâmica da janela (Viewport), garantindo círculos e quadrados perfeitos em qualquer resolução.

**Parâmetros & calibração recomendada:**

- Viewport: Leia sempre a saída Aspect (laranja) para adaptação responsiva automática.

### Blueprint #15 — Pulso Rítmico Normalizado (Senoide Calibrada)

`UV, Distorção & Animação` · **Essencial** · [UTI] [OUT]

**Resumo:** Converte ondas senoidais (-1 a +1) para a faixa segura de [0.0, 1.0].

**Topologia de encadeamento:**

1. **Time** — OUT: Value _(escalar)_
2. **Math [Sine]** — IN: A · OUT: Value _(escalar)_
3. **Remap [-1..1 → 0..1]** — IN: In · OUT: Value _(escalar)_
4. **Material Output** — IN: Emissive _(cor)_

**Utilidade & comportamento no grafo:** Evita valores negativos inválidos gerados por funções trigonométricas ao remapear a saída do seno para [0.0, 1.0], criando pulsações suaves de luz ou escala.

**Parâmetros & calibração recomendada:**

- Math [Multiply]: Insira entre Time e Sine para controlar a velocidade do ciclo.

### Blueprint #16 — Erosão / Dissolve Orgânico com Histogram Scan

`UV, Distorção & Animação` · **Intermediário** · [GEN] [FIL] [UTI] [OUT]

**Resumo:** Anima o surgimento ou dissolução de materiais varrendo a faixa tonal de um ruído.

**Topologia de encadeamento:**

1. **Noise** — OUT: Value _(escalar)_
2. **Histogram Scan** — IN: In · OUT: Value _(escalar)_
3. **Clamp** — IN: In · OUT: Value _(escalar)_
4. **Material Output** — IN: Opacity _(escalar)_

**Utilidade & comportamento no grafo:** Permite controlar com precisão a erosão progressiva de uma máscara para efeitos de teletransporte, queima de papel ou aparição mágica.

**Parâmetros & calibração recomendada:**

- Histogram Scan: Aumente o contraste para criar recortes nítidos sem zonas semitransparentes.

### Blueprint #17 — Madeira Procedural com Veios Orgânicos

`UV, Distorção & Animação` · **Intermediário** · [VEC] [GEN] [COL] [OUT]

**Resumo:** Distorce coordenadas UV antes de gerar ondas para criar anéis naturais de madeira.

**Topologia de encadeamento:**

1. **UV ➔ Directional Warp (+ Noise)** — OUT: Color _(vetor)_
2. **Wave** — IN: Coord · OUT: Value _(escalar)_
3. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade & comportamento no grafo:** Ao deformar o domínio UV antes do gerador Wave, listras paralelas transformam-se em veios orgânicos e nós de madeira.

**Parâmetros & calibração recomendada:**

- Mapping: Estique a escala em um dos eixos (ex: X=2, Y=12) antes do Warp para alongar as fibras.

## 4. Áudio, Cursor & Dados (18–22)

### Blueprint #18 — Visualizador de Espectro de Áudio (Spectrum Bars)

`Áudio, Cursor & Dados` · **Intermediário** · [VEC] [INP] [UTI] [COL] [OUT]

**Resumo:** Mapeia bandas de frequência sonoras ao longo do eixo horizontal para gráficos reativos.

**Topologia de encadeamento:**

1. **UV** — OUT: UV _(vetor)_
2. **Audio Input** — OUT: Spectrum _(escalar)_
3. **Step** — IN: In · OUT: Value _(escalar)_
4. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
5. **Material Output** — IN: Emissive _(cor)_

**Utilidade & comportamento no grafo:** Alimenta o pino U do Audio Input com a coordenada UV.x para consultar a energia de cada frequência em tempo real e acender barras luminosas.

**Parâmetros & calibração recomendada:**

- Audio Input: Certifique-se de ativar a captura de microfone ou áudio do sistema no painel do node.

### Blueprint #19 — Batida Musical Pulsando Geometria e Luz (Beat Trigger)

`Áudio, Cursor & Dados` · **Essencial** · [INP] [UTI] [GEO] [OUT]

**Resumo:** Sincroniza deformações da malha 3D e picos de brilho com os graves e batidas da música.

**Topologia de encadeamento:**

1. **Audio Input** — OUT: Beat & Bass _(escalar)_
2. **Smoothstep** — IN: In · OUT: Value _(escalar)_
3. **Deform (Height) + Material Output (Emissive)** — IN: Height / Emissive _(escalar)_

**Utilidade & comportamento no grafo:** Conecta diretamente os detectores de batida (Beat) e graves (Bass) ao deslocamento de vértices e intensidade emissiva.

**Parâmetros & calibração recomendada:**

- Smoothstep: Suaviza o decaimento do sinal para criar um movimento elástico orgânico.

### Blueprint #20 — Pincel / Halo Interativo com o Cursor (Pointer Tracking)

`Áudio, Cursor & Dados` · **Avançado** · [VEC] [INP] [UTI] [OUT]

**Resumo:** Cria áreas luminosas ou ondas que seguem o mouse/toque enquanto pressionado.

**Topologia de encadeamento:**

1. **UV (UV) vs Pointer (UV)** — OUT: Vector _(vetor)_
2. **Math [Distance] ➔ Smoothstep** — IN: A / B · OUT: Value _(escalar)_
3. **Math [Multiply] (+ Pointer Down)** — IN: A / B · OUT: Value _(escalar)_
4. **Material Output** — IN: Emissive _(cor)_

**Utilidade & comportamento no grafo:** Mede a distância entre cada pixel e o cursor normalizado (Pointer UV), multiplicando o resultado pelo estado do clique (Pointer Down) para ativar o efeito sob demanda.

**Parâmetros & calibração recomendada:**

- Pointer: Use Delta para modular a intensidade conforme a velocidade do movimento do cursor.

### Blueprint #21 — Variação Automática por Objeto na Cena (Object ID)

`Áudio, Cursor & Dados` · **Essencial** · [INP] [UTI] [COL] [OUT]

**Resumo:** Rotaciona a matiz automaticamente para cada instância de objeto usando seu ID único.

**Topologia de encadeamento:**

1. **Object Info** — OUT: ID _(escalar)_
2. **Math [Multiply]** — IN: A · OUT: Value _(escalar)_
3. **Hue Shift** — IN: In · OUT: Color _(cor)_
4. **Material Output** — IN: Base Color _(cor)_

**Utilidade & comportamento no grafo:** Permite aplicar um único material compartilhado a dezenas de props na cena garantindo que cada objeto exiba uma variação cromática distinta.

**Parâmetros & calibração recomendada:**

- Math [Multiply]: Multiplique o ID por 0.37 para distribuir bem as cores ao longo do círculo cromático.

### Blueprint #22 — Visualização de Gráficos Guiada por Planilha (Data)

`Áudio, Cursor & Dados` · **Intermediário** · [INP] [UTI] [GEO] [COL]

**Resumo:** Conecta tabelas externas diretamente à elevação e cor de malhas 3D.

**Topologia de encadeamento:**

1. **Data (T / Coluna U)** — OUT: Value _(escalar)_
2. **Remap** — IN: In · OUT: Value _(escalar)_
3. **Deform (Height) + Color Ramp (Fac)** — IN: Height / Fac _(escalar)_

**Utilidade & comportamento no grafo:** Transforma valores tabulares em altura física e gradiente de cor em tempo real, ideal para infográficos 3D e animações orientadas por dados.

**Parâmetros & calibração recomendada:**

- Data: Use o pino Count para normalizar os índices de leitura ao longo da tabela.

## 5. Geometria Procedural (23–26)

### Blueprint #23 — Terreno Procedural Esculpido (Primitive + Deform)

`Geometria Procedural` · **Essencial** · [GEO] [GEN]

**Resumo:** Desloca vértices de uma malha primitiva usando um ruído contínuo para gerar relevo.

**Topologia de encadeamento:**

1. **Primitive (Plano) + Noise (Value)** — OUT: Geo / Scalar _(geometria)_
2. **Deform** — IN: Geometria / Height · OUT: Geometria _(geometria)_
3. **Geometry Output** — IN: Geometria _(geometria)_

**Utilidade & comportamento no grafo:** Cria montanhas, dunas ou superfícies rochosas em tempo real modificando diretamente a posição dos vértices da malha.

**Parâmetros & calibração recomendada:**

- Primitive: Aumente a subdivisão de vértices para capturar detalhes finos sem facetas poligonais.

### Blueprint #24 — Ecossistema / Floresta com Clareiras Naturais (Scatter)

`Geometria Procedural` · **Intermediário** · [GEO] [GEN]

**Resumo:** Espalha instâncias sobre um terreno usando um mapa de ruído para modular a densidade.

**Topologia de encadeamento:**

1. **Deform (Terreno) + Primitive (Árvore)** — OUT: Geometria _(geometria)_
2. **Scatter (+ Noise em Densidade)** — IN: Superfície / Instância / Densidade · OUT: Instâncias _(instância)_
3. **Geometry Output** — IN: Geometria & Instâncias _(instância)_

**Utilidade & comportamento no grafo:** Popula superfícies complexas com milhares de cópias leves (instâncias), criando agrupamentos orgânicos e clareiras naturais através da entrada Densidade.

**Parâmetros & calibração recomendada:**

- Scatter: Conecte tanto a Geometria (terreno) quanto as Instâncias (árvores) no Geometry Output.

### Blueprint #25 — Colorização Aleatória de Instâncias (Instance Info)

`Geometria Procedural` · **Essencial** · [GEO] [COL] [OUT]

**Resumo:** Atribui cores distintas por instância espalhada sem duplicar materiais ou malhas.

**Topologia de encadeamento:**

1. **Instance Info** — OUT: Aleatório _(escalar)_
2. **Color Ramp** — IN: Fac · OUT: Color _(cor)_
3. **Material Output** — IN: Base Color _(cor)_

**Utilidade & comportamento no grafo:** Lê o valor pseudoaleatório individual (0.0 a 1.0) de cada cópia gerada pelo Scatter para variar tons de folhagem, pedras ou cristais.

**Parâmetros & calibração recomendada:**

- Instance Info: Combine com o pino Escala para também variar o tamanho ou brilho das instâncias maiores.

### Blueprint #26 — Deformação Ondulante Animada em Malha

`Geometria Procedural` · **Essencial** · [UTI] [VEC] [GEN] [GEO]

**Resumo:** Anima ondas físicas diretamente nos vértices da geometria ao longo do tempo.

**Topologia de encadeamento:**

1. **Time ➔ Mapping ➔ Wave** — OUT: Value _(escalar)_
2. **Deform (+ Primitive)** — IN: Height / Geometria · OUT: Geometria _(geometria)_
3. **Geometry Output** — IN: Geometria _(geometria)_

**Utilidade & comportamento no grafo:** Simula superfícies oceânicas, tecidos tremulando ao vento ou pisos pulsantes deformando continuamente a malha 3D.

**Parâmetros & calibração recomendada:**

- Wave: Some dois geradores Wave rotacionados em ângulos diferentes para evitar ondas unidirecionais artificiais.

## 6. Partículas & VFX (27–30)

### Blueprint #27 — Fogo / Fumaça Ascendente com Turbulência

`Partículas & VFX` · **Intermediário** · [VFX]

**Resumo:** Pipeline completo de combustão com movimento orgânico, transição térmica e fade suave.

**Topologia de encadeamento:**

1. **Particle ➔ Emitter ➔ Motion** — OUT: Position _(vetor)_
2. **Turbulence** — IN: Position · OUT: Position _(vetor)_
3. **Color over Life + Fade + Sprite** — OUT: Color / Opacity _(cor)_
4. **VFX Output** — IN: Position, Color, Opacity, Sprite _(vetor)_

**Utilidade & comportamento no grafo:** Controla todo o ciclo de vida das partículas desde o lançamento no Emitter, adicionando ondulação caótica via Turbulence e resfriamento gradual de cor.

**Parâmetros & calibração recomendada:**

- Color over Life: Branco/Amarelo (Age 0.0) ➔ Laranja Vivo (0.45) ➔ Cinza Escuro (1.0).

### Blueprint #28 — Portal Mágico / Tornado em Espiral (Vortex)

`Partículas & VFX` · **Intermediário** · [VFX]

**Resumo:** Gira partículas continuamente em redemoinho ao redor de um eixo no espaço.

**Topologia de encadeamento:**

1. **Motion (Position) + Particle (Time s)** — OUT: Vector/Scalar _(vetor)_
2. **Vortex (variante VFX)** — IN: Position / Time (s) · OUT: Position _(vetor)_
3. **Size over Life + Sprite** — OUT: Size _(escalar)_
4. **VFX Output** — IN: Position, Size, Sprite _(vetor)_

**Utilidade & comportamento no grafo:** Aplica um campo de força rotacional para criar portais arcanos, vórtices de energia, espirais de fogo ou tempestades de poeira.

**Parâmetros & calibração recomendada:**

- Vortex: Encadeie Turbulence logo após o Vortex para quebrar a simetria perfeita da espiral.

### Blueprint #29 — Absorção de Energia / Buraco Negro (Attractor)

`Partículas & VFX` · **Essencial** · [VFX]

**Resumo:** Atrai partículas espalhadas em direção a um ponto focal conforme envelhecem.

**Topologia de encadeamento:**

1. **Emitter (Origin) + Particle (Age 0-1)** — OUT: Vector/Scalar _(vetor)_
2. **Attractor (variante VFX)** — IN: Position / Age 0-1 · OUT: Position _(vetor)_
3. **Fade (Opacity) + VFX Output** — IN: Position / Opacity _(vetor)_

**Utilidade & comportamento no grafo:** Cria efeitos de implosão, coleta de energia ou carregamento de magia puxando partículas periféricas para o centro.

**Parâmetros & calibração recomendada:**

- Size over Life: Reduza a escala próximo de Age 1.0 para que as partículas desapareçam ao tocar o núcleo.

### Blueprint #30 — Enxame de Vaga-Lumes / Brasas Reativas ao Áudio

`Partículas & VFX` · **Avançado** · [VFX] [INP]

**Resumo:** Faz partículas flutuantes pulsarem em tamanho e brilho no ritmo da música.

**Topologia de encadeamento:**

1. **Turbulence (Position) ➔ VFX Output (Position)** — OUT: Position _(vetor)_
2. **Audio Input (Level)** — OUT: Level _(escalar)_
3. **VFX Output** — IN: Size & Opacity (+ Sprite) _(escalar)_

**Utilidade & comportamento no grafo:** Une o movimento orgânico errático do campo Turbulence à amplitude sonora em tempo real para criar atmosferas musicais interativas.

**Parâmetros & calibração recomendada:**

- Audio Input: Use Level ou Bass para controlar o pulso simultâneo de todas as partículas ativas.
