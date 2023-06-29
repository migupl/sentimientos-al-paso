# Sentimientos al paso

Una mirada a los sentimientos asociados a los '[Versos al paso](https://versosalpaso.madrid.es/)' que acompañan al viandante en los pasos de cebra de Madrid.

Se tomará como base la relación de frases en formato CSV de [versosalpaso.madrid.es.csv](https://github.com/jagedn/versosalpaso.madrid.es.csv).

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

Suerte, espero que te haya aportado.

## Licencia

[MIT license](http://www.opensource.org/licenses/mit-license.php)

[^1]: Se usa 'jupy-sentimiento-versos' como nombre del contenedor para separar este experimento de cualquier otro. La imagen define *jovyan* como el usuario no 'root' (uid=1000, gid=100) con privilegios completos sobre los directorios */home/jovyan/* y */opt/conda*.
