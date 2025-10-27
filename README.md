<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&height=180&section=header&text=robotic-MOTOMAN%20%E2%80%A2%20RoboDK&fontSize=36&desc=Práctica%20de%20Laboratorio%20%E2%80%A2%20MOTOMAN%20MH6&descSize=14&animation=fadeIn" width="100%" />
</div>

---

# 🤖 robotic-MOTOMAN — RoboDK · Yaskawa motoman MH6

> **Resumen:** Práctica de laboratorio del curso *Robótica Industrial* que integra programacion y simulación en RoboDK y ejecución real con **Motoman MH6**. El sistema automatiza el trazo de una trayectoria polar sobre un espacio de trabajo inclinado.

---

## Cuadro comparativo de características técnicas

| Característica                     | **Yaskawa Motoman MH6** | **ABB IRB 140** |
|------------------------------------|--------------------------|-----------------|
| **Carga máxima (payload)**         | 6 kg                     | 6 kg            |
| **Alcance máximo**                 | 1422 mm                  | 810 mm          |
| **Grados de libertad (ejes)**      | 8                        | 6               |
| **Repetibilidad**                  | ±0.08 mm                 | ±0.03 mm        |
| **Velocidad máxima de ejes**       | J1: 220°/s<br>J4–J5: 410°/s<br>J6: 610°/s | Ejes 1–2: 200°/s (aprox.) |
| **Peso del robot**                 | 130 kg (aprox.)          | 98 kg (aprox.)  |
| **Controlador típico**             | DX100                    | IRC5            |
| **Aplicaciones típicas**           | Manufactura aditiva, ensamblado, dispensado , soldadura ligera, manipulacion de materiales | Soldadura por arco, ensamblaje, manipulación, embalaje, pulido |
| **Ventajas principales**           | Gran alcance con baja carga útil; estructura ligera | Alta precisión, tamaño compacto, fácil integración |
| **Recomendado para**               | Trabajos de alcance extendido | Espacios reducidos o tareas de alta repetibilidad |

---

## Características posiciones Home y Second Home

La posición **Home** es la postura de calibración del manipulador, con referencias de eje como chaveteros o flechas de alineación, donde se registran los datos absolutos del codificador de cada eje. Esto permite que el controlador lea todos los 0’ para cada eje bajo la posición actual en esta postura.

Esta posicion normalmente no debe ser modificada ni eliminada, solo en situaciones de reemplazar piezas del manipulador referentes al motor/codificador, placa de circuitos, desvio de las marcas por impactos, problemas de perdida de energía, etc.

La posición **Home2** por su parte se utiliza como punto de control para la calibración de *Home*, a menudo cuando ocurre la alarma 4107 (Out of Range Abso Data). La ubicación predeterminada de SECOND HOME (Punto especificado) para el robot es donde los datos de pulso para cada eje se muestran como todos ceros y las flechas de alineación o las teclas para cada eje están alineadas.

***¿Cual posicion es mejor?***

En general,, si bien abas posiciones existe con propositos distintos, Home1 (la “Home Position” de fábrica) es la ideal, pues representa la calibración original de todos los ejes y sirve como referencia precisa para la repetibilidad, mantenimiento y diagnósticos. Home2 es útil como respaldo o posición de chequeo, pero no reemplaza la Home1 salvo en situaciones de fallo o recalibración de la posicion Home1.

Por tanto, se puede considerar la mejor(o al menos la que es utilizada de forma normal en el robot) como Home1, porque garantiza que todos los ejes están en su referencia original y permite que el controlador y los programas trabajen con los valores que fueron definidos en fábrica. Además, emplear consistentemente Home1 favorece la trazabilidad, repetibilidad y mantenimiento predictivo del sistema.

## 3. Procedimiento detallado para movimientos manuales

Este procedimiento describe cómo realizar movimientos manuales en el robot **Yaskawa Motoman MH6**, incluyendo el cambio entre modos de operación (*articulaciones* y *cartesiano*) y la ejecución de traslaciones y rotaciones en los ejes **X, Y, Z**.

---

