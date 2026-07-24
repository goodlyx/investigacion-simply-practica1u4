# Ejemplo 3: Taquilla de un Cine

Aquí vemos cómo llegan clientes a comprar boletos. Usamos la librería `random` para hacer que el tiempo de compra varíe, ya que en la vida real algunas personas tardan más en elegir sus asientos que otras.

```python
import simpy
import random

def comprar_boleto(env, cliente, taquilla):
    print(f'🚶‍♂️ {cliente} se forma en la taquilla en el minuto {env.now}')
    
    with taquilla.request() as turno:
        yield turno
        
        print(f'🎟️ {cliente} pasa a la ventanilla en el minuto {env.now}')
        tiempo_compra = random.randint(1, 3) # Tarda entre 1 y 3 minutos al azar
        yield env.timeout(tiempo_compra)
        print(f'🍿 {cliente} ya tiene su boleto en el minuto {env.now}')

# Configuración
env = simpy.Environment()
taquilla = simpy.Resource(env, capacity=1)

# Generamos 3 clientes
for i in range(3):
    env.process(comprar_boleto(env, f'Cliente {i+1}', taquilla))

print("--- INICIANDO SIMULACIÓN DE TAQUILLA ---")
env.run()
