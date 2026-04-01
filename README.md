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
- Silenciador reemplazado (estaba tapado)
- Precamara de salida del turbo anulada
- Wastegate: regulada precarga, verificada mariposa libre, manguera y niple OK
- No hay fugas ni perdidas de liquidos

### Incidente durante diagnostico (2026-04-01)
- Paleta del ventilador se rompio durante acelerada en vacio a 4000 RPM
- Daño colateral: radiador y encausador rotos
- **Pendiente reemplazo:** radiador + encausador + viscoso + paletas (2026-04-02)

## Hipotesis Principal: Wastegate No Abre — Causa Raiz Pendiente

**Nivel de confianza: ALTO (wastegate confirmada como problema, causa raiz en investigacion)**

```
Wastegate no abre en operacion (todos los componentes OK individualmente)
        |
Posibles causas restantes:
├── Resorte con constante incorrecta (turbo reconstruido, pieza de otro modelo)
├── Turbo no genera suficiente boost real (daño interno, circulo vicioso con PCM)
└── Bomba de inyeccion: presion rail 460 bar ralenti sin explicar (VCV/PCV spec?)
        |
Turbo sobrealimenta o PCM recorta por anomalias → ~30% de potencia
```

**Evidencia:**
- Presion en mangueras de boost es excesiva (mucho mas de lo normal)
- Wastegate probada con compresor de aire → costaba abrir, precarga muy alta
- Se redujo precarga del resorte pero la valvula sigue sin abrir bajo operacion
- Diafragma/pulmon del actuador funciona OK (probado con compresor)
- Mariposa verificada: **se mueve libremente** con varilla desconectada → mecanismo OK
- Rearmada con 3 vueltas de rosca de precarga
- **No llega suficiente aire por la manguera al actuador** → causa raiz del no-apertura
- Presion de rail alta en ralenti (460 bar) encaja con PCM compensando condiciones anormales
- Sin DTCs = la SID 901 no tiene codigo especifico para sobrealimentacion (turbo no pilotado)

**Resultado prueba de escape (2026-04-01):**
- Silenciador estaba muy tapado → reemplazado
- Precamara a la salida del turbo → anulada
- Mejora leve pero insuficiente → escape no era la causa principal
- Descubierta la wastegate trabada durante la inspeccion

**Hipotesis secundaria:** PCM con calibracion incorrecta (por reparacion + eliminacion PATS). A verificar si la reparacion/reemplazo de wastegate no resuelve.

## Valores Medidos con Scanner

| Parametro | Valor medido | Valor esperado | Estado |
|-----------|-------------|----------------|--------|
| Presion rail ralenti | 460 bar | 250-350 bar | ⚠️ ALTA |
| Presion rail 2000 RPM en ruta | 1100 bar | - | Normal (carga parcial) |
| Presion rail maxima (plena carga) | 1400 bar | 1200-1600 bar | ✅ OK |
| Boost turbo (sobrepresion) plena carga | 1.5 bar (*) | 1.0-1.5 bar | ⚠️ Ver nota |
| Correccion inyectores >2000 RPM | 0.980 | ~1.000 | ✅ OK |
| RPM maxima en vacio | 4000 RPM | 4640 RPM (max libre) | ✅ Razonable |
| RPM maxima 3ra a fondo | 3500 RPM | >4000 RPM | ⚠️ BAJA |
| Wastegate | No abre | Debe abrir a ~0.8-1.0 bar | ❌ TRABADA |
| DTCs | P0704 (sensor embrague) | - | No relevante |

(*) El valor de 1.5 bar fue medido con el motor ya recortado por la PCM. Con wastegate trabada, la presion real sin recorte podria ser significativamente mayor.

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