###  **1. Preparación del sistema**
Antes de realizar cualquier movimeinto con el robot es necesario:
1. Asegurar el area de trabajo(Correcta posicion inicial y condicion de l robot, evitar obstaculos en el area).
2. Encender los breakers del Motoman y el breaker totalizador, para despues encender el controlador **DX100** por medio de la perilla, y verificar su funcionamiento correcto.
3. Colocar la **llave de modo** del Teach pendant en posición **TEACH** (modo de enseñanza).
4. Verifica que el boton de parada de emergencia este desactivado y que el indicador **SERVO ON** esté activado; de lo contrario, presiónar el boton **SERVO ON READY** del Teach pendant.

---

###  **2. Selección del modo de operación**

El robot puede operarse manualmente en dos modos principales:

#### 🔹 Modo por Articulaciones (*Joint Jog*)
Permite mover **cada eje (J1 a J6)** de forma individual.

**Pasos:**
1. En el péndulo de enseñanza, presiona la tecla **COORD** hasta que aparezca **JOINT** en pantalla.
2. Mantener presionado el boton de Hombre Muerto para energizar los motores.
3. Usa las teclas de movimiento de eje (**+ / -**) para cada eje numerado *S, L, U, R, B, T, E, 8*.  
4. Observar en la pantalla el ángulo de cada articulación mientras se realiza.

---

#### 🔹 Modo Cartesiano (*Linear / TCP Jog*)
- Permite mover el **punto de herramienta (TCP)** en los ejes cartesianos **X, Y, Z**, ideal para movimientos precisos o alineación con piezas.

**Pasos:**
1. Presiona la tecla **COORD** hasta que aparezca el sistema deseado:
   - **BASE**: movimiento respecto a la base del robot.  
   - **WORLD**: movimiento global.  
   - **TOOL**: movimiento respecto a la herramienta (TCP).  
2. Usar los botones **+ / -** del eje que desea mover (**X, Y, Z** en los botones izquierdos del Teach Pendant) o rotar (**X, Y, Z** en los botones del lado derecho del Teach Pendant).
3. Observar en la pantalla el cambio de coordenadas mientras el movimiento se realiza.
---

### **3. Ejecución de movimientos**

1. Mantener presionado el **botón de habilitación (Enable / Deadman switch)** mientras realiza los movimientos.
2. Ejecutar los desplazamientos de forma **suave y progresiva** para evitar choques.
3. Monitorear la pantalla: se mostrará el modo actual y las coordenadas en tiempo real.
4. De necesitar un movimiento preciso modifica la velocidad del movimiento con los botones del Teach Pendant

---

## 4. Niveles de velocidad para movimientos manuales

El controlador del robot **Motoman MH6** permite seleccionar **tres niveles de velocidad** en el modo manual (*Teach Mode*). Estos niveles se ajustan directamente desde el **teach pendant**, y su estado se visualiza en una **barra de velocidad** en la pantalla principal.

---

###  **1. Niveles de velocidad disponibles**

| Nivel de velocidad | Descripción | Botón en teach pendant |
|--------------------|--------------|-------------------------|
| **SLOW (lento)**  | Movimiento seguro y preciso, ideal para ajustes finos. | `SLOW` |
| **FAST (medio)**  | Velocidad intermedia para desplazamientos normales. | `FAST` |
| **HIGH SPEED (rápido)** | Movimiento a la máxima velocidad manual permitida (solo cuando es seguro). | `HIGH SPEED` |

> 🔸 *La velocidad en modo manual nunca alcanza la velocidad máxima de ejecución automática; está limitada por seguridad.*

---

###  **2. Procedimiento para cambiar el nivel de velocidad**

1. Estar en **modo TEACH** y con el **Servo Power** activado.  
2. Observar la pantalla del teach pendant: en la parte superior aparece una **barra o indicador de velocidad**.  
3. Usar los botones dedicados:
   - Presiona **`SLOW`** → velocidad baja.  
   - Presiona **`FAST`** → velocidad media.  
   - Presiona **`HIGH SPEED`** → velocidad alta.  
4. El cambio es inmediato, el nuevo nivel se muestra actualizado en la barra de velocidad.  
5. Ejecutar el movimiento deseado.

---
