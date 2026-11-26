# Centro de mando Zunko: pantallas y plantillas

Borrador v1 · 26 nov 2026

Una app instalable (PWA) en un solo `index.html`, igual que Bolsillo: sin servidor, con los datos guardados en el celular (`localStorage`), copia de seguridad en JSON y publicada en GitHub Pages.

## Reparto de trabajo

| Lo hace la app (código, gratis) | Lo hace Claude (estratégico) |
|---|---|
| Mover productos por etapas y recordar en qué va cada uno | Elegir qué producto entra al radar y cuál pasa a pauta |
| Calcular precio sugerido, BREAKEVEN y proyección | Elegir el ángulo de venta y escribir los hooks |
| Aplicar las reglas fijas de pauta (48 h, CTR 1,5 %, día 3, escalar 20–30 %) | Leer los resultados y decidir qué cambiar |
| Rellenar plantillas de creativos y descargarlas en PNG | (Más adelante, Gemini: escenas del producto) |
| Llevar los pendientes | |

**El puente para ahorrar tokens:** cada producto tiene un botón **«Copiar para Claude»** que arma un resumen corto en texto (datos, costeo, métricas por día, pregunta). Se pega en el chat y Claude no tiene que consultar Dropi, Dropkiller ni Meta para reconstruir el contexto.

---

## Navegación

Barra inferior con 5 pestañas, una columna de máximo 480 px (como Bolsillo):

**Hoy · Productos · Calcular · Creativos · Ajustes**

---

## 1. Hoy

Lo primero que se ve al abrir. Responde «¿qué toca hacer hoy?».

- **Alertas de pauta**, calculadas desde el registro diario de cada producto en pauta:
  - «No tocar: faltan 31 h para cumplir las 48 h» (cuenta regresiva desde el lanzamiento).
  - «Día 1: ningún creativo pasa de 1,5 % de CTR. El problema es el hook».
  - «Día 3: 2 creativos superan el BREAKEVEN de $17.600. Apágalos».
  - «Día 4+: el ganador va bien. Sube máximo 20–30 % (de $80.000 a $96.000–104.000)».
  - «Antes de pasar $150.000/día confirma stock por escrito y primeras entregas» (bloquea hasta marcar las dos casillas).
  - «Falta el registro de hoy» si un producto en pauta no tiene métricas del día.
- **Pendientes de hoy y vencidos**, con check rápido. Cada uno puede ir ligado a un producto.
- **Resumen por etapa**: cuántos productos hay en Radar, Testeo, Costeo y Pauta. Tocar uno abre el tablero filtrado.

## 2. Productos (tablero)

Columnas por etapa, deslizables en el celular: **Radar → Testeo → Costeo → Pauta**, más **Descartados** (plegada, con el motivo).

Tarjeta: foto, nombre, costo proveedor, BREAKEVEN si ya se calculó, días en la etapa y un punto de color (verde = listo para avanzar, ámbar = le falta un dato, rojo = no cabe).

Botón **+ Producto** abre un formulario corto: nombre, link de Dropi o Dropkiller, costo proveedor, foto (subida desde el celular).

### Ficha de producto

Una pantalla por producto con secciones según la etapa. Cada etapa tiene una **condición para avanzar**; la app avisa pero deja avanzar igual (la decisión es tuya).

| Etapa | Qué se llena | Condición para avanzar |
|---|---|---|
| **Radar** | Link del proveedor, costo, link de la competencia, días al aire del anuncio de la competencia, precio que cobra la competencia, notas | Tener costo y al menos un competidor |
| **Testeo** | Ángulo elegido (el que la competencia ya validó), 4–6 hooks, fotos reales recibidas o no, stock que dice el proveedor | Ángulo y al menos 4 hooks |
| **Costeo** | Flete cotizado en Dropi, efectividad y cancelaciones, precio final. Usa la misma calculadora de la pestaña Calcular, guardada en el producto | BREAKEVEN ≥ $15.000 y precio final ≤ precio de la competencia |
| **Pauta** | Fecha y hora de lanzamiento, presupuesto diario, registro diario por creativo (gasto, impresiones, clics, pedidos), entregas reales | — |

Arriba de la ficha, siempre: precio final, BREAKEVEN, CPA actual y el botón **Copiar para Claude**. Abajo: **historial de decisiones** (fecha + qué se decidió + por qué), que también va en el resumen para Claude.

Con las entregas reales, la app sugiere reemplazar la efectividad supuesta (70 %) por la real y recalcula el BREAKEVEN.

## 3. Calcular

La Calculadora de Precio 2026 del curso, celda por celda. Se puede usar suelta o abrirla desde un producto (ahí guarda).

**Entradas:** precio proveedor, flete base, efectividad (70 % por defecto), cancelaciones (20 %), administrativos (0), fulfillment (0), CPA del Ads Manager ($20.000 por defecto), importe a gastar.

**Salidas, en este orden:**

1. **Precio sugerido** a 15 %, 20 % y 25 % de margen, con botón para fijar el margen propio.
2. **Precio final**: campo con el sugerido redondeado a precio comercial (ej. $89.900). Todo lo de abajo se recalcula con este.
3. **BREAKEVEN (CPA techo)**, en grande. En rojo si queda bajo $15.000 («no aguanta pauta en Meta Colombia»), ámbar entre $15.000 y $20.000, verde arriba.
4. **Barra de % del precio**: proveedor, flete con devoluciones, CPA real, utilidad. Se ve de un vistazo cuál de los tres mata el producto.
5. Utilidad por entregado, utilidad por pedido en Shopify, ROAS neto real, precio de comparación (P ÷ 0,7).
6. **Proyección** con el importe a gastar: pedidos totales, despachados, entregados, facturación, utilidad neta.

