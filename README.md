---
Com certeza! Aqui está o conteúdo do `README.md` já formatado e pronto para você colar diretamente no GitHub.

---

# Detector de Moedas em Tempo Real

Este projeto é um sistema de visão computacional que detecta e classifica moedas brasileiras (1 Real, 50, 25, 10 e 5 centavos) em tempo real. Ele utiliza sua webcam, OpenCV para processamento de imagem e um modelo de inteligência artificial (Keras) para identificação. O valor total das moedas detectadas é exibido na tela.

---

## Funcionalidades

* **Detecção Automática**: Identifica moedas em tempo real através do feed de vídeo da sua webcam.
* **Classificação Inteligente**: Classifica as moedas em suas respectivas denominações (1 Real, 50, 25, 10 e 5 centavos) utilizando um modelo de IA pré-treinado.
* **Contagem de Valor**: Calcula e exibe o valor monetário total das moedas detectadas.
* **Processamento Otimizado**: Emprega técnicas de pré-processamento de imagem (como desfoque, detecção de bordas e operações morfológicas) e recortes de imagem com margem (padding) para otimizar a detecção de contornos e a precisão da classificação pelo modelo de IA.

---

## Requisitos

Certifique-se de ter o **Python** instalado, junto com as seguintes bibliotecas:

* **OpenCV**: `opencv-python`
* **NumPy**: `numpy`
* **Keras**: `keras==2.6.0`
* **TensorFlow**: `tensorflow==2.9.1`

Você pode instalá-las facilmente via pip:

```bash
pip install opencv-python numpy keras==2.6.0 tensorflow==2.9.1
```

**Nota Importante**: As versões específicas de Keras e TensorFlow (`2.6.0` e `2.9.1`, respectivamente) são recomendadas para garantir a compatibilidade com o modelo de IA pré-treinado (`Keras_model.h5`).

---

## Como Usar

### 1. Configure seu Ambiente

* Tenha o arquivo do modelo de inteligência artificial, **`Keras_model.h5`**, na mesma pasta do seu script Python (`.py`). Este arquivo é essencial para a classificação das moedas.
* Conecte uma **webcam** ao seu computador.

### 2. Execute o Projeto

1.  Abra seu terminal ou prompt de comando.
2.  Navegue até o diretório onde você salvou os arquivos do projeto.
3.  Execute o script Python usando o comando:

    ```bash
    python seu_script_principal.py
    ```
    (Substitua `seu_script_principal.py` pelo nome do seu arquivo Python, por exemplo, `detector_moedas.py`).

### 3. Visualização

Ao executar o script, duas janelas serão abertas:

* **`IMG`**: Exibirá o vídeo da sua webcam. Moedas detectadas serão marcadas com um retângulo verde e sua classificação. O valor total acumulado será mostrado no canto superior direito.
* **`IMG PRE`**: Mostrará a imagem pré-processada (bordas detectadas em branco sobre um fundo preto), o que é útil para visualizar como o sistema está detectando os contornos antes da classificação.

---

## Estrutura do Código (Visão Geral)

O script funciona processando cada frame do vídeo da seguinte forma:

1.  **`preProcess(img)`**: Esta função aplica desfoque Gaussiano e o algoritmo de bordas Canny. Em seguida, usa operações morfológicas (dilatação e erosão) para refinar as bordas, preparando a imagem para a detecção de contornos mais limpos.
2.  **`DetectarMoeda(img)`**: Recebe um recorte de uma possível moeda. Ela redimensiona e normaliza a imagem para o formato esperado pelo modelo de IA. Então, o modelo faz a previsão, retornando a classe da moeda e a confiança dessa previsão.
3.  **Loop Principal**:
    * Captura frames da webcam e os redimensiona.
    * Aplica `preProcess` para obter as bordas.
    * Usa `cv2.findContours` para detectar os contornos externos.
    * Filtra os contornos por **área** (ignorando ruídos pequenos) e **circularidade** (focando em objetos redondos).
    * Para cada contorno que se assemelha a uma moeda, calcula uma **caixa delimitadora com padding**. Este recorte expandido é crucial para garantir que a moeda inteira seja enviada para o modelo de IA, melhorando a estabilidade da classificação.
    * Chama `DetectarMoeda` com o recorte otimizado.
    * Se a confiança da classificação for alta (acima de 70%), a classe da moeda é exibida na tela e seu valor é adicionado à soma total.
    * As janelas de visualização são atualizadas.

---
