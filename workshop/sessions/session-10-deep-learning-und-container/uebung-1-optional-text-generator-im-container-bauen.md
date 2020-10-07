# Übung 1: \(optional\)Text Generator im Container bauen

In Übung 1 geht es darum mit einer GPT2 Library, welche Tensorflow nutzt ein Deep Learning Modell zu erstellen.

Getreu unserem bisherigen Motto arbeiten wir natürlich mit Containern. 

Der Code, welcher uns ein Neuronales Netz baut das selbstständig, neuartige und ..eigenwillige Game of Thrones Skripte schreiben kann, liegt hier: [https://github.com/maxisses/GoT-Mining/tree/master/gpt2-got/gpt2-build](https://github.com/maxisses/GoT-Mining/tree/master/gpt2-got/gpt2-build)

Wer möchte kann gerne in die Details schauen. Wir wollen uns hier auf das Dockerfile konzentrieren und einen Blick in das python Skript werfen.

{% hint style="info" %}
Quitessenz für Deep & Maschine Learning im Container ist, dass man

* ständig neue Dependencies hat, die in bestimmten Versionen vorliegen müssen \(hier zB Tensorflow\)
* diese können schnell mal GBs groß sein \(wie hier zB cuda, cudnn und tensorflow\)
* die Ausführung lokal anstrengend ist wenn man an mehreren Projekten arbeitet, denn insbesondere bei python gibt es verschiedene, verbreitete Möglichkeiten des Paketmgmts \(venv, pipenv, conda, ..\)
* sein Projekt v.a. wegen der drei vorigen Punkte nicht vernüftig teilen kann

Container lösen das, halten das System sauber und machen den Code portabel.
{% endhint %}

Hier sehen wir das Beispiel.

```text
FROM tensorflow/tensorflow:1.15.0-gpu-py3

RUN apt-get -y update && apt-get -y install gcc

COPY requirements-docker.txt requirements.txt
RUN pip install -r requirements.txt

WORKDIR /
COPY GoT_textonly.txt /GoT_textonly.txt
##models will be downloaded by the running container according to below modelsize
COPY models /models
COPY app.py /

ENV MODELSIZE="124M"

RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENTRYPOINT ["python3", "-X", "utf8", "app.py"]
```

Um jetzt loszulegen auf der eigenen Maschine reichen 2 Befehle:

Clone the repo, build the docker image and run it with mount of the "checkpoint" folder of the container to your disk.

```text
docker build -t yourgpt2builder .
docker run -v $PWD/checkpoint:/checkpoint yourgpt2builder
```

The checkpoint folder is where the model will be put.

The container is based on tensorflow-gpu==1.15.0 so you can run it with gpus enabled.

```text
docker run --gpus all -v /pathonmysys/:/checkpoint yourgpt2builder
```

