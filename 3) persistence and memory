
# 🔧 Configuración de Persistencia y Memoria en Redis (Windows + Docker)

Este documento explica cómo **activar la persistencia (RDB + AOF)** y **configurar la gestión de memoria** en una instalación de Redis que corre dentro de **Docker en Windows**, **sin recrear el contenedor**.

---

## 🧩 1️⃣ Verificar configuración actual

Ejecuta dentro del CLI:

```bash
docker exec -it redis redis-cli
```

Luego, ejecuta estos comandos para ver la configuración actual:

```bash
CONFIG GET save
CONFIG GET appendonly
CONFIG GET appendfsync
CONFIG GET dir
```

Esto mostrará:
- Si los snapshots (RDB) están activos  
- Si el modo AOF está habilitado  
- Dónde Redis guarda los archivos (`/data` normalmente)

---

## 💾 2️⃣ Activar Snapshots (RDB)

```bash
CONFIG SET save "900 1 300 10 60 10000"
CONFIG SET dbfilename "dump.rdb"
BGSAVE
```

✅ Esto hace que Redis guarde snapshots automáticamente cuando haya:
- 1 cambio en 900 segundos  
- 10 cambios en 300 segundos  
- 10.000 cambios en 60 segundos  

y crea uno inmediatamente (`BGSAVE`).

📍 Verifica:
```bash
CONFIG GET save
```

---

## 📜 3️⃣ Activar Append Only File (AOF)

```bash
CONFIG SET appendonly yes
CONFIG SET appendfsync everysec
CONFIG SET appendfilename "appendonly.aof"
BGREWRITEAOF
```

✅ Con esto activas la escritura secuencial (modo seguro y recomendado).

Verifica:
```bash
CONFIG GET appendonly
```

💡 Los archivos se guardan en la carpeta que viste antes (`CONFIG GET dir`), normalmente `/data`.

---

## 🧱 4️⃣ Hacer persistentes los cambios

Por defecto, estos cambios se pierden si el contenedor se reinicia.

Para guardarlos de forma permanente:

```bash
CONFIG REWRITE
```

Redis escribirá un nuevo `redis.conf` interno con tus ajustes.

---

## ⚙️ 5️⃣ Configurar límites de memoria y políticas de expulsión

### 🔹 Límite de memoria (por ejemplo 200 MB)
```bash
CONFIG SET maxmemory 200mb
```

### 🔹 Política de eliminación (recomendada: LRU)
```bash
CONFIG SET maxmemory-policy allkeys-lru
```

### 🔹 Verificar:
```bash
CONFIG GET maxmemory
CONFIG GET maxmemory-policy
```

---

## 📊 6️⃣ Pruebas rápidas

### 🔸 Crear clave temporal
```bash
SET sesion "usuario123" EX 10
TTL sesion
```

### 🔸 Forzar snapshot y AOF
```bash
BGSAVE
BGREWRITEAOF
```

### 🔸 Ver memoria usada
```bash
INFO memory
```

---

## 🧹 7️⃣ Si quieres limpiar o probar desde cero

```bash
FLUSHALL
```

---

## ✅ Resumen express

| Acción | Comando |
|--------|----------|
| Activar snapshots | `CONFIG SET save "900 1 300 10 60 10000"` |
| Guardar snapshot ahora | `BGSAVE` |
| Activar AOF | `CONFIG SET appendonly yes` |
| Sincronización segura | `CONFIG SET appendfsync everysec` |
| Limitar memoria | `CONFIG SET maxmemory 200mb` |
| Política LRU | `CONFIG SET maxmemory-policy allkeys-lru` |
| Hacer cambios persistentes | `CONFIG REWRITE` |

---

## 🧠 Recomendaciones finales

- Revisa regularmente los archivos `dump.rdb` y `appendonly.aof` en `/data` o en tu volumen montado.  
- Usa `INFO persistence` para verificar el estado.  
- Ejecuta `CONFIG REWRITE` siempre después de hacer cambios importantes.  
- No ejecutes `FLUSHALL` en producción sin respaldo previo.

---

© 2025 - Taller de Redis • Docente: Mauricio Muñoz
