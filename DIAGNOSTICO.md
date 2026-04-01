# Proceso de Diagnostico - Descarte Sistematico

## Metodologia

Diagnostico por descarte sistematico: se verifico cada sistema del motor hasta aislar la causa raiz.

## Fase 0: Antecedentes del Vehiculo (hallazgo tardio - critico)

**Este dato se obtuvo avanzado el diagnostico y cambio el analisis completo.**

### Estado previo del motor
- Motor con aros desgastados: **consumo de aceite 1L cada 100 km**
- **Humo blanco masivo** por escape durante meses/años de uso
- El aceite quemado paso continuamente al sistema de escape

### Cronologia de eventos
1. Motor funcionando con aros gastados (humo blanco, consumo aceite) → **contamino el catalizador**
2. **Reparacion del motor**: aros nuevos, tapa de cilindros reparada
3. **Cortocircuito en la BJB** (fusiblera vano motor): daño electrico
4. **Reparacion del PCM** + eliminacion del sistema PATS (inmovilizador)

### Implicancias
- El aceite quemado (1L/100km) genera depositos duros en el sustrato ceramico del catalizador
- A diferencia del hollin de gasoil, los residuos de aceite NO se limpian con temperatura
- El catalizador se fue tapando progresivamente durante toda la vida util del motor viejo
- Al reconstruir el motor, el escape ya no genera humo pero el catalizador quedo obstruido
- La reparacion del PCM + eliminacion PATS implica reflash completa del firmware → posible calibracion incorrecta (sospecha secundaria)

---

## Fase 1: Identificacion del Sintoma

**Sintoma reportado:** "No tiene la fuerza que deberia tener para acelerar"

**Caracterizacion detallada:**
- Motor en vacio: llega a 4000 RPM ✅
- 1ra marcha: salida lenta hasta 2500 RPM
- 2da-4ta marcha: motor llega a 3000-3500 RPM
- 5ta marcha: tope 120 km/h a 2000 RPM, no sube
- Sin humo de ningun tipo
- Turbo se siente a ~1600 RPM
- 3ra a fondo: maximo 3500 RPM (deberia superar 4000)

**Calculo de potencia estimada:**
A 120 km/h en 5ta sin poder acelerar:
- Resistencia aerodinamica: ~600-800 N
- Resistencia de rodadura: ~300-400 N
- Potencia = ~1100 N x 33.3 m/s ≈ 37 kW ≈ **50 HP**
- Motor nominal: 163 HP
- **Produce ~30% de su capacidad**

## Fase 2: Descarte del Sistema de Combustible

### 2.1 Circuito de Baja Presion
| Componente | Verificacion | Resultado |
|------------|-------------|-----------|
| Bomba de levante | Nueva. Test caudal: 1.4L en 30s | ✅ OK (spec: >1.35L/30s) |
| Filtro combustible | Nuevo | ✅ OK |
| Flujo pre/post filtro | Mismo caudal en ambos puntos | ✅ Filtro no restringe |
| Interruptor inercial | Verificado, no saltado | ✅ OK |

**Conclusion baja presion:** Sistema de baja presion funciona correctamente. Descartado.

### 2.2 Circuito de Alta Presion
| Componente | Verificacion | Resultado |
|------------|-------------|-----------|
| Sensor FRP | Nuevo | ✅ |
| Valvula VCV | Nueva | ✅ |
| Valvula PCV | Nueva | ✅ |
| Presion rail ralenti | 460 bar (esperado 250-350) | ⚠️ Alta, PCM compensa |
| Presion rail plena carga | 1400 bar (esperado 1200-1600) | ✅ Alcanza rango |

**Conclusion alta presion:** El sistema alcanza la presion necesaria (1400 bar). Los componentes criticos son nuevos. **Descartado como causa principal.**

> **Nota:** La presion de ralenti alta (460 bar) sugiere que el PCM esta compensando algo. Esto podria ser consecuencia (no causa) de la restriccion de escape — el motor necesita mas presion para mantener el ralenti contra la contrapresion.

