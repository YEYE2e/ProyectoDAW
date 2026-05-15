# AURA | Premium Tees

Proyecto e-commerce para una marca de ropa minimalista y sostenible ("Silent Luxury"). 
Desarrollado con una arquitectura estática pura, enfocada en alto rendimiento y experiencia de usuario premium.

## Arquitectura y Tecnologías

- HTML5: Estructura semántica.
- CSS3: Diseño responsivo, variables CSS, Flexbox, Grid y animaciones personalizadas sin dependencias.
- JavaScript (Vanilla): Lógica de interacción de interfaz, carrito de compras asíncrono y selectores dinámicos de color.
- Fuentes e Iconos: Google Fonts (Outfit) y FontAwesome.

## Estructura del Proyecto

El repositorio está estructurado de la siguiente forma:

ProyectoDAW/
|-- index.html                 (Estructura DOM y lógica Javascript del carrito/interfaz)
|-- stylesheets/
|   |-- styles.css             (Tokens de diseño globales, variables y media queries)
|-- assets/
|   |-- images/                (Imágenes de productos, UI y favicon.svg)
|-- .gitattributes             (Normalización de saltos de línea para servidor)
|-- README.md                  (Documentación técnica)

## Guía de Mantenimiento

Para realizar modificaciones técnicas en el sitio web, seguir las siguientes directrices estructurales:

1. Estilos y Tema Global (CSS):
   - Paleta de Colores: Los colores globales se gestionan exclusivamente mediante variables nativas en la pseudo-clase `:root` del archivo styles.css.
   - Grid de Productos: Las secciones "The Drop" y "The Essentials" heredan las propiedades de la clase utilitaria `.products-grid` (distribución de 3 columnas). Cualquier nueva colección añadida a futuro debe instanciar esta clase para mantener la consistencia visual.
   - Tooltips y Medidas: Queda obsoleto el uso de tablas estáticas. La información de dimensiones de las prendas (S, M, L, XL) está embebida en el atributo `data-tooltip` de la clase `.size-pill` y se revela mediante pseudoelementos dinámicos en CSS.

2. Interactividad (JavaScript):
   - Selectores de Variante: La transición entre colores de una misma prenda se maneja mediante la función `changeProductColor()`. Esta función recibe la imagen primaria, secundaria y opcionalmente filtros de CSS (invert, sepia, hue-rotate) para simular variaciones tonales sin necesidad de cargar imágenes adicionales.
   - Carrito Deslizable (Off-Canvas): El carrito no navega a otra ventana ni lanza alertas invasivas. Toda inserción a través de `addToCart()` inyecta el producto en memoria y dispara la visibilidad de un panel lateral dinámico actualizando los montos y contadores.

3. Control de Versiones y Formateo:
   - El archivo `.gitattributes` con la instrucción `* text=auto eol=lf` está activo para forzar la estandarización LF en servidores Unix y así evitar problemas de compilación en GitHub Actions a causa de formato CRLF generado por sistemas operativos locales.

## Despliegue Automatizado (GitHub Pages)

El proyecto está configurado para integración y despliegue continuo (CI/CD) transparente mediante GitHub Actions sobre GitHub Pages.

Pasos y confirmación de despliegue:
1. Código Limpio: Subir los cambios a la rama principal ejecutando add, commit y push a `main`.
2. Verificación de Entorno: En el repositorio remoto en GitHub, dirigirse a Settings > Pages. 
3. Fuente de Compilación: Verificar que "Build and deployment Source" esté configurado como "Deploy from a branch", señalando explícitamente a `main` sobre la carpeta raíz `/ (root)`. Alternativamente, si se usa el método de GitHub Actions predeterminado, verificar que exista un workflow activo en la pestaña "Actions".
4. Permisos de Workflow: En Settings > Actions > General > Workflow permissions, la opción "Read and write permissions" debe estar habilitada para permitir que el script suba los archivos de compilación estática.
5. Monitoreo: Al ejecutar el push a la rama principal, se desencadenará un flujo de trabajo visible en la pestaña "Actions". Al obtener el estado verde ("Success"), el sitio estático estará compilado y desplegado de manera pública.
