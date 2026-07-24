# Ejemplo 2: Simulación de un Autolavado

En este caso, aumentamos un poco la capacidad. Simulamos un autolavado que tiene **dos máquinas** de lavado trabajando al mismo tiempo.

```python
import simpy

def lavado_auto(env, nombre, autolavado):
    print(f'🚙 {nombre} llega al autolavado en el minuto {env.now}')
    
    with autolavado.request() as peticion:
        yield peticion
        
        print(f'💦 {nombre} entra a lavarse en el minuto {env.now}')
        yield env.timeout(10) # El proceso de lavado dura 10 minutos
        print(f'✨ {nombre} sale limpio en el minuto {env.now}')

# Configuración
env = simpy.Environment()
autolavado = simpy.Resource(env, capacity=2) # Hay 2 espacios para lavar

# Simulamos 4 autos llegando al mismo tiempo
for i in range(4):
    env.process(lavado_auto(env, f'Coche {i+1}', autolavado))

print("--- INICIANDO SIMULACIÓN DE AUTOLAVADO ---")
env.run()
