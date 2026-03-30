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
| Sobrepresion plena carga | 1.5 bar | 1.0-1.5 bar | ✅ NORMAL |
| Entrada en boost | ~1600 RPM | ~1500-1800 RPM | ✅ NORMAL |
| Silbido turbo | Se escucha | - | ✅ |
| Tipo de turbo | Wastegate mecanica | - | Info |

**Conclusion turbo:** Genera presion de boost correcta (1.5 bar). **Descartado.**

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

## Fase 7: Sistema de Escape — PENDIENTE DE VERIFICACION

### Por que el escape es la unica variable restante

Todos los sistemas de ENTRADA (aire, combustible, electronica, mecanica) estan verificados y funcionan correctamente. El motor recibe:
- ✅ Combustible suficiente (1400 bar rail)
- ✅ Aire suficiente (1.5 bar boost)
- ✅ Timing correcto (distribucion verificada)
- ✅ Compresion (motor recien armado)
- ❌ **NO se verifico la SALIDA de gases**

### Evidencia que apunta al escape

1. **En vacio vs bajo carga:** Motor llega a 4000 RPM en vacio (poco flujo de escape) pero solo 3500 RPM en 3ra a fondo (mucho flujo). Un escape tapado restringe mas a mayor caudal de gases.

2. **Perdida progresiva con la marcha:** En marchas cortas la multiplicacion de la caja compensa, pero en 5ta la falta de torque se expone completamente.

3. **Sin humo:** El motor no puede quemar mas combustible porque no puede evacuar los gases quemados.

4. **Presion de ralenti alta (460 bar):** El PCM podria estar compensando la contrapresion de escape inyectando mas combustible para mantener el ralenti.

5. **Sin DTCs:** La Ranger con SID 901 **NO tiene sensor de contrapresion de escape** ni sonda lambda post-catalizador, por lo que un catalizador tapado no genera codigo de error.

### Componentes del escape identificados

```
[TURBO] → [Downpipe] → [TACHO CORTO = Catalizador] → [Caño] → [TACHO GRANDE = Silenciador] → [Salida]
                                    ↑
                            SOSPECHA PRINCIPAL
```

El "tacho corto" ubicado antes del puente de la caja es el catalizador catalitico. El "tacho grande" posterior es el silenciador.

### Estado
**⏳ PENDIENTE — Prueba programada para 2026-03-30**

### Causa raiz probable: aceite quemado del motor viejo

El antecedente de **1L de aceite cada 100 km + humo blanco masivo** durante meses/años es la "pistola humeante". Ese aceite quemado se deposito dentro del catalizador formando una costra dura e irreversible que obstruye el paso de gases.

Esto explica por que:
- Se cambiaron sensores, bomba, filtros y nada mejoro → el problema nunca fue el motor
- Todos los sistemas de entrada funcionan perfecto → el cuello de botella esta en la salida
- Sin humo actual → no es exceso de combustible, es que el motor no puede exhalar
- En vacio rinde bien (poco flujo de escape) pero bajo carga se ahoga (mucho flujo)

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
**⏳ PENDIENTE — A verificar solo si la prueba de escape no da resultado**

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
Turbo                      ──── ✅ Descartado (1.5 bar boost = normal)
T-MAP                      ──── ✅ Descartado (limpio, sin DTCs)
Distribucion               ──── ✅ Descartado (verificada)
Embrague                   ──── ✅ Descartado (reparado, no patina)
Intercooler/mangueras      ──── ✅ Descartado (inflan correctamente)
EGR                        ──── ✅ No aplica (este modelo no tiene)
Electronica/DTCs           ──── ✅ Descartado (sin codigos relevantes)
                                    │
ESCAPE (catalizador)       ──── ❓ PENDIENTE ← SOSPECHA PRINCIPAL (confianza ALTA)
                                    │         Causa: aceite quemado del motor viejo
                                    │
PCM (calibracion)          ──── ❓ PENDIENTE ← SOSPECHA SECUNDARIA
                                              Causa: reflash por reparacion + eliminacion PATS
```
