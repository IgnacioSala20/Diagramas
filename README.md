DUDAS:
      Si te dice, genera un PDF y lo muestra, es interfaz??
      Si te dice genera un PDF y lo descarga?
      Si te dice genera un PDF nomas

      Todo lo que sea generado por un pdf y que muestra y permite descargar y demas, esta sera una responsabilidad de lo qwue es la interfaz que lo genera, no es algo que le pertenece al gestor o pantalla
      Si dice que genera el pdf de igual modo lo mandaria a la interfaz, pero esto seria un error que no lo mostrase


      Los atributos que van por ej en Evento, tambien son los del select Evento
      Si, son respecto al evento, ya que este es un objeto del mismo

      Cuando tenemos un evento con varias Categorias, es decir Evento tiene un array con los punteros [1,2,3,4]
      Nosotros hacemos un getNombre()* a la clase con todas las categorias? O deberiamos hacer un loop preguntando
      si la categoria del evento es igual al de categoria, y si es asi pide el nombre
      EJEMPLO:
        group loop [Mientra haya categorias]
            SE --> C : esDelEvento()
            SE --> C : getNombre()
        end

      En este caso la entidad Categoria que contiene todas las entidades, estaria haciendo referencia a los punteros que tenemos en Evento seleccionado, por lo tanto hariamos solo un getNombre()* debido a que esa entidad que representa los muchos, serian los seleccionados,
      NOSOTROS NO DISTINGUIMOS LO QUE SON LOS SELECCIONADOS DE LO QUE SON LA ENTIDAD CON TODOS
      ENTONCES LA ENTIDAD QUE ESTA PINTADA, REPRESENTARIA NUESTROS 4 PUNTEROS DE CATEGORIA
      Preguntar por el de reportes de Campo
      EJEMPLO: 
        group loop [Mientras haya lotes para eso campos]
            CR --> C : esCampoSeleccionado() Aca verifico que el puntero del seleccionado con el de la entidad
            C --> L: 11.getNombreLote() y aqui le pido el nombre del lote a ese campo
        end

      EN ESTE CASO *NO* HARIA FALTA EL LOOP, YA QUE  IRIAMOS DESDE EL GESTOR A LA ENTIDAD CON TODOS LOS CAMPOS, EL CUAL REPRESENTARIA LOS CAMPOS QUE NOSOTROS SELECCIONAMOS, Y LUEGO IRIAMOS A LA ENTIDAD DE TODOS LOS LOTES, EN EL CUAL, CAMPO TIENE LOS PUNTEROS A LOTES, POR LO TANTO ESA ENTIDAD QUE REPRESENTA TODOS LOS LOTES, ESTARIA INDICANDO LOS PUNTEROS QUE TIENE CAMPO SOBRE LOTE

      PREGUNTAR SI CUANDO PONEMOS UNA INTERFAZ EXTERNA, EJ: IMPRESORA, LA CLASE VA EN EL DIAGRAMA DE CLASES CON SU MENSAJE CORRESPONDIENTE (Si, va en el diagrama de clases, ImpresorInforme ImpresorPedido, el metodo es el que le llega y como atributos pueden ir o no, dependiendo lo que le mandemos)

      la sesion va a tener, fecha y hora de inicio, y fecha de hora fin

      PREGUNTAR POR EL TEMA DE LA SELECCION MULTIPLE POR EJ DE CAMPOS, COMO SE MANEJA EN EL DIAGRAMA DE CLASES, VA COMO punterosCampo O LISTA CAMPOS (MISMA PREGUNTA PARA CUANDO ES MULTIPLE Y CUANDO ES SELECCION UNICA)

      PREGUNTAR POR GENERAR DIAGRAMACION de folklore, en el cual generamos la diagramacion como completada, pero en ningun lado dice que cambia el estado, ademas que es una salida, por lo tanto, esto seria una interfaz que genera y maneja todo el?

      Preguntar si es lo mismo hacer un obtenerClasificacion(self en lo que es la entidad o gestor) y luego getNombre a Clasificacion, o solo con getNombre es suficiente

      Preguntar por los loops cuando ingresan datos o seleccionan
      Seleccionar varios elementos, incluye adentro del loop el pedirSelccion...
      Mi pregunta eso, no hay un disparador para ese loop? EJ: el de PPAI de darOrden 

      No hace falta hacer el inicio de sesion, ya que es otro CU, podemos instanciar lo que es la sesion en el main y luego se lo pasamos al gestor

## ¿Cómo se maneja la selección múltiple de entidades en el sistema?
**Pregunta:**  
¿Cómo se maneja la selección múltiple de entidades en el sistema, especialmente cuando luego necesito buscar y procesar datos asociados a cada una de ellas?  
*Ejemplo: el sistema pide que se seleccionen más de un evento.*
**Respuesta:**
- Cuando hay una selección múltiple, el **gestor** (o **controlador**) mantiene una **lista** de todas las entidades seleccionadas.  
  Luego, se utiliza un **bucle (loop)** que recorre esa lista.  
  Por cada entidad seleccionada, se obtiene un **puntero o referencia** a su información completa dentro de la estructura de datos correspondiente.

