# 📋 CONTEXTO DEL PROYECTO - Portfolio Astro

## 🎯 MISIÓN
Crear un portfolio personal profesional integrado con Hub Personal (aplicación de notas).

## 📍 UBICACIONES IMPORTANTES

### Local (Development)
- **Ruta:** `C:\Users\JoseA\portfolio\`
- **Repo:** https://github.com/c0hete/astro-portfolio
- **GitHub User:** c0hete

### Server (Production)
- **IP:** 147.93.176.241
- **SSH:** `ssh root@147.93.176.241`
- **Portfolio Path:** `/var/www/portfolio/`
- **Hub Path:** `/var/www/hub/`
- **Mail:** mail.alvaradomazzei.cl (Mailcow)

### Local Hub Development
- **Ruta:** `C:\Users\JoseA\Projects\hub-personal\`
- **Repo:** https://github.com/c0hete/hub-personal
- **User:** c0hete

---

## ✅ COMPLETADO

### FASE 1: Infraestructura (COMPLETADA)
- ✅ PostgreSQL 15 container (Docker)
- ✅ PHP-FPM 8.3 container (Docker) 
- ✅ Nginx reverse proxy configurado
- ✅ SSL/TLS con LetsEncrypt
- ✅ Database migrations ejecutadas
- ✅ Git SSH keys generadas en servidor

### Portfolio Astro (COMPLETADO)
- ✅ Proyecto Astro creado desde cero
- ✅ Inicializado Git repository
- ✅ Pusheado a GitHub (c0hete/astro-portfolio)
- ✅ Buildado y desplegado en servidor
- ✅ **SIRVIENDO EN:** https://alvaradomazzei.cl/ (HTTP 200)
- ✅ Deploy script creado (deploy.sh)
- ✅ .gitignore configurado (seguridad)
- ✅ Local development setup completado

---

### Hub Laravel (COMPLETADO)
- ✅ HTTP 500 error SOLUCIONADO
- ✅ Permisos de storage/bootstrap corregidos
- ✅ Rutas funcionando: /hub (HTTP 302) → /dashboard (HTTP 200)
- **SIRVIENDO EN:** https://alvaradomazzei.cl/hub (Redirect a dashboard)

## ⚠️ EN PROGRESO / PENDIENTE

### DNS PTR Records
- **Status:** Pending
- **Objetivo:** Arreglar reverse DNS para que Gmail acepte emails
- **Ubicación:** Contabo control panel
- **Acción:** Configure reverse DNS en Contabo

---

## 🚀 WORKFLOW DESARROLLO

### Setup Local (Ya Hecho)
```bash
cd C:\Users\JoseA\portfolio
npm install
```

### Development Local
```bash
npm run dev
# Abre http://localhost:3000 con hot-reload
```

### Editar Pages/Components
- **Pages:** `src/pages/*.astro` (se convierten en rutas automáticamente)
- **Components:** `src/components/*.astro`
- **Estilos:** `src/styles/`
- **Activos:** `public/`

### Deploy a Servidor
```bash
./deploy.sh
# Automáticamente:
# 1. npm run build
# 2. Crea tarball de dist/
# 3. Sube a servidor vía SCP
# 4. Extrae en /var/www/portfolio/dist/
# 5. Fija permisos
```

### Git Workflow
```bash
git add .
git commit -m "feat: description"
git push origin main
# NOTA: deploy.sh NO se incluye en Git (en .gitignore)
```

---

## 🔐 SEGURIDAD - NUNCA COMMITEAR

Archivos/información que NUNCA deben subirse a Git:
- `.env` (variables de ambiente)
- `*.key`, `*.pem` (certificados/keys)
- `deploy.sh` (scripts de deployment)
- Cualquier archivo con credenciales
- Documentación interna/sensible

**Ver `.gitignore` para lista completa**

---

## 🌐 ARQUITECTURA ACTUAL

```
Internet (HTTPS)
    ↓
Nginx (alvaradomazzei.cl)
    ├─ / → Portfolio Astro (/var/www/portfolio/dist/) ✅ HTTP 200
    ├─ /hub → Laravel Hub (/var/www/hub) ✅ HTTP 302 → /dashboard (HTTP 200)
    └─ mail.alvaradomazzei.cl → Mailcow ✅ HTTP 200

Docker Network (app-network)
    ├─ app_php (PHP-FPM 8.3)
    ├─ app_postgres (PostgreSQL 15)
    └─ mailcow-dockerized (17 containers)
```

---

## 📝 PRÓXIMOS PASOS

### Inmediatos
1. **Crear contenido en Portfolio**
   - Editar `src/pages/index.astro` (home)
   - Crear `src/pages/about.astro`
   - Crear `src/pages/projects.astro`
   - Crear `src/pages/contact.astro`

2. **Agregar estilos**
   - Usar CSS en `src/styles/`
   - O integrar Tailwind/UI framework si deseas

3. **Agregar assets**
   - Fotos, logos en `public/`
   - Imágenes de proyectos

### Medium Term
1. **Arreglar Hub HTTP 500**
   - Investigar logs de Laravel
   - Revisar Inertia.js configuration
   - Posibles causas: rutas no encontradas, componentes Vue faltantes

2. **Configurar DNS PTR**
   - Para que emails desde Hub se entreguen correctamente

3. **Integrar Hub con Portfolio**
   - Decidir si se accede desde /hub o dominio separado
   - Configurar navegación entre ambos

---

## 📦 ÚTILES - MOVER DESDE JRAM-Portfolio

**ARCHIVOS A COPIAR SI NECESITAS:**

De `C:\Users\JoseA\OneDrive\Desktop\JRAM-Portfolio\`:
- `FASE-1-COMPLETADO.md` - Resumen de FASE 1 completada
- `ENTREGA-FASE-1.txt` - Checklist de deployment
- Scripts de deployment (si necesitas recrear infraestructura):
  - `01-DEPLOY-FASE1-docker-network.sh`
  - `02-DEPLOY-FASE1-postgres.sh`
  - `03-DEPLOY-FASE1-php-fpm.sh`
  - `04-DEPLOY-FASE1-nginx.sh`
  - `05-DEPLOY-FASE1-migrate.sh`
- Config files:
  - `Dockerfile.php-fpm`
  - `php.ini`
  - `www.conf`

---

## 🔧 COMANDOS ÚTILES

### Local Development
```bash
cd C:\Users\JoseA\portfolio

# Iniciar dev server
npm run dev

# Build para producción
npm run build

# Preview del build local
npm run preview

# Deploy a servidor
./deploy.sh
```

### Server (SSH)
```bash
ssh root@147.93.176.241

# Ver contenedores
docker ps

# Logs
docker logs app_php
docker logs app_postgres
tail -f /var/log/nginx/portfolio_error.log

# Restart servicios
docker restart app_php
sudo systemctl reload nginx

# Ver archivos
ls -la /var/www/portfolio/
ls -la /var/www/hub/
```

### Git
```bash
cd C:\Users\JoseA\portfolio

# Ver estado
git status

# Commit y push
git add .
git commit -m "feat: description"
git push origin main

# Ver historial
git log --oneline -10
```

---

## 📞 CONTACTOS/REFERENCIAS

- **GitHub User:** c0hete
- **Email:** jose.alvarado.mazzei@gmail.com
- **Server IP:** 147.93.176.241
- **Domain:** alvaradomazzei.cl

---

## 📚 DOCUMENTOS RELACIONADOS

En esta carpeta:
- `README.md` - Proyecto Astro README
- `.gitignore` - Seguridad

En JRAM-Portfolio:
- `FASE-1-COMPLETADO.md` - Resumen infraestructura
- `ENTREGA-FASE-1.txt` - Checklist
- Deployment scripts

---

**Última actualización:** 2025-11-25
**Status:** ✅ Desarrollo Local + Producción COMPLETO
- Portfolio: ✅ HTTP 200
- Hub: ✅ HTTP 200 (redirect a /dashboard)
- Mail: ✅ HTTP 200
- Database: ✅ Migrations completadas
