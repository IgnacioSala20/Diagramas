DUDAS:


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

<<<<<<< HEAD

*Esto es para la clase CambioEstado*
- buscar puntero a estado 
- obtener fecha y hora actual
- obtener datos necesarios para nuevo cambio de estado (empleado)
- buscar actual cambio de estado
- setear fecha fin al actual cambio de estado
- crear nuevo cambio de estado
### Solo si la clase principal(ej: EventoSismico) esta relacionada con estado 
- [setEstado a la clase que cambia de estado (selec:evento)] 
=======
[PorLasRelacionesSucedeEsto]
- Si quiero por ej: un dato del empleado, tengo que ir hasta usuario y luego a empleado
- Si quiero por ej: el estado del evento sismico, tengo que ir hasta el evento sismico y luego a su estado

[ObtencionDeDatos]
- Cuando tenes el puntero lo que podes hacer es ir a la entidad y pedirle los datos
- Cuando no tenes el puntero, tenes que ir a la entidad y pedirle el puntero de la entidad que queres recorriendo todas las entidades