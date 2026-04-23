# Utiliza la imagen oficial de Spark 4.1.1 como base
FROM almondsh/almond:latest

USER root

# Instalación de dependencias del sistema y Jupyter
RUN apt-get update && apt-get install -y \
    git \
    openjdk-17-jdk 

# Instalación de Coursier (gestor de dependencias de Scala) y Almond
# Almond 0.14.1+ es compatible con Scala 2.13, requerida para Spark 4.x
# RUN curl -fL https://github.com | gzip -d > cs && \
#     chmod +x cs && \
#     ./cs launch almond:0.14.1 -- --install && \
#     rm cs

RUN curl -fL -o /usr/local/bin/cs.gz https://github.com/coursier/launchers/raw/master/cs-x86_64-pc-linux.gz
RUN gunzip /usr/local/bin/cs.gz
RUN chmod +x /usr/local/bin/cs

RUN /usr/local/bin/cs install scala:2.13.18 
RUN /usr/local/bin/cs install scalac:2.13.18

USER jovyan
RUN /usr/local/bin/cs launch --use-bootstrap almond --scala 2.13.18 -- --install --id "scala21318" --display-name "Scala 2.13.18"

USER root
RUN rm -rf /root/.cache/coursier
