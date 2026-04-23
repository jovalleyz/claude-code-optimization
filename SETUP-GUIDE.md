# CLAUDE CODE OPTIMIZATION — Setup Guide for New Projects

**Tiempo:** 10 minutos | **Dificultad:** Muy fácil | **Impacto:** 65-75% token reduction

---

## QUÉ TIENES

3 templates genéricos **reutilizables** para cualquier proyecto nuevo en Claude Code:

1. **`claude.md`** — Contexto optimizado para cada sesión
2. **`MEMORY-CORE.md`** — Esenciales comprimidos (schema, endpoints, patterns)
3. **`.claudeignore`** — Archivos que Claude NO debe cargar

---

## POR QUÉ IMPORTA

Claude en Antigravity IDE (o Claude Code) carga automáticamente estos archivos cada sesión.

**Sin optimization:**
```
Sesión 1: Pierdes 2-3 turnos contextualizando
Costo: 30-40% tokens en setup inútil
```

**Con optimization:**
```
Sesión 1: Contexto automático desde inicio (-30-40% tokens)
Sesión 2+: Caching + compactación (-65-75% tokens)
```

---

## CÓMO USARLOS

### Paso 1: Copiar templates a tu proyecto

Cuando empieces un proyecto nuevo:

```bash
# En la raíz del proyecto
cp claude.md-TEMPLATE claude.md
cp MEMORY-CORE.md-TEMPLATE MEMORY-CORE.md
cp .claudeignore-TEMPLATE .claudeignore
```

### Paso 2: Personalizar para tu proyecto

Abre `claude.md` y reemplaza **TODOS los placeholders** (busca `[PLACEHOLDER]`):

```markdown
# [PROJECT_NAME] — Claude Context Template
↓
# My Awesome App — Claude Context
```

**Secciones a personalizar:**

#### STACK
```markdown
## 🏗️ STACK

- **Frontend:** [React 18 + Vite / Next.js / Vue / etc]
- **Backend:** [Firebase / Node.js / Python / etc]
- **Database:** [Firestore / PostgreSQL / MongoDB / etc]
- **AI/LLM:** [Gemini / Claude API / OpenAI / etc]
- **Hosting:** [Vercel / Firebase / AWS / etc]
- **Auth:** [Firebase Auth / NextAuth / JWT / etc]
```

Reemplaza con TU stack real:

```markdown
## 🏗️ STACK

- **Frontend:** React 18 + Vite + TypeScript
- **Backend:** Firebase Cloud Functions
- **Database:** Firestore
- **AI/LLM:** Gemini 2.0 Flash
- **Hosting:** Vercel (frontend) + Firebase (backend)
- **Auth:** Firebase Authentication
```

#### DATABASE SCHEMA
```markdown
## 📊 DATABASE SCHEMA (Current)

### Main Collections/Tables

```
[COLLECTION_1]/{id}
├── field1, field2
├── relationship to [COLLECTION_2]
└── timestamps
```

Reemplaza con TU schema actual. Ejemplo:

```
users/{uid}
├── email, displayName
├── createdAt, updatedAt
└── preferences {}

products/{id}
├── name, description, price
├── userId (creator)
├── inventory (quantity)
└── createdAt
```

#### KEY ENDPOINTS
```markdown
| Endpoint | Method | Purpose | Auth |
|----------|--------|---------|------|
| `/api/endpoint1` | POST | Description | User/Admin |
```

Reemplaza con TUS endpoints. Ejemplo:

```
| `/api/products` | GET | List all products | Public |
| `/api/products` | POST | Create product | Admin |
| `/api/products/{id}` | PUT | Update product | Admin |
| `/api/cart/add` | POST | Add to cart | User |
```

#### CRITICAL FILES
```markdown
| File | Lines | Risk | Reason |
|------|-------|------|--------|
| `App.jsx / main.jsx` | XXX | 🔴 | Auth/state management hub |
```

Reemplaza con TUS archivos críticos:

```
| `src/App.jsx` | 1,200 | 🔴 | Auth state + main render |
| `src/components/ProductCard.jsx` | 350 | 🟡 | High reuse, layout critical |
| `src/services/api.js` | 500 | 🔴 | All API calls |
```

#### CODE PATTERNS
```javascript
// Replace this section with YOUR actual patterns
// Examples:
// - How you name components/functions
// - How you structure database queries
// - How you handle errors
// - How you structure custom hooks
```

Ejemplo:

```javascript
// Components: PascalCase, functional + hooks only
UserProfile.jsx

// Database queries: Always filter by userId first
const q = query(collection(db, 'products'),
  where('userId', '==', currentUser.uid)
);

