# Training a Quantum Model on a Real Data Set - NUTI
En este repositorio se realizará un símil del desempeño de modelos entrenados usando el aprendizaje clásico y el aprendizaje cuántico. 

Lo primero que se hace es adecuar el computador para que cuente con las librería necesarias, como ya tengo instalado Python y algunas librerías de ML, sólo me falta instalar las que sean de Qiskit usando el PowerShell de Windows.

![image](https://user-images.githubusercontent.com/63861040/227810647-02e2da78-3bf5-410a-9c8f-487a40f1c970.png)

Se instala qiskit visualization dado que se trabajará con Jupyter Notebook.

![image](https://user-images.githubusercontent.com/63861040/227810727-e24f6eb8-4fe0-4a2d-9320-61bada7cff87.png)

Y finalmente se instala qiskit especificamente para Machine Learning.

![image](https://user-images.githubusercontent.com/63861040/227810761-c33f262b-2d06-4bec-aa9b-d639bae2da93.png)

Habiendo finalizado la instalación de qiskit se procede a seleccionar el tutorial de interés que para este caso es el “Entrenamiento de un Modelo Cuántico en un conjunto de Datos Real”.

El tutorial demostrará cómo entrenar un modelo de aprendizaje automático cuántico para abordar un problema de clasificación. A lo largo del notebook se entrenan cinco modelos de ML, dos modelos clásicos de ML y tres modelos cuánticos de ML. El fin de esto es comparar la precisión de cada modelo y obtener conclusiones al respecto.

El notebook se compone de 24 entradas las cuales serán explicadas a continuación.

1. Se importa el conjunto de datos que se utilizará para los entrenamientos de los modelos.
2. Se describe el conjunto de datos para tener el contexto real de los datos.
3. Se declaran las características y las clases de Iris que existen en el conjunto de datos.
4. Se normalizan los datos para trabajar con valores entre 0 y 1. Esto es una buena práctica para entrenar modelos.
5. Se grafican las características por pares para analizar si hay alguna correlación observable entre ellas. Aquí se puede observar que las características de las clases de iris 1 y 2 se entrelazan en la mayoría de las gráficas mientras que los datos muestran que las características de la clase 0 se separan de las características de las otras dos clases.

![image](https://user-images.githubusercontent.com/63861040/227811203-5a39603d-1d97-446b-812d-f404e7408f20.png)

6. Se realiza la división del conjunto de datos de modo que el 80% sea para entrenamiento y el 20% para las pruebas del modelo entrenado.
7. Se selecciona el modelo de ML Support Vector Machine que es apropiado para tareas de clasificación. En esta entrada ocurre el entrenamiento del modelo.
8. Se calcula la precisión del modelo entrenado utilizando los mismos datos de entrenamiento y los datos de prueba. Se observa que se logra una precisión del 97% con los datos de prueba.

![image](https://user-images.githubusercontent.com/63861040/227811419-3e9f1e39-0394-4eff-8950-b145746140a3.png)

9. Ahora, se procede a seleccionar el modelo cuántico que se quiere entrenar, para este caso se selecciona el modelo clasificador cuántico variacional (VQC). En esta entrada particular, se declara el mapa de características definiendo que su dimensión sea de 4 considerando que es el número de características de nuestro conjunto de datos. El mapa de características luce así.

![image](https://user-images.githubusercontent.com/63861040/227811534-d04ede44-7930-4326-af9a-70ae995605d6.png)

10. También es necesario declarar el circuito cuántico parametrizado que se utilizará. Este paso es importante dado que en el modelo clásico los datos se almacenan en bits, pero para entrenar el modelo cuántico es necesario que los datos se almacenen en qubits. El circuito o ansatz que se utilizará en este caso es "RealAmplitud" de la librería de Qitskit. En esta imagen se presenta el circuito que se utilizará para el entrenamiento.

![image](https://user-images.githubusercontent.com/63861040/227811713-bc067b1d-4a13-4f10-9e89-f1f6efbd207f.png)

11. Otro elemento importante es el optimizador, necesario para minimizar la función objetivo. como argumento recibe la cantidad de iteraciones que debe hacer en busca de optimizar la función objetivo. 
12. Adicionalmente, se debe indicar si el entrenamiento se realizará utilizando un computador cuántico simulador o real. Para este caso se usará una simulación.
13. Se define una función encargada de graficar la función objetivo en cada iteración del optimizador.
14. En este entrada ocurre el entrenamiento del modelo, se define inicialmente el modelo que se utilizará y finalmente es entrenado con los datos de entrenamiento que se definieron. La gráfica siguiente muestra como iba cambiando el valor de la función objetivo conforme iba aumentando las iteraciones. 

![image](https://user-images.githubusercontent.com/63861040/227812204-5f9e41ac-415c-4c24-b50f-b8366e6016f2.png)

La idea es que el valor de la función objetivo se acerce a 1, si su comportamiento comienza a ser plano quiere decir que adicionar más iteraciones no mejorará el modelo. En este caso apenas sobre la iteración 100 comenzaba a aplanarse por lo que 100 iteraciones es un buen valor para este caso. 

15. En esta entrada se evalúa la precisión del modelo cuántico entrenado, se observa que alcanza un 87% de precisión media utilizando el conjunto de datos de prueba.

![image](https://user-images.githubusercontent.com/63861040/227812380-ea8a62aa-e534-4041-82e7-e53ce0449cb1.png)

16. A partir de esta entrada se busca reducir el número de características del conjunto de datos por lo que se aplica una transformación PCA a las características para lograrlo. En la siguiente imagen se grafican los datos con una característica en cada eje para analizar la distribución de los datos luego de la transformación. 

![image](https://user-images.githubusercontent.com/63861040/227812454-26721149-18fc-403e-8836-cc3703649eed.png)

17. Se realiza en entrenamiento del modelo clásico ahora con sólo dos características y se evalúa su precisión. Se ve reducida respecto al primer modelo entrenado pero sigue siendo alta.

![image](https://user-images.githubusercontent.com/63861040/227812842-9fd1c3f5-007d-4567-b55b-3f711d7232bd.png)

18. Ahora, se hace lo propio con el modelo cuántico, se define en este caso el nuevo mapa de características luego del cambio y se calcula así mismo el ansatz teniendo en cuenta que el número de qubits ahora será de dos.
19. Se declara el optimizador COBYLA ahora configurando sólo 40 iteraciones.
20. Se entrena de nuevo el modelo cuántico con los nuevos parametros declarados observándose ahora que la función objetivo llega a aplanarse apenas con 22 iteraciones. 

![image](https://user-images.githubusercontent.com/63861040/227813021-38b30427-6b0b-410b-a65c-90ab12a71777.png)

21. Para este caso la precisión se reduce considerablemente hasta el 63% si lo analizamos con el conjunto de prueba.

![image](https://user-images.githubusercontent.com/63861040/227813152-0de848cc-34ac-471c-9559-b1621a728594.png)

22. La prueba final consiste en cambiar el circuito cuántico parametrizado o ansatz por el "EfficientSU2". Se declara de nuevo los parametros con el nuevo ansatz y se entrena el modelo de nuevo. Aquí se observa que la función objetivo fluctua mucho alrededor de las 40 iteraciones, esto quiere decir que con 10 o 20 iteraciones más se podría mejorar el valor de la función objetivo. 

![image](https://user-images.githubusercontent.com/63861040/227813473-4c74a922-c2f8-4c46-9ddf-496e4fa8aa28.png)

23. Se calcula la precisión para este nuevo modelo evidenciándose una mejoría alcanzando un 67% con el conjunto de datos de prueba. 

![image](https://user-images.githubusercontent.com/63861040/227813537-2dcea72b-bbfc-4896-bfc7-184a48c35574.png)

24. Finalmente, en la última entrada se muestra la precisión de los modelos entrenados concluyéndose que con la tecnología actual los modelos clásicos de ML tienen un mejor desempeño tanto en tiempo como en precisión. Aún así, el primer modelo cuántico entrenado mostró una precisión aceptable en la práctica. 

![image](https://user-images.githubusercontent.com/63861040/227813661-b8df8f5f-0f7a-4c5a-b726-00ab34ed521a.png)
