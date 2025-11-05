# 🧩 Taller 2: Comandos Intermedios de Redis

Este taller está diseñado para practicar los comandos **EXPIRE**, **EXISTS**, **KEYS**, **SCAN** y **MGET** en Redis. A través de ejercicios guiados, los estudiantes comprenderán cómo administrar la vida útil de las claves, buscar datos eficientemente y realizar consultas múltiples.

---

## 🎯 Objetivo general

Aprender a utilizar comandos intermedios de Redis para:

* Manejar tiempos de expiración de datos.
* Validar la existencia de claves.
* Buscar claves por patrón.
* Escanear grandes conjuntos de datos sin bloquear Redis.
* Recuperar múltiples valores en una sola operación.

---

## 🧱 Parte 1. EXPIRE y TTL

### 🎯 Objetivo

Aprender a asignar un tiempo de vida (TTL) a las claves.

### 🧪 Ejercicios

1. Crea una clave `token:usuario1` con el valor `abc123`.
2. Asigna un tiempo de expiración de **15 segundos**.

   ```bash
   EXPIRE token:usuario1 15
   ```
3. Verifica cuántos segundos le quedan con:

   ```bash
   TTL token:usuario1
   ```
4. Espera 15 segundos y comprueba si aún existe con `EXISTS token:usuario1`.

💡 *Tip:* Puedes usar `SETEX` para crear una clave con expiración directa:

```bash
SETEX sesion:101 30 "activo"
```

---

## 🧩 Parte 2. EXISTS

### 🎯 Objetivo

Verificar la existencia de claves en Redis.

### 🧪 Ejercicios

1. Crea dos claves:

   ```bash
   SET producto:1 "Camisa"
   SET producto:2 "Pantalón"
   ```
2. Verifica su existencia:

   ```bash
   EXISTS producto:1
   EXISTS producto:3
   ```
3. Elimina una clave (`DEL producto:2`) y verifica nuevamente.

📘 *Observa cómo Redis devuelve:*
`1` si la clave existe, `0` si no existe.

---

## 🔍 Parte 3. KEYS

### 🎯 Objetivo

Aprender a listar claves usando patrones.

### 🧪 Ejercicios

1. Crea varias claves con prefijos similares:

   ```bash
   SET usuario:1 "Ana"
   SET usuario:2 "Juan"
   SET usuario:3 "Laura"
   ```
2. Lista todas las claves:

   ```bash
   KEYS *
   ```
3. Muestra solo las que empiecen por `usuario:`:

   ```bash
   KEYS usuario:*
   ```

⚠️ *Advertencia:* No uses `KEYS` en producción, puede ser lento con miles de claves.

---

## 🧭 Parte 4. SCAN

### 🎯 Objetivo

Aprender a recorrer claves de manera segura con SCAN.

### 🧪 Ejercicios

1. Crea las siguientes claves:

   ```bash
   SET pedido:1 "Enviado"
   SET pedido:2 "Pendiente"
   SET pedido:3 "Cancelado"
   SET pedido:4 "En proceso"
   ```
2. Usa `SCAN` para buscar todas las claves que empiecen con `pedido:`

   ```bash
   SCAN 0 MATCH pedido:* COUNT 2
   ```
3. Interpreta el resultado: el primer número es el **cursor** (para continuar el recorrido).
4. Repite usando el nuevo cursor hasta que Redis devuelva `0`.

💡 *Diferencia clave:* `SCAN` es seguro para producción, `KEYS` no.

---

## 📦 Parte 5. MGET

### 🎯 Objetivo

Recuperar múltiples valores en una sola operación.

### 🧪 Ejercicios

1. Crea tres claves:

   ```bash
   SET producto:1 "Camisa"
   SET producto:2 "Pantalón"
   SET producto:3 "Zapatos"
   ```
2. Recupera los valores al mismo tiempo:

   ```bash
   MGET producto:1 producto:2 producto:3
   ```
3. Intenta obtener una clave inexistente:

   ```bash
   MGET producto:1 producto:5
   ```

   Redis devolverá `(nil)` para la que no exista.

📦 *Conclusión:* `MGET` reduce las llamadas al servidor y mejora el rendimiento.

---

## 🧠 Desafío final

1. Crea un conjunto de 10 claves que representen sesiones de usuario (`sesion:1`, `sesion:2`, ... `sesion:10`).
2. Asigna una expiración de **10 segundos** a las cinco primeras.
3. Usa `SCAN` para listar las que queden activas.
4. Espera 10 segundos y verifica con `EXISTS` cuáles expiraron.
5. Usa `MGET` para consultar el valor de las sesiones activas.

---

🎓 **Resultado esperado:**

* Los estudiantes comprenderán el uso de comandos intermedios para administrar claves, expiraciones y consultas eficientes.
* Podrán diferenciar entre `KEYS` y `SCAN`, y entender la importancia del uso responsable de cada comando.
