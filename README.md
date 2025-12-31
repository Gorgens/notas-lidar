
# Processamento de Dados LiDAR para Análise de Vegetação

Este repositório contém uma coleção de scripts e dados de exemplo para o processamento de dados LiDAR, focados na análise de vegetação. Os materiais aqui presentes demonstram como realizar um fluxo de trabalho completo, desde a classificação da nuvem de pontos até a extração de métricas e a identificação de árvores individuais. O projeto utiliza duas abordagens principais: o software **FUSION** e o pacote **lidR** para a linguagem de programação R.

## Estrutura do Projeto

O repositório está organizado da seguinte forma:

-   **/docs:** Contém a documentação teórica e material de apoio em formato PDF.
-   **/fusion:** Scripts em lote (`.bat`) e R (`.R`) para o processamento de dados LiDAR com o FUSION.
-   **/las:** Arquivos de dados LiDAR de exemplo no formato `.laz`.
-   **/lidr:** Scripts em R para o processamento de dados LiDAR com o pacote `lidR`.
-   **/transecto:** Scripts em R para análises mais específicas e avançadas, como a análise de fronteira de eficiência.

## Pré-requisitos

Para executar os scripts e processar os dados, é necessário instalar o seguinte software:

### 1. LAStools

O LAStools é uma suíte de ferramentas para o processamento de dados LiDAR. Embora não seja diretamente utilizado pelos scripts deste repositório, é uma ferramenta essencial para a manipulação e visualização de dados LiDAR.

