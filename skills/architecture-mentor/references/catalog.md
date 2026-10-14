# Catálogo de opciones por capa

Material de partida. Los precios y límites de planes cambian: verifícalos antes de afirmarlos.

## Forma de la aplicación
- **Web responsive**: mejor si se usa desde cualquier dispositivo y no necesita hardware.
- **PWA**: web instalable, con offline y notificaciones básicas; mejor para uso móvil sin pasar por tiendas.
- **App nativa / React Native / Flutter**: mejor si necesitas sensores, rendimiento o presencia en tiendas.
- **CLI / script**: mejor si lo usas tú solo y es automatización.

## Arquitectura
- **Monolito**: un solo despliegue. Mejor casi siempre al empezar; simple de operar y depurar.
- **Monolito modular**: monolito con fronteras internas claras; mejor si prevés crecer.
- **Serverless / funciones**: pagas por uso, sin servidor que mantener; mejor con tráfico irregular; ojo con cold starts y lock-in.
- **Microservicios**: servicios independientes; mejor solo con equipos y escalas distintas por servicio. Coste operativo alto.

## Backend
- **Python (FastAPI/Django)**: mejor si hay datos, IA o automatización, o ya lo sabes. FastAPI para APIs ligeras; Django si quieres panel de admin y todo incluido.
- **Node/TypeScript (Express/Nest/Next API)**: mejor si quieres un solo lenguaje con el front y ecosistema web.
- **Java/Kotlin (Spring)**: mejor en entornos corporativos grandes, tipado fuerte; pesado para proyectos pequeños.
- **Go**: mejor para servicios rápidos y binarios simples; menos ecosistema web "todo incluido".
- **BaaS (Supabase, Firebase)**: sin backend propio; mejor para prototipar rápido; atención al lock-in y a reglas de seguridad.

## Frontend
- **React (+ Vite o Next.js)**: ecosistema enorme, UIs ricas; Next.js si necesitas SSR/SEO.
- **Vue / Svelte**: curva más suave, menos boilerplate.
- **HTML + HTMX / plantillas del servidor**: mejor si la interactividad es poca y quieres simplicidad.

## Datos
- **SQLite**: un fichero; mejor para un usuario o pocos, sin servidor. Backup = copiar el fichero.
- **PostgreSQL**: referencia relacional; mejor por defecto para algo que crece. Gestionado (Supabase, Neon, Render) o propio.
- **NoSQL documental (MongoDB, Firestore)**: mejor si los datos son realmente documentos flexibles; no por moda.
- **Redis / cachés / colas**: solo con necesidad medida.

## Autenticación
- **Proveedor gestionado (Supabase Auth, Clerk, Auth0, Firebase)**: rápido y seguro; mejor si no quieres implementar contraseñas.
- **Propia (sesiones/JWT)**: control total, más responsabilidad de seguridad.
- **Sin auth / enlace compartido**: válido solo en red privada o uso personal.

## Hosting
- **Vercel / Netlify**: front y funciones; excelente para web estática/Next; límites en backend persistente.
- **Render / Railway / Fly.io**: contenedores y servicios con BD; mejor para backend "normal"; revisa límites del plan gratis (dormirse, expiración de BD).
- **VPS (Hetzner, DigitalOcean)**: máximo control y coste fijo bajo; tú operas todo.
- **Cloud (AWS/GCP/Azure)**: potente y complejo; mejor si necesitas servicios concretos o ya lo usas.
- **En casa (Raspberry Pi/NAS)**: gratis y privado; ojo con disponibilidad, acceso externo y backups.

## Despliegue y operación
- **Git push → despliegue automático** (proveedor o GitHub Actions); **Docker** si quieres entornos reproducibles; **backups automáticos de la BD** y prueba de restauración; **logs y alertas mínimas**.
