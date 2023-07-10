# Sentimientos al paso

Una mirada a los sentimientos asociados a los '[Versos al paso](https://versosalpaso.madrid.es/)' que acompañan al viandante en los pasos de cebra de Madrid.

Se tomará como base la relación de frases en formato CSV de [versosalpaso.madrid.es.csv](https://github.com/jagedn/versosalpaso.madrid.es.csv).

## Stack a utilizar

Para el análisis de sentimientos se utilizará un stack Python para la ejecución de Cuadernos Jupyter. Más concretamente la imagen [jupyter/minimal-notebook](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/selecting.html#jupyter-minimal-notebook) ejecutado como un contenedor con [Docker CLI](https://jupyter-docker-stacks.readthedocs.io/en/latest/using/running.html).

Para ejecutar el contenedor en modo interactivo[^1] se puede usar

```bash
$ docker run -it -p 8888:8888 --name jupy-sentimiento-versos -v "$PWD/notebooks":/home/jovyan jupyter/minimal-notebook:latest
Entered start.sh with args: jupyter lab
Executing the command: jupyter lab
...
    
    To access the server, open this file in a browser:
        file:///home/jovyan/.local/share/jupyter/runtime/jpserver-7-open.html
    Or copy and paste one of these URLs:
        http://8c9f88170ebf:8888/lab?token=cd4244c9cf09993eaf6edea2b65540e242db9444847dbbe4
        http://127.0.0.1:8888/lab?token=cd4244c9cf09993eaf6edea2b65540e242db9444847dbbe4

```

Pulsando 'Ctrl-C' dos veces se para la ejecución del servidor pero deja intacto el contendor en disco para un posterior rearranque

```bash
$ docker start --attach jupy-sentimiento-versos
Entered start.sh with args: jupyter lab
Executing the command: jupyter lab
...
    To access the server, open this file in a browser:
        file:///home/jovyan/.local/share/jupyter/runtime/jpserver-7-open.html
    Or copy and paste one of these URLs:
        http://16630a0d866f:8888/lab?token=7b2f13ad3887d835b370097bdba7f8df125f58ee2a027b95
        http://127.0.0.1:8888/lab?token=7b2f13ad3887d835b370097bdba7f8df125f58ee2a027b95
```

o borrado permanente.

```bash
$ docker rm jupy-sentimiento-versos
jupy-sentimiento-versos
```

## Clasificación por el sentimiento asociado

Inspirado en el breve curso de una hora [ChatGPT Prompt Engineering for Developers](https://www.deeplearning.ai/short-courses/chatgpt-prompt-engineering-for-developers/) por DeepLearning.AI se explora en un proceso iterativo la pregunta que mejor puede ayudarnos en esta [clasificación](#sentimientos-al-paso) tal y como se pude ver en el cuaderno Jupyter '[Iterative Prompt using Chat-GPT](./docs/Iterative%20Prompt%20using%20Chat-GPT.pdf)'.

En dicha exploración se utiliza el modelo 'gpt-3.5-turbo' con la [API ChatCompletion](https://platform.openai.com/docs/guides/gpt/chat-completions-api). Para el propósito de [clasificación](#sentimientos-al-paso) de todos los 'versos' se utilizara la [API Completions](https://platform.openai.com/docs/guides/gpt/completions-api) con el modelo '[text-davinci-003](https://platform.openai.com/docs/models/gpt-3-5)'.

## Explorando la tokenización

El modelo '[text-davinci-003](https://platform.openai.com/docs/models/gpt-3-5) define un máximo de 4.000 tokens para la petición y la respuesta que se realice con OpenAI.

En el cuaderno Jupyter '[Explore tokenization](./docs/Explore%20tokenization.pdf)' se explora el límite de tokens a utilizar en cada petición así como el procedimiento de agrupamiento de los versos por este límite para la petición a la [API Completions](https://platform.openai.com/docs/guides/gpt/completions-api)

## Añadir el sentimiento asociado a cada verso

El proceso de obtención del sentimiento asociado a cada uno de los versos se define en el cuaderno Jupiter 'Classify verses by sentiment' y el resultado se guardará en un nuevo fichero CSV [versosalpaso_sentiment_text-davinci-003.csv](./notebooks/output/versosalpaso_sentiment_text-davinci-003.csv). Este fichero es copia del original [versos al paso](./notebooks/input/versosalpaso.csv) al que se le ha añadido la columna 'sentiment' con los posibles valores: '*positive*'; '*neutral*'; or, '*negative*'.




Suerte, espero que te haya aportado.

## Licencia

[MIT license](http://www.opensource.org/licenses/mit-license.php)

[^1]: Se usa 'jupy-sentimiento-versos' como nombre del contenedor para separar este experimento de cualquier otro. La imagen define *jovyan* como el usuario no 'root' (uid=1000, gid=100) con privilegios completos sobre los directorios */home/jovyan/* y */opt/conda*.
