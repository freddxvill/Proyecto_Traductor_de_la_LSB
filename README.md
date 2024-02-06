# Traductor del deletreo manual de la Lengua de Señas Boliviana a texto

Programa traductor de la lengua se señas boliviana a texto  utilizando Pytorch y PyQt5. El programa fue entrenado para reconocer el alfabeto dactilologico boliviano, numeros del 0-10 y otras 19 palabras, con el fin de desarrollar un modelo que sea capaz predecir tanto señas estaticas como dinámicas. El tamaño del conjunto de datos fue de 5800 secuencias capturadas con ayuda de Mediapipe. El modelo fue desarrollado utilizando el framework de aprendizaje profundo [Pytorch](https://pytorch.org/) y [Pytorch lightning](https://lightning.ai/). L interfaz de usuario se creo usando la libreria de PyQt5, que puede ser actualizado a la version 6.

Se utilizo el bloque `Transformer Encoder` de la arquitectura Transformers publicado en el paper [Attention Is All You Need](https://proceedings.neurips.cc/paper_files/paper/2017/file/3f5ee243547dee91fbd053c1c4a845aa-Paper.pdf) para realizar la clasificación de secuencias, que en este caso se captura la posicion de las manos y la pose del cuerpo utilizando la camara frontal del computador con OpenCV y Mediapipe. No se entrena al modelo con los puntos o coordenadas obtenidos sino que se realizo el proceso de Data Augmentation para obtener nuevas relaciones o caracteristicas. Se calculo distancias dentro de las manos y fuera de ellas, asi como tambien angulos. 

El programa puede ser ejecutado con Python o mediante un ejecutable .exe para windows sin necesidad de instalar librerias externas. Para su ejecución con Python seguir el proceso de instalación.

## Instalación

- Instalar [Python](https://www.python.org/downloads/). La version utilizada en este proyecto fue Python 3.10.10
- Descargar o clonar el codigo en una carpeta con git.

```bash
git clone https://github.com/freddxvill/Proyecto_Traductor_de_la_LSB
```
- Crear un **entorno virtual** de python dentro de la carpeta. Con [virtualenv](https://virtualenv.pypa.io/en/latest/) utilizar el siguiente comando:

```bash
virtualenv venv
```
- **Activa** el entorno. En Windows con Powershell:

```bash
.\venv\Scripts\activate
```
- Instalar las dependencias del archivo **requirements.txt** en el entorno.

```bash
pip install -r requirements.txt
```

## Ejecución del programa

Ejecutar el archivo Traductor_LSB.py (con el entorno activado)

```bash
python Traductor_LSB.py
```

Se mostrara la interfaz de usuario del programa.

[![GUI-LSB.png](https://i.postimg.cc/PfzPJpXT/GUI-LSB.png)](https://postimg.cc/9z0WNfwn)

## Funcionamiento del programa

El programa inicia pulsando el boton iniciar. Se debe seleccionar la camara, 0 indica que se usara la camara interna del computador en otro caso sera una camara externa conectada. El programa captura a una persona realizando una seña durante 30 fotogramas, ya sea una seña estatica o dinámica. Luego de los 30 fotogramas capturados, los datos se envian al modelo para realizar la prediccion de la seña. El program muestra debajo la letra,número o palabra predicha. El texto predicho se va concatenando formando asi oraciones mas largas. 

## Notas

- Se puede implementar un pipeline de reentrenamiento. Esto se sigue desarrollando y lo tendra en una version futura.
- Las datos de utilizados se guardaron en formato Zarr, ya que maneja y reduce el tamaño de arreglos multidimensionales que alimentan al modelo. Las etiquetas se guardaron en formato numpy.
