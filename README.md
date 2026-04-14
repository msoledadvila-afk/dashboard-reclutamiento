# Dashboard Reclutamiento · RRHH

Panel de seguimiento de candidatos y búsquedas para equipos de selección. Conecta con Google Sheets como fuente de datos, sin backend ni base de datos propia.

![demo](https://img.shields.io/badge/estado-demo%20activo-2dd4a0?style=flat-square) ![sheets](https://img.shields.io/badge/backend-Google%20Sheets-4f7cff?style=flat-square) ![html](https://img.shields.io/badge/stack-HTML%20vanilla-f5a623?style=flat-square)

---

## Qué hace

- Vista general con KPIs: búsquedas activas, candidatos en proceso, tiempo promedio, score promedio
- Pipeline kanban con las etapas del proceso de selección adaptadas al mercado argentino
- Tabla filtrable de candidatos con búsqueda por nombre o DNI
- Tarjetas de búsquedas con estado, urgencia, rango salarial y modalidad
- Conexión directa a Google Sheets vía Apps Script (sin exponer datos públicamente)
- Modo demo funcional sin configurar nada

---

## Stack

| Capa | Tecnología |
|---|---|
| Frontend | HTML + CSS + JS vanilla (sin frameworks) |
| Fuente de datos | Google Sheets |
| API | Google Apps Script (`doGet`) |
| Deploy | GitHub Pages |
| Tipografía | DM Sans + DM Mono |

Un solo archivo `index.html`. Sin dependencias, sin build, sin node_modules.

---

## Estructura del repositorio

```
dashboard-reclutamiento/
├── index.html                    # Dashboard completo
├── dashboard_reclutamiento.gs    # Apps Script (pegar en Google Sheets)
├── Reclutamiento_Template.xlsx   # Plantilla Excel con datos de muestra
└── README.md
```

---

## Cómo usar

### 1. Clonar o descargar

```bash
git clone https://github.com/tu-usuario/dashboard-reclutamiento.git
```

O simplemente descargá el `index.html` y abrilo en el navegador. Arranca en modo demo sin configurar nada.

### 2. Preparar el Google Sheets

1. Subí el archivo `Reclutamiento_Template.xlsx` a Google Drive
2. Abrilo → convertilo a Google Sheets
3. Extensiones → Apps Script → pegá el contenido de `dashboard_reclutamiento.gs`
4. Guardá el script
5. Implementar → Nueva implementación → Tipo: **Aplicación web**
   - Ejecutar como: **Yo mismo**
   - Quién tiene acceso: **Cualquiera**
6. Autorizá los permisos → copiá la URL generada

### 3. Conectar el dashboard

Abrí el dashboard → sección **Configuración** → pegá la URL del script → **Conectar y cargar datos**.

La URL se guarda en `localStorage`, no hay que pegarla de nuevo.

---

## Estructura del Google Sheets

El script espera tres hojas con estos nombres exactos:

| Hoja | Descripción |
|---|---|
| `Candidatos` | Registro de postulantes con etapa, estado y evaluaciones |
| `Búsquedas` | Puestos a cubrir con urgencia, modalidad y rango salarial |
| `Pipeline` | Historial de movimientos de etapa por candidato |

### Etapas del pipeline (mercado argentino)

```
CV Recibido → Pre-filtro → Entrevista RRHH → Evaluación Técnica
→ Psicotécnico → Referencias → Entrevista Final → Propuesta → Ingresado
```

### Fórmula de score

```
Score = (Ev. Técnica × 40%) + (Competencias × 35%) + (Fit Cultural × 25%) × 20
```

Escala de 0 a 100. Se calcula automáticamente en el Sheets.

---

## API endpoints

La URL del Apps Script acepta el parámetro `action`:

| Endpoint | Descripción |
|---|---|
| `?action=all` | Candidatos + búsquedas + pipeline (default) |
| `?action=candidatos` | Solo candidatos |
| `?action=busquedas` | Solo búsquedas |
| `?action=stats` | KPIs precalculados |

Para restringir acceso, activá el token en el script:

```javascript
const CONFIG = {
  TOKEN: "mi-token-secreto",
  ...
};
```

Y llamá con `?action=all&token=mi-token-secreto`.

---

## Deploy en GitHub Pages

1. Subí `index.html` a la raíz del repositorio
2. Settings → Pages → Branch: `main` → `/` (root) → Save
3. En 2 minutos queda publicado en `https://tu-usuario.github.io/dashboard-reclutamiento`

---

## Roadmap

- [x] Dashboard de solo lectura con conexión a Google Sheets
- [x] Pipeline kanban
- [x] Tabla de candidatos filtrable
- [x] Modo demo sin configuración
- [ ] Escritura desde el dashboard (agregar candidato, cambiar etapa)
- [ ] Notificaciones de búsquedas estancadas
- [ ] Exportación de reportes
- [ ] Multiusuario con roles

---

## Parte de

Este proyecto es parte del repositorio **MSV Vibe Coder** — una colección de dashboards, apps internas y herramientas de automatización para profesionales independientes y pymes.

| # | Proyecto | Estado |
|---|---|---|
| 01 | Dashboard Contadora | En desarrollo |
| 02 | Dashboard Reclutamiento RRHH | ✅ Activo |
| 03 | App Prompts RRHH | Próximamente |
| 04 | CRM Simple | Próximamente |
| 05 | Herramientas Freelance | Próximamente |
| 06 | Soluciones Pymes | Próximamente |

---

## Autora

**MSV · Vibe Coder & Arquitecta Digital**  
Diseño y construcción de soluciones simples, eficientes y escalables para profesionales independientes, pymes y equipos de RRHH.

---

*Construido con Vibe Coding. Sin over-engineering.*
