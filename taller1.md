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
