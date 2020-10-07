# Übung 1: \(optional\)Text Generator im Container bauen

In Übung 1 geht es darum mit einer GPT2 Library, welche Tensorflow nutzt ein Deep Learning Modell zu erstellen.

Getreu unserem bisherigen Motto arbeiten wir natürlich mit Containern. 



* Dockerfile erläutern
* warum ist es super das im container zu machen: system bleibt sauber, versionsproblematik, verteilbarkeit ...
* * herausforderungen: machine learning besteht aus zwei teilen training und inferencing

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



[https://github.com/maxisses/GoT-Mining/tree/master/gpt2-got/gpt2-build](https://github.com/maxisses/GoT-Mining/tree/master/gpt2-got/gpt2-build)

