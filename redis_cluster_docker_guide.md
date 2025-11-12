# 🧩 Guía de Redis Cluster con Docker Compose

## 🚀 Levantar el cluster

Ejecuta los siguientes comandos en el directorio donde tengas tu archivo `docker-compose.yml` configurado para los nodos de Redis:

```bash
docker compose up -d
```

👉 Esto levanta los contenedores definidos (por ejemplo, `redis-node-1`, `redis-node-2`, `redis-node-3`).

Verifica que estén corriendo:

```bash
docker ps
```

Deberías ver tus tres nodos de Redis en ejecución.

---

## ⚙️ Crear el cluster

Conecta al primer nodo y crea el cluster entre los tres nodos:

```bash
docker compose exec redis-node-1 redis-cli --cluster create redis-node-1:6379 redis-node-2:6379 redis-node-3:6379 --cluster-replicas 0
```

> 🔹 `--cluster-replicas 0` indica que no se crearán réplicas (solo 3 nodos maestros).  
> 🔹 Si quisieras réplicas, necesitarías al menos 6 nodos (3 masters + 3 replicas).

---

## 🔗 Probar la conexión

Puedes acceder al cliente del primer nodo en modo cluster con:

```bash
docker compose exec redis-node-1 redis-cli -c
```

> La opción `-c` permite que el cliente siga las redirecciones del cluster automáticamente.

---

## 🧠 Comandos básicos de prueba

Dentro del cliente (`redis-cli -c`):

```bash
SET hola 1
GET hola
```

> Redis te indicará a qué nodo se asignó la clave `hola` según el *hash slot*.

Ver información del cluster:

```bash
CLUSTER INFO
```

Listar los nodos del cluster:

```bash
CLUSTER NODES
```

---

## 🌍 URL de conexión

Tu aplicación puede conectarse a cualquiera de los nodos, por ejemplo:

```
redis://redis-node-1:6379
```

---

## 🧹 Eliminar el cluster y limpiar volúmenes

Cuando termines las pruebas, puedes eliminar todo el entorno (contenedores, redes y volúmenes) con:

```bash
docker compose down -v
```

> `-v` elimina los volúmenes asociados para limpiar completamente el entorno.

---

## ✅ Resumen rápido

| Acción | Comando |
|--------|----------|
| Iniciar cluster | `docker compose up -d` |
| Ver contenedores | `docker ps` |
| Crear cluster | `docker compose exec redis-node-1 redis-cli --cluster create redis-node-1:6379 redis-node-2:6379 redis-node-3:6379 --cluster-replicas 0` |
| Conectarse al cluster | `docker compose exec redis-node-1 redis-cli -c` |
| Ver info del cluster | `CLUSTER INFO` |
| Ver nodos del cluster | `CLUSTER NODES` |
| Eliminar cluster | `docker compose down -v` |
