## 🟦 POST /api/campos-personalizados

### 📘 Descripción
Crea un nuevo campo personalizado para los leads.

---

### 🔐 Autenticación
Requiere token JWT válido en el header:
`Authorization: Bearer <token>`

---

### 📨 Request (Body)
```json
{
  "nombre": "interes_principal",
  "etiqueta": "Interés principal",
  "tipo": "string",
  "requerido": true
}
