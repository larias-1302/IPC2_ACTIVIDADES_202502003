# Parte 1: Investigación Teórica y Análisis de Casos

## 1. El Límite de las Rotaciones Simples y Desbalanceo en "Zig-Zag"

### El Problema Cruzado

Los árboles AVL son estructuras de datos autoequilibradas que garantizan que la diferencia de altura entre los subárboles izquierdo y derecho de cualquier nodo no exceda una unidad. Esta diferencia se representa mediante el Factor de Equilibrio (FE), el cual se calcula como la diferencia entre las alturas de los subárboles.

Cuando una operación de inserción provoca que un nodo alcance un factor de equilibrio fuera del rango permitido (-1, 0 o +1), es necesario aplicar rotaciones para restaurar el balance. Sin embargo, las rotaciones simples únicamente son efectivas cuando el crecimiento ocurre en la misma dirección que el desbalance. Cuando el crecimiento se produce en direcciones opuestas aparece el denominado caso cruzado o patrón "Zig-Zag".

En estas situaciones, una rotación simple no corrige completamente la estructura debido a que el nodo causante del desequilibrio se encuentra en una posición intermedia entre el abuelo y el hijo. Como consecuencia, la rotación simple únicamente desplaza el problema hacia otra parte del árbol sin lograr una distribución adecuada de alturas.

Para resolver este escenario se utilizan las rotaciones dobles, las cuales consisten en la ejecución secuencial de dos rotaciones simples. Estas operaciones permiten reorganizar la jerarquía de nodos de manera que el elemento intermedio ocupe la posición central y se restablezca el equilibrio estructural.

Desde el punto de vista matemático, una Rotación Doble Izquierda-Derecha (RID) se activa cuando:

- El nodo desbalanceado presenta un Factor de Equilibrio igual a -2.
- Su hijo izquierdo presenta un Factor de Equilibrio igual a +1.

Esta combinación indica que el crecimiento responsable del desequilibrio ocurrió inicialmente hacia la izquierda y posteriormente hacia la derecha, generando un patrón que no puede corregirse mediante una única rotación.

El objetivo final de la rotación doble es reducir la altura del subárbol afectado, distribuir correctamente los nodos y restablecer factores de equilibrio válidos en todos los elementos involucrados.

### Principio DRY (Don't Repeat Yourself)

El principio DRY constituye una de las bases fundamentales de la ingeniería de software moderna. Su propósito es evitar la duplicación innecesaria de lógica dentro de un sistema, promoviendo la reutilización de componentes ya existentes.

En la implementación de árboles AVL, las rotaciones dobles pueden construirse reutilizando las operaciones de rotación simple previamente desarrolladas. Esta estrategia aporta múltiples beneficios técnicos.

En primer lugar, reduce significativamente la cantidad de código necesario para implementar el algoritmo, lo que disminuye la probabilidad de errores relacionados con la manipulación de referencias y estructuras enlazadas. Al reutilizar funciones previamente probadas también se incrementa la confiabilidad del sistema.

Además, la reutilización mejora la mantenibilidad del código. Si una rotación simple requiere una corrección o una optimización futura, los cambios se reflejarán automáticamente en las rotaciones compuestas que dependan de ella. Esto evita modificaciones repetitivas y reduce los costos de mantenimiento.

Otro beneficio importante es la claridad conceptual. Al construir una rotación doble como la combinación de dos rotaciones simples, el algoritmo refleja directamente la teoría utilizada en el balanceo AVL, facilitando la comprensión por parte de otros desarrolladores y mejorando la documentación interna del proyecto.

Por estas razones, la aplicación del principio DRY en la implementación de árboles AVL representa una práctica recomendada desde el punto de vista de la calidad del software y del diseño orientado a la reutilización.

---

## 2. Fundamentos de Arquitectura Web y Protocolo HTTP

### El Modelo Cliente-Servidor

El modelo cliente-servidor es una arquitectura distribuida que divide las responsabilidades de un sistema en dos componentes principales: los clientes y los servidores.

El cliente es la entidad encargada de iniciar la comunicación mediante una solicitud de información o de ejecución de una operación. Por su parte, el servidor es responsable de procesar la petición recibida, ejecutar la lógica de negocio correspondiente y generar una respuesta adecuada.

La comunicación entre ambos componentes se realiza generalmente a través del protocolo HTTP sobre una red TCP/IP. Este mecanismo permite que aplicaciones ubicadas en diferentes dispositivos y sistemas operativos puedan intercambiar información de manera estandarizada.

Cuando un cliente solicita un recurso, genera una petición HTTP que contiene información como el método utilizado, la dirección del recurso solicitado, encabezados de control y, en algunos casos, datos adicionales en el cuerpo de la solicitud. Esta petición es enviada al servidor, donde es interpretada y procesada.

Posteriormente, el servidor genera una respuesta HTTP que incluye un código de estado, encabezados descriptivos y, opcionalmente, un cuerpo con los datos solicitados. Dichos datos suelen intercambiarse en formatos estructurados como JSON o XML debido a su facilidad de procesamiento por distintas plataformas tecnológicas.

Este modelo ofrece ventajas importantes como escalabilidad, modularidad, independencia entre componentes y facilidad de mantenimiento, convirtiéndose en la base de la mayoría de aplicaciones web modernas y servicios distribuidos.

### Semántica de Operaciones

El protocolo HTTP define distintos métodos para expresar la intención de una operación. Entre los más utilizados se encuentran GET y POST, los cuales poseen comportamientos claramente diferenciados.

El método GET está diseñado para la recuperación de información. Su principal característica es que no debe modificar el estado interno del servidor. Debido a esta propiedad se considera una operación segura e idempotente, ya que múltiples ejecuciones producen el mismo resultado sin generar efectos secundarios. Las solicitudes GET suelen emplearse para consultar recursos existentes y obtener representaciones de datos almacenados.

Por otro lado, el método POST está orientado al envío de información hacia el servidor con el propósito de crear recursos nuevos o ejecutar operaciones que impliquen cambios en el estado del sistema. A diferencia de GET, POST no es necesariamente idempotente, ya que múltiples solicitudes pueden producir resultados distintos o generar nuevos registros.

Dentro del contexto de estructuras de datos expuestas mediante APIs, el método GET resulta apropiado para recuperar el estado actual de una estructura, visualizar su contenido o consultar información almacenada. En contraste, el método POST es adecuado para operaciones que impliquen inserciones, modificaciones o transformaciones de dicha estructura, debido a que estas acciones alteran el estado interno mantenido por el servidor.

La correcta utilización de estos métodos permite respetar los principios arquitectónicos de los servicios web, mejorar la interoperabilidad entre sistemas y facilitar el diseño de interfaces consistentes y predecibles para los consumidores de una API.
