# Ejemplo 1: Simulación de una Gasolinera

Este ejemplo simula un escenario muy sencillo donde varios autos llegan a una gasolinera que solo tiene **una bomba** disponible. Si la bomba está ocupada, el auto tiene que esperar.

```python
import simpy

def auto(nombre, env, gasolinera):
    print(f'🚗 {nombre} llega a la gasolinera en el minuto {env.now}')
    
    # Solicita usar la bomba de gasolina
    with gasolinera.request() as peticion:
        yield peticion # Espera su turno si está ocupada
        
        print(f'⛽ {nombre} empieza a cargar gasolina en el minuto {env.now}')
        yield env.timeout(5) # Tarda 5 minutos en llenar el tanque
        print(f'✅ {nombre} termina y se va en el minuto {env.now}')

# Configuración de la simulación
env = simpy.Environment()
gasolinera = simpy.Resource(env, capacity=1) # Capacidad de 1 sola bomba

# Creamos 3 autos
for i in range(3):
    env.process(auto(f'Auto {i+1}', env, gasolinera))

# Iniciamos la simulación
print("--- INICIANDO SIMULACIÓN DE GASOLINERA ---")
env.run()
