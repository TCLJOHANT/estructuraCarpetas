# Estructura de Archivos y Carpetas para Aplicaciones Angular

Angular ha experimentado un renacimiento sin módulos, lo que plantea la pregunta: ¿Cómo agrupar de manera efectiva los elementos? Tener un sólido andamiaje es fundamental para un desarrollo exitoso, y seguir la Guía de Estilo de Angular es el primer paso. En este artículo, recopilaré buenas prácticas y consejos para la creación de estructuras de archivos y carpetas para aplicaciones Angular, inspirados en la guía oficial y en los principios LIFT (Localizar, Identificar, Flat - Plano, Try-DRY).

## Convención de Nombres de Archivos y Responsabilidad Única

La Guía de Estilo de Angular sugiere dedicar un archivo a cada artefacto necesario, encapsulando el código relacionado en clases o módulos y exportándolo en su propio archivo. Para nombrar cada archivo, se propone componer el nombre a partir de su naturaleza funcional y técnica, utilizando el formato funcional.técnica.ts.

Ejemplos:
- Servicio para gestionar datos de usuarios: `users.service.ts`
- Componente para mostrar reservas: `bookings-list.component.ts` o también `bookings.list.ts`

## Atributo Tipo

Los servicios y componentes son artefactos comunes en Angular, y desde Angular 14, el CLI puede generar componentes con nombres específicos mediante el atributo --type. Se sugiere utilizar subtipos propios para discriminar el propósito principal de los componentes, como *.page.ts para componentes utilizados en rutas y *.widget.ts para componentes independientes que obtienen y escriben datos.

## Agrupación en Carpetas

La organización se vuelve crucial al enfrentarnos a cientos o miles de archivos. Se propone una estructura de carpetas principal basada en la experiencia histórica de Angular:

- **/core**: Servicios para ser utilizados desde la raíz.
- **/routes**: Ramas funcionales del árbol de navegación.
- **/shared**: Utilidades para ser utilizadas desde las ramas funcionales.

## Tamaño y Profundidad de Carpetas

La estructura de carpetas debe mantenerse lo menos anidada posible, siguiendo el principio Flat de LIFT. Se sugiere aplicar la regla 5–15 para subdividir carpetas:

- Una carpeta con menos de 5 elementos no necesita ser subdividida.
- Una carpeta con más de 15 elementos debe ser subdividida.
- Las carpetas entre 6 y 14 elementos se dividen si surge un criterio obvio.

## Ejemplo de Estructura de Carpetas

### /routes:

Las rutas son representadas como un árbol de navegación. Se propone implementar el árbol de rutas como un árbol de carpetas siempre que sea posible. La carpeta de rutas se dedica a contener toda la funcionalidad de la aplicación.

### /core:

Esta carpeta alberga cosas de uso único en toda la aplicación, como interceptores y guardias. Puede subdividirse cuando supera los 15 archivos.

### /shared:

Esta carpeta captura todo lo no relacionado con una característica específica. Se propone una estructura genérica con subcarpetas para organizar compartidos por dominio, servicios y componentes de interfaz de usuario.

## Código de Ejemplo

Puedes explorar un ejemplo práctico aplicando estos consejos en el proyecto de laboratorio en [GitHub - AlbertoBasalo/ng-lab](https://github.com/AlbertoBasalo/ng-lab).

## Resumen

Cuando se organiza el código en Angular, es fundamental seguir principios como LIFT y utilizar convenciones de nombres claras. La estructura de carpetas debe mantenerse plana siempre que sea posible, subdividiéndola solo cuando sea necesario. La agrupación de archivos debe ser más funcional que tecnológica, y la carpeta compartida puede organizarse por dependencias y tecnologías específicas.

![Árbol de Carpetas](https://media.licdn.com/dms/image/D4D12AQHAeq4kaZKjTQ/article-inline_image-shrink_1500_2232/0/1702974181569?e=1709769600&v=beta&t=y4MyfFHNrVF4JNz8FD51l2fH2xpXUTAYxPrr99m35L8)