### 2.3 Inyectores
| Parametro | Valor | Estado |
|-----------|-------|--------|
| Correccion >2000 RPM | 0.980 | ✅ Cercano a 1.0 (normal) |
| Retorno | No medido | ⚠️ Pendiente si falla test escape |

**Conclusion inyectores:** Correcciones normales. Probablemente OK. Descartado provisionalmente.

## Fase 3: Descarte del Sistema de Admision de Aire

### 3.1 Filtro y Ductos
| Componente | Verificacion | Resultado |
|------------|-------------|-----------|
| Filtro de aire | Nuevo | ✅ |
| Mangueras intercooler | Se inflan bajo presion | ✅ No hay fugas |

### 3.2 Turbocompresor
| Parametro | Valor | Esperado | Estado |
|-----------|-------|----------|--------|
| Sobrepresion plena carga | 1.5 bar (*) | 1.0-1.5 bar | ⚠️ Ver nota |
| Entrada en boost | ~1600 RPM | ~1500-1800 RPM | ✅ NORMAL |
| Silbido turbo | Se escucha | - | ✅ |
| Tipo de turbo | Wastegate mecanica | - | Info |
| **Wastegate** | **No abre** | Debe abrir a ~0.8-1.0 bar | **❌ TRABADA** |

(*) 1.5 bar fue medido con motor recortado por PCM. Sin recorte, la presion real seria mayor.

**Conclusion turbo:** El compresor funciona correctamente pero la **wastegate esta trabada** (precarga excesiva, no es el diafragma). Sin wastegate funcional → sobrealimentacion → PCM recorta potencia. **CAUSA PRINCIPAL IDENTIFICADA (2026-04-01).**

### 3.3 Sensor T-MAP
| Verificacion | Resultado |
|-------------|-----------|
| Limpieza | Realizada |
| DTCs relacionados | Ninguno |

**Conclusion T-MAP:** Sin codigos de error. Descartado provisionalmente.

## Fase 4: Descarte de Distribucion

| Verificacion | Resultado |
|-------------|-----------|
| Marcas ciguenal/arbol de levas | Verificadas, correctas |
| Tensores de cadena | OK |

**Conclusion distribucion:** Puesta a punto correcta. **Descartado.**

## Fase 5: Descarte de Transmision

| Componente | Verificacion | Resultado |
|------------|-------------|-----------|
| Embrague | Reparado | ✅ No patina |
| Caja de cambios | Funciona en todas las marchas | ✅ |

**Conclusion transmision:** Descartado.

## Fase 6: Descarte de Electronica

| Verificacion | Resultado |
|-------------|-----------|
| DTCs almacenados | Solo P0704 (sensor embrague removido) |
| DTCs motor/inyeccion | Ninguno |
| Inmovilizador PATS | Funciona normal |
| Comunicacion scanner | OK |

**Conclusion electronica:** Sin fallas. Descartado.

## Fase 7: Sistema de Escape ✅ COMPLETADO (2026-04-01)

### Trabajos realizados
- **Silenciador:** Estaba muy tapado → **reemplazado por silenciador nuevo**
- **Precamara (salida del turbo):** **Anulada**
- **Prueba de ruta post-reparacion:** Mejora leve pero insuficiente

### Resultado
El escape contribuia parcialmente al problema (silenciador tapado) pero **no era la causa principal**. Despues de reemplazar silenciador y anular precamara, la falta de potencia persiste en ~80% de su severidad original.

### Conclusion
Escape descartado como causa principal. La restriccion del silenciador sumaba al problema pero la causa raiz es otra → ver Fase 7B.

---

## Fase 7B: Wastegate del Turbo — CAUSA PRINCIPAL IDENTIFICADA (2026-04-01)

### Descubrimiento
Durante la inspeccion del sistema de escape se descubrio que la **valvula wastegate del turbo NO abre**. La presion en las mangueras de boost es excesiva.