-   **Download:** [https://rapidlasso.de/downloads/](https://rapidlasso.de/downloads/)
-   **Instalação:**
    1.  Baixe a versão mais recente do LAStools.
    2.  Extraia o conteúdo para um diretório em seu computador (ex: `C:\LAStools`).
    3.  Adicione o diretório `bin` do LAStools (ex: `C:\LAStools\bin`) à variável de ambiente `PATH` do seu sistema.

### 2. FUSION

O FUSION é um software desenvolvido pelo Serviço Florestal dos EUA para visualização e análise de dados LiDAR.

-   **Download:** [http://forsys.cfr.washington.edu/fusion/fusionlatest.html](http://forsys.cfr.washington.edu/fusion/fusionlatest.html)
-   **Instalação:**
    1.  Baixe a versão mais recente do FUSION.
    2.  Execute o instalador e siga as instruções. Recomenda-se instalar em um diretório como `C:\FUSION\`.
    3.  Adicione o diretório de instalação do FUSION (ex: `C:\FUSION\`) à variável de ambiente `PATH` do seu sistema.

### 3. R e RStudio

R é uma linguagem de programação para computação estatística e gráficos. RStudio é um ambiente de desenvolvimento integrado para R.

-   **Download do R:** [https://cran.r-project.org/](https://cran.r-project.org/)
-   **Download do RStudio:** [https://www.rstudio.com/products/rstudio/download/](https://www.rstudio.com/products/rstudio/download/)
-   **Instalação:** Instale o R primeiro e, em seguida, o RStudio.

#### Bibliotecas R

Após a instalação do R e do RStudio, abra o RStudio e instale as seguintes bibliotecas, que são necessárias para executar os scripts R deste repositório:

```r
install.packages(c("lidR", "raster", "terra", "sf", "rgdal", "tidyverse", "ggplot2", "gridExtra", "future", "RCSF"))
```

## Fluxo de Trabalho de Processamento

Este repositório apresenta dois fluxos de trabalho principais para o processamento de dados LiDAR:

### 1. Fluxo de Trabalho com FUSION

Os scripts no diretório `/fusion` utilizam as ferramentas de linha de comando do FUSION para realizar o processamento. Este fluxo de trabalho é adequado para a automação de tarefas em lote e é controlado principalmente por scripts R que chamam os executáveis do FUSION. As etapas incluem:

-   Classificação de pontos de solo.
-   Criação de Modelos Digitais de Terreno (MDT).
-   Criação de Modelos de Altura do Dossel (MDC).
-   Cálculo de métricas da vegetação.
-   Detecção de árvores individuais.

### 2. Fluxo de Trabalho com lidR

Os scripts no diretório `/lidr` utilizam o pacote `lidR` em R. O `lidR` fornece um ambiente completo para o processamento de dados LiDAR, com uma ampla gama de funcionalidades e algoritmos. As etapas são semelhantes às do FUSION, mas são executadas inteiramente dentro do ambiente R:

-   Classificação de pontos de solo.
-   Geração de MDT.
-   Normalização da nuvem de pontos.
-   Geração de MDC.
-   Segmentação de árvores individuais.

## Exemplos de Uso

### Exemplo 1: Processamento com FUSION

Este exemplo mostra como modificar e executar o script `Using FUSION v1.0.R` para processar um conjunto de dados.

1.  **Abra o script** `fusion/Using FUSION v1.0.R` no RStudio.
2.  **Modifique os caminhos:** Altere as variáveis `WORK.PATH` e `ORIG.LAS` para apontar para os seus diretórios. Por exemplo:

    ```r
    # Caminho para o diretório de trabalho do projeto
    WORK.PATH = "C:\\Users\\SeuUsuario\\Documents\\nativa-lidar\\"

    # Caminho para os arquivos .las de origem
    ORIG.LAS = "C:\\Users\\SeuUsuario\\Documents\\nativa-lidar\\las\\"

    setwd(WORK.PATH)
    ```

3.  **Execute o script:** Você pode executar o script inteiro ou selecionar e executar partes do código para realizar etapas específicas do processamento.

### Exemplo 2: Processamento com lidR

Este exemplo mostra como executar o fluxo de trabalho de processamento usando os scripts do diretório `/lidr`.

1.  **Defina o diretório de trabalho:** Abra o script `lidr/010set_wd.R` e altere o caminho para o diretório raiz do seu projeto.

    ```r
    # Defina o caminho para o diretório do projeto
    setwd('C:/Users/SeuUsuario/Documents/nativa-lidar/')
    ```

2.  **Execute os scripts em ordem:** Execute os scripts de `010set_wd.R` a `061chm2tree.R` na sequência numérica para completar o fluxo de trabalho. Cada script realiza uma etapa do processo, como a classificação de solo, a geração do MDT e a detecção de árvores.

## Resultados Esperados

Após a execução dos scripts de processamento, você obterá uma série de produtos derivados dos dados LiDAR. Abaixo estão alguns exemplos dos resultados esperados:

### Modelo Digital de Terreno (MDT)

O MDT representa a superfície do terreno, sem a vegetação. Ele é essencial para a normalização da nuvem de pontos e para a análise topográfica.

*(Placeholder para imagem de um MDT)*

### Modelo de Altura do Dossel (MDC)

O MDC representa a altura da vegetação acima do terreno. É útil para a visualização da estrutura da floresta e para a detecção de árvores individuais.

*(Placeholder para imagem de um MDC)*

### Detecção de Árvores

Os scripts de detecção de árvores irão gerar um arquivo de pontos (geralmente um *shapefile*) que marca a localização de cada árvore individual detectada.

*(Placeholder para imagem de um shapefile de árvores sobreposto a um MDC)*

## Visualização dos Resultados

Os resultados do processamento podem ser visualizados com uma variedade de softwares, incluindo:

-   **QGIS:** Um software GIS de código aberto que pode visualizar arquivos raster (`.asc`, `.tif`) e vetoriais (`.shp`).
-   **LAStools:** A ferramenta `lasview` pode ser usada para visualizar os arquivos `.las` e `.laz`.
-   **FUSION:** O próprio FUSION possui uma ferramenta de visualização para dados LiDAR.
-   **R:** Os resultados podem ser plotados e visualizados diretamente no R.

### Exemplo de Visualização no R

Você pode visualizar um Modelo Digital de Terreno (MDT) gerado pelo `lidR` com o seguinte código:

```r
# Carregue as bibliotecas necessárias
require(raster)
require(lidR)

# Carregue o catálogo de MDTs
dtm_ctg = readLAScatalog("./dtm/")

# Plote o MDT em 3D
plot_dtm3d(dtm_ctg, bg = "white")
```

## Contribuições

Contribuições para este repositório são bem-vindas. Se você tiver sugestões, correções ou novos scripts, sinta-se à vontade para abrir uma *issue* ou enviar um *pull request*.
