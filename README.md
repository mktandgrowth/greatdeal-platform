# GreatDeal Platform

Plataforma inmobiliaria todo-en-uno para el mercado chileno: tasación, búsqueda, generación de reels y asesoría con IA.

## 🏗️ Arquitectura

Este repo es el **shell unificado** que conecta los 3 sub-productos en una sola URL pública (`greatdeal.com`). Cada sub-producto vive en su propio repo y se deploya por separado.

```
greatdeal.com/                  ← este repo (shell + home + nav)
greatdeal.com/tasar             → ia-prop (Oscar)
greatdeal.com/buscar            → ia-prop (Oscar)
greatdeal.com/reels             → greatdeal-app (Vale)
```

Vercel maneja la magia de los **rewrites** — el usuario solo ve una URL, pero internamente cada ruta sirve contenido de su sub-proyecto correspondiente.

## 📂 Repos de sub-productos

| Producto | Repo | Owner | Stack |
|---|---|---|---|
| Tasación + Búsqueda | https://github.com/oscargreene-stack/ia-prop | Oscar | Next.js 14 |
| Generación de reels | https://github.com/mktandgrowth/greatdeal-app | Vale | HTML + FastAPI |

Cada socio mantiene SU repo y deploya por separado. Cero conflictos de código.

## 🎨 Design system compartido

`shared/design.css` contiene la paleta y tipografías comunes (dark + champagne gold + Cormorant Garamond + Montserrat). **Ambas sub-apps deben importar este CSS** para mantener look unificado.

Para importarlo desde una sub-app:
```html
<link rel="stylesheet" href="https://greatdeal.com/shared/design.css">
```

O alternativamente copiar el contenido del archivo a la sub-app.

## 🚀 Deploy

Este repo es ultra simple: HTML estático + vercel.json. Vercel lo deploya en 30 segundos sin builds.

```bash
# Una sola vez:
vercel link
# Después cada cambio:
git push  # Vercel redeploya automático
```

## 📝 Para agregar/cambiar rutas

Editar `vercel.json`. Cada entrada de `rewrites` mapea una URL pública a un destino real.

```json
{
  "source": "/nueva-seccion/:path*",
  "destination": "https://otro-proyecto.vercel.app/:path*"
}
```

## 🔗 URLs en producción

- **Plataforma:** https://greatdeal-platform.vercel.app (pendiente custom domain)
- **Tasar:** https://ia-prop.vercel.app
- **Reels:** https://greatdeal-app-7b95.vercel.app

## 👥 Owners

- **Vale** (valentina@mktandgrowth.com) — Reels
- **Oscar** — Tasación + Búsqueda
