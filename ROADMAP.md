# Roadmap de Verificacion - Paso a Paso

## Estado General

```
[██████████████████░░] 90% — En curso: reparacion profesional del turbo
```

**Fecha inicio diagnostico:** 2026-03-29
**Ultimo hallazgo:** 2026-04-01 — Wastegate no abre (componentes OK, sospecha resorte incorrecto)
**Proximo paso:** 2026-04-02 — Reemplazo radiador/viscoso + desmontaje turbo para taller

---

## Paso 1: Caracterizacion del Sintoma ✅
- [x] Identificar tipo de falla (no potencia vs tironeo vs no arranque)
- [x] Determinar condiciones de operacion (RPM, marchas, carga)
- [x] Verificar presencia/ausencia de humo
- [x] Verificar testigos en tablero
- [x] Identificar DTCs con scanner

**Resultado:** Falta de potencia severa (~30% de capacidad). Sin humo. Sin DTCs relevantes.

## Paso 2: Verificacion de Combustible - Baja Presion ✅
- [x] Estado bomba de levante (nueva)
- [x] Test de caudal bomba: 1.4L en 30 segundos (spec: >1.35L/30s)
- [x] Comparar caudal pre y post filtro (identico = filtro OK)
- [x] Verificar filtro de combustible (nuevo)
- [x] Verificar interruptor inercial (normal)

**Resultado:** Circuito de baja presion OK.

## Paso 3: Verificacion de Combustible - Alta Presion ✅
- [x] Sensor FRP (nuevo)
- [x] Valvula VCV (nueva)
- [x] Valvula PCV (nueva)
- [x] Presion de rail en ralenti: 460 bar
- [x] Presion de rail en ruta 2000 RPM: 1100 bar
- [x] Presion de rail maxima plena carga: 1400 bar (dentro de rango)

**Resultado:** Sistema de alta presion funcional. Alcanza 1400 bar.

## Paso 4: Verificacion de Inyectores ✅ (parcial)
- [x] Verificar correccion de inyectores con scanner: 0.980 (normal)
- [ ] *(Opcional si falla test escape)* Medir retorno individual de cada inyector

**Como medir retorno de inyectores (si se necesita):**
1. Desconectar mangueras de retorno de cada inyector
2. Colocar un recipiente graduado en cada salida
3. Arrancar motor en ralenti durante 1 minuto
4. Comparar volumen de retorno entre los 4 inyectores
5. Si uno devuelve significativamente mas que los otros → fuga interna

**Resultado parcial:** Correcciones normales. Descartado provisionalmente.

## Paso 5: Verificacion de Admision de Aire ✅
- [x] Filtro de aire (nuevo)
- [x] Mangueras de intercooler (se inflan bajo presion, sin fugas)
- [x] Sensor T-MAP (limpio, sin DTCs)

**Resultado:** Admision de aire OK.

## Paso 6: Verificacion de Turbo ⚠️ WASTEGATE TRABADA
- [x] Silbido del turbo (se escucha)
- [x] RPM de entrada en boost: ~1600 RPM (normal)
- [x] Presion de boost a plena carga: 1.5 bar de sobrepresion (medido con motor recortado)
- [x] Tipo de turbo confirmado: wastegate mecanica, no pilotado
- [x] **Wastegate NO abre** — presion en mangueras excesiva
- [x] Probada con compresor de aire — precarga excesiva del resorte
- [x] Regulada para reducir precarga — sigue sin abrir
- [x] Diafragma/pulmon del actuador funciona OK (descartado)

**Resultado:** Turbo comprime correctamente pero la wastegate esta trabada. No hay control de presion maxima de boost. La PCM recorta potencia como proteccion.

## Paso 7: Verificacion de Distribucion ✅
- [x] Marcas de puesta a punto ciguenal/arbol de levas (correctas)

**Resultado:** Timing correcto.

## Paso 8: Verificacion de Transmision ✅
- [x] Embrague reparado, no patina
- [x] Caja funciona en todas las marchas

**Resultado:** Transmision OK.

## Paso 9: Verificacion de Sistema de Escape ✅ COMPLETADO
- [x] Identificar componentes del escape (2 tachos: catalizador + silenciador)
- [x] Silenciador tapado → **reemplazado por silenciador nuevo**
- [x] Precamara a la salida del turbo → **anulada**
- [x] Prueba de ruta post-reparacion

**Resultado:** Mejora leve pero insuficiente. El escape estaba parcialmente obstruido (silenciador tapado) pero **no era la causa principal**. Durante esta inspeccion se descubrio que la wastegate del turbo no abre → ver Paso 6 actualizado.

