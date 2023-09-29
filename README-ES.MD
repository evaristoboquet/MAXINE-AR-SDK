# README
## SDK NVIDIA MAXINE AR: código fuente API y aplicaciones de muestra

NVIDIA MAXINE AR SDK ofrece seguimiento y modelado de caras en 3D en tiempo real basado en IA, así como una estimación de la pose del cuerpo basada en una alimentación de cámara web estándar. Los desarrolladores pueden crear efectos AR únicos, como superponer el contenido 3D en una cara, generar caracteres 3D e interacciones virtuales en tiempo real. El SDK funciona con unidades de procesamiento de gráficos NVIDIA ( GPU ) con núcleos tensores y, como resultado, el rendimiento del algoritmo se acelera enormemente y se reduce la latencia.

El SDK tiene las siguientes características:

- **Seguimiento de la cara**,  que detecta, localiza y rastrea rostros humanos en imágenes o videos mediante el uso de cuadros delimitadores.
- **Seguimiento de punto de referencia facial**, que predice y rastrea las ubicaciones de píxeles de los puntos de referencia faciales humanos utilizando 68 o 126 puntos de referencia. Los 68 puntos de referencia faciales detectados siguen la información de márgenes de 68 puntos Multi-PIE en [anotaciones en puntos faciales](https://ibug.doc.ic.ac.uk/resources/facial-point-annotations/). El detector de 126 puntos históricos puede predecir más puntos en las mejillas, los ojos y las líneas de risa. Además, rastrea la pose de la cabeza y la deformación facial debido al movimiento de la cabeza y la expresión en tres grados de libertad en tiempo real.
- **Malla facial**, que reconstruye y rastrea un rostro humano a través de una malla 3D, así como su pose de cabeza, desde los puntos de referencia faciales proporcionados.
- **Estimación de la dosis del cuerpo**, que predice y rastrea 34 puntos clave del cuerpo humano, con ángulos articulares, en 2D y 3D. También es compatible con el seguimiento en varias personas.
- **Contacto visual**,  que simula el contacto visual al estimar y alinear la mirada con la cámara para mejorar el compromiso en la comunicación por video.
- **Estimación de expresión facial**, que estima los coeficientes de expresión facial ( forma de mezcla ) de los puntos de referencia faciales proporcionados.
<p align="center">
<img src="https://github.com/NVIDIA/MAXINE-AR-SDK/blob/master/resources/ar_001.png" alt="Face tracking" width="320" height="180"/>
<img src="https://github.com/NVIDIA/MAXINE-AR-SDK/blob/master/resources/ar_002.png" alt="Face landmark tracking - 68 pts" width="320" height="180" />
</p><p align="center">
<img src="https://github.com/NVIDIA/MAXINE-AR-SDK/blob/master/resources/ar_003.png" alt="Face landmark tracking - 126 pts" width="320" height="180"/>
<img src="https://github.com/NVIDIA/MAXINE-AR-SDK/blob/master/resources/ar_004.png" alt="Face mesh" width="320" height="180"/>
</p>
</p><p align="center">
<img src="https://github.com/NVIDIA/MAXINE-AR-SDK/blob/master/resources/ar_005.png" alt="Body Pose estimation" width="480" height="270"/>
</p><p align="center">
<img src="https://github.com/NVIDIA/MAXINE-AR-SDK/blob/master/resources/ar_006.png" alt="Eye contact" width="640" height="237"/>
</p><p align="center">
<img src="https://github.com/NVIDIA/MAXINE-AR-SDK/blob/master/resources/ar_007.png" alt="Face Expression Estimation" width="640" height="175"/>
</p>

El SDK proporciona cuatro aplicaciones de muestra que demuestran las características enumeradas anteriormente en tiempo real mediante el uso de una cámara web o videos fuera de línea.
- **FaceTrack App** que demuestra el seguimiento de la cara, el seguimiento de puntos de referencia y las características de seguimiento de malla de la cara.
- **BodyTrack App** que demuestra la característica de estimación de la postura del cuerpo.
- **GazeRedirect App** que demuestra la función Eye Contact.
- **ExpressionApp** que demuestra la función de estimación de expresión facial.

NVIDIA MAXINE AR SDK se distribuye en las siguientes partes:

- Este repositorio de código abierto que incluye el [API SDK y código fuente de enlace proxyAPI SDK y código fuente de enlace proxy](https://github.com/NVIDIA/MAXINE-AR-SDK/tree/master/nvar), y [aplicaciones de muestra y sus bibliotecas de dependencia](https://github.com/NVIDIA/MAXINE-AR-SDK/tree/master/samples).
- Un instalador alojado en [NVIDIA Maxine Página de redistribuibles para usuarios finales](https://www.nvidia.com/broadcast-sdk-resources) que instala las DLL de SDK, los modelos y las bibliotecas de dependencia de SDK.

Por favor refiérase a la [Guía del sistema SDK](https://docs.nvidia.com/deeplearning/maxine/ar-sdk-system-guide/index.html) para configurar e integrar el SDK, compilar y ejecutar las aplicaciones de muestra. Por favor visite el [SDK NVIDIA MAXINE AR](https://developer.nvidia.com/maxine-getting-started) página web para más información sobre el SDK.

## Requisitos del sistema
El SDK es compatible con GPU NVIDIA que se basan en la arquitectura NVIDIA ® Turing ™, Ampere ™ o Ada ™ y tienen núcleos tensores.

* Sistema operativo Windows compatible: Windows 10 de 64 bits o posterior
* Microsoft Visual Studio: 2017 ( MSVC15.0 ) o posterior
* CMake: v3.12 o posterior
* Controlador de gráficos NVIDIA para Windows: 511.65 o posterior

## Pautas de marca NVIDIA MAXINE
Si integra un SDK NVIDIA MAXINE dentro de su producto, siga las pautas de marca requeridas que están disponibles [aquí](
https://www.nvidia.com/maxine-sdk-guidelines)

## Compilación de la aplicación de muestra

### Pasos

El repositorio de código abierto incluye el código fuente para construir la aplicación de muestra y un archivo proxy nvARProxy.cpp para permitir la compilación sin vincular explícitamente contra la SDK DLL.

**Nota: Para descargar los modelos y las dependencias de tiempo de ejecución requeridas por las funciones, debe ejecutar el [Instalador SDK.](https://www.nvidia.com/broadcast-sdk-resources).**

1.	En la carpeta raíz del código fuente descargado, inicie la GUI de CMake y especifique la carpeta fuente y una carpeta de compilación para los archivos binarios.
* Para la carpeta de origen, asegúrese de que la ruta termine en OSS.
* Para la carpeta de compilación, asegúrese de que la ruta termine en OSS / build.
2.  Use CMake para configurar y generar el archivo de solución de Visual Studio.
* Haz clic en Configurar.
* Cuando se le solicite confirmar que CMake puede crear la carpeta de compilación, haga clic en Aceptar.
* Seleccione Visual Studio para el generador y x64 para la plataforma.
* Para completar la configuración del archivo de solución de Visual Studio, haga clic en Finalizar.
* Para generar el archivo de solución de Visual Studio, haga clic en Generar.
* Verifique que la carpeta de compilación contenga el archivo NvAR_SDK.sln.
3.  Use Visual Studio para generar el archivo FaceTrack.exe, BodyTrack.exe, GazeRedirect.exe o ExpressionApp.exe a partir del archivo NvAR_SDK.sln.
*	En CMake, para abrir Visual Studio, haga clic en Abrir proyecto.
* En Visual Studio, seleccione Construir > Construir solución.

## Documentación

Consulte las guías de documentación en línea: -
* [Guía de programación de SDK de NVIDIA AR](https://docs.nvidia.com/deeplearning/maxine/ar-sdk-programming-guide/index.html)
* [Guía del sistema SDK de NVIDIA AR](https://docs.nvidia.com/deeplearning/maxine/ar-sdk-system-guide/index.html)
* [Guía API de NvCVImage](https://docs.nvidia.com/deeplearning/maxine/nvcvimage-api-guide/index.html)

Las versiones en PDF de estas guías también están disponibles en las siguientes ubicaciones: - 
* [Guía de programación de SDK de NVIDIA AR](https://docs.nvidia.com/deeplearning/maxine/pdf/ar-sdk-programming-guide.pdf)
* [Guía del sistema SDK de NVIDIA AR](https://docs.nvidia.com/deeplearning/maxine/pdf/ar-sdk-system-guide.pdf)
* [Guía API de NvCVImage](https://docs.nvidia.com/deeplearning/maxine/pdf/nvcvimage-api-guide.pdf)