// Error handling
try {
  // operation
} catch(error) {
  if (error.code === 'permission-denied') {
    // redirect to login
  }
}
```

#### SECURITY NOTES
```markdown
**Critical security rules:**
1. [Rule 1] - [Explanation]
2. [Rule 2] - [Explanation]
```

Ejemplo:

```markdown
**Critical security rules:**
1. Users can only read/write their own data
2. Admin endpoints require backend verification (never trust client)
3. Never log sensitive data (passwords, tokens, API keys)
4. Validate all user input before database operations
```

#### KNOWN BUGS / GOTCHAS
```markdown
| ID | Problem | Root Cause | Fix | Status |
|----|---------|-----------|-----|--------|
| BUG-001 | [Description] | [Cause] | [Solution] | ✅ Fixed |
```

Ejemplo (empty at start, fill as you discover bugs):

```markdown
| ID | Problem | Root Cause | Fix | Status |
|----|---------|-----------|-----|--------|
| BUG-001 | Users can't upload images >5MB | No size validation | Add client-side check | ✅ Fixed |
| BUG-002 | Race condition on rapid adds | No atomic transaction | Use Firestore batch | 🔄 Monitoring |
```

### Paso 3: Personalizar MEMORY-CORE.md

Similar a `claude.md`, pero más comprimido:

```markdown
## 📊 SCHEMA / DATA MODEL (Current)

```
users/{uid}
├── email (string)
├── displayName (string)
└── createdAt (timestamp)

products/{id}
├── name, description, price
├── userId (creator)
└── inventory
```

## 🔗 KEY ENDPOINTS / API

```
GET /api/products
  Returns: [{id, name, price, inventory}]
  Auth: Public

POST /api/products
  Input: {name, description, price, inventory}
  Auth: Admin
```

[Include only the essential patterns + gotchas specific to YOUR project]
```

### Paso 4: Personalizar .claudeignore

Generalmente funciona como está, pero ajusta si necesario:

```
node_modules/
dist/
build/
.env*
docs/
[ADD CUSTOM FOLDERS IF NEEDED]

# Keep these:
# ✅ src/
# ✅ package.json
# ✅ claude.md
# ✅ MEMORY-CORE.md
```

**Ejemplos por framework:**

**Next.js:**
```
.next/        ← Add
out/          ← Add (static export)
```

**Django:**
```
venv/         ← Add
migrations/   ← Maybe (if huge)
```

**Monorepo:**
```
packages/*/node_modules/    ← Be specific
apps/*/dist/                ← Be specific
```

### Paso 5: Commit y push

```bash
git add claude.md MEMORY-CORE.md .claudeignore
git commit -m "docs: add claude code optimization files (token efficiency)"
git push
```

---

## PRÓXIMA SESIÓN EN CLAUDE CODE

1. Abre tu IDE (Antigravity, VS Code + Claude extension, etc)
2. Abre Claude Code widget
3. Claude **automáticamente** carga:
   - ✅ `claude.md`
   - ✅ `MEMORY-CORE.md`
   - ✅ Respeta `.claudeignore`

**Listo.** Sin hacer nada más.

---

## ACTUALIZAR CON EL TIEMPO

**`claude.md` actualizar si:**
- [ ] Cambias framework/stack (React → Vue, Firebase → Node, etc)
- [ ] Agregas librería crítica nueva
- [ ] Cambias endpoints principales
- [ ] Cambias hosting/deployment

**Frecuencia:** Raro (1-2 veces/año)

**`MEMORY-CORE.md` actualizar si:**
- [ ] Cambias schema (agregar/remover campos, collections)
- [ ] Agregas/eliminas endpoints
- [ ] Descubres bug importante (agrega a tabla)
- [ ] Agregas patrón/gotcha nuevo

**Frecuencia:** Ocasional (1-2 veces/mes)

**`.claudeignore` actualizar si:**
- [ ] Agregas carpeta grande nueva (data/, cache/, etc)
- [ ] Cambias estructura radicalmente

**Frecuencia:** Raro (1-2 veces/año)

---

## STRUCTURE RECOMENDADA

```
your-project/
├── src/
│   ├── components/
│   ├── pages/
│   ├── services/
│   ├── utils/
│   └── App.jsx
├── public/
├── .env.example
├── package.json
├── claude.md          ← Auto-loaded by Claude Code
├── MEMORY-CORE.md     ← Auto-loaded by Claude Code
├── .claudeignore      ← Respected by Claude Code
└── docs_optimized/    ← OPTIONAL (reference archive)
    ├── session-log-*.md
    ├── SESSION-DIGEST.md
    └── MEMORY.md
