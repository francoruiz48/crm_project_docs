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
Obtiene el detalle de un solo workspace por su ID.

**Parámetros (Path)**
* `id` (int): ID único
---

## 🟠 Endpoints de Escritura  
### 🟩 `POST /workspaces`  
Crea un nuevo workspace.

**Body:**

```json
{
  "name": "Equipo X",
  "description": "Equipo de ejemplo"
}

```

| Campo | Tipo | Obligatorio | Descripción |
| --- | --- | --- | --- |
| `name` | `str` | Sí* | Nombre del workspace |
| `description` | `str` | No | Descripción del workspace |

---

### 🟧 `PUT /workspaces/{id}`  
Actualiza la información de un workspace

**Body:**

```json
{
  "name": "iGV Youth",
  "description": "iGV Youth",
}
```

---

## 🔴 Endpoints de Estado y Borrado###🟥 
`DELETE /workspaces/{id}`  
Elimina físicamente el wokspace junto con sus campañas asociadas, y su vez borra los leads de los campañas. 

---

### 🟧 `PUT /workspaces/disable/{id}`  
Desactivación lógica (Soft Delete).

* El workspace deja de ser visible
* Los datos históricos se conservan.

---

### 🟩 `PUT /workspaces/active/{id}`  
Restaura un workspace previamente desactivado.

* El workspace vuelve a ser visible y operativa.

```

```
