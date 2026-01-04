# 🗂️ API Reference: Campaña (`/campaigns`)

El recurso `campaigns` administra las camapañas. Las campañas sirven para agrupar leads. 

---

## 🟢 Endpoints de Lectura

### 🟦 `GET /campaigns`
Obtiene el listado de tipos de datos configurados en el sistema.

**Parámetros (Query Params)**

| Parámetro | Tipo | Default | Descripción |
| :--- | :--- | :--- | :--- |
| `only_active` | `bool` | `true` | Si es `true`, devuelve solo los tipos de datos activos (visibles en formularios). Si es `false`, incluye también los deshabilitados. |
| `detailed` | `bool` | `false` | Si es `true`, devuelve el mayor detalle de la campaña |

---

### 🟦 `GET /campaigns/{id}`
Obtiene el detalle de una sola campaña por su ID.

**Parámetros (Path)**
* `id` (int): ID único de la campaña.
---

## 🟢 Endpoints de Escritura