### Pruebas realizadas
| Prueba | Resultado |
|--------|-----------|
| Presion en mangueras de boost | Excesiva (mucho mas de lo normal) |
| Wastegate con compresor de aire | Costaba abrir — precarga muy alta |
| Regulacion de precarga del resorte | Reducida, pero sigue sin abrir en operacion |
| Diafragma/pulmon del actuador | Funciona OK (descartado como causa) |
| **Mariposa con varilla desconectada** | **Se mueve libremente** → mecanismo OK ✅ |
| Rearmado con precarga | 3 vueltas de rosca |
| **Aire en manguera al actuador** | **No llega suficiente presion** ← CAUSA RAIZ |

### Analisis

**¿Por que la wastegate no abre? → No recibe señal de presion**

```
Manguera de señal no entrega presion de boost al actuador
        |
Actuador wastegate nunca recibe la señal de "hay sobrePresion"
        |
Wastegate permanece cerrada → turbo sobrealimenta sin control
        |
T-MAP reporta sobrePresion a la PCM
        |
PCM aplica smoke limiter / torque limiter como proteccion
        |
Motor recortado por software → ~30% de potencia efectiva
```

**Descarte progresivo de la wastegate:**
1. ~~Mecanismo de la valvula trabado~~ → Mariposa se mueve libre ✅
2. ~~Diafragma/pulmon roto~~ → Funciona con compresor ✅
3. ~~Resorte con precarga excesiva~~ → Regulado, sigue sin abrir ✅
4. **Manguera de señal / niple de toma → NO LLEGA PRESION** ← PENDIENTE

**¿Por que no se detecto antes?**
- La medicion de scanner mostro 1.5 bar de boost → parecia "normal"
- Pero ese valor se midio con el motor YA recortado por la PCM
- Sin el recorte de la PCM, la presion de boost seria mucho mayor (turbo sin freno)
- La SID 901 no tiene DTC especifico para sobrealimentacion (turbo no pilotado electronicamente)

### Verificacion adicional (2026-04-01)

| Prueba | Resultado |
|--------|-----------|
| Aire comprimido por niple de toma | ✅ Fluye correctamente |
| Manguera de señal | ✅ Sin obstruccion |

**Todos los componentes individuales de la wastegate verificados OK.** Sin embargo, la wastegate sigue sin abrir en operacion. Esto sugiere que el problema puede ser:

1. **Resorte del actuador con constante incorrecta** — instalado durante la reparacion del turbo, de otro modelo con mayor resistencia. Aunque la precarga se regulo, la fuerza necesaria para comprimir el resorte supera la presion de boost disponible.

2. **Presion de boost real menor a la esperada** — los 1.5 bar medidos por scanner son con motor recortado por PCM. Menos combustible → menos gases → menos velocidad de turbina → menos boost → wastegate no abre. Circulo vicioso.

3. **Turbo con problemas internos** — juego excesivo en rodamientos, rueda dañada, sellos con fuga → no genera presion suficiente para abrir la wastegate.

### Estado
**⏳ PENDIENTE — Verificar turbo internamente, bomba de inyeccion y datos de scanner**

---

## Fase 7C: Bomba de Inyeccion — Anomalia de Presion de Rail (2026-04-01)

### Anomalia no resuelta
La presion de rail en ralenti de **460 bar** (esperado 250-350) nunca fue explicada satisfactoriamente. Los sensores VCV y PCV son nuevos, pero:

- ¿Son del numero de parte correcto para Ranger 2008 3.0L SID 901?
- ¿La PCM esta COMANDANDO 460 bar (calibracion) o la bomba esta forzando esa presion?

### Importancia
Si la PCM esta compensando una condicion anormal, la presion alta de rail puede ser un **sintoma** de otro problema (ej: sobreboost, sensor incorrecto). Pero si la bomba/PCV son de spec incorrecta, la presion alta de rail seria una **causa** adicional de mal funcionamiento.

### Verificacion critica con scanner
Leer **presion de rail DESEADA vs REAL** en ralenti:
- Si deseada ≈ real ≈ 460 bar → PCM lo comanda asi (problema de calibracion o compensacion)
- Si deseada ≈ 300 bar y real ≈ 460 bar → PCV no alivia o VCV deja pasar demasiado

## Fase 7D: Inyectores — Evaluacion (2026-04-01)

