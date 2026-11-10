# D&D Glowy — Tienda de packs de belleza (Perú) 💗👑

Sitio web estático (HTML + CSS + JavaScript) para **D&D Glowy**, una tienda que vende
**packs de belleza, packs para uñas, packs para pestañas y packs para cejas**.
Todos los precios están expresados en **soles peruanos (S/)** y los pedidos se
envían directamente por **WhatsApp al 912 304 989**.

Diseño con identidad propia: tema *"Glow Pink"* (rosa neón sobre fondo oscuro),
logo con corona, brillos animados y tarjetas con efecto hover. Bootstrap 5.3.3 se
utiliza como base de maquetación responsive y componentes; los estilos propios se
reservan principalmente para los colores, efectos y animaciones de la marca.

---

## 1. Estructura del proyecto

```
/
├── index.html              → Página principal (usa archivos separados)
├── dd-glowy-tienda.html    → ⭐ Versión TODO EN UN ARCHIVO (para Visual Studio)
├── CSS/
│   └── style.css           → Estilos del sitio (tema Glow Pink + responsive)
├── JS/
│   ├── products.js         → Catálogo de packs y precios (editable)
│   └── main.js             → Carrito, filtros, WhatsApp, pedidos, cuenta regresiva
├── images/
│   ├── logo-dd-glowy.png           → Logo D&D Glowy
│   ├── pack-belleza-esencial.jpg
│   ├── pack-belleza-premium.jpg
│   ├── pack-unas-basico.jpg
│   ├── pack-unas-pro.jpg
│   ├── pack-pestanas-inicial.jpg
│   ├── pack-pestanas-pro.jpg
│   ├── pack-cejas-define.jpg
│   └── pack-cejas-pro.jpg
└── README.md
```

### 🖥️ Cómo visualizarlo en Visual Studio / VS Code

**Opción A — versión de un solo archivo (la más fácil):**
1. Crea una carpeta, por ejemplo `DYDGlowy`.
2. Copia dentro **`dd-glowy-tienda.html`** y la carpeta **`images/`**.
3. Abre `dd-glowy-tienda.html` en Visual Studio / VS Code y pulsa *Abrir en el navegador*
   (o clic derecho → *Open with Live Server*).

> ⚠️ Importante: la carpeta `images/` debe quedar **al lado** del archivo `.html`,
> porque las rutas son relativas (`images/...`). Si mueves el `.html` solo, el logo
> y las fotos no se verán.

**Opción B — estructura completa (recomendada para publicar):**
Copia toda la carpeta del proyecto (con `CSS/`, `JS/` e `images/`) y abre `index.html`.

---

## 2. Funcionalidades completas

- ✅ **Catálogo dinámico** de 8 packs + 1 combo, generado por JavaScript.
- ✅ **Filtros por categoría**: Belleza, Uñas, Pestañas, Cejas (+ "Todos").
- ✅ **Buscador** de packs en tiempo real (nombre, descripción o contenido).
- ✅ **Carrito de compras lateral** con: agregar, sumar/quitar unidades, eliminar,
  vaciar, subtotal, envío y total. Se guarda en el navegador (`localStorage`).
- ✅ **Finalizar compra por WhatsApp** al **912 304 989**: el botón verde del carrito
  valida que escribas tu **nombre** y **distrito/ciudad** de entrega, y luego abre
  WhatsApp con el mensaje del pedido ya redactado (packs, cantidades, subtotal,
  envío, total, nombre y lugar de entrega).
- ✅ **Ventana de confirmación** después de finalizar: indica que el pedido está listo,
  permite **reabrir WhatsApp** con un clic y cerrar el aviso.
- ✅ **Botón "Finalizar compra" inteligente**: muestra el total (ej. *Finalizar compra (S/ 327.00)*)
  y se desactiva cuando el carrito está vacío.
- ✅ **Registro del pedido** en la API de tablas (`pedidos`) de forma silenciosa
  (si no está disponible, el pedido igual se envía por WhatsApp).
- ✅ **Cuenta regresiva** de la oferta "Combo Glowy Total -25%".
- ✅ **Precios en soles peruanos (S/)** con precio anterior tachado y precio actual.
- ✅ **Secciones**: Inicio (hero), Categorías, Packs, Promos, Beneficios,
  Opiniones, Contacto y Footer.
