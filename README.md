<p align="center">
<img src="https://github.com/user-attachments/assets/df5a0b14-2842-4af8-901a-3b5c22fe57ab" alt="Logo FIUBA" width="600" align="center"/>
</p>
<h1 align="center"> Repositorio de Desafios PNL 15co2024 </h1>
<h2>Alumna Sofia Speri</h2>
Este es mi portafolio de Desafíos realizados durante la cursada de Procesamiento Natural del Lenguaje de la Especialización en Inteligencia Artificial de la FIUBA. 

<h3>Desafio 1: Vectorización de texto y modelo de clasificación Naïve Bayes con el dataset 20 newsgroups</h3>
<p>En este desafío se vectorizó el dataset 20 newagroup a través de <i>TfidfVectorizer</i> para luego poder tomar ciertos documentos del corpus al hacer y buscar sus documentos más relacionados a través de la Similitud de coseno. Por otro lado, se entrenaron dos modelos de clasifiación para los documentos de <i> NB -Multinomial y Complement- </i> obteniendo un F1-Score de 0.68 y 0.69 respecitvamente. Por último, se traspudo la matriz documento-término y se buscó la similiridad entre 5 palabras y sus 5 más similares. </p>

Notbook y documentos del Desafío: [Desafío 1](./Desafio_1/)

<h3>Desafio 2: Custom embedddings con Gensim</h3>
<p>En este desafío se buscó crear vectores de embeddings con Gensim. El Dataset utilizado son un grupo de preguntas y respuestas de FAQ's medical question-answer pairs created from 12 NIH websites (e.g. cancer.gov, niddk.nih.gov, GARD, MedlinePlus Health Topics). Fuente: https://www.kaggle.com/datasets/jpmiller/layoutlm.
A partir del dataset se entrenaron los embeddings usando modelo <i>Word2Vec</i> y se buscaron por un lado las palabras más similares para <i>Sangre, Mujer y Gen</i> y por otro lado se probaron 2 analogías:
  - La analogía para "hombre" de la relación "mujer-mama" es: [('prostate', 0.4577924311161041)]
  - La analogía para "vejiga" de la relación "sangre-vaso" es: [('urine', 0.4657147228717804)]
Por último se graficaron los vectores con reducción de dimensiones en 2 y 3d, y se obtuvieron los datos para la garficación con projector.tensorflow.org lo cuál mostró, incluisve con reduccipin de dimensionalidad a través de PCA o TSNE, cercanía entre los conceptos que tienen similaridad. Por ejemlo: Childohood-chlren-growth-hormones; o sunscreen-protecting-uv-sun-avoid-exposure
</p>

Notbook y documentos del Desafío: [Desafío 2](./Desafio_2/)

<h3>Desafio 3: Modelo de lenguaje con tokenización por caracteres y palabras</h3>
<p>Este desafío está dividido en 2 notebooks, por un lado la tokenización por caracteres y otro por palabras. Se utilizó el mismo dataset que el Desafío 2.
<b>Tokenización por caracteres</b>
Para la tokenización por carcateres se definió un tamaño de contexto de 150 carcateres y se realizó la tokenización. Una vez obtenidos los tokens se definió el modelo, usando una primera capa de Catgory Encoding y Time Distributed que convierte los tokens en vectores One-Hot y luego se usó una capa SimpleRNN con dropout de 0.1 y una capa Densa cn activación Softmax. Se entrenó el modelo para 10 épocas, observando descenso de la perplejidad a lo largo del entrenamiento. Se realzó el ensayo de generación del proximo carcater, que se muestran en las imágenes dentro del repositorio; y  se hizo predicción con Beam Search con modo estocástico para el <i>input: the cancer is obteniendo como resultado: the cancer is a clinical trials t'</i>
Si bien las predicciónes no son las mejores posibles en cuánto a significado, se logró un modelo que logra separar bien palabras y espacios a pesaar de ser entrenado con un corpus acotado.
<b>Tokenización por palabras</b>
Para la tokenización por palabras se realizó el procesamiento del modelo para todas oraciones con menos de 300 palabras y se tomó un contexto máximo de 176. Se hizo la tokenización y se definió un modelo de 1 capa de embeddings, 1 capa LSTM, una capa de dropout (0.2) y la capa densa. S realizó el entrenamiento para 15 épocas con un batch de 256, observando un descenso de la perplejidad durante el entrenamiento.
Una vez obtenido el modelo se hizo la prueba de generacipon de secuencias. Input = 'WHAT IS THE RISK' obteniendo OUTPUT = 'WHAT IS THE RISK of adult soft tissue sarcoma a sign of adult soft'
Por último se hizo predicción con Beam Search con modo estocástico obteniendo la siguiente salida para el mismo INPUT anterior: what is the risk of lung cancer lung cancer is
</p>

Notbook y documentos del Desafío: [Desafío 3](./Desafio_3/)

<h3>Desafio 4: LSTM Bot QA</h3>
<p>En este desafío se buscó construir un BOT para responder preguntas de usuario (QA) a partir de datos disponibles del challenge ConvAI2 (Conversational Intelligence Challenge 2) de conversaciones en inglés. Se utilizó el modelo <i>cc.en.300.bin</i> de FastText (https://fasttext.cc/docs/en/crawl-vectors.html) para obtener los embeddings del inglés. 
Se entrenó un modelo con el esquema encoder-decoder usando para ambos una capa de embeddings, una capa LSTM y una capa densa. El modelo se entrenó para 50 épocas obteniendo un accuracy de entrenamiento de 0.86 y de validacion de 0.74. Y luego se realizó la inferencia para distitos inputs de entrada:
Input: nice do you have any hobbies 
  Response: i like to play video games  
Input: How old are you?
  Response: i am 32 i am 32
Input: Where do yoy come from?
  Response: i do not know what to say
Input: Do you have any pet?
  Response: i have two dogs
</p>

Notbook y documentos del Desafío: [Desafío 4](./Desafio_4/)

<h3>Desafio 5: Bert Sentiment Analysis</h3>
<p>El desafío es entrenar un modelo BERT para clasificación de sentimientos a partir de un datset de opiniones de usuarios que definen un score de 1 a 5 sobre su experiencia. El dataset elegido está desbalanceado, teniendo mayor cantidaad de opiniones de categoria 3 o Neutra que del resto. 
El modelo utilizado es  TFBertModel.from_pretrained("bert-base-uncased") cargado a partir de pesos pre-entrenados. En este desafío se trabajó solo con Transfer Learning, pero uno de los próximos pasos es poder hacer Fine Tuning para mejores resultados. Los valores de accuracy de entrenaimiento y validación están en torno a 0.42.
Se realizaron 3 ensayos:
- Input = "I love this app!"
  - Clasificación: very positive
- Input = "I hate this page!"
  - Clasificación: very negative
- Input = "Some things are good but it could be better in UX"
  - Clasificación: neutral
</p>

Notbook y documentos del Desafío: [Desafío 5](./Desafío_5/)

<h2>Contacto</h2>


Por cualquier consulta o comentario, pueden contactarme a [sofia.speri@gmail.com](mailto:sofia.speri@gmail.com)
