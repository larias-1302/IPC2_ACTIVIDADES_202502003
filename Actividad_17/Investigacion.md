# Fundamentación Teórica y Análisis Crítico

## El Tránsito hacia los Sistemas Distribuidos y Multi-Capa

### La Limitación del Monolito Local

Cuando la interfaz de usuario, la lógica de negocio y el almacenamiento de datos se encuentran en una única máquina física, la aplicación presenta problemas de escalabilidad y mantenimiento. Si varios usuarios necesitan acceder simultáneamente a la información, los recursos del equipo pueden agotarse rápidamente. Además, la sincronización de datos se vuelve complicada cuando existen múltiples copias del sistema en diferentes computadoras. Cualquier fallo en la máquina provoca la interrupción total del servicio.

### Distinción Crítica (Layers vs. Tiers)

**Capas (Layers):** Son divisiones lógicas dentro del código fuente. Organizan responsabilidades como presentación, negocio y acceso a datos.

**Niveles (Tiers):** Son divisiones físicas de la infraestructura. Cada nivel puede ejecutarse en servidores distintos conectados mediante una red.

Por lo tanto, las capas representan una separación lógica del software, mientras que los niveles representan una separación física del hardware y los servicios.

### Responsabilidades en la Arquitectura de 3 Niveles

#### Nivel 1: Capa de Presentación (Presentation Tier)

Su función es interactuar con el usuario, mostrar información y capturar datos de entrada. Generalmente utiliza tecnologías como HTML, CSS, JavaScript y Razor Views en ASP.NET Core.

#### Nivel 2: Capa de Aplicación o Negocio (Application Tier)

Contiene las reglas de negocio, validaciones y procesamiento de información. Actúa como intermediaria entre la interfaz y la base de datos. En .NET suele implementarse mediante controladores, servicios y lógica empresarial.

#### Nivel 3: Capa de Datos (Data Tier)

Se encarga del almacenamiento, consulta y actualización de la información. Utiliza sistemas gestores de bases de datos como SQL Server, MySQL o PostgreSQL.

### Seguridad Perimetral

Exponer directamente una base de datos a Internet representa un grave riesgo de seguridad porque permite intentos de acceso no autorizado, ataques de fuerza bruta, robo de información y explotación de vulnerabilidades.

La buena práctica consiste en mantener la base de datos dentro de una red privada y permitir el acceso únicamente a través de la capa de aplicación, utilizando firewalls, autenticación y conexiones seguras.

---

# Desacoplamiento Lógico con el Patrón MVC

## La Crisis del Código Espagueti

Cuando se mezclan consultas SQL, lógica de negocio y elementos visuales en un mismo archivo, el código se vuelve difícil de entender, mantener y probar. Un cambio pequeño puede afectar múltiples funcionalidades, aumentando los errores y reduciendo la calidad del software. Además, las pruebas unitarias se vuelven complejas porque los componentes dependen fuertemente entre sí.

## Separación de Preocupaciones (SoC)

### Modelo (Model)

Representa los datos y las reglas de negocio de la aplicación. Debe ser independiente de la interfaz gráfica para poder reutilizarse en diferentes contextos. El modelo no debe conocer cómo se presentan los datos al usuario.

### Vista (View)

Es responsable de mostrar la información al usuario. Se considera una entidad pasiva porque recibe datos preparados y los presenta. No debe contener lógica de negocio ni acceso directo a bases de datos.

### Controlador (Controller)

Actúa como intermediario entre la vista y el modelo. Recibe las solicitudes del usuario, coordina las operaciones necesarias y selecciona la vista adecuada para generar la respuesta.

## Métricas de Ingeniería de Software

MVC favorece una alta cohesión porque cada componente realiza una tarea específica. También promueve un bajo acoplamiento debido a que los componentes interactúan mediante interfaces claramente definidas. Esto facilita el mantenimiento, las pruebas unitarias y la escalabilidad del sistema.

---

# Modelado del Ciclo de Vida y Enrutamiento Semántico

## Mapeo Analítico de URLs

| URL Entrante                                                 | Clase Controladora         | Método Ejecutado | Parámetro id       |
| ------------------------------------------------------------ | -------------------------- | ---------------- | ------------------ |
| https://ingenieria.usac.edu.gt/ControlAcademico/Login        | ControlAcademicoController | Login            | Ninguno            |
| https://ingenieria.usac.edu.gt/Estudiante/Historial/20260123 | EstudianteController       | Historial        | 20260123           |
| https://ingenieria.usac.edu.gt/Asignacion/Detalle/10         | AsignacionController       | Detalle          | 10                 |
| https://ingenieria.usac.edu.gt/Home                          | HomeController             | Index            | Ninguno / Opcional |

---

# Diagramación del Flujo Interactivo

## Viaje de una petición HTTP en MVC

### Paso 1

El usuario realiza una acción en el navegador, como presionar un botón o ingresar una URL.

### Paso 2

La solicitud HTTP llega al sistema de enrutamiento de ASP.NET Core, el cual analiza la URL y determina qué controlador y acción deben ejecutarse.

### Paso 3

El controlador recibe la petición y solicita al modelo los datos necesarios o ejecuta las reglas de negocio correspondientes.

### Paso 4

El modelo procesa la información y devuelve los resultados al controlador.

### Paso 5

El controlador envía los datos a la vista. La vista genera el HTML dinámicamente y el navegador muestra la respuesta al usuario.

---

# Auditoría y Control de Calidad

## 1. Prueba de Cohesión (GET)

La acción `Listar()` mantiene una alta cohesión porque únicamente obtiene la información almacenada y la envía a la vista. No realiza cálculos complejos ni mezcla consultas SQL dentro del controlador.

## 2. Evaluación de Antipatrones

El archivo `EstudianteController.cs` cumple con el principio de **Skinny Controllers**, ya que cada método tiene menos de 20 líneas y delega la lógica principal a otras capas, evitando el antipatrón de los **Controladores Gordos (Fat Controllers)**.

---

# Referencias

1. Facultad de Ingeniería, USAC. (2026). *Sesión 11: Modelado Base y Arquitecturas de Despliegue. Evolución de Sistemas Distribuidos, Fundamentos del Modelo Cliente-Servidor y Diseño Físico Multi-Capas (N-Tier).* Laboratorio del curso Introducción a la Programación y Computación 2. Guatemala.

2. Facultad de Ingeniería, USAC. (2026). *Sesión 12: Arquitectura y Componentes del Patrón MVC. Desacoplamiento Lógico de Software, Ciclo de Vida de las Peticiones y Enrutamiento en Aplicaciones Interactivas Modernas.* Laboratorio del curso Introducción a la Programación y Computación 2. Guatemala.
