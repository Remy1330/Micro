# FlotaCost — Calculadora de Viajes de Transporte
**Versión 1.0 | PWA — Funciona offline**

---

## ¿Qué incluye?
```
flotacost/
├── index.html      ← App principal (toda la lógica)
├── manifest.json   ← Configuración PWA (ícono, nombre, colores)
├── sw.js           ← Service Worker (funcionalidad offline)
└── README.md       ← Este archivo
```

---

## Cómo instalar / usar

### Opción 1: En tu computadora (sin servidor)
1. Abrí la carpeta `flotacost/`
2. Doble clic en `index.html`
3. Se abre en tu navegador — listo para usar

> ⚠️ El modo offline y la instalación como app requieren un servidor (ver opciones abajo)

---

### Opción 2: Instalar como app en el celular (recomendado)
Para que funcione como app nativa en Android/iPhone necesitás servirla con HTTPS.

**Forma más fácil — Netlify Drop (gratis, 2 minutos):**
1. Ve a https://app.netlify.com/drop
2. Arrastrá toda la carpeta `flotacost/` a la pantalla
3. Netlify te da una URL tipo `https://nombre-random.netlify.app`
4. Abrí esa URL en el celular
5. Android: menú del navegador → "Agregar a pantalla de inicio"
6. iPhone (Safari): botón compartir → "Agregar a pantalla de inicio"

**Otras opciones gratuitas:**
- **GitHub Pages**: sube los archivos a un repositorio y activa Pages
- **Vercel**: arrastrá la carpeta en https://vercel.com/new

---

### Opción 3: Servidor local para desarrollo
Si tenés Node.js instalado:
```bash
cd flotacost
npx serve .
# Abrí http://localhost:3000
```

Si tenés Python:
```bash
cd flotacost
python -m http.server 8080
# Abrí http://localhost:8080
```

---

## Agregar íconos de la app (opcional pero recomendado)
El `manifest.json` referencia dos íconos que debés crear:
- `icon-192.png` — 192×192 px
- `icon-512.png` — 512×512 px

Podés usar https://favicon.io o Canva para crearlos con el logo de tu empresa.
Si no los agregás, la app funciona igual pero sin ícono personalizado.

---

## Funcionalidades incluidas

| Feature | Estado |
|---|---|
| Cálculo de costo base (km × $0.48) | ✅ |
| Precio de combustible (diésel/gasolina) | ✅ Editable |
| Costos variables por viaje | ✅ |
| Costos fijos prorrateados por viaje | ✅ Con toggle |
| Margen de ganancia con slider | ✅ 5%–150% |
| Múltiples paradas en la ruta | ✅ |
| Soporte flota mixta (bus + sedan) | ✅ |
| Historial de cálculos (hasta 20) | ✅ Guardado local |
| Compartir cotización | ✅ |
| Funciona sin internet | ✅ Tras primera carga |
| Instalable como app | ✅ Con HTTPS |
| Diseño responsive (móvil/escritorio) | ✅ |

---

## Próximas mejoras planeadas
- [ ] Integración Google Maps (cálculo automático de km por dirección)
- [ ] Precio diésel en tiempo real (API Ministerio de Economía SV)
- [ ] Exportar cotización como PDF
- [ ] Soporte múltiples vehículos con perfiles guardados
- [ ] Modo multi-usuario con sincronización en la nube

---

## Variables de cálculo
```
Costo Base        = km × $0.48 (ajustable)
Combustible       = (km ÷ km/gal) × precio_combustible
Costos Variables  = Motorista + Imprevistos + Limpieza
Costos Fijos/viaje= (Cuota + Seguro + Mant.) ÷ viajes_mes
Costo Operativo   = Base + Combustible + Variables + Fijos/viaje
Precio Final      = Costo Operativo × (1 + margen/100)
```