```

---

## TIPS POR TIPO DE PROYECTO

### Frontend Only (React, Vue, Svelte)

**En `claude.md` STACK:**
```
- Frontend: React 18 + Vite + TypeScript
- State: Context API / Zustand
- Styling: Tailwind CSS
- Build: Vite
```

**En `MEMORY-CORE.md` PATTERNS:**
```
- Components: PascalCase, functional + hooks
- Custom hooks: useData, useFetch in hooks/ folder
- Styling: Utility-first Tailwind
```

### Backend Only (Node, Python, Go)

**En `claude.md` STACK:**
```
- Backend: Node.js + Express / FastAPI / Gin
- Database: PostgreSQL / MongoDB
- Auth: JWT / Session
- API: REST / GraphQL
```

**En `MEMORY-CORE.md` PATTERNS:**
```
- Routes: /api/v1/resource/{id}
- Middleware: authentication, validation, error-handling
- Database: Connection pooling, migrations
- Testing: Jest / PyTest
```

### Full Stack (Frontend + Backend)

**En `claude.md` STACK:**
```
- Frontend: React 18 + Vite
- Backend: Firebase / Node.js + Express
- Database: Firestore / PostgreSQL
- Hosting: Vercel (frontend) + Cloud Run/Heroku (backend)
```

**En `MEMORY-CORE.md` PATTERNS:**
```
- Frontend queries: Always include userId filter
- Backend auth: Verify Firebase token before operations
- Async operations: Use Promise.all for parallel requests
```

### AI/ML Project (Python)

**En `claude.md` STACK:**
```
- Runtime: Python 3.10+
- Framework: FastAPI / Flask
- ML: TensorFlow / PyTorch / scikit-learn
- LLM: Gemini API / Claude API / OpenAI
```

**En `MEMORY-CORE.md` PATTERNS:**
```
- Models: In models/ folder
- Training: notebooks/ for experiments
- Inference: API routes with model caching
- Rate limits: Track API usage
```

---

## CHECKLIST PARA CADA PROYECTO NUEVO

Cuando empieces un proyecto nuevo:

- [ ] Copiar templates (`claude.md-TEMPLATE`, etc) a raíz
- [ ] Renombrar: Remove `-TEMPLATE` suffix
- [ ] Buscar TODOS los `[PLACEHOLDER]` en `claude.md`
- [ ] Reemplazar con tus valores reales
- [ ] Buscar TODOS los `[PLACEHOLDER]` en `MEMORY-CORE.md`
- [ ] Reemplazar con tus valores reales
- [ ] Ajustar `.claudeignore` si necesario (usualmente no)
- [ ] Commit + push a GitHub
- [ ] ✅ Próxima sesión Claude Code: Optimización activa

**Tiempo total:** 10-15 minutos

---

## ANTES vs DESPUÉS

### SIN Optimization

```
Abre Claude Code → Sin contexto
"¿Cuál es tu schema?"
Claude responde genéricamente (training data)
Pierdes 2-3 turnos re-contextualizando
Gastas 30-40% tokens en setup inútil
```

### CON Optimization

```
Abre Claude Code → Carga automático claude.md + MEMORY-CORE.md
"¿Cuál es tu schema?"
Claude responde con TU schema específico
Primer turno ya productivo
Ahorras 30-40% tokens sesión 1
Ahorras 65-75% tokens sesión 2+ (con caching)
```

---

## PREGUNTAS FRECUENTES

**P: ¿Puedo usar los templates sin personalizar?**
A: No. Los placeholders son inútiles. Dedica 10 minutos — vale mucho la pena.

**P: ¿Obligatorio crear `docs_optimized/` también?**
A: No. Es para archivar `session-log-*.md` y `SESSION-DIGEST.md`. Útil si el proyecto tiene vida larga.

**P: ¿Qué pasa si cambio stack a mitad del proyecto?**
A: Edita `claude.md` (5 minutos). Claude cargará el nuevo context próxima sesión.

**P: ¿Cuántos tokens ahorro realmente?**
A: 30-40% sesión 1, 65-75% sesión 2+ (con caching + `/compact`).

**P: ¿Funciona en todos los IDEs?**
A: Sí. Cualquier IDE que soporte Claude Code (Antigravity, VS Code extension, etc).

**P: ¿Debo hacer update frecuente?**
A: No. Actualiza `claude.md` 1-2 veces/año. `MEMORY-CORE.md` 1-2 veces/mes. `.claudeignore` raramente.

**P: ¿Y si mi proyecto es muy pequeño?**
A: Aún vale. Incluso en proyectos small, ahorras tokens significativamente.

**P: ¿Puedo compartir los templates?**
A: Sí, totalmente. Están hechos para compartir. Manda a tus compañeros.

---

## RESUMEN RÁPIDO

**3 archivos. 15 minutos. 65-75% token reduction.**

1. Copiar templates a tu proyecto
2. Personalizar placeholders
3. Commit + push
4. Próxima sesión: ¡automático!

---

**Made for sharing with your community. Happy coding.**
