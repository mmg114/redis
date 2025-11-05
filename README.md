# 🧠 Guía de Redis: Tipos de Datos y Comandos Básicos

Esta hoja contiene los **principales tipos de datos en Redis** y los **comandos más usados** con ejemplos prácticos. Además, incluye un **taller final** para practicar en clase.

---

## 🔹 1. Cadenas (Strings)

Son el tipo más simple: almacenan texto o números.

### 🧩 Comandos principales:

```bash
SET saludo "Hola Mundo"      # Guarda una cadena
GET saludo                   # Recupera el valor
DEL saludo                   # Elimina la clave

SET contador 10              # Crea un contador
INCR contador                # Incrementa en 1 → 11
DECR contador                # Decrementa en 1 → 10
```

📦 **Usos comunes:** tokens, configuraciones, contadores, valores simples.

---

## 🔹 2. Listas (Lists)

Son colecciones ordenadas de elementos (como pilas o colas).

### 🧩 Comandos principales:

```bash
LPUSH tareas "Estudiar Redis"      # Inserta al inicio
RPUSH tareas "Hacer ejercicio"    # Inserta al final
LRANGE tareas 0 -1                 # Muestra todos los elementos
LPOP tareas                        # Saca el primer elemento
RPOP tareas                        # Saca el último elemento
LLEN tareas                        # Muestra cuántos elementos hay
```

📦 **Usos comunes:** colas de tareas, logs, listas de espera.

---

## 🔹 3. Conjuntos (Sets)

Colecciones **no ordenadas** y **sin duplicados**.

### 🧩 Comandos principales:

```bash
SADD etiquetas "redis" "backend" "java" "redis"   # Agrega elementos (sin duplicar)
SMEMBERS etiquetas                                # Muestra todos los miembros
SISMEMBER etiquetas "java"                        # Verifica si existe
SREM etiquetas "redis"                            # Elimina un elemento
```

📦 **Usos comunes:** almacenar usuarios únicos, etiquetas o intereses.

---

## 🔹 4. Hashes

Estructuras tipo JSON o mapa de campos y valores.

### 🧩 Comandos principales:

```bash
HSET usuario:100 nombre "Laura" correo "laura@ejemplo.com" nivel "intermedio"  # Crea un hash
HGET usuario:100 nombre       # Obtiene un solo campo
HGETALL usuario:100           # Muestra todos los campos y valores
HSET usuario:100 nivel "avanzado"  # Actualiza un campo
HDEL usuario:100 correo       # Elimina un campo
```

📦 **Usos comunes:** perfiles de usuario, configuraciones, objetos.

---

## 🔹 5. Sets ordenados (Sorted Sets)

Colecciones con un **puntaje (score)** que define su orden.

### 🧩 Comandos principales:

```bash
ZADD ranking 200 "Juan" 300 "Laura" 250 "Sofía"  # Agrega elementos con puntaje
ZRANGE ranking 0 -1 WITHSCORES                    # Muestra de menor a mayor
ZREVRANGE ranking 0 -1 WITHSCORES                 # Muestra de mayor a menor
ZINCRBY ranking 5 "Juan"                          # Aumenta el puntaje de un miembro
ZRANK ranking "Laura"                             # Muestra la posición de un elemento
```

📦 **Usos comunes:** rankings, puntuaciones, sistemas de reputación.

---

## 🔹 6. Comandos útiles generales

```bash
KEYS *          # Muestra todas las claves existentes
DEL clave       # Elimina una clave específica
FLUSHDB         # Borra todas las claves de la base de datos actual
FLUSHALL        # Borra todas las bases de datos de Redis
```

---

# 🧩 Taller Práctico de Redis

### 🎯 Objetivo

Aprender a manipular los principales tipos de datos en Redis mediante ejemplos.

---

### 🧱 Parte 1. Cadenas (Strings)

1. Crea una clave `saludo` con el valor `"Hola clase de Redis"`.
2. Muestra su valor con `GET`.
3. Modifícala para que diga `"Hola clase de Redis 2025"`.
4. Borra la clave y verifica que ya no exista.

---

### 📋 Parte 2. Listas (Lists)

1. Crea una lista llamada `tareas`.
2. Agrega tres tareas: `"Leer documentación"`, `"Ver video"`, `"Practicar comandos"`.
3. Muestra todas las tareas.
4. Saca una tarea del inicio (`LPOP`).
5. Muestra la lista actualizada.

---

### 🔤 Parte 3. Conjuntos (Sets)

1. Crea un conjunto `lenguajes` con los valores `java`, `redis`, `python`, `redis`.
2. Muestra los elementos.
3. Elimina uno de ellos.
4. Verifica si `java` aún existe.

---

### 🧾 Parte 4. Hashes

1. Crea un hash `usuario:101` con los campos:

    * `nombre`: "Camila"
    * `correo`: "[camila@example.com](mailto:camila@example.com)"
    * `nivel`: "básico"
2. Muestra todos los datos.
3. Actualiza `nivel` a `intermedio`.
4. Borra el campo `correo`.

---

### 🏆 Parte 5. Sorted Sets

1. Crea un ranking `puntajes` con los siguientes datos:

    * Ana: 85
    * Carlos: 90
    * Luisa: 78
2. Muestra el ranking completo.
3. Incrementa el puntaje de `Luisa` en 10.
4. Muestra el nuevo ranking de mayor a menor.

---

### 🎓 Bonus final

* Usa `KEYS *` para ver todas las claves creadas.
* Ejecuta `FLUSHDB` para limpiar todo tu entorno al final del taller.

---

🧩 **Resultado esperado:** Los estudiantes comprenderán cómo manipular cadenas, listas, conjuntos, hashes y sets ordenados en Redis mediante comandos prácticos.