## Paso 9B: Circuito de Señal Wastegate ✅ PARCIALMENTE DESCARTADO

### Diagnostico completo de la wastegate
| Componente | Prueba | Resultado |
|------------|--------|-----------|
| Mariposa | Varilla desconectada, movimiento manual | ✅ Se mueve libremente |
| Diafragma/pulmon | Probado con compresor | ✅ Funciona OK |
| Precarga resorte | Reducida, regulada 3 vueltas | ✅ Ajustada |
| Manguera de señal | Verificada flujo | ✅ Fluye correctamente |
| Niple de toma | Aire comprimido por niple | ✅ Fluye correctamente |

**Resultado:** Todos los componentes del circuito de señal de wastegate verificados individualmente y funcionan. Sin embargo, **la wastegate sigue sin abrir en operacion**.

### Sospechas restantes sobre la wastegate

**1. Resorte con constante incorrecta (del turbo reconstruido)**
- Si durante la reparacion del turbo se instalo un resorte de otro modelo (mayor constante), aunque la precarga sea correcta, la fuerza necesaria para abrir podria ser mayor que la presion de boost disponible
- Verificar: ¿el taller de turbo uso repuestos originales o genericos?

**2. Presion de boost real insuficiente para abrir**
- Los 1.5 bar medidos por scanner son la lectura del T-MAP con motor recortado
- Si la PCM esta limitando combustible (smoke/torque limiter), el motor genera menos gases → menos velocidad de turbina → menos boost real
- Es un circulo vicioso: PCM recorta → menos boost → wastegate no abre → PCM sigue recortando

**3. Turbo con daño interno (ver Paso 9C)**

## Paso 9C: Reparacion Profesional del Turbo ⏳ EN CURSO

**Decision (2026-04-01):** Llevar el turbo a un taller especializado para reparacion profesional. Se descarto comprar un turbo generico/chino — mejor invertir en reparar el actual con repuestos correctos.

### Plan
1. [x] Reemplazo radiador + encausador + viscoso + paletas (2026-04-02)
2. [ ] Desmontar turbo del vehiculo (2026-04-02)
3. [ ] Llevar a taller de turbocompresores
4. [ ] Solicitar al taller:
   - Verificar juego axial y radial del eje
   - Inspeccionar ruedas de compresor y turbina (depositos de aceite carbonizado)
   - Verificar sellos de aceite (lado frio y caliente)
   - Verificar estado de carcasas (roce, grietas)
   - **CRITICO: Verificar/reemplazar resorte de wastegate con spec correcta para Ranger 3.0 NGD**
   - Confirmar presion de apertura de wastegate: debe ser **~0.7-1.0 bar**
   - Verificar largo correcto de varilla del actuador
5. [ ] Retirar turbo reparado
6. [ ] Montar turbo + prueba de ruta

### Puntos importantes para el taller
- Informar que la wastegate **no abria** a pesar de que mariposa, actuador y manguera funcionan OK individualmente
- El turbo fue reparado anteriormente — preguntar si el resorte instalado es el correcto
- Antecedente: motor viejo consumia 1L aceite/100km → posibles depositos internos en turbina
- Modelo turbo: **GT25 / GT20** — Part# **754743-0001 / 754743-0002**

### Alternativa evaluada y descartada
Se evaluaron turbos nuevos en MercadoLibre ($147K-$1.3M ARS):
- Garrett genuino: $1.3M (fuera de presupuesto)
- Master Power: ~$870K (fuera de presupuesto)
- Mahle: consultar (probablemente fuera de presupuesto)
- Genericos/chinos: $150K-$400K — **descartados por calidad de balanceo y durabilidad**
- **Presupuesto disponible: $380.000** → se opto por reparacion profesional del turbo actual

## Paso 9D: Bomba de Inyeccion y Alta Presion ⏳ PENDIENTE

La presion de rail en ralenti de **460 bar (normal: 250-350)** es una anomalia no resuelta. VCV y PCV son nuevos pero podrian ser de especificacion incorrecta.

### Anomalia de presion de rail en ralenti

| Parametro | Valor medido | Valor esperado | Diferencia |
|-----------|-------------|----------------|------------|
| Rail ralenti | 460 bar | 250-350 bar | **+30-80% sobre normal** |

### Posibles causas

