# Utiliza la imagen oficial de Spark 4.1.1 como base
FROM almondsh/almond:latest

USER root

# Instalación de dependencias del sistema
RUN apt-get update && apt-get install -y \
    git \
    nano \
    openjdk-17-jdk \
    python3-pip \
    python3-dev \
    && apt-get clean

ENV JAVA_TOOL_OPTIONS="--add-opens=java.base/sun.nio.ch=ALL-UNNAMED \
                       --add-opens=java.base/java.nio=ALL-UNNAMED \
                       --add-opens=java.base/java.lang=ALL-UNNAMED \
                       --add-opens=java.base/java.lang.invoke=ALL-UNNAMED \
                       --add-opens=java.base/java.util=ALL-UNNAMED"

# Instalar librerías de datos y el kernel de Jupyter para Python
RUN /opt/conda/bin/pip install --no-cache-dir \
    pandas \
    numpy \
    pyspark \
    matplotlib \
    seaborn \ 
    sklearn \ 
    ipykernel
    
# Registrar el kernel de Python en el Jupyter de la imagen
RUN /opt/conda/bin/python -m ipykernel install --user --name python3 --display-name "Python 3 (Conda)"
# RUN python3 -m ipykernel install --user --name python3 --display-name "Python 3 (PySpark)"
    
# Instalar el gestor de dependencias de Scala (Coursier)
RUN curl -fL -o /usr/local/bin/cs.gz https://github.com/coursier/launchers/raw/master/cs-x86_64-pc-linux.gz
RUN gunzip /usr/local/bin/cs.gz
RUN chmod +x /usr/local/bin/cs
RUN /usr/local/bin/cs install scala:2.13.18 
RUN /usr/local/bin/cs install scalac:2.13.18
RUN rm -rf /root/.cache/coursier

# Registrar el kernel de Scala2.13.18 para que VS Code lo detecte
USER jovyan
RUN /usr/local/bin/cs launch --use-bootstrap almond --scala 2.13.18 -- --install --id "scala21318" --display-name "Scala 2.13.18"
# Machacamos fichero configuración para corregir problema de la libreria KRYO 
# COPY ./kernel.json /home/jovyan/.local/share/jupyter/kernels/scala21318/kernel.json

# USER root
# RUN rm -rf /root/.cache/coursier