Cada número muestra si es **supuesto** o **real** (etiqueta pequeña).

La app trae una prueba interna con el ejemplo de la hoja (C 40.000, F 18.000, E 80 %, X 20 %, CPA 20.000, P 90.000 → BREAKEVEN 17.600, utilidad por entregado −3.750). Si alguna vez no da, la app lo dice.

> **Decisión pendiente.** La skill de pauta usa otra fórmula de CPA techo (utilidad × entrega − devolución × (1 − entrega)). La propuesta es usar solo el **BREAKEVEN de la hoja del curso** en toda la app para que haya un único número. Confírmalo.

## 4. Creativos

Rellena plantillas en código (dibujadas en `<canvas>`) y descarga PNG. Sin IA y sin costo.

**Flujo:** elegir producto → elegir plantilla → elegir tamaño → revisar los textos (vienen prellenados desde la ficha) → **Descargar**. O bien **Lote de hooks**: una plantilla × los 4–6 hooks del producto → descarga un `.zip` con todas las variantes, listas para el conjunto de prueba.

**Tamaños:** 1080×1350 (feed 4:5, el principal), 1080×1920 (historias y reels), 1080×1080 (cuadrado).

**Sistema visual Zunko** (igual que las landings): Bricolage Grotesque 800 para titulares, Instrument Sans para texto, ámbar `#E08C0B` solo para precio y llamado a la acción, fondo según la familia del producto (nogal, pino, azul noche). Marca `zunko` con la «o» en ámbar en una esquina.

### Las 7 plantillas

| # | Plantilla | Para qué | Campos |
|---|---|---|---|
| 1 | **Hook + foto** | La base del lote de prueba: misma foto, hook distinto | Hook (máx. 8 palabras), foto, sello «Pagas al recibir» |
| 2 | **Antes / después** | El contraste contra el método viejo, lo que más convierte en tráfico frío | Título, foto y 2–3 molestias del «antes»; foto y 2–3 ventajas del «con [producto]» |
| 3 | **Oferta con precio** | Remarketing y cierre | Foto, nombre, precio tachado (P ÷ 0,7), precio final, ahorro en pesos, «Envío gratis · Pagas al recibir» |
| 4 | **Precio por unidad** | Volver barato un precio alto con aritmética | «$239.990 por 1.000 luces = $240 por luz», comparación con el rango de mercado (sin marcas) |
| 5 | **3 lugares de uso** | Vender dónde se usa, no qué trae | 3 fotos pequeñas con su etiqueta (el balcón, la reja, el antejardín) + titular |
| 6 | **Garantía** | Responder el miedo de contraentrega | «Si no te sirve, no lo pagas», tres puntos: no pagas nada por adelantado · 5 días hábiles de retracto (Ley 1480 de 2011) · te confirmamos por WhatsApp |
| 7 | **Lleva 2** | Oferta por volumen | Precio de 1 y de 2, ahorro en pesos, foto doble |

### Reglas que la app impone (no se pueden saltar)

- **No hay campo de reseñas ni testimonios** en ninguna plantilla.
- Si la foto se marca como generada con IA, se añade sola una línea pequeña: «Imagen ilustrativa».
- Aviso si el texto trae palabras de una lista de marcas registradas comunes.
- Aviso si el hook pasa de 8 palabras o el texto se sale de la zona segura de historias (franjas de 250 px arriba y abajo).

### Más adelante: Gemini para escenas

Botón **«Generar escena»** en la foto de una plantilla (el producto en el balcón, en la reja, etc.). La app nunca guarda la clave: llama a un intermediario pequeño (un Cloudflare Worker gratis) que tiene la clave de Gemini guardada, limita las llamadas por día y solo acepta pedidos desde el dominio de la app. Las escenas se marcan como IA automáticamente.

## 5. Ajustes

- Supuestos por defecto: efectividad, cancelaciones, CPA esperado, presupuesto de prueba ($80.000), administrativos y fulfillment.
- Familias de color y logo.
- Copia de seguridad: descargar, copiar y restaurar (mismo esquema que Bolsillo).
- Instalar la app.

---

## Datos (resumen)

```js
{
  productos: [{
    id, nombre, etapa, // radar | testeo | costeo | pauta | descartado
    fotos: [{id, ia:false}], familia, // nogal | pino | noche
    proveedor: {link, costo, stock},
    competencia: [{link, precio, diasAlAire}],
    angulo, hooks: [],
    costeo: {flete, efectividad, cancelaciones, admin, fulfillment, cpa, precioFinal, real:{efectividad:false}},
    pauta: {lanzamiento, presupuesto, stockConfirmado:false, entregasConfirmadas:false,
            dias: [{fecha, creativos:[{hook, gasto, impresiones, clics, pedidos}]}]},
    decisiones: [{fecha, texto}],
    motivoDescarte
  }],
  pendientes: [{id, texto, fecha, productoId, hecho}],
  ajustes: {...}
}
```

Las fotos van en IndexedDB (no caben en `localStorage`); la copia de seguridad las incluye.

## Orden de construcción propuesto

1. Calculadora (con la prueba del ejemplo de la hoja).
2. Tablero, ficha de producto y pendientes.
3. Registro de pauta y las alertas de Hoy.
4. Plantillas de creativos 1, 2, 3 y 6, más el lote de hooks.
5. Plantillas 4, 5 y 7.
6. Intermediario y escenas con Gemini.