**1. VCV (Volume Control Valve) de especificacion incorrecta**
- La VCV controla cuanto combustible ENTRA a la bomba de alta presion
- Normal Cerrada, resistencia 2-3 Ohm (tipica 2.75 Ohm)
- [ ] Verificar numero de parte de la VCV instalada vs original Ranger 2008 3.0L SID 901
- [ ] Medir resistencia de la VCV: debe ser 2-3 Ohm
- [ ] Si es de otro modelo → diferente caudal → presion alterada

**2. PCV (Pressure Control Valve) de especificacion incorrecta**
- La PCV controla cuanta presion se LIBERA del rail (valvula de alivio)
- Normal Abierta, resistencia 2.8-4 Ohm (tipica 3 Ohm)
- [ ] Verificar numero de parte de la PCV instalada vs original
- [ ] Medir resistencia de la PCV: debe ser 2.8-4 Ohm
- [ ] Si la PCV no alivia lo suficiente → presion de rail excesiva

**3. PCM comandando presion alta (compensacion)**
- [ ] Leer con scanner "Presion de rail DESEADA" vs "Presion de rail REAL" en ralenti
- [ ] Si deseada = real = 460 bar → la PCM QUIERE esa presion (calibracion incorrecta o compensacion)
- [ ] Si deseada = 300 bar y real = 460 bar → la bomba/PCV no responden correctamente

### Verificacion con scanner (critica)
- [ ] Presion rail deseada vs real en ralenti
- [ ] Presion rail deseada vs real a 2000 RPM sin carga
- [ ] Presion rail deseada vs real a fondo en 3ra
- [ ] "Cantidad de inyeccion deseada" vs "real" (mg/inyeccion) a fondo
- [ ] "Limitador de humo" (smoke limiter) — valor en mg/inj a plena carga
- [ ] Posicion del acelerador: ¿llega a 100%?

## Paso 9E: Inyectores — Evaluacion Detallada ⏳ PENDIENTE (baja prioridad)

### Estado actual
- Correccion >2000 RPM: 0.980 (normal, rango aceptable 0.95-1.05)
- Inyectores ruidosos (pero corrección estable)
- Tipo: piezoelectricos

### Evaluacion
| Parametro | Valor | Estado |
|-----------|-------|--------|
| Correccion >2000 RPM | 0.980 | ✅ Normal |
| Ruido | Algo ruidosos | ⚠️ Puede ser normal en piezoelectricos |
| Retorno individual | No medido | ⏳ Pendiente si otros pasos no resuelven |

**Nota:** El ruido en inyectores piezoelectricos puede ser normal si es **parejo entre los 4**. Si uno suena marcadamente distinto → posible fuga interna en ese inyector. La correccion de 0.98 estable indica que la PCM no necesita compensar mucho, lo cual es buena señal.

- [ ] *(Solo si otros pasos no resuelven)* Medir retorno individual de cada inyector en ralenti (1 minuto, comparar volumen)

### Prueba de verificacion post-reparacion (aplica a todos los pasos 9B-9E)
1. Motor en ralenti: verificar que boost sea ~0 bar (sin carga)
2. Acelerar a fondo en 3ra: boost debe subir a 1.0-1.5 bar y **estabilizarse** (wastegate abre)
3. En 5ta: debe superar 120 km/h con margen
4. RPM maxima en 3ra a fondo: debe superar 4000 RPM
5. Verificar presion de rail ralenti: debe bajar a 250-350 bar (PCM deja de compensar)

## Paso 10: Verificacion de Calibracion PCM (si escape no da resultado)

**Contexto:** La PCM fue reparada y se elimino el PATS despues de un cortocircuito en la BJB. La flash fue reprogramada, lo que pudo alterar los mapas de calibracion del motor.

### 10.1 Verificacion por scanner (gratis)
- [ ] Leer "Cantidad de inyeccion deseada" vs "Cantidad de inyeccion real" (mg/inj) a fondo en 3ra
- [ ] Leer "Presion de rail deseada" vs "Presion de rail real" a fondo
- [ ] Verificar "Posicion del acelerador" llegue a 100% a fondo
- [ ] Leer "Limitador de humo" (mg/inj) — si es bajo, esta capando combustible

### 10.2 Lectura de la flash del PCM
- [ ] Conseguir herramienta MPPS v18/v21 (~$50-80 USD, MercadoLibre/AliExpress)
- [ ] Conectar MPPS al OBD2 (contacto ON, motor apagado)
- [ ] Leer flash completa — guardar 3 copias de backup
- [ ] Leer segunda vez y comparar que sea identica (verificacion de integridad)
- [ ] Abrir en WinOLS / ECM Titanium con damos SID 901

