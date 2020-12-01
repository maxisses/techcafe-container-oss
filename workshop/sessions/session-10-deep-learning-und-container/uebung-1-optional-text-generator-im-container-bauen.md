# Übung 1: \(optional\)Text Generator im Container bauen

In Übung 1 geht es darum mit einer GPT2 Library, welche Tensorflow nutzt ein Deep Learning Modell zu erstellen.

Der Code, welcher uns ein Neuronales Netz baut das selbstständig, neuartige und ..eigenwillige :\) Game of Thrones Skripte schreiben kann, liegt hier: [https://github.com/maxisses/GoT-Mining/tree/master/gpt2-got/gpt2-build](https://github.com/maxisses/GoT-Mining/tree/master/gpt2-got/gpt2-build)

Klont euch gerne das ganze Repo - und geht dann in den entsprechenden Unterordern gpt2-got/gpt2-build

```text
git clone https://github.com/maxisses/GoT-Mining.git
```

In diesem Ordner liegt eine Textdatei "GoT\_textonly.txt", welche das gesamte Game of Thrones Skript enthält und von dieser Website stammt: [https://genius.com/Game-of-thrones-winter-is-coming-annotated](https://genius.com/Game-of-thrones-winter-is-coming-annotated)

![](../../.gitbook/assets/image%20%28178%29.png)

Das Notebook um das Skript als \*.csv Datei von der Website zu scrapen liegt auch im repo. Das ist aber Out-of-Scope an dieser Stelle. Wir schauen uns jetzt erstmal an wie das python Skript zum Training bzw. Finetunen des Modells aussieht.

[https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/fb1412c3-a906-4ab1-a7a0-5745de86ce0e/view?access\_token=2c233034fd88fe01e1506ce7b6bcdcfffe86dedb9e8b055b92417c195ed23bda](https://dataplatform.cloud.ibm.com/analytics/notebooks/v2/fb1412c3-a906-4ab1-a7a0-5745de86ce0e/view?access_token=2c233034fd88fe01e1506ce7b6bcdcfffe86dedb9e8b055b92417c195ed23bda)

{% hint style="info" %}
Was ihr hier seht ist Transfer Learning, d.h. wir nutzen das bereits mit Tonnen von \(englischen\) Textdaten \(Wikipedia & Co.\)von OpenAI trainierte GPT2 Netz und "finetunen" es nun mit unserem eigenen Netz.
{% endhint %}

![](../../.gitbook/assets/image%20%28162%29.png)

Hier seht ihr einmal wie das Training inklusive voll ausgelasteter GPU abläuft. Damit das Modell etwas halbwegs sinnvolles ausspuckt sind hier 1000 Training-"Steps" eingebaut und 200 davon sind in 238 Sekunden abgelaufen \(Geforce RTX 2080 Super\). Aller 200 gibt es ein kleines Sample.

![](../../.gitbook/assets/image%20%28176%29.png)

Getreu unserem bisherigen Motto arbeiten wir natürlich mit Containern.

Wer möchte kann gerne in die Details schauen. Wir wollen uns hier auf das Dockerfile konzentrieren.

{% hint style="info" %}
Warum nun Deep & Maschine Learning im Container?

* man hat ständig neue Dependencies, die in bestimmten Versionen vorliegen müssen \(hier zB Tensorflow immer bestens abgestimmt auf CUDA\)
* diese können schnell mal GBs groß sein \(wie hier zB cuda, cudnn und tensorflow\)
* die Ausführung ist lokal anstrengend wenn man an mehreren Projekten arbeitet, denn insbesondere bei python gibt es verschiedene, verbreitete Möglichkeiten des Paketmgmts \(venv, pipenv, conda, ..\)
* man sein sein Projekt v.a. wegen der drei vorigen Punkte nicht vernüftig teilen kann

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
## models will be downloaded by the running container 
## according to below modelsize, if not copied into directly
# COPY models /models
COPY app.py /
RUN apt-get clean && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

ENV MODELSIZE="124M"

ENTRYPOINT ["python3", "-X", "utf8", "-u", "app.py"]
```

Um jetzt loszulegen auf der eigenen Maschine reichen 2 Befehle:

Repo wie oben beschrieben clonen, docker image bauen und ausführen. Wichtig ist darauf zu achten den checkpoint folder lokal zu mounten, denn das python Program schreibt das Modell in diesen Ordner und wir brauchen ihn später bei der Ausführung bzw. Anwendung \("Inferencing"\).

```text
docker build --file Dockerfile-GPU -t gpt2trainmodel .
docker run -v $PWD/checkpoint:/checkpoint gpt2trainmodel
```

Wer hat, der kann es natürlich mit GPU ausführen. Das führt je nach Einstellung auf dem eigenen System aber doch immer wieder zu Inkompatibilitäten, deshalb habe ich ein cpu-only Dockerfile daneben gelegt, welches man ebenfalls nutzen kann. Training dauert dann aber einige ... Stunden!!. :\)

```text
docker run --gpus all -v $PWD/checkpoint:/checkpoint gpt2trainmodel
```

