# 🗂️ API Reference: Campaña (`/campaigns`)

El recurso `campaigns` administra las camapañas. Las campañas sirven para agrupar leads. 

---

## 🟢 Endpoints de Lectura

### 🟦 `GET /campaigns`
Obtiene el listado de campañas que hay en el sistema.

**Parámetros (Query Params)**

| Parámetro | Tipo | Default | Descripción |
| :--- | :--- | :--- | :--- |
| `only_active` | `bool` | `true` | Si es `true`, devuelve solo las campañas activas. Si es `false`, incluye también los deshabilitados. |
| `detailed` | `bool` | `false` | Si es `true`, devuelve el mayor detalle de la campaña |

---

### 🟦 `GET /campaigns/{id}`
Obtiene el detalle de una sola campaña por su ID.

**Parámetros (Path)**
* `id` (int): ID único de la campaña.
---

## 🟠 Endpoints de Escritura  
### 🟩 `POST /campaigns`  
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

### 🟧 `PUT /campaigns/{id}`  
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
`DELETE /campaigns/{id}`  
Elimina físicamente la campaña junto con sus leads, y nomencladores asociados.

---

### 🟧 `PUT /campaigns/disable/{id}`  
Desactivación lógica (Soft Delete).

* La campaña deja de ser visible
* Los datos históricos se conservan.

---

### 🟩 `PUT /campaigns/active/{id}`  
Restaura una campaña previamente desactivado.

* La campaña vuelve a ser visible y operativa.

```

```
