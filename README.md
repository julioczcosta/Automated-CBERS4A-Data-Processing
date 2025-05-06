# Automated-CBERS4A-Data-Processing

Este repositório contém um pipeline automatizado para o **download**, **processamento** e **análise** de imagens do satélite **CBERS-4A**. O código realiza a coleta de imagens com base no ID da cena, faz o pré-processamento (como recorte, redimensionamento e fusão de imagens) e gera produtos finais, como imagens RGB, NIRGB e NDVI.

## Objetivo
O objetivo deste código é facilitar a aquisição e o processamento de dados de satélite para análise ambiental, de uso do solo e monitoramento da vegetação. Ele pode ser utilizado para estudar áreas de interesse com a utilização de diferentes bandas do satélite CBERS-4A e produzir produtos como NDVI, imagens RGB e imagens Pansharpened.

## Funcionalidades

### Funcionalidades principais:
- **Download de Imagens**: Baixa imagens do satélite CBERS-4A com base no `scene_id`.
- **Processamento de Imagens**: Recorta as imagens usando uma geometria definida (shapefile) e realiza o redimensionamento das imagens para uma resolução comum.
- **Fusão de Imagens (Pansharpening)**: Combina as imagens multiespectrais (RGB, NIRGB) com a imagem de alta resolução PAN para melhorar a qualidade espacial.
- **Cálculo de NDVI**: Gera o índice de vegetação NDVI a partir das bandas do vermelho e infravermelho próximo.
- **Correção de Geometria**: Verifica e corrige a geometria do shapefile antes de ser usada no recorte da imagem.

### Produtos Gerados:
- **Imagens RGB**: Compostas pelas bandas vermelho, verde e azul.
- **Imagens NIRGB**: Compostas pela banda infravermelha próxima (NIR) junto com as bandas RGB.
- **Imagens Pansharpened RGB**: Imagens RGB com alta resolução, combinadas com a imagem panorâmica (PAN) utilizando a técnica de fusão.
- **Imagens Pansharpened NIRGB**: Imagens NIRGB com alta resolução, também utilizando a fusão com a imagem panorâmica.
- **NDVI**: Índice de Vegetação por Diferença Normalizada, útil para monitoramento de vegetação.

## Como Usar

### 1. **Configuração do Ambiente**:
Certifique-se de ter o Python 3.6 ou superior e as bibliotecas necessárias instaladas.

### 2. **Baixando as Imagens**:
Modifique os parâmetros no início do código, como shp_path (caminho do shapefile), scene_id (ID da cena do CBERS-4A, **produto WPM_L4_DN**), user_cbers (usuário do CBERS) e out_dir (diretório de saída), conforme necessário para seu caso específico.

### 3. **Processamento de Imagens**:
Após modificar os parâmetros, o código realizará automaticamente o download das imagens, o recorte e o redimensionamento, e a geração dos produtos finais (**RGB**, **NIRGB**, **PAN-RGB**, **PAN-NIRGB** e **NDVI**).


## Filtro de Suavização para Pansharpening
No processo de fusões de imagens (Pansharpening), é utilizado um filtro de suavização aplicado à imagem PAN. Este filtro tem o objetivo de reduzir o ruído de alta frequência e melhorar a qualidade da fusão das imagens multiespectrais com a imagem PAN de alta resolução.

### **Detalhes do Filtro de Suavização**:
- **Filtro de Suavização:** O filtro utilizado é o `cv2.blur()` do OpenCV, que aplica uma suavização simples à imagem PAN, utilizando uma janela de tamanho 5x5. A suavização ajuda a evitar artefatos que poderiam ser introduzidos durante a fusão das imagens.
- **Evitar Divisão por Zero:** Para garantir que não ocorram erros de divisão por zero durante a fusão das imagens, qualquer valor de zero no resultado do filtro é substituído por um valor muito pequeno (1e-6). Isso é feito para preservar a integridade dos cálculos de fusão, sem causar distorções.
- **Objetivo da Suavização:** O objetivo da suavização é garantir que a fusão das imagens RGB e NIRGB com a imagem PAN seja realizada de forma fluida, com detalhes mais nítidos e sem ruídos indesejados.