- Por ejemplo, si el usuario selecciona **4 eventos sísmicos** y desea consultar su clasificación, el sistema recorre (con un loop que abarca la entidad `EventoSismico` y su `clasificación`) la lista de eventos seleccionados.  
  Para cada uno, busca su clasificación accediendo al objeto de datos completo a través de su puntero o referencia, y así se procesan uno por uno.

### En términos de implementación:
	punteroEntidadSeleccionada == punteroEntidadDatos



## ¿Cómo se maneja la acción de imprimir un reporte en el sistema?
**Pregunta:**  
¿Cómo se maneja la acción de imprimir un reporte en el sistema? ¿Se utiliza algún método como `pedirSeleccionImpresion()`?
**Respuesta:**

Para imprimir un reporte, el flujo generalmente **parte desde el gestor**.  
Este realiza un **self (auto-referencia)** para tomar los datos necesarios y luego invoca un **método o interfaz específica de impresión**.

Esta **interfaz o módulo de impresión** se encarga exclusivamente de **generar y mostrar el reporte**, de forma **desacoplada del resto de la lógica del sistema**.

Podría existir un método del tipo `pedirSeleccionImpresion()` que permita al usuario definir qué desea imprimir, y con esa selección, el gestor pasa los datos al componente de impresión.

Este enfoque mantiene la *responsabilidad separada*: 
	-El gestor organiza los datos
    - Y un componente externo especializado se encarga de la presentación e impresión.


## En el caso del ejercicio Línea Aérea, ¿cómo se contempla la notificación a los interesados una vez que se actualiza el estado del vuelo a "aterrizado"?

**Pregunta:**  
En el caso del ejercicio Línea Aérea, ¿cómo se contempla la notificación a los interesados una vez que se actualiza el estado del vuelo a "aterrizado"?
**Respuesta:**
Para notificar a los interesados tras la actualización del vuelo, el sistema implementa un **mecanismo de comunicación** con **interfaces específicas para cada tipo de interesado**.

### Interesados en este caso:
- Las **pantallas informativas del aeropuerto**  
- La **pantalla de consulta de vuelos del sitio web**

### Por lo tanto, el sistema debe contar con:
- Una **interfaz de notificación para el sitio web**, que permita **actualizar en tiempo real** el estado del vuelo mostrado en la web.

- Una **interfaz de notificación para las pantallas del aeropuerto**, que puede ser un **módulo o servicio** que sincroniza los datos con el **sistema local de señalización**.

Estas **interfaces actúan como puentes de comunicación** entre el **sistema principal (gestor de vuelos)** y los **sistemas externos encargados de mostrar la información**.

### Analogía conceptual
Este enfoque es similar a cómo el sistema se comunicaría con una **impresora**:  
a través de una **interfaz que abstrae el canal de comunicación**, manteniendo **bajo acoplamiento entre los componentes**.


### ACLARACIONES
- Los atributos se piden los datos que se necesitan para la secuencia, puede haber dependencia entre entidades
- En la implementacion podemos tener en el main todos los datos, en un array y luego se lo mandamos al gestor, cosa de evitar usar una BD

*Esto es para la clase CambioEstado*
- buscar puntero a estado 
- obtener fecha y hora actual
- obtener datos necesarios para nuevo cambio de estado (empleado)
- buscar actual cambio de estado
- setear fecha fin al actual cambio de estado
- crear nuevo cambio de estado
### Solo si la clase principal(ej: EventoSismico) esta relacionada con estado 
- [setEstado a la clase que cambia de estado (selec:evento)] 


[PorLasRelacionesSucedeEsto]
- Si quiero por ej: un dato del empleado, tengo que ir hasta usuario y luego a empleado
- Si quiero por ej: el estado del evento sismico, tengo que ir hasta el evento sismico y luego a su estado

[ObtencionDeDatos]
- Cuando tenes el puntero lo que podes hacer es ir a la entidad y pedirle los datos
- Cuando no tenes el puntero, tenes que ir a la entidad y pedirle el puntero de la entidad que queres recorriendo todas las entidades

### Preguntar si cuando pongo mostrarOrdenes y despues pongo pedirSeleccionDeOrdenes, siemopre va del gestor a la pantalla
- En este caso lo que se hace es poner un metodo que va de gestor a pantalla que sea mostrar y otro de gestor a pantalla que sea pedirSeleccionOrden

Debemos tener en la clase pantalla los botones de cancelar y confirmar

Hay que hacer al menos 2 alternativas de lo que es nuestro diagrama de secuencia
