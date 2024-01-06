Estructura de archivos y carpetas para aplicaciones Angular

     Angular ha renacido sin módulos, ¿cómo agrupo las cosas? 

Tener un buen andamiaje es la base para un desarrollo exitoso. Seguir la Guía de Estilo de Angular es solo el primer paso. Casi debería decir era... porque necesitamos mucha más orientación al iniciar un nuevo proyecto en el nuevo Renacimiento de Angular sin módulos.

En este artículo voy a recopilar algunas buenas prácticas y consejos para crear estructuras de archivos y carpetas para aplicaciones Angular inspiradas en la guía oficial, y sus principios LIFT, que es con lo que voy a empezar:

    Localizar: Agrupar coherentemente
    Identificar: Nombrar para indicar el contenido
    Flat - Plano: Crear subcarpetas sólo si es necesario
    Try-DRY: Alguna redundancia puede ser beneficiosa

Si no tienes tiempo, o te basta con ver la idea general, esta es la imagen final que me queda:
<img src="https://media.licdn.com/dms/image/D4D12AQEDl_CU0-tHgw/article-inline_image-shrink_1500_2232/0/1702974458728?e=1709769600&v=beta&t=W0sNJklTEeMxTgRjFh3DqL4qKFFNcfu3QjvoyPa_gIk" />
 Sigue leyendo si quieres profundizar sobre los motivos que me llevan a esta estructura para empezar caulquier proyecto tipo de Angular.
Convención de nombres de archivos.
Responsabilidad única

La Guía de Estilo de Angular nos anima a dedicar un archivo a cada artefacto necesario, es decir, encapsular el código relacionado en clases o módulos y exportarlo en su propio archivo.

Luego, para nombrar cada archivo, nos dicen que compongamos el nombre del archivo a partir de su naturaleza funcional y técnica. Es decir, ese artefacto sirve para algo y pertenece a alguna categoría sintáctica. Solución concatenar ambas separadas por un punto funcional.técnica.ts

Por ejemplo, un servicio para gestionar los datos de los usuarios se debería llamar users.service.ts, mientras que un componente para mostrar tus reservas se debería llamar bookings-list.component.ts o bien moderna y abreviadamente, como te muestro a continuación bookings.list.ts
El atributo Tipo.

Los servicios y los componentes son artefactos técnicos comunes en Angular; lo mismo ocurre con los guardias, los interceptores, etc. Pero puedes ir más allá y usar tus propios subtipos.

De hecho, desde Angular 14, el CLI puede generar componentes con nombres específicos (mediante el atributo --type) que nos ayudan a subclasificar nuestro concepto genérico de componentes.

Suelo usar un pequeño conjunto de tipos para discriminar el propósito principal de mis componentes:

    Componentes inteligentes: Uso *.page.ts para los que se usan en rutas (muy numerosos) y *.widget.ts para cualquier componente que obtiene y escribe datos por su cuenta (pocos casos).
    Componentes tontos: El predeterminado .component.ts (la mayoría), o, en ciertos casos, optar por sufijos específicos como *.form.ts , *.table.ts o *.list.ts

Puedes hacer esto con el CLI para los componentes, pero nada te impide usar la misma idea con los servicios, pero en este caso es a mano. Yo acabo teniendo cosas como *.repository.ts , *.store.ts o *.validations.ts
Agrupar en carpetas

La organización es muy fácil si solo tienes una docena de archivos. Pero en el mundo real nos enfrentaremos a cientos o miles de archivos. ¿Cómo los mantenemos bajo control?

Puede que esperes que entre de lleno en la famosa dicotomía: ¿agrupar por función o por tipo?. Por supuesto que esta es una pregunta legítima; está basada en las dos dimensiones que aplicamos para nombrar nuestros archivos (funcional.técnica). Pero no siempre es tan sencillo.

Intentemos encontrar una solución de mínimos.
Un acuerdo base universal.

En los primeros días de Angular, dividir las aplicaciones en módulos era casi obligatorio. La naturaleza de las cosas que solíamos declarar en esos viejos módulos nos llevó a segregarlos en tres categorías principales:

    Cosas usadas por la raíz. Normalmente incluye el layout de la aplicación y muchos servicios inyectables proporcionados en la raíz. Lo llamábamos el módulo core.
    Las funcionalidades que se asignan a rutas. Para cada una su carga perezosa y su módulo con sus routes.
    Cosas usadas en las páginas de características. Aquí, solíamos encontrar componentes tontos, directivas y tuberías de presentación. Esta vez, el nombre era shared.