### 10.3 Analisis de mapas
- [ ] Verificar numero de calibracion vs original Ranger 2008 3.0L
- [ ] Revisar mapa Injection Quantity (IQ) — valores maximos
- [ ] Revisar mapa Rail Pressure Target — presiones objetivo
- [ ] Revisar Torque Limiter — tope de torque
- [ ] Revisar Smoke Limiter — limite anti-humo
- [ ] Revisar Speed Limiter
- [ ] Revisar Driver Wish / Pedal Map — respuesta al acelerador

### 10.4 Correccion
- [ ] Si calibracion es incorrecta: flashear firmware original correcto
- [ ] Si calibracion es correcta: verificar retorno de inyectores, T-MAP, TPS/APP

**Nota:** Siempre verificar checksum antes de escribir. Los clones MPPS no corrigen checksum automaticamente — usar plugin de WinOLS/ECM Titanium.

## Paso 11: Diagnostico Alternativo (solo si escape Y PCM estan OK)

Si ninguna de las dos sospechas principales se confirma:

- [ ] Medir retorno individual de inyectores (Paso 4 completo)
- [ ] Verificar cableado del T-MAP con multimetro (5V referencia, senal en ralenti y acelerando)
- [ ] Verificar que el sensor de posicion del acelerador (TPS/APP) llegue a 100%
- [ ] Verificar estado del turbo internamente (juego axial/radial del eje)

---

## Registro de Pruebas

### 2026-03-29 — Diagnostico Inicial
- Recopilacion de sintomas y datos de scanner
- Descarte sistematico de todos los sistemas verificables
- Conclusion: unica variable sin verificar = sistema de escape
- Identificacion de catalizador (tacho corto antes del puente de la caja)
- Programada prueba de escape para 2026-03-30
- **Hallazgo tardio critico:** motor previo consumia 1L aceite/100km con humo blanco masivo
- Esto contamino el catalizador con depositos de aceite quemado → causa raiz probable
- **Hallazgo adicional:** PCM fue reparada + PATS eliminado post cortocircuito en BJB
- Flash del PCM fue reprogramada → posible calibracion incorrecta (sospecha secundaria)

### 2026-04-01 — Prueba de Escape + Wastegate + Rotura Ventilador
- [x] **Resultado escape:** Silenciador muy tapado → reemplazado. Precamara anulada.
- [x] **Mejora:** Leve, insuficiente. Escape no era la causa principal.
- [x] **Descubrimiento critico:** Wastegate del turbo NO abre
  - Presion en mangueras de boost excesiva
  - Probada con compresor → precarga del resorte muy alta, costaba abrir
  - Regulada para reducir precarga → sigue sin abrir en operacion
  - Diafragma/pulmon del actuador funciona OK
  - Varilla desconectada: mariposa se mueve libremente → mecanismo OK
  - Rearmada con 3 vueltas de rosca de precarga
  - **No llega suficiente aire por la manguera al actuador** ← causa raiz
- [x] **Conclusion:** El circuito de señal de presion al actuador de la wastegate esta fallando (manguera tapada/pinchada o niple obstruido). Sin señal de presion, el actuador no abre la wastegate, el turbo sobrealimenta y la PCM recorta potencia.
- [x] **Siguiente paso:** Inspeccionar manguera de señal y niple de toma de presion (Paso 9B)
- [x] **Niple de toma:** probado con aire comprimido → fluye correctamente
- [x] **Manguera de señal:** verificada → fluye correctamente
- [x] **INCIDENTE:** Durante acelerada en vacio a 4000 RPM con wastegate desacoplada, se rompio paleta del ventilador → daño a radiador + encausador
  - Repuestos necesarios: radiador, encausador, viscoso + paletas
  - Programado reemplazo: 2026-04-02

---

## Datos del Vehiculo para Referencia Rapida

```
Vehiculo:        Ford Ranger 2008
Motor:           International NGD 3.0E Power Stroke
Inyeccion:       Siemens SID 901 CAN (Common Rail 3ra gen)
Potencia:        163 CV @ 3800 RPM
Torque:          380 Nm @ 1600-2200 RPM
Presion max:     1600 bar
Inyectores:      Piezoelectricos
Turbo:           Wastegate mecanica (no electronica)
Compresion:      17.0:1
Orden inyeccion: 1-3-4-2
Ralenti:         800 RPM (750 en Troller)
RPM max libre:   4640 RPM
```
