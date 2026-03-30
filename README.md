# Ford Ranger 2008 Power Stroke 3.0L - Diagnostico de Falta de Potencia

## Vehiculo
| Dato | Valor |
|------|-------|
| **Vehiculo** | Ford Ranger 2008 |
| **Motor** | International NGD 3.0E Power Stroke Turbo Diesel |
| **Inyeccion** | Siemens SID 901 CAN - Common Rail 3ra generacion |
| **Potencia nominal** | 163 CV @ 3800 RPM |
| **Torque nominal** | 380 Nm @ 1600-2200 RPM |
| **Presion maxima rail** | 1600 bar |
| **Inyectores** | Piezoelectricos |
| **Turbo** | Wastegate mecanica (NO pilotado electronicamente) |
| **EGR** | No posee (norma Euro III) |
| **Transmision** | Manual 5 velocidades |

## Sintoma Principal

La camioneta **no tiene la fuerza que deberia** para acelerar. Especificamente:

- En vacio llega a 4000 RPM sin problemas
- En ruta, la salida en 1ra es lenta hasta que el motor alcanza 2500 RPM
- En 2da, 3ra y 4ta puede llevar el motor a 3000-3500 RPM
- **En 5ta marcha pierde fuerza**: mantiene 120 km/h a 2000 RPM en ruta plana pero no sube mas
- No hay humo de ningun tipo (negro, blanco ni azul)
- El turbo se siente que entra en accion a ~1600 RPM
- En 3ra marcha a fondo, alcanza maximo 3500 RPM (deberia poder mas)

**Estimacion de perdida:** A 120 km/h en 5ta sin poder acelerar, el motor produce ~50 HP de los 163 nominales (~30% de capacidad).

## Antecedentes Criticos

### Estado previo del motor (ANTES de la reparacion)
- **Consumo de aceite: 1 litro cada 100 km** (aros desgastados)
- **Mucho humo blanco** por escape durante meses/años
- El aceite quemado paso al sistema de escape durante todo ese periodo

### Cronologia de reparaciones
1. **Reparacion del motor**: cambio de aros y reparacion de tapa de cilindros
2. **Cortocircuito en la BJB** (fusiblera del vano motor): daño electrico posterior
3. **Reparacion del PCM**: se reparo el modulo y se elimino la seguridad PATS (inmovilizador)

### Trabajos realizados
- Motor completo: cambio de aros y reparacion de tapa de cilindros
- Turbo reparado
- Bomba de combustible de levante nueva
- Filtro de combustible nuevo
- Filtro de aire nuevo
- Sensor de presion de rail (FRP) nuevo
- Sensores VCV y PCV de la bomba de alta nuevos
- Sensor T-MAP limpio
- Embrague reparado (no patina)
- Mangueras de intercooler verificadas (se inflan correctamente)
- PCM reparada + eliminacion PATS (post cortocircuito BJB)
- No hay fugas ni perdidas de liquidos

## Hipotesis Principal: Catalizador Tapado por Aceite Quemado

**Nivel de confianza: MUY ALTO**

```
Motor con aros gastados (consumo aceite 1L/100km)
        |
Humo blanco constante por escape durante meses/años
        |
Aceite quemado tapo el sustrato ceramico del catalizador
        |
Se reconstruyo el motor (aros nuevos, tapa reparada)
        |
Motor ahora perfecto, NO consume aceite ni larga humo
        |
PERO el catalizador quedo tapado por el daño del motor anterior
        |
Motor nuevo no puede evacuar gases → ~30% de potencia
```

**Evidencia que soporta esta hipotesis:**
- El motor previo consumia 1L aceite/100km con humo blanco masivo → contamino el catalizador
- Todos los sistemas de ENTRADA (aire, combustible, electronica) estan verificados y OK
- Turbo genera 1.5 bar de boost (normal) y rail llega a 1400 bar (normal)
- Sin humo actual = motor no puede quemar mas porque no puede exhalar
- Sin DTCs de escape = la Ranger SID 901 NO tiene sensor de contrapresion de escape
- En vacio llega a 4000 RPM (poco flujo) pero bajo carga solo 3500 RPM (mucho flujo, se ahoga)

**Hipotesis secundaria:** PCM con calibracion incorrecta (por reparacion + eliminacion PATS). A verificar si la prueba de escape no da resultado.

## Valores Medidos con Scanner

| Parametro | Valor medido | Valor esperado | Estado |
|-----------|-------------|----------------|--------|
| Presion rail ralenti | 460 bar | 250-350 bar | ⚠️ ALTA |
| Presion rail 2000 RPM en ruta | 1100 bar | - | Normal (carga parcial) |
| Presion rail maxima (plena carga) | 1400 bar | 1200-1600 bar | ✅ OK |
| Boost turbo (sobrepresion) plena carga | 1.5 bar | 1.0-1.5 bar | ✅ OK |
| Correccion inyectores >2000 RPM | 0.980 | ~1.000 | ✅ OK |
| RPM maxima en vacio | 4000 RPM | 4640 RPM (max libre) | ✅ Razonable |
| RPM maxima 3ra a fondo | 3500 RPM | >4000 RPM | ⚠️ BAJA |
| DTCs | P0704 (sensor embrague) | - | No relevante |

## Documentacion de Referencia

Los manuales tecnicos estan en la carpeta del proyecto (no incluidos en el repo por copyright):

| Archivo | Contenido | Paginas |
|---------|-----------|---------|
| `Ranger-3-0-manual1.pdf` | Manual diagnostico fallas Siemens SID 901 | 134 pags |
| `Power-Stroke-30-l.pdf` | Especificaciones tecnicas motor NGD 3.0E (linea Cargo) | 56 pags |

### Datos clave extraidos de los manuales

**Sistema de inyeccion (Manual 1):**
- PCM Siemens SID 901 con 3 pineras
- Bomba de alta con control por Entrada (VCV) y Salida (PCV)
- VCV: Normal Cerrada, resistencia 2-3 Ohm (tipica 2.75 Ohm)
- PCV: Normal Abierta, resistencia 2.8-4 Ohm (tipica 3 Ohm)
- Fallas VCV causan tironeo 1800-2200 RPM
- Presion baja de levante (<0.2 bar) causa tironeo 1800-2500 RPM

**Turbo (Manual 1, pag 31):**
> "El Sistema de Admision de Aire de la Ranger cuenta con un Turbocompresor **no Pilotado** que limita la maxima presion del Sistema mediante una Valvula **WASTE GATE** conectada directamente en paralelo con la Admision."
>
> "La Ranger **no posee ningun control Electronico sobre el Turbo**."

**Presion de bomba de levante (Manual 1, pag 20-23):**
- Tipica: 0.35 bar
- Maxima: 1 bar
- Minima: 0.2 bar
- Test caudal: >1350 ml en 30 segundos

**Sensor FRP (Manual 1, pag 96):**
- En arranque: 1.4V a 1.7V (si no supera 1.3V no arranca)
- A 3000 RPM: 1.8V a 2V

---

Consultar [DIAGNOSTICO.md](DIAGNOSTICO.md) para el proceso completo de descarte y [ROADMAP.md](ROADMAP.md) para los proximos pasos.