Incluso hoy en día, sin la necesidad de módulos, seguimos creando cosas para ser aprovisonadas en la raíz, y otras para ser usadas en las páginas...

Así que, es natural para los desarrolladores de Angular experimentados sentirse como en casa con los conceptos routes, core y shared; mi propuesta para las carpetas de primer nivel.

    /core (servicios para ser usados desde la raíz)
    /routes (las ramas funcionales del árbol de navegación)
    /shared (utilidades para ser usadas desde las ramas funcionales)

Ahora que ya sabemos cómo nombrar los archivos y las tres carpetas generarles para guardarlos, es hora de analizar estas carpetas. 
Plano o profundo, una cuestión de tamaño.

A partir de aquí, ya no hay una regla fija, sino algo que depende del número de archivos (tamaño de la aplicación) y el estilo arquitectónico aplicado.

Cumpliendo con el principio Flat de LIFT, mantendré la estructura de carpetas lo menos anidada posible; algunos consejos pueden surgir de esta regla que me saco de la manga...

Regla 5–15:

    Una carpeta con menos de 5 elementos no necesita ser subdividida 

    Una carpeta con más de 15 elementos tiene que ser subdividida 

    Las carpetas entre 6 y 14 elementos se dividen si surge un criterio obvio 

Apliquemos este consejo a las tres carpetas principales: routes, core y shared.
Routes: 

    Las rutas son un árbol de navegación. 

Empecemos con la carpeta funcional, la que llamo routes. (He visto gente que la llama features y otros pages).

Puedes ver todas las rutas de tu aplicación como un array con arrays anidados… En informática, lo llamamos un árbol. ¿Y qué otra cosa es también un árbol? El paradigma y la visualización de carpetas/archivos desde hace medio siglo.

Así que, propongo implementar el árbol de rutas como un árbol de carpetas. Cuando sea posible, por supuesto. Pero si estoy trabajando en una ruta como /activities/surf/bookings me gustaría tener mi bookings.component.ts debajo de esta ruta de carpetas /activities/name/.

Esta carpeta de rutas está dedicada a contener toda la funcionalidad de la aplicación. Necesitaremos más que componentes de página para satisfacer las necesidades de los usuarios. Al menos debérias dar soporte a la página con algún servicio y algún componente tonto presentacional.

Mantén todas esas cosas relacionadas cerca unas de otras, escribe servicios personalizados para cada página y proveelos localmente. En este nivel estamos agrupando por funcionalidad, no por tecnología, así que, mezcla componetes y servicios en el mismo nivel funcional.

Poco a poco detectarás servicios comunes, lógica duplicada, componentes de presentación similares. Todos deben ser abstraídos y reutilizados lo máximo posible. Es hora de los viejos amigos core y shared.
Core: 

    Poco numeroso y superficial. 

Esta carpeta será el hogar de cosas que usarás una vez en la vida… de la aplicación. Cosas que solíamos llamar singletons eran proporcionados en la raíz como servicios inyectables.

Hoy en día ya se usan menos las clases injectables y provided in-root. Por ejemplo, los interceptores y las guardias se codifican como funciones y se proporcionan con una sintaxis especial. Ser una función ya no significa nada en términos de singletons…

Pero, siguen siendo proveedores de la raíz, y sólo los referenciamos mientras la aplicación se inicia. Razón suficiente para mantener su propia carpeta, y, por respeto a la tradición, mantener el respetable nombre de core.

Tampoco es que vaya a ser muy numerosa, así que, normalmente podrás apañarte sin subdividirla. Pero llegados a 15 o más ficheros, seguro que te aparece un criterio natural para agruparlos.

Alternativamente, todo esto podría ir muy bien en nuestra última carpeta; porque ahí cabe de todo.
Shared: 

    El atrapa todo que puede ser profundo. 

Todas las cosas no relacionadas con una característica específica, o no proporcionadas como servicios a nivel de aplicación tienen cabida aquí. 

