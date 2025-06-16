# Avaliação para o Processo Seletivo de Estagiários Desenvolvedores da Metta Innovations

Esse repositório apresenta o enunciado, regras e objetivos da avaliação prática que os candidatos a estagiários desenvolvedores da Metta Innovations deverão cumprir e apresentar ao vivo na próxima etapa de entrevista online. Leia com atenção as seções abaixo e entre em contato com os e-mails [jose.sapienza@mettainnovations.com.br](mailto:jose.sapienza@mettainnovations.com.br) e [rafaelsm@mettainnovations.com.br](rafaelsm@mettainnovations.com.br) em caso de dúvidas.

## Objetivos

O candidato deve demostrar sua capacidade em estruturar um código para o problema técnico apresentado abaixo no prazo estipulado. É importante ressaltar que o candidato pode escolher a linguagem, bibliotecas e frameworks que serão aplicadas a partir de seu conhecimento pregresso ou motivações técnicas. Todavia, na seção [Sugestões de Tecnologias](#sugestões-tecnológicas) indicamos a combinação de algumas linguagens e bibliotecas a fim de orientação.

O candidato pode desenvolver a solução em seu computador pessoal utilizando um editor de sua preferência como o gratuito [VSCODE](https://code.visualstudio.com/), ou então em um framework na nuvem como [Google Colab](https://colab.research.google.com/), [Kaggle Notebooks](https://www.kaggle.com/code) ou [Hugging Face Spaces](https://huggingface.co/spaces).

### O que deve ser entregue?

Um link para um repositório público do tipo Git (GitLab, GitHub, entre outros) contendo, pelo menos:
- O código-fonte da aplicação documentado e bem estruturado com boas práticas de Orientação a Objetos.
- Um arquivo README.md com as orientações sobre como instalar as dependências e executar o código do repositório.
- Um arquivo ABOUT.md com uma explicação sobre a solução desenvolvida, abordagens aplicadas, justificativas e print screens de exemplo da aplicação rodando.
- Uma pasta ```output_results``` com o resultados do processamento do seu programa a partir dos dados de entrada fornecidos nesse repositório.

### Como deve ser entregue?

O candidato deve enviar um e-mail até a data e hora limite para [jose.sapienza@mettainnovations.com.br](mailto:jose.sapienza@mettainnovations.com.br) e [rafaelsm@mettainnovations.com.br](mailto:rafaelsm@mettainnovations.com.br) com o título "[Processo Seletivo] Estagiário de Desenvolvimento". Informe no corpo do e-mail o seu nome e a URL do seu repositório Git.

**Importante**: apenas serão consideradas as atualizações do repositório (i.e. _commits_) até a data limite de entrega. Todas as atualizações depois da data limite serão desconsiderados no processo de avaliação.

### Prazo de submissão da avaliação

As avaliações devem ser enviadas para os destinatários descritos acima até o **prazo limite de 23/06/2025 às 12:00**. Extensões de prazo não serão concedidas.

### O que será avaliado?

1) Qualidade da documentação do código.
2) Boas práticas de programação, em especial técnicas de Orientação a Objetos e organização em classes.
3) Soluções técnicas encontradas para resolver o problema proposto.
4) Clareza e qualidade do README.md e do ABOUT.md.
5) Sustentação oral sobre a solução que será realizada na entrevista online (limite de 10 minutos).
6) Qualidade visual e técnicas de UX (User eXperience) front-end apresentando os resultados.

## Problema proposto

