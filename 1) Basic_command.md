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
