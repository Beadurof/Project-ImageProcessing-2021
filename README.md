# Image colorization (from Grayscale to RGB)

## Membros do projeto
- Lucas Sobral Fontes Cardoso
- Ewerton Patrick Silva do Amaral
- Marcelo Temoteo de Castro

## Objetivos do projeto (Abstract)

  Esse projeto busca utilizar aprendizado de máquina, utilizando um modelo para transformar imagens originalmente em escala de cinza em imagens colorizadas. Usaremos uma base de dados pública com imagens com duas versões, colorizadas e em escalas de cinza, ou transformaremos imagens colorizadas para preto e branco para poder utilizar as mesmas no treinamento do modelo. Uma vez que o modelo tenha sido treinado, utilizaremos imagens em preto e branco para poder gerar versões colorizadas das mesmas. Normalmente é necessário a assistência humana para colorização de imagens, uma aplicação desse projeto é automatizar o processo de colorização de imagens **buscando reduzir** a perda de informação. 
  
   <img src="https://github.com/Beadurof/Project-ImageProcessing-2021/blob/main/example0-grayscale.jpg" width="200" height="200" /> <img src="https://github.com/Beadurof/Project-ImageProcessing-2021/blob/main/example0-colorized.jpg" width="200" height="200" />
  <img src="https://github.com/Beadurof/Project-ImageProcessing-2021/blob/main/example1-grayscale.jpg" width="200" height="200" /> <img src="https://github.com/Beadurof/Project-ImageProcessing-2021/blob/main/example1-colorized.jpg" width="200" height="200" />
  <img src="https://github.com/Beadurof/Project-ImageProcessing-2021/blob/main/example2-grayscale.jpg" width="200" height="200" /> <img src="https://github.com/Beadurof/Project-ImageProcessing-2021/blob/main/example2-colorized.jpg" width="200" height="200" />
  
## Descrição da imagem de entrada
  As imagens foram obtidas no [kaggle](https://www.kaggle.com/theblackmamba31/landscape-image-colorization), nele temos uma pasta com um conjunto de imagens panoramicas coloridas contendo ruas, edifícios, montanhas, geleiras, árvores e entre outras coisas, as imagens correspondentes em escalas de cinzas estão separadas em outra pasta. Será utilizada apenas a pasta que contem imagens coloridas, a partir dessas imagens obteremos as imagens correspondentes em escalas de cinzas em uma etapa do próprio código. As imagens estão com tamanho de 150x150.

## Descrição dos passos
  - Redimensionaremos a imagens para o tamanho de 256x256
  - Etapa associada a análise de cor: convertemos a imagem para Lab pois assim as reduzimos o número de canais que representam cor, sendo 3 em RGB para 2 em Lab. Por consequencia essa etapa de conversão para Lab reduz a complexidade do problema permitindo a colorização das imagens até mesmo com redes mais simples
  - A partir da conversão para Lab, obtemos o canal L de luminosidade para obtenção da imagem em escala de cinza que será usada como entrada no modelo de rede neural. Já os outros 2 canais (ab), que contem informação de cor, serão utilizadas para avaliar o modelo durante o treinamento.
  - Pensamos em explorar alguns modelos de redes neurais para avaliar o impacto na colorização das imagens. Os modelos testados serão redes neurais convolucionais, que combinam técnicas de processamento de imagem com aprendizado de redes neurais. Para o problema de colorização consideramos utilizar os seguintes tipos de camadas:
    - Camadas de convolução 2D: Ao invés de ajustar pesos de uma função, como é feito em redes neurais tradicionais, neste tipo de camada são ajustados os valores de filtros que são aplicados na imagem da mesma forma que os filtros observados na disciplina. Em cada camada, diversos filtros são ajustados e tem como objetivo extrair características importantes da imagem que não são conhecidas, como encontrar a melhor cor.
    - Camadas de Max Pooling: Esta camada consiste em técnicas de diminuição da resolução da imagem. Este tipo de processo é importante para o treinamento de redes neurais em aplicações de imagem, pois permitem reduzir o custo computacional do treinamento. Espera-se que com o treinamento e a redução de dimensões seja adquirido as cores desejadas na imagem, embora seja reduzido a informação dessas cores. Esta redução de dimensão é feita aplicando um filtro de Max, onde apenas o valor máximo dos dados, na janela do filtro, seja apresentado no resultado.
    - Camadas de upsampling: Essas camadas incrementam a resolução dos dados, buscando retornar a dimensão original da imagem de entrada, permitindo que as cores selecionadas pela rede sejam atribuidas novamente a cada pixel da imagem de entrada.
  - Utilizaremos o RMSE para estimar o erro obtido entre a imagem colorizada pelo modelo e imagem original, sendo que essas duas imagens estarão no espaço de cor Lab. 
  - Converteremos a imagem em RGB depois para a exibição dos resultados.
  
  
  Após a colorização e avaliação dos resultados, pretendemos estudar a possibilidade de inclusão do erro gaussiano nas imagens de treinamento como uma forma de aperfeiçoar o modelo. Seguiremos essa linha de estudo, pois ao nos aprofundar mais sobre o tema de colorização vimos que esse método pode melhorar a predição dos resultados colorização das imagens.

## Resultados obtidos

- Com 9 imagens de treinamento e 1 de teste
  <img src="https://github.com/Beadurof/Project-ImageProcessing-2021/blob/main/out1.jpg" width="400" height="400" /> <img src="https://github.com/Beadurof/Project-ImageProcessing-2021/blob/main/out1.jpg" width="400" height="400" />


