# Übung 1: \(optional\)Text Generator im Container bauen

In Übung 1 geht es darum mit einer GPT2 Library, welche Tensorflow nutzt ein Deep Learning Modell zu erstellen.

{% hint style="info" %}
Was ihr hier seht ist Transfer Learning, d.h. wir nutzen das bereits mit Tonnen von Textdaten trainierte GPT2 Netz und "finetunen" es nun mit unserem eigenen Netz. 
{% endhint %}

![](../../.gitbook/assets/image%20%28162%29.png)

Hier seht ihr einmal wie das Training inklusive voll ausgelasteter GPU abläuft. Damit das Modell etwas halbwegs sinnvolles ausspuckt sind hier 1000 "Steps" eingebaut und 200 davon sind in 238 Sekunden abgelaufen. 

![](../../.gitbook/assets/image%20%28176%29.png)

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

Repo wie oben beschrieben clonen, docker image bauen und ausführen. Wichtig ist darauf zu achten den checkpoint folder lokal zu mounten, denn das python Program schreibt das Modell in diesen Ordner und wir brauchen ihn später bei der Ausführung bzw. Anwendung \("Inferencing"\).

```text
docker build --file Dockerfile-GPU -t gpugpt2builder .
docker run -v $PWD/checkpoint:/checkpoint gpugpt2builder
```

Wer hat, der kann es natürlich mit GPU ausführen. Das führt je nach Einstellung auf dem eigenen System aber doch immer wieder zu Inkompatibilitäten, deshalb habe ich ein cpu-only Dockerfile daneben gelegt, welches man ebenfalls nutzen kann. Training dauert dann aber einige Stunden. 

```text
docker run --gpus all -v $PWD/checkpoint:/checkpoint gpugpt2builder
```

