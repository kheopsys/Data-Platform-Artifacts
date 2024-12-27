FROM apache/airflow:2.10.4

USER root

# Installation de JDK, Wget et Scala
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        default-jdk \
        scala \
        wget \
        vim \
        procps \
    && apt-get autoremove -yqq --purge \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Installer les dépendances PostgreSQL
RUN apt-get update && \
    apt-get install -y libpq-dev python3.11-dev build-essential \
    && rm -rf /var/lib/apt/lists/*


USER airflow

# Définition de JAVA_HOME
ENV JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64

# Copie du fichier requirements.txt dans l'image
COPY requirements.txt /requirements.txt

# Installation des paquets Python répertoriés dans requirements.txt sans mise en cache
RUN pip install --no-cache-dir -r /requirements.txt

USER root

RUN  mkdir -p /airflow/dags /airflow/logs /airflow/plugins /airflow/config

USER airflow

RUN echo -e "AIRFLOW_UID=$(id -u)\nAIRFLOW_GID=0" > .env
