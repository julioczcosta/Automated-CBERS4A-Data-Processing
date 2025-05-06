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