- ✅ **Botón flotante de WhatsApp**, botón "volver arriba", menú móvil hamburguesa.
- ✅ **Diseño responsive** (escritorio, tablet y celular) y animaciones al hacer scroll (AOS).
- ✅ **Bootstrap 5.3.3**: sistema de rejilla y utilidades responsive en hero, categorías,
  catálogo, promociones, beneficios, opiniones, contacto y pie de página; componentes
  tarjetas `card`, navegación `nav`/`nav-link`, botones, alertas, grupos de entrada
  y controles de formulario en ambas versiones.
- ✅ **Accesibilidad**: textos alternativos, etiquetas ARIA y navegación semántica.
- ✅ **Panel de configuración, asistente de packs y 5 animaciones CSS** (ver sección 8).

---

## 3. Rutas / puntos de entrada del sitio

| Ruta | Descripción |
|------|-------------|
| `index.html` | Página principal (estructura completa, usa `CSS/` y `JS/`) |
| `index.html#inicio` | Sección hero / portada |
| `index.html#packs` | Catálogo de packs con filtros y buscador |
| `index.html#promos` | Oferta "Combo Glowy Total" + cuenta regresiva |
| `index.html#beneficios` | Beneficios de compra |
| `index.html#opiniones` | Testimonios de clientas |
| `index.html#contacto` | Datos de contacto (WhatsApp, correo, ubicación) |
| `dd-glowy-tienda.html` | Versión autocontenida (un solo archivo) |

### Flujo de compra (carrito → WhatsApp)

1. La clienta agrega packs con el botón **+** de cada tarjeta (se abre el carrito).
2. Ajusta cantidades con **– / +** o elimina productos con la **✕**.
3. Completa **Tu nombre** y **Distrito / Ciudad de entrega** (obligatorios).
4. Pulsa **“Finalizar compra por WhatsApp”** (muestra el total en el botón).
5. Se abre WhatsApp con el pedido redactado y aparece la **ventana de confirmación**
   con la opción de *Abrir WhatsApp de nuevo*.

> El pedido queda registrado en la tabla `pedidos` y el mensaje de WhatsApp
> contiene: número de ítems, cantidades, subtotal, envío, **TOTAL**, nombre y lugar de entrega.

### API de tablas (uso interno)
| Método | Endpoint | Uso |
|--------|----------|-----|
| `POST` | `tables/pedidos` | Registra el pedido generado desde el carrito |
| `GET`  | `tables/pedidos` | Lista los pedidos registrados |

---

## 4. Contacto de la tienda

- 📱 **WhatsApp / Pedidos:** 912 304 989 → `https://wa.me/51912304989`
- ✉️ **Correo:** ventas@ddglowy.pe
- 📍 **Ubicación:** Av. Los Glow 123, Lima – Perú
- 🕘 **Horario:** lunes a sábado, 9:00 a.m. – 8:00 p.m.
- 💳 **Pagos:** Yape, Plin, transferencia BCP / Interbank y contra entrega (Lima).

---

## 5. Lista de precios actual (en soles)

| Pack | Categoría | Antes | Ahora |
|------|-----------|-------|-------|
| Pack Belleza Esencial | Belleza | S/ 119 | **S/ 89** |
| Pack Belleza Premium | Belleza | S/ 199 | **S/ 159** |
| Pack Uñas Básico | Uñas | S/ 89 | **S/ 69** |
| Pack Uñas Pro Nail Art | Uñas | S/ 159 | **S/ 129** |
| Pack Pestañas Inicial | Pestañas | S/ 129 | **S/ 99** |
| Pack Pestañas Pro Volumen | Pestañas | S/ 169 | **S/ 139** |
| Pack Cejas Define | Cejas | S/ 69 | **S/ 49** |
| Pack Cejas Pro Studio | Cejas | S/ 129 | **S/ 104** |
| Combo Glowy Total (3 packs) | Promo | S/ 372 | **S/ 279** |

> Envío: **gratis** en pedidos desde **S/ 150**; en Lima se considera **S/ 12** por debajo de ese monto.

---

## 6. Cómo personalizar

- **Cambiar precios o packs:** edita `JS/products.js` (o el bloque `PACKS` dentro de
  `dd-glowy-tienda.html`). Cada pack tiene `price` (precio actual) y `priceOld` (precio anterior).
- **Cambiar el número de WhatsApp:** edita la constante `WHATSAPP_NUMBER` en `JS/main.js`
  y en `dd-glowy-tienda.html`, y actualiza los enlaces `wa.me/...` del HTML.
- **Cambiar imágenes:** reemplaza los archivos dentro de `images/` manteniendo los mismos nombres.
- **Cambiar colores:** modifica las variables en `:root` dentro de `CSS/style.css`
  (por ejemplo `--pink-500` para el rosa principal).

---

## 7. Modelo de datos (tabla `pedidos`)

