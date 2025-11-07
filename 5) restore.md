
# 📦 Redis Persistencia: Snapshots (RDB) y Append-Only File (AOF)

## 🧠 Introducción
Redis permite mantener los datos incluso después de reiniciar el servidor mediante dos mecanismos de persistencia:

1. **RDB (Snapshot):** Guarda una copia completa de la base de datos en un archivo binario (`dump.rdb`).
2. **AOF (Append Only File):** Registra cada operación de escritura en un archivo (`appendonly.aof`), lo que permite reconstruir el estado exacto.

---

## ⚙️ 1. Verificar configuración actual

Ejecuta en tu Redis CLI (por ejemplo con `docker exec -it redis redis-cli`):

```bash
CONFIG GET dir
CONFIG GET dbfilename
CONFIG GET appendonly
CONFIG GET appendfilename
```

Ejemplo de salida:
```
dir
/data
dbfilename
dump.rdb
appendonly
no
appendfilename
appendonly.aof
```

---

## 💾 2. Crear Snapshot (RDB)

### 2.1 Crear Snapshot manualmente

```bash
SAVE
```
Guarda el estado actual en `dump.rdb`.

O de forma **asíncrona**:

```bash
BGSAVE
```
Crea el snapshot en segundo plano (sin bloquear).

Verifica el último guardado:
```bash
LASTSAVE
```

### 2.2 Copiar Snapshot fuera del contenedor (Docker)

```bash
docker cp redis:/data/dump.rdb ./dump.rdb
```

### 2.3 Restaurar Snapshot

1. Detén el contenedor Redis:
   ```bash
   docker stop redis
   ```
2. Copia el archivo de respaldo al contenedor:
   ```bash
   docker cp ./dump.rdb redis:/data/dump.rdb
   ```
3. Inicia el contenedor nuevamente:
   ```bash
   docker start redis
   ```

Redis cargará automáticamente el snapshot al iniciar.

---

## 🧱 3. Crear y Activar Append-Only File (AOF)

### 3.1 Habilitar AOF temporalmente

No se puede cambiar `appendfilename` directamente porque es inmutable, pero puedes activar AOF con:

```bash
CONFIG SET appendonly yes
```

Redis comenzará a registrar cada operación de escritura en el archivo `appendonly.aof`.

Puedes confirmar:
```bash
CONFIG GET appendonly
```

Debe mostrar `appendonly` = `yes`.

### 3.2 Forzar escritura manual del AOF

```bash
BGREWRITEAOF
```

Esto crea o reescribe el archivo `appendonly.aof` en el directorio de datos.

### 3.3 Ver archivo AOF

Si estás en Docker:

```bash
docker exec -it redis ls /data
```

Verás algo como:
```
appendonly.aof
dump.rdb
```

---

## 🔁 4. Restaurar desde AOF

1. **Detén Redis:**
   ```bash
   docker stop redis
   ```

2. **Copia el archivo AOF de respaldo al contenedor:**
   ```bash
   docker cp ./appendonly.aof redis:/data/appendonly.aof
   ```

3. **Asegúrate de tener AOF habilitado en la configuración:**
   ```bash
   docker exec -it redis redis-cli CONFIG SET appendonly yes
   ```

4. **Inicia Redis nuevamente:**
   ```bash
   docker start redis
   ```

Redis reconstruirá automáticamente la base de datos a partir del archivo `appendonly.aof`.

---

## ⚙️ 5. Configuración combinada (RDB + AOF)

Redis permite usar **ambos mecanismos simultáneamente**:

```bash
CONFIG SET save "900 1 300 10 60 10000"
CONFIG SET appendonly yes
CONFIG SET appendfsync everysec
```

- `save`: snapshots automáticos cada cierto tiempo.
- `appendonly yes`: activa el registro de comandos.
- `appendfsync everysec`: sincroniza cada segundo (equilibrio entre rendimiento y durabilidad).

---

## ✅ 6. Verificación final

Entra al CLI para revisar los datos y la persistencia activa:

```bash
docker exec -it redis redis-cli
KEYS *
CONFIG GET appendonly
CONFIG GET dir
```

---

## 🧩 Resumen de Comandos

| Acción | Comando |
|--------|----------|
| Crear snapshot | `SAVE` o `BGSAVE` |
| Exportar snapshot | `docker cp redis:/data/dump.rdb ./dump.rdb` |
| Restaurar snapshot | `docker cp ./dump.rdb redis:/data/dump.rdb` + `docker restart redis` |
| Activar AOF | `CONFIG SET appendonly yes` |
| Reescribir AOF | `BGREWRITEAOF` |
| Restaurar AOF | `docker cp ./appendonly.aof redis:/data/appendonly.aof` + `docker restart redis` |

---

📘 **Consejo final:**  
- Usa RDB para respaldos periódicos (más ligeros).  
- Usa AOF si necesitas máxima durabilidad en caso de apagones o caídas del sistema.  
- Puedes usar ambos simultáneamente para tener respaldo rápido y log detallado.