### Observaciones
- Inyectores algo ruidosos
- Correccion se estabiliza en 0.980 apenas suben RPM
- Tipo: piezoelectricos

### Evaluacion
La correccion de 0.98 es aceptable (rango normal 0.95-1.05). El ruido en inyectores piezoelectricos puede ser normal si es **parejo** entre los 4 cilindros. Si un inyector suena marcadamente distinto, podria tener fuga interna.

**Prioridad:** BAJA — los inyectores son improbables como causa principal dado que la correccion es estable.

---

## Fase 8: PCM Reparada — Sospecha Secundaria

### Hallazgo
La PCM fue reparada y se elimino el sistema PATS (inmovilizador) despues de un cortocircuito en la BJB. Esto implica que la flash del PCM fue reprogramada.

### Riesgo
Si el tecnico que reparo la PCM uso un firmware generico, de otro modelo, o una calibracion incorrecta, los mapas de inyeccion (cantidad de combustible, presion de rail objetivo, limite de torque, smoke limiter) podrian estar mal. Esto limitaria la potencia por software.

### Verificacion
- Leer la flash del PCM con herramienta MPPS/KESSv2/KTag
- Comparar calibracion contra archivo original de Ranger 2008 3.0 SID 901
- Verificar mapas de IQ (injection quantity), torque limiter, smoke limiter, rail pressure target

### Herramientas necesarias para reprogramacion DIY
| Elemento | Precio aprox (USD) |
|----------|-------------------|
| MPPS v18/v21 (clon) | $50-80 |
| WinOLS o ECM Titanium | $0-50 (community) |
| Notebook con USB | Ya disponible |

### Estado
**⏳ PENDIENTE — A verificar solo si la reparacion/reemplazo de wastegate no resuelve**

---

## Resumen del Descarte

```
Motor reconstruido         ──── ✅ Descartado
Bomba de levante           ──── ✅ Descartado (nueva, caudal OK)
Filtro combustible         ──── ✅ Descartado (nuevo)
VCV / PCV                  ──── ✅ Descartado (nuevos)
Sensor FRP                 ──── ✅ Descartado (nuevo)
Presion de rail            ──── ✅ Descartado (1400 bar a plena carga)
Inyectores                 ──── ✅ Descartado (correccion ~1.0)
Filtro de aire             ──── ✅ Descartado (nuevo)
Turbo (compresion)         ──── ✅ Descartado (genera boost correctamente)
T-MAP                      ──── ✅ Descartado (limpio, sin DTCs)
Distribucion               ──── ✅ Descartado (verificada)
Embrague                   ──── ✅ Descartado (reparado, no patina)
Intercooler/mangueras      ──── ✅ Descartado (inflan correctamente)
EGR                        ──── ✅ No aplica (este modelo no tiene)
Electronica/DTCs           ──── ✅ Descartado (sin codigos relevantes)
Silenciador                ──── ✅ Tapado → REEMPLAZADO (mejora leve)
Precamara turbo            ──── ✅ ANULADA (mejora leve)
                                    │
WASTEGATE TURBO            ──── ❌ NO ABRE (todos los componentes verificados OK individualmente)
  Actuador                 ────── ✅ Funciona OK (probado con compresor)
  Mariposa                 ────── ✅ Se mueve libre (verificada a mano)
  Manguera señal           ────── ✅ Fluye correctamente
  Niple de toma            ────── ✅ Fluye correctamente
  Resorte                  ────── ❓ ¿Constante correcta? (¿pieza del turbo reconstruido?)
                                    │
TURBO (estado interno)     ──── ❓ PENDIENTE ← verificar juego, ruedas, sellos
BOMBA INYECCION (VCV/PCV)  ──── ❓ PENDIENTE ← rail 460 bar en ralenti sin explicar
                                    │         ¿Numero de parte correcto?
                                    │         ¿PCM comanda o bomba fuerza?
Inyectores                 ──── ✅ Probablemente OK (correccion 0.98, ruido parejo)
                                    │
                                    │
PCM (calibracion)          ──── ❓ PENDIENTE ← SOSPECHA SECUNDARIA
                                              Causa: reflash por reparacion + eliminacion PATS
```