| Campo | Tipo | Descripción |
|-------|------|-------------|
| `id` | text | Identificador único del pedido |
| `customer_name` | text | Nombre de la clienta |
| `customer_place` | text | Distrito / ciudad de entrega |
| `phone` | text | WhatsApp de contacto de la tienda |
| `items` | text | Detalle de packs y cantidades |
| `units` | number | Total de unidades |
| `subtotal` | number | Subtotal en soles (sin envío) |
| `shipping` | number | Costo de envío en soles |
| `total` | number | Total del pedido en soles |
| `status` | text | nuevo / contactado / pagado / enviado / entregado / cancelado |

**Servicios usados:** tipografías de Google Fonts, iconos de Font Awesome y
animaciones de AOS (todo vía CDN). Los pedidos se almacenan con la API de tablas
del proyecto (almacenamiento gestionado).

**Bootstrap 5.3.3** se carga por CDN en ambas versiones del sitio. La rejilla
responsive Bootstrap (`container`, `row`, columnas breakpoint y utilidades flex)
organiza las secciones principales y sus tarjetas. También se emplean componentes
`card`, `nav`/`nav-link`, botones, alertas, grupos de entrada y controles de formulario;
los estilos personalizados conservan la paleta Glow Pink y sus efectos.

---

## 9. Bootstrap como base de maquetación (≈ 70 %+)

La maquetación se reorganizó para que **Bootstrap 5.3.3 sea la base** y `style.css` quede
solo para la identidad visual (colores, degradados, brillos, animaciones).

| Medición | Antes | Ahora |
|----------|-------|-------|
| Clases Bootstrap / clases de maquetación (sin contar iconos Font Awesome) — HTML estático | 51 % | **79 %** |
| Mismo cálculo sobre el DOM ya renderizado (incluye las tarjetas que genera JS) | 45 % | **76 %** |
| Elementos HTML con al menos una clase Bootstrap | 30 % | **70 %** |
| Clases Bootstrap / todas las clases (contando iconos `fa-*`) | 39 % | 68 % |

### Qué se cambió
- **Rejilla correcta:** cada tarjeta (categorías, packs, beneficios, opiniones, contacto) ahora vive
  dentro de su columna `col-*`, con `card h-100` dentro. Antes la columna y la tarjeta eran el mismo
  elemento y se perdían los espacios (gutters) entre tarjetas.
- **Utilidades en lugar de CSS propio:** `d-flex`, `flex-column`, `gap-*`, `align-items-*`,
  `justify-content-*`, `py-*`/`px-*`/`mb-*`, `text-center`, `rounded-4/5/pill/circle`,
  `position-*`, `border-top`, `overflow-*`, `fw-*`, `lh-*`, `list-unstyled`, `d-none d-lg-inline-flex`,
  `d-lg-none`, etc. Las reglas de `style.css` equivalentes se eliminaron.
- **Menú móvil:** el punto de corte pasó de 900 px a **992 px** (`lg` de Bootstrap) en CSS y JS;
  el botón hamburguesa usa `d-lg-none` y el botón "Pedir ahora" `d-none d-lg-inline-flex`.
- **Variables de Bootstrap con la marca:** en `:root` se definieron `--bs-border-color`,
  `--bs-border-radius-xl` (20 px, `.rounded-4`) y `--bs-border-radius-xxl` (30 px, `.rounded-5`).
- **Tarjetas del catálogo (JS):** cada pack se genera como `<div class="col-12 col-sm-6 col-xl-4">`
  con la tarjeta dentro, usando utilidades Bootstrap para pie, precios, valoración y botón.

### Errores del original que quedaron corregidos
- **Hero:** el `div.container` se cerraba antes de tiempo y el logo caía debajo del texto en escritorio.
- **Promo "Combo Glowy Total":** la cuenta regresiva quedaba fuera de la caja rosa.
- **Ventana de confirmación y aviso "Agregado…":** nunca se veían porque las clases `.modal` y
  `.toast` chocaban con las de Bootstrap (que las ocultan). Se renombraron a `.confirm-modal`
  y `.glow-toast`.

### Nota
Las clases propias que se conservan son las de identidad visual (`btn--primary`, `chip`, `text-glow`,
`hero__*`, `product__*`, `ticker`, `settings`…) y las que usa `main.js` (`.cat-card`, `.filter`,
`.nav__link`, `.quiz__opt`). El espaciado vertical de las secciones usa `py-5` (3 rem) en lugar
del `clamp()` anterior (3–5 rem), por lo que en pantallas grandes es algo más compacto.