Así que esto va a crecer. Mucho. Más temprano que tarde superará con creces el límite de 15 elementos. Solo puedo recomendarte que cumplas la regla de lo menos profundo posible. 

Aquí no importa tanto agrupar las cosas por su función o por su naturaleza técnica. Es una cuestión de sentido común. 

Así que tener una carpeta /shared/components/ podría estar bien a este nivel. Igualmente, una carpeta más funcional como /shared/auth/ para cosas relacionadas con la seguridad.

Pero has llegado hasta aquí en busca de consejo, así que me lanzo. Para empezar te propongo una estructura genérica basada en agrupar las cosas por su naturaleza y su dependencia. 

    /domain (tipos, funciones y utilidades sin dependencias de Angular)
    /services (servicios y funciones injectables de Angular)
    /ui (componentes tontos y otros declarables reutilizables)

De esta forma todo lo compartido se organiza en estas tres subcarpetas de shared: domain, services y ui. 

Este criterio técnico te resultará más útil si das el salto a dividir el monolito en librerías. De esa forma cada una puede tener su propio ecosistema de dependencias y tipos de pruebas específicos. 

Repito, un criterio de reparto funcional es igualmente adecuado. Por ejemplo, hablemos de la carpeta de servicios (son utilidades basadas en tecnología Angular y utilizadas en varias rutas o funcionalidades core). Con el tiempo, crecerá y algunos de sus ficheros se relacionaran de forma cohesiva y merecerán su propia carpeta. Los casos más claros pueden ser los de instrumentación y seguridad. En mi caso dando lugar a las carpetas log y auth. 
<img src="https://media.licdn.com/dms/image/D4D12AQET11YQWoH5BA/article-inline_image-shrink_1500_2232/0/1702972992320?e=1709769600&v=beta&t=InvZWrBdo-WKVkf9LC5lG_ezJRY-qeQVSD9pCSCVU3s"  />

 Ambas carpetas las meto dentro de la de servicios para mantener esa coherencia tecnológica. Pero es igulamente válido subirlas un nivel y hacerlas hijas directas de shared.
Código de ejemplo:

Show me the code. Para familizarizarte con esta arquitectura lo mejor es que lo navegues por tu cuenta. 

    Aquí tienes un ejemplo con todos esos consejos aplicados: GitHub - AlbertoBasalo/ng-lab 

Es un proyecto de laboratorio para mis talleres, y puede ayudarte a entender cómo nombrar las cosas de Angular. Esta es la imagen final que me queda: 
<img src="https://media.licdn.com/dms/image/D4D12AQEWJTPBf3J8HA/article-inline_image-shrink_1500_2232/0/1701768488545?e=1709769600&v=beta&t=HmNpew9OveUtYFeIqVvM_zkYkIQpN8GrKGODNd62UJ8" />

 Resumen: 

Cuando se trata de organizar tu código Angular, podría haber tantas formas de hacerlo como desarrolladores. Aquí tienes algunas pautas que vi en soluciones exitosas. Espero que te puedan ayudar.

    Principios LIFT: Localizar, Identificar, Plano y Tratar-DRY. Estos principios ayudan a organizar el código de manera coherente, clara y concisa. 
    Convención de nombres de archivos: Utiliza una combinación de dominios funcionales y técnicos para nombrar los archivos, como nombre-funcional.tipo-tecnológico.ts 
    Carpetas de primer nivel: Tres carpetas principales para reflejar la funcionalidad básica de Angular: /routes /core /shared 
    Estructura plana sobre estructura profunda: Mantén la estructura de carpetas lo más plana posible y solo crea subcarpetas cuando haya más de 15 archivos o cuando haya un criterio obvio.
    Funcional sobre tecnológico: En caso de duda, fomenta que vayan juntos los ficheros que uses comunmente para resolver una funcionalidad.
    Lo compartido puede agruparse por tecnología: En la carpeta shared agrupo según las dependencias y tecnologías en /domain /services /ui


En resumen, el árbol de carpetas queda más o menos así: 
<img src="https://media.licdn.com/dms/image/D4D12AQHAeq4kaZKjTQ/article-inline_image-shrink_1500_2232/0/1702974181569?e=1709769600&v=beta&t=y4MyfFHNrVF4JNz8FD51l2fH2xpXUTAYxPrr99m35L8" />
