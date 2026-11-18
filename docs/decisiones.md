# Documento de decisiones de diseño

> Cada decisión indica qué se ha elegido, por qué y qué alternativa se ha descartado.

## Ruta de trabajo

- [ ] Ruta A · Figma (enlace con permiso de lectura: no utilizado).
- [x] Ruta B · VS Code (diseño directamente en `guia.html`).

Se ha elegido trabajar directamente en código porque el objetivo de esta fase es construir una guía de estilos funcional utilizando HTML y SCSS. Así se pueden comprobar desde el principio los estilos, los componentes y su comportamiento en los distintos estados. Se descarta Figma porque supondría mantener un diseño visual separado de su implementación.

## 1. Color (RA1 · CE b)

- **Tono de acento y escala:** Se ha elegido un verde de tono base 142º, indicado en la ficha del caso 6. La escala 50–950 se ha construido manteniendo ese matiz y reduciendo progresivamente la luminosidad: los niveles claros se reservan para superficies y los oscuros para texto y acentos.
- **Contraste del acento:** Se utilizan tonos diferentes según el tema para mantener la legibilidad. En el tema claro se emplea un tono oscuro para el texto o los elementos de acento, mientras que en el tema oscuro se utiliza uno más claro. Así se evita que el acento pierda visibilidad sobre el fondo.
- **Tokens semánticos añadidos:** Se han definido tokens para fondo, superficie, texto, texto suave, bordes, acento, foco, éxito, error, aviso y elementos desactivados. Esto permite identificar los colores por su función y no por su valor hexadecimal.
- **Pares de contraste añadidos a `$pares-contraste`:** Se han contemplado combinaciones de texto y fondo, texto y superficie, texto suave y superficie, acento y superficie, texto sobre acento, estados de éxito, error y aviso, bordes de controles y foco. Se busca cumplir al menos 4,5:1 para texto normal y 3:1 para elementos de interfaz y texto grande.

Se descarta utilizar colores directamente en cada componente porque dificultaría mantener la coherencia y cambiar los temas.

## 2. Tipografía (RA1 · CE b)

- **Familia elegida:** Se utiliza una tipografía del sistema (`system-ui`) para el texto general. Ofrece buena legibilidad, carga rápida y no requiere descargar fuentes externas ni gestionar licencias adicionales.
- **Base en móvil y escritorio:** Se parte de una base de 16 px en móvil y se aumenta en escritorio para mejorar la comodidad de lectura en pantallas grandes. Se evita utilizar tamaños demasiado pequeños.
- **Medida de línea:** Se limita la anchura de los párrafos mediante `max-inline-size` expresado en `ch`, para evitar líneas excesivamente largas y facilitar la lectura.

Se descarta depender de una fuente externa porque la tipografía del sistema ofrece un buen equilibrio entre rendimiento, disponibilidad y legibilidad.

## 3. Espaciado y forma

Se utiliza una escala de espaciado basada en múltiplos de 4 px: 4, 8, 12, 16, 24, 32, 48 y 64 px. Esta escala permite mantener distancias coherentes entre elementos y facilita la reutilización de valores.

Los radios se utilizan para suavizar los bordes de botones, campos y superficies, manteniendo una apariencia uniforme. Se descarta asignar medidas arbitrarias a cada elemento porque dificultaría la consistencia visual.

## 4. Componentes (RA1 · CE f)

| Componente | Estados | Cómo se resuelve cada estado en CSS |
| --- | --- | --- |
| Botón | normal, hover, foco, desactivado, secundario | Estilos base para el estado normal; `:hover` para interacción; `:focus-visible` para mostrar el foco; `:disabled` para desactivar; y una variante secundaria con menor protagonismo visual. |
| Turno | disponible, seleccionado, ocupado, foco | Estilo base para disponible; `:has(:checked)` para seleccionado; `:has(:disabled)` para ocupado; y `:has(:focus-visible)` para el foco. |
| Contador de invitados | normal, seleccionado, foco | Se agrupan las opciones en un `fieldset` con controles de tipo radio. Se diferencia la opción seleccionada y se mantiene visible el indicador de foco. |
| Aviso de pago | informativo | Se utiliza una sección con título, importe, teléfono y concepto. La jerarquía tipográfica y el espaciado permiten distinguir la información importante. |

Los estados no dependen únicamente del color: también se utilizan bordes, cambios de grosor, texto e indicadores de foco. Se procura que los controles interactivos tengan un área táctil mínima de 44 × 44 px.

## 5. Comparativa de tecnologías (RA1 · CE e · RA2 · CE i)

| Criterio | Figma | Penpot | Diseño en código |
| --- | --- | --- | --- |
| Coste / licencia | Plan gratuito limitado y opciones de pago. | Alternativa de código abierto con opciones de uso gratuitas. | Se utilizan herramientas gratuitas como VS Code y Sass. |
| Traslado a código (handoff) | Facilita compartir diseños y especificaciones. | Permite compartir diseños y especificaciones. | El diseño ya está implementado en HTML y SCSS, por lo que no necesita trasladarse. |
| Mantenimiento del sistema | Permite mantener componentes visuales. | Permite mantener componentes visuales. | Los tokens y componentes se mantienen directamente en los archivos del proyecto. |

| Criterio | Sass + CSS propio | CSS nativo sin preprocesador | Bootstrap / Tailwind |
| --- | --- | --- | --- |
| Tokens y temas | Permite organizar variables, módulos y temas reutilizables. | Permite utilizar propiedades personalizadas, aunque sin las funciones propias de Sass. | Ofrecen sistemas de configuración y utilidades propias. |
| Peso del CSS final | Permite generar CSS propio sin incorporar un framework completo. | No necesita compilación ni preprocesador. | Puede añadir estilos y dependencias que no siempre se necesitan. |
| Control de la cascada | Permite organizar estilos mediante módulos y capas. | Ofrece control directo mediante CSS. | Se trabaja siguiendo la estructura y convenciones del framework. |

**Decisión y motivo:**

Se ha elegido la ruta de diseño directamente en código, utilizando Sass y CSS propio. Esta combinación permite organizar los estilos en módulos, reutilizar tokens, mantener los temas y controlar la cascada mediante capas. Además, evita depender de un framework externo y permite que el diseño coincida directamente con la implementación final.

Se descarta Figma y Penpot para esta fase porque no es necesario mantener un prototipo separado. También se descarta utilizar Bootstrap o Tailwind porque se busca construir un sistema de diseño propio y controlar sus componentes y estilos.
