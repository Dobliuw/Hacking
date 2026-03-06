# AI

La **Inteligencia Artificial** (**AI**) es un *campo de la informática* enfocado en *desarrollar sistemas* capaces de realizar tareas que requieren inteligencia humana, como *aprender*, *razonar*, *percibir* y *tomar decisiones*.

Utiliza algoritmos, redes nueronales y grandes cantidades de datos para identificar patrones y mejorar su precisión con el tiempo. Algunas de las caracteristicas que podemos encontrar en esta son:

- *Perception*: Interpreta datos sensoriales como imágenes, audio o señales.
- *Reasoning*: Trabaja con lógica, reglas o patrones para llegar a conclusiones.
- *Learning*: Permite que los sistemas mejoren su rendimiento usando datos.
- *Robotic*: Combinada con cuerpos físicos, permite que un agente tome acciones en el mundo real.

----
# History

La siguiente imagen represente una línea temporal conceptual del desarrollo de la Inteligencia Artificial, mostrando cómo la disciplina evolucionó en varias etapas con diferentes enfoques técnicos y paradigmas computacionales.

Cada etapa surge como respuesta a *limitaciones técnicas o conceptuales de la anterior*.

![[Pasted image 20260305162154.png]]

###### Simbolic AI (1950s - 1970s)

La **IA Simbólica** fue el primer enfoque dominante en inteligencia artifical. Se basaba en la idea de que la inteligencia puede moldearse mediante símbolos y reglas lógicas explícitas.

Este paradigma parte de una premisa fuerte: 

> Si el conocimiento humano puede representarse formalmente, una máquina puede razonar sobre él.

Los sistemas se construían mediante:

- Lógica formal.
- Sistemas de reglas (if-then).
- Representaciones simbólicas del conocimiento.
- Búsqueda en espacios de estados.


A nivel técnico, muchos sistemas se implementaban en lenguajes como *Lisp* y *Prolog*, ya que estos lengguajes facilitaban manipular listas, árboles y expresiones lógicas, estructuras ideales para representar conocimiento simbólico.

> [!error] Main problem
> El *problema principal* fue el **Knowledge Bottleneck**: Introducir manualmente todo el conocimiento necesario era extremadamente costoso y poco práctico.

###### Expert Systems (1970s - 1980s)

Los **Sistemas Expertos** fueron una evolución directa de la IA simbólica. En lugar de intentar construir inteligencia general, se enfocaban en *dominios específicos*.

La arquitectura típica incluía:

- *Kwnoledge Base*: Reflas definidas por expertos humanos.
- *Inference Engine*: Motor que aplicaba reglas.
- *Working Memory*: Hechos conocidos en ese momento.

Un sistema famoso de este tipo fue *MYCIN*, el cual diagnosticaba infecciones bacterianas utilizando cientos de reglas médicas.

> [!error] Main problem
> Dentro de las limitaciones más importantes, se presentaban las siguientes:
> - Difícil mantenimiento de reglas.
> - Incapacidad de aprender.
> - Explosión combinatoria en reglas complejas.
> 
> Esto llevó al siguiente problema histórico.

###### AI Winters (End 1970s & 1980s)

Los **AI Winters** fueron *periodos donde la inversión en IA colapsó*. Las principales causas fueron:

1. Expectativas exageradas.
2. Limitaciones computacionales.
3. Resultados prácticos pobres.

Muchos sistemas prometían capacidades que el hardware de la época no podía soportar.

> [!error] Main problem
> Tecnologías (Software y hardware como GPUs) que simplemente no existían aún, dando como resultado que gobiernos e industrias retiraran el financiamiento.

###### Machine Learning (1990s - 2010)

En este punto ocurre un cambio conceptual enorme, en lugar de programar reglas, los investigadores empiezan a desarrollar un *aprendizaje automático*, que permite a los sistemas aprender y mejorar automáticamente a través de la experiencia y los datos, sin ser programadas explícitamente para cada tarea. Utiliza algoritmos para identifiar patrones en grandes volúmenes de datos yrealizar predicciones.

> [!danger] Main problem
> El principal problema del **Machine Learning** (**ML**) fue la necesidad de la ingenieria de características manual. Esto ya que los expertos humanos debían identificar, extraer y seleccionar manulamente qué características de los datos eran relevantes para que el algoritmo pudiera aprender. (Ejemplo, definir uqé formas o colores distinguen a un objeto de una imagen).

###### Deep Learning (~2012)

El **Deep Learning** nace tras que los factores como GPU, datasets grandes y mejora de algoritmos de entrenamiento converjan. Se desarrollan e implementan redes neuronales con múltiples capas, permitiendo a las máquinas aprender patrones complejos, reconocer imágenes y procesar lenguaje de forma autónoma sin programación explícita.

Las arquitecturas típicas incluyen:

- CNNs (Convolutional Neural Networks).
- RNNs (Recurrent Neural Networks).
- Transformers.

> [!danger] Main problem
> Incapacidad de las arquitecturas tradicionales para procesar secuencias largas de datos de manera eficiente y paralela, dando lugar a problemas conocidos como *Vanishing Gradient* evitando que el modelo recordara correctamente el contexto inicial de cualquier conversación.

###### LLMs (~2018)

Los **Largue Language Models** (**LLMs**) son modelos de deep learning diseñados para entender, generar y manipular lenaguje humano de forma coherente y contextualmente relevante. A día de hoy, estos modelos son la tecnología base que permite el funcionaineto de herramientas mundialmente conocidas y utilizadas como ChatGPT, Claude, Gemini, entre otras.

Su base es la arquitectura *Transformer* y se entrenan prediciendo la siguiente palabra en enromes corpus de texto. Dando así lugar a nuevas capacidades emergentes:

- Razonamiento aproimado. 
- Generación de código.
- Análisis de texto.
- Planificación.
 
-----

