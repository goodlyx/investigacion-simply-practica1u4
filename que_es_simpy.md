# ¿Qué es la librería SimPy?

**SimPy** es un *framework* (o marco de trabajo) escrito en Python que se utiliza para la simulación de eventos discretos. Básicamente, es una herramienta que nos permite modelar procesos de la vida real donde el tiempo avanza en saltos o eventos específicos, en lugar de ser un flujo de tiempo continuo.

## ¿Para qué sirve?
Imagina que quieres saber cuánto tiempo va a esperar la gente en la fila de un banco, o cuántos cajeros necesitas en un supermercado para que no se hagan filas enormes. SimPy te ayuda a programar esos escenarios, correr la simulación virtualmente y analizar los resultados para tomar mejores decisiones en la vida real.

## Conceptos clave de SimPy
Para entender cómo funciona, es importante conocer tres conceptos básicos:

1. **Entorno (Environment):** Es el "mundo" donde ocurre la simulación. Se encarga de manejar el reloj interno y de que los eventos pasen en el orden correcto.
2. **Procesos (Processes):** Son las entidades activas del modelo. Por ejemplo: clientes, vehículos, o paquetes. En Python, se programan usando generadores (con la instrucción `yield`).
3. **Recursos (Resources):** Son elementos que los procesos necesitan para hacer su trabajo, y que tienen una capacidad limitada. Por ejemplo, las bombas de una gasolinera o los servidores de una página web.
