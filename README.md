# Contagem-Moedas
Este projeto é um sistema de visão computacional que detecta e classifica moedas brasileiras (1 Real, 50, 25, 10 e 5 centavos) em tempo real, usando a webcam, OpenCV e um modelo de inteligência artificial (Keras). Ele exibe o valor total das moedas detectadas na tela.

# Funcionalidades Principais
Detecção Automática: Identifica moedas em vídeo ao vivo da sua webcam.
Classificação Inteligente: Classifica moedas em 1 Real, 50, 25, 10 e 5 centavos usando um modelo de IA.
Contagem de Valor: Soma o valor das moedas detectadas e exibe o total.
Processamento Otimizado: Utiliza técnicas de pré-processamento de imagem e recortes precisos para melhorar a detecção e classificação.

# Como Rodar
1. Pré-requisitos
Certifique-se de ter Python e as seguintes bibliotecas instaladas:

  OpenCV: opencv-python
  NumPy: numpy
  Keras: keras==2.6.0
  TensorFlow: tensorflow==2.9.1

Você pode instalá-las com pip:
pip install opencv-python numpy keras==2.6.0 tensorflow==2.9.1
Importante: Use as versões especificadas de Keras e TensorFlow para garantir compatibilidade com o modelo de IA.

2. O Modelo de IA
Você precisa ter o arquivo do modelo Keras_model.h5 na mesma pasta do script Python. Este modelo é o "cérebro" que classifica as moedas.
3. Execução
Conecte sua webcam.

Abra seu terminal ou prompt de comando.

Navegue até a pasta onde salvou os arquivos do projeto.

Execute o script com o comando:

python seu_script_nome.py
(Substitua seu_script_nome.py pelo nome do seu arquivo, por exemplo, detector_moedas.py).

4. O que você verá
Duas janelas aparecerão:
IMG: Mostra a imagem da sua webcam com as moedas detectadas em um retângulo verde, sua classificação e o valor total em Reais.
IMG PRE: Exibe a imagem pré-processada (em preto e branco com as bordas), útil para entender como o sistema está "vendo" as moedas antes da detecção.

# Como Funciona
O script segue estes passos para cada quadro de vídeo:
Captura e Pré-processamento: A imagem é capturada, redimensionada e processada (desfoque, detecção de bordas Canny, dilatação e erosão) para isolar as bordas das moedas.
Detecção de Moedas: Contornos externos são encontrados na imagem pré-processada. Filtros de área e circularidade são aplicados para identificar objetos que realmente se parecem com moedas.
Recorte Otimizado: A região de cada moeda é recortada da imagem original. Um padding (margem) de 10 pixels é adicionado a este recorte. Isso garante que a moeda inteira seja capturada, mesmo com pequenas variações na detecção, o que é crucial para a precisão do modelo de IA.
Classificação com IA: O recorte de cada moeda é redimensionado e normalizado, então enviado ao modelo Keras_model.h5 para prever a qual denominação de moeda ela pertence.
Exibição e Soma: Se a confiança da previsão for alta (acima de 70%), a classe da moeda é exibida. O valor é somado ao total geral, que é mostrado no canto superior direito da tela.
