# 🥜 HealthyNuts

Tienda web de **frutos secos y fruta deshidratada** premium, orientada a atletas (entrenamiento cruzado, híbridos, halterofilia, ciclismo, gimnastas) y a toda la familia. Nutrición deportiva **basada en evidencia**. Pago con **Mercado Pago**.

Sitio estático, listo para **GitHub Pages**. Sin dependencias ni build.

---

## 🚀 Publicar en GitHub Pages

1. Crea un repositorio nuevo en GitHub (ej. `healthynuts`).
2. Sube el contenido de esta carpeta (`healthynuts-site/`) a la raíz del repo:
   ```bash
   cd healthynuts-site
   git init
   git add .
   git commit -m "HealthyNuts: sitio inicial"
   git branch -M main
   git remote add origin https://github.com/TU-USUARIO/healthynuts.git
   git push -u origin main
   ```
3. En GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, elige `main` y carpeta `/ (root)`. Guarda.
4. En 1–2 minutos tu tienda estará en `https://TU-USUARIO.github.io/healthynuts/`.

> El archivo `.nojekyll` ya está incluido para que GitHub Pages sirva los assets tal cual.

---

## ⚙️ Configuración (precios, Mercado Pago y WhatsApp)

Todo se edita en **un solo archivo**: [`js/products.js`](js/products.js). No necesitas tocar nada más.

### 1) Link de pago de Mercado Pago
```js
const CONFIG = {
  mercadoPagoLink: "https://mpago.la/XXXXXXX",   // ← pega aquí tu link
  ...
}
```
Cómo obtenerlo: en tu cuenta de Mercado Pago → **Cobros → Link de pago** (o *Checkout*), genera un link y pégalo. Mientras esté vacío, el botón avisará que falta configurarlo.

> Nota: en un sitio 100% estático el link de Mercado Pago no puede calcular el total dinámico de forma segura. Por eso, al pulsar **Pagar con Mercado Pago** la web copia el resumen del pedido al portapapeles y abre tu link. Para cobro automático por monto necesitarías un pequeño backend (ver más abajo).

### 2) WhatsApp (opcional, recomendado)
```js
  whatsappNumber: "5214771234567",   // formato internacional, solo dígitos
```
Con esto aparece el botón **Enviar pedido por WhatsApp**, que manda el pedido completo (productos, gramaje, cantidad) a tu número. Ideal para confirmar y cobrar manualmente. Si lo dejas vacío, el botón se oculta.

### 3) Precios por gramaje
Los gramajes son fijos: **250 g, 500 g y 1 kg**. Solo completa los precios cuando los tengas:
```js
{
  id: "almendras",
  ...
  prices: { 250: 75, 500: 140, 1000: 260 }   // en MXN; null = "Precio pendiente"
}
```
Mientras un precio sea `null`, la web muestra *"Precio pendiente"* y el total como *"Por confirmar"*.

---

## 🗂️ Estructura

```
healthynuts-site/
├── index.html              # Página única
├── css/styles.css          # Estilos (paleta salud & bienestar)
├── js/
│   ├── products.js         # ← EDITA AQUÍ: precios, MP, WhatsApp, productos
│   └── main.js             # Lógica del carrito y checkout
├── assets/
│   ├── logo/               # Isotipo, wordmark, foto de perfil, brand.css
│   ├── mascot/             # Almendro (base + 3 variantes / stickers)
│   └── products/           # Ilustraciones de cada producto
├── .nojekyll
├── BRANDING.md             # Guía de marca
└── README.md
```

## 🎨 Marca
Ver [`BRANDING.md`](BRANDING.md) para paleta de colores, tipografías y uso del logo y la mascota.

## 💳 (Opcional) Cobro automático con monto
Si más adelante quieres que Mercado Pago cobre el total exacto automáticamente, se necesita un backend mínimo que cree una *preference* con el Access Token (no se puede exponer en el navegador). Opciones sencillas: una función serverless en Vercel/Netlify/Cloudflare Workers. Avísame y lo añadimos.