Deve ser desenvolvido um código que processe todos os frames de um vídeo de entrada, execute uma rede neural que identifique pessoas no vídeo e registre algumas análises em JSONs de saída. Deve ser utilizada uma rede neural pré-treinada, ou seja, a avaliação não contempla o treinamento de redes neurais. Vide seção [Sugestões Tecnológicas](#sugestões-tecnológicas) para indicações de quais redes podem ser utilizadas.

A lógica alto-nível do que precisa ser desenvolvido é:
- Em um loop, leia cada frame do vídeo.
- Para cada frame, use a rede neural para identificar as pessoas presentes no frame.
- Leia o resultado da rede neural com as detecções e atualize as saídas solicitadas abaixo. As saídas precisam ser atualizadas ao final de cada frame.

### Saídas a serem geradas

Devem ser geradas três saídas na pasta ```output_results```:
- Um vídeo de saída contendo todos os frames do vídeo de entrada com as detecções das pessoas (i.e. bounding boxes) desenhadas frame a frame.
- Um JSON com o nome ```history.json``` contendo um array de objetos com o id do frame e a quantidade de pessoas detectadas para todos os frames do vídeo. Vide [Exemplo simples de processamento](#exemplo-simples-de-processamento) para a estrutura que o JSON precisa ter.
- Um JSON com o nome ```alerts.json``` contendo um array de objetos com o id do frame, id do alerta e a quantidade de pessoas para os frames onde a quantidade de pessoas é igual ou maior que um limiar de corte informado. Vide [Exemplo simples de processamento](#exemplo-simples-de-processamento) para a estrutura que o JSON precisa ter.

Os ids dos frames e dos alertas são inteiros autoincrementais, ou seja, 0, 1, 2, 3, 4, 5, ...

### GUI

A aplicação deve apresentar os resultados em uma Graphical User Interface (GUI) com o vídeo de saída e um gráfico apresentando a quantidade de pessoas (eixo Y) ao longo do frames (eixo X).

### Parâmetros de entrada

O código deve possuir, pelo menos, os seguintes parâmetros de entrada:
- O caminho (_path_) para o vídeo a ser processado.
- Um número inteiro com o limite de pessoas detectadas em um frame para se escrever um alerta em ```alerts.json```.

No caminho ```./sample/people-walking.mp4``` ([link](sample/people-walking.mp4)) desse repositório há um vídeo para ser usado como exemplo nos processamentos. Use um valor de limite de pessoas que gere um arquivo ```alerts.json``` com um array pelo pelo menos com 5 registros.

### Exemplo simples de processamento

A fim de explicação do problema que está sendo apresentado, vamos tomar um exemplo hipotético e bem simples. Suponha um vídeo com apenas 5 frames chamado ```./input/exemplo.mp4``` e um limiar de corte igual a ```2``` para se usar como regra para se inserir dados em ```alerts.json```. Os 5 frames são processados em loop, gerando ao final o seguinte ```history.json```:

```json
[
    {
        "id": 0,
        "count": 0
    },
    {
        "id": 1,
        "count": 1
    },
    {
        "id": 2,
        "count": 1
    },
    {
        "id": 3,
        "count": 2
    },
    {
        "id": 4,
        "count": 2
    }
]
```

Por sua vez, o arquivo ```alerts.json``` ficaria nesse exemplo simples:

```json
[
    {
        "id": 3,
        "count": 2
    },
    {
        "id": 4,
        "count": 2
    }
]
```

## Sugestões Tecnológicas

O candidato pode escolher o conjunto de linguagens, módulos e frameworks que achar melhor para resolver o desafio com base em sua experiência anterior, todavia é sugerido utilizar alguns conjuntos de soluções.

### Sugestão 1 - Python

A linguagem Python uma das melhores suítes de módulos em alto-nível para se trabalhar com Visão Computacional e Inteligência Artifical, além de frameworks online e formas de execução que não dependem de um computador com GPU para rodar a rede neural, por exemplo. Há módulos como transformers, ultralytics e torch com diferentes redes neurais treinadas que podem ser utilizadas para detectar pessoas e processar os resultados.

### Sugestão 2 - Javascript/NodeJS

Também é possível executar o desafio com NodeJS, principalmente com módulos como tfjs-node e coco-ssd. Outra alternativa é propor uma GUI sendo feito com JavaScript e o uso da rede neural com Python, por exemplo.

### Redes Neurais Treinadas

Hoje existem diferentes repositórios (Model Zoo) com diferentes redes neurais para detecção de pessoas. Citam-se aqui algumas entre as redes mais conhecidas para detecção de pessoas e outros tipos de objetos: YOLO, Grounding DINO, Faster R-CNN e RetinaNet. Dependendo da linguagem e dos módulos escolhidos pelo candidato, a compatibilidade com uma determinada rede treinada é melhor.

## Nota sobre o uso de redes generativas de texto (p.e. ChatGPT)

O uso de redes generativas de textos e códigos de programação como ChatGPT não é proibido, todavia os avaliadores levarão em conta a originalidade das propostas e a capacidade de sustentação oral.
