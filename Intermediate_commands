# ⚙️ Guía de Comandos Intermedios de Redis

Esta guía explica los comandos **EXPIRE**, **EXISTS**, **KEYS**, **SCAN** y **MGET**, con ejemplos y usos prácticos para clases o talleres.

---

## ⏳ 1️⃣ EXPIRE

Permite asignar un **tiempo de vida (TTL)** a una clave. Una vez pasado el tiempo, Redis elimina la clave automáticamente.

### 🧩 Sintaxis

```bash
EXPIRE clave segundos
```

### 🧪 Ejemplo

```bash
SET saludo "Hola Mundo"
EXPIRE saludo 10       # La clave 'saludo' expira en 10 segundos
TTL saludo             # Muestra cuántos segundos le quedan
```

🔹 Si esperas 10 segundos y haces:

```bash
GET saludo
```

👉 Redis responderá `(nil)` porque ya expiró.

📦 **Usos comunes:**

* Manejar sesiones de usuario
* Implementar caché temporal
* Tokens o llaves con tiempo de expiración

---

## 🧩 2️⃣ EXISTS

Verifica si una **clave existe** en la base de datos actual.

### 🧪 Ejemplo

```bash
SET usuario "Camila"
EXISTS usuario      # → 1 (existe)
EXISTS saludo       # → 0 (no existe)
```

📦 **Resultados posibles:**

* `1` → la clave existe
* `0` → la clave no existe

📘 **Uso típico:** validación de claves antes de intentar leerlas o borrarlas.

---

## 🔍 3️⃣ KEYS

Devuelve todas las claves que coinciden con un **patrón** específico.

### 🧩 Sintaxis

```bash
KEYS patron
```

### 🧪 Ejemplo

```bash
KEYS *              # Muestra todas las claves
KEYS usuario:*      # Muestra las que comienzan por 'usuario:'
KEYS tareas*        # Muestra las que comienzan por 'tareas'
```

⚠️ **Advertencia:** `KEYS` puede ser lento en bases de datos con miles de claves. Úsalo solo para desarrollo o debugging.

---

## 🧭 4️⃣ SCAN

Permite recorrer las claves de Redis de forma **segura y por lotes**. Es una versión optimizada de `KEYS` para entornos de producción.

### 🧩 Sintaxis

```bash
SCAN cursor [MATCH patron] [COUNT cantidad]
```

### 🧪 Ejemplo

```bash
SCAN 0 MATCH usuario:* COUNT 10
```

🔹 Explicación:

* `0` → cursor inicial (Redis devuelve un nuevo cursor para continuar)
* `MATCH` → filtra claves que coincidan con un patrón
* `COUNT` → número aproximado de claves por lote

💡 **Tip:** repite el comando con el nuevo cursor hasta que devuelva `0`, lo que significa que no quedan más claves.

---

## 📦 5️⃣ MGET

Permite obtener **varios valores a la vez** (solo para claves tipo String).

### 🧩 Sintaxis

```bash
MGET clave1 clave2 clave3 ...
```

### 🧪 Ejemplo

```bash
SET nombre "Laura"
SET ciudad "Bogotá"
SET edad "28"

MGET nombre ciudad edad
```

📦 **Resultado:**

```
1) "Laura"
2) "Bogotá"
3) "28"
```

👉 Ideal para reducir múltiples llamadas de red cuando se necesitan varios valores a la vez.

---

## 🧠 Resumen rápido

| Comando  | Descripción                        | Ejemplo                   | Resultado           |
| -------- | ---------------------------------- | ------------------------- | ------------------- |
| `EXPIRE` | Define tiempo de vida de una clave | `EXPIRE saludo 10`        | Se borra tras 10 s  |
| `EXISTS` | Verifica si existe una clave       | `EXISTS usuario`          | 1 o 0               |
| `KEYS`   | Lista claves por patrón            | `KEYS usuario:*`          | Claves coincidentes |
| `SCAN`   | Recorre claves por lotes (seguro)  | `SCAN 0 MATCH tareas:*`   | Claves por grupo    |
| `MGET`   | Obtiene múltiples valores          | `MGET nombre ciudad edad` | Lista de valores    |

---

🧩 **Recomendación:**

* Usa `KEYS` solo en desarrollo.
* En producción, prefiere `SCAN`.
* Combina `EXPIRE` con tus `SET` para crear cachés automáticos.

---

📘 **Ejercicio sugerido:**

1. Crea tres claves (`producto:1`, `producto:2`, `producto:3`) con nombres de productos.
2. Asigna a cada una una expiración distinta con `EXPIRE`.
3. Verifica si existen usando `EXISTS`.
4. Usa `MGET` para traer todas a la vez.
5. Recorre todas las claves con `SCAN 0 MATCH producto:*`.
