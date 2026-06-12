# Actividad de Investigación y Práctica
# Estructuras de Datos Avanzadas y APIs con ASP.NET Core

## Parte 1: Investigación Teórica

---

# 1. Estructuras de Datos Eficientes

## Árboles Binarios de Búsqueda (ABB)

Un Árbol Binario de Búsqueda (ABB) es una estructura de datos jerárquica donde cada nodo puede tener como máximo dos hijos:

- Hijo izquierdo.
- Hijo derecho.

La regla principal de ordenamiento es:

- Todos los valores del subárbol izquierdo deben ser menores que el valor del nodo actual.
- Todos los valores del subárbol derecho deben ser mayores que el valor del nodo actual.

### Ejemplo

```text
        10
       /  \
      5    15
     / \   / \
    3   7 12 20
```

En este ejemplo:

- 5 es menor que 10, por lo que se encuentra a la izquierda.
- 15 es mayor que 10, por lo que se encuentra a la derecha.
- La misma regla se aplica recursivamente a todos los nodos.

### Principal desventaja

Cuando los datos se insertan en orden secuencial (por ejemplo: 1, 2, 3, 4, 5), el árbol pierde su estructura balanceada y se convierte en una lista enlazada.

#### Ejemplo de degeneración

```text
1
 \
  2
   \
    3
     \
      4
       \
        5
```

Este fenómeno se conoce como **degeneración del árbol**.

Como consecuencia:

- Las búsquedas se vuelven más lentas.
- Las inserciones y eliminaciones también se vuelven menos eficientes.
- La complejidad pasa de O(log n) a O(n).

---

## Árboles AVL

Un Árbol AVL es un Árbol Binario de Búsqueda auto-balanceado.

Fue desarrollado por Adelson-Velsky y Landis, de quienes proviene el nombre AVL.

La característica principal es que mantiene equilibradas las alturas de los subárboles izquierdo y derecho para garantizar operaciones eficientes.

### Factor de Balanceo

El factor de balanceo se calcula mediante la fórmula:

```text
Factor = AlturaIzquierda - AlturaDerecha
```

Los valores permitidos son:

- -1
- 0
- 1

Si el factor de balanceo de algún nodo sale de este rango, el árbol realiza rotaciones para recuperar el equilibrio.

### Rotaciones

Las rotaciones permiten reorganizar los nodos sin perder el orden del árbol.

Tipos principales:

- Rotación simple a la derecha.
- Rotación simple a la izquierda.
- Rotación doble izquierda-derecha.
- Rotación doble derecha-izquierda.

### Complejidad O(log n)

Gracias a que el árbol siempre permanece balanceado:

- Búsqueda: O(log n)
- Inserción: O(log n)
- Eliminación: O(log n)

Esto ocurre porque la altura del árbol crece de forma logarítmica respecto a la cantidad de elementos almacenados.

Por esta razón los árboles AVL son más eficientes que los ABB tradicionales cuando se manejan grandes cantidades de datos.

---

# 2. Fundamentos de Web APIs

## ¿Qué es una API?

API significa **Application Programming Interface** (Interfaz de Programación de Aplicaciones).

Es un conjunto de reglas y mecanismos que permiten que diferentes aplicaciones se comuniquen entre sí.

Una API actúa como intermediaria entre un cliente y un servidor.

### Ejemplo

- Una aplicación móvil solicita información.
- La API recibe la solicitud.
- El servidor procesa la petición.
- La API devuelve la respuesta al cliente.

---

## Modelo Cliente-Servidor

El modelo Cliente-Servidor consiste en dos componentes principales:

### Cliente

Es quien realiza la solicitud.

Ejemplos:

- Navegador web.
- Aplicación móvil.
- Aplicación de escritorio.
- Postman.

### Servidor

Es quien recibe la solicitud, procesa la información y devuelve una respuesta.

---

## Funcionamiento mediante HTTP

La comunicación se realiza mediante el protocolo HTTP.

### Request (Petición)

El cliente envía una solicitud al servidor.

La petición puede incluir:

- Método HTTP.
- URL.
- Encabezados.
- Datos.

### Response (Respuesta)

El servidor procesa la solicitud y devuelve:

- Código de estado HTTP.
- Encabezados.
- Datos solicitados.

### Flujo de comunicación

```text
Cliente
   |
   | Request HTTP
   v
Servidor / API
   |
   | Response HTTP
   v
Cliente
```

---

# Verbos HTTP

Los verbos HTTP indican la acción que el cliente desea realizar sobre un recurso.

---

## GET

### Función

Se utiliza para recuperar información existente.

### Ejemplo

```http
GET /api/nodos
```

### Resultado

Devuelve una lista de nodos almacenados.

### Idempotencia

GET es idempotente.

Esto significa que realizar la misma petición varias veces produce exactamente el mismo resultado y no modifica los datos del servidor.

### Características

- No crea información.
- No modifica información.
- No elimina información.
- Solo consulta datos.

---

## POST

### Función

Se utiliza para crear nuevos recursos en el servidor.

### Ejemplo

```http
POST /api/nodos
```

### Cuerpo de la petición

```json
{
    "id": 15,
    "valor": "Nuevo Nodo Derecho"
}
```

### Resultado

El servidor crea un nuevo recurso y normalmente responde con el código:

```http
201 Created
```

### Idempotencia

POST NO es idempotente.

Si la misma petición se envía varias veces, se pueden crear múltiples registros.

### Características

- Crea información nueva.
- Modifica el estado del servidor.
- Generalmente devuelve código 201 Created.

---

# Diferencia entre GET y POST

| Característica | GET | POST |
|---------------|------|------|
| Objetivo | Consultar datos | Crear datos |
| Modifica información | No | Sí |
| Envía datos en Body | No normalmente | Sí |
| Idempotente | Sí | No |
| Código exitoso común | 200 OK | 201 Created |

---

# Conclusión

Los Árboles Binarios de Búsqueda permiten organizar información de manera jerárquica, mientras que los Árboles AVL mejoran su rendimiento manteniendo el balance de la estructura. Por otro lado, las APIs permiten la comunicación entre aplicaciones mediante el protocolo HTTP, utilizando métodos como GET para consultar información y POST para crear nuevos recursos. Estos conceptos son fundamentales para el desarrollo de aplicaciones modernas y servicios web utilizando ASP.NET Core.
