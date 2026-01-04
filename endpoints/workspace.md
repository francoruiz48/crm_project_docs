# 🗂️ API Reference: Workspace (`/workspaces`)

El recurso `workspace` administra los workspaces. Los workspaces sirven para agrupar campañas. 

---

## 🟢 Endpoints de Lectura

### 🟦 `GET /workspaces`
Obtiene el listado de workspaces que hay.

**Parámetros (Query Params)**

| Parámetro | Tipo | Default | Descripción |
| :--- | :--- | :--- | :--- |
| `only_active` | `bool` | `true` | Si es `true`, devuelve solo los  activos (visibles en formularios). Si es `false`, incluye también los deshabilitados. |
| `detailed` | `bool` | `false` | Si es `true`, devuelve el mayor detalle de la campaña |

---

### 🟦 `GET /workspaces/{id}`
Obtiene el detalle de una sola campaña por su ID.

**Parámetros (Path)**
* `id` (int): ID único de la campaña.
---

## 🟠 Endpoints de Escritura  
### 🟩 `POST /workspaces`  
Crea una nueva campaña.

**Body:**

```json
{
  "name": "iGV Youth",
  "description": "iGV Youth",
  "workspace_id": 1
}

```

| Campo | Tipo | Obligatorio | Descripción |
| --- | --- | --- | --- |
| `name` | `str` | Sí* | Nombre de la campaña |
| `description` | `str` | No | Descripción de la campaña |
| `workspace_id` | `int` | Si | Se indica el id del workspace al que pertenece la campaña |

---

### 🟧 `PUT /workspaces/{id}`  
Actualiza la información de una campaña

**Body:**

```json
{
  "name": "iGV Youth",
  "description": "iGV Youth",
  "workspace_id": 2
}
```

---

## 🔴 Endpoints de Estado y Borrado###🟥 
`DELETE /workspaces/{id}`  
Elimina físicamente la campaña junto con sus leads, y workspaces asociados.

---

### 🟧 `PUT /workspaces/disable/{id}`  
Desactivación lógica (Soft Delete).

* La campaña deja de ser visible
* Los datos históricos se conservan.

---

### 🟩 `PUT /workspaces/active/{id}`  
Restaura una campaña previamente desactivado.

* La campaña vuelve a ser visible y operativa.

```

```
