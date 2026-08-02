# Burnmile — landing page

Landing page estática de **Burnmile Clothing Co.** (burnmile.com), pensada para publicarse gratis en
GitHub Pages y enviar tráfico a la tienda de Etsy.

## Estructura

```
index.html      → toda la página (HTML + CSS + JS en un solo archivo)
images/logo.png → logo badge western (también se usa como favicon y como imagen de compartir)
CNAME           → dominio personalizado para GitHub Pages
```

## Cómo añadir o cambiar un producto

Todos los productos viven en un único array `PRODUCTS`, al final de `index.html`.
No hace falta tocar nada más:

```js
{
  name: "Nombre corto del diseño",
  desc: "Una frase de venta.",
  col:  "analog",          // "analog" o "road" → controla el filtro y la etiqueta
  url:  "https://www.etsy.com/listing/XXXXXXXX/slug",
  img:  "https://i.etsystatic.com/..."   // o "images/mi-foto.jpg"
}
```

### Sobre las imágenes

Ahora mismo las fotos se cargan directamente desde los servidores de Etsy (`i.etsystatic.com`).
Funciona y es cero mantenimiento, pero **si cambias la foto de portada de un listing en Etsy, la URL
cambia y aquí saldría rota**. Cuando quieras blindarlo: descarga las fotos, mételas en `images/`
y cambia el campo `img` a `images/nombre.jpg`.

---

## Publicar en GitHub Pages (gratis)

### 1. Crear el repositorio

En github.com → **New repository** → nombre `burnmile-web` → **Public** → *Create*.
(Debe ser público: GitHub Pages con dominio propio requiere plan de pago si el repo es privado.)

### 2. Subir los archivos

Desde esta carpeta:

```bash
git init -b main
git add .
git commit -m "Landing page de Burnmile"
git remote add origin https://github.com/TU-USUARIO/burnmile-web.git
git push -u origin main
```

### 3. Activar Pages

Repositorio → **Settings** → **Pages**
→ *Source*: **Deploy from a branch**
→ *Branch*: `main`, carpeta `/ (root)` → **Save**

En 1-2 minutos la web está en `https://TU-USUARIO.github.io/burnmile-web/`.

### 4. Conectar burnmile.com

En **Namecheap** → dominio `burnmile.com` → pestaña **Advanced DNS**:

1. **Borra** el registro `CNAME Record  www → parkingpage.namecheap.com` y cualquier
   *URL Redirect Record* que venga por defecto.
2. Añade estos **cuatro A Records** (Host `@`, TTL Automatic):

   | Type | Host | Value |
   |---|---|---|
   | A Record | @ | 185.199.108.153 |
   | A Record | @ | 185.199.109.153 |
   | A Record | @ | 185.199.110.153 |
   | A Record | @ | 185.199.111.153 |

3. Añade un **CNAME Record**: Host `www` → Value `TU-USUARIO.github.io.`

Después, en GitHub → **Settings → Pages → Custom domain**: escribe `burnmile.com` y guarda.
Espera a que aparezca el check verde de verificación DNS (de minutos a 24 h) y entonces
marca la casilla **Enforce HTTPS**.

> El archivo `CNAME` de este repo ya contiene `burnmile.com`, así que GitHub lo detecta solo.
> No lo borres ni le cambies el nombre.

### 5. Comprobar

- https://burnmile.com → carga la landing con candado HTTPS
- https://www.burnmile.com → redirige a la anterior

---

## Actualizar la web más adelante

```bash
git add .
git commit -m "Nuevos diseños"
git push
```

GitHub Pages redespliega solo en ~1 minuto.
