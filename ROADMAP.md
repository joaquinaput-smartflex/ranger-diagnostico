# Roadmap de Verificacion - Paso a Paso

## Estado General

```
[██████████████████░░] 90% — Pendiente: prueba de escape
```

**Fecha inicio diagnostico:** 2026-03-29
**Proxima prueba programada:** 2026-03-30

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

## Paso 6: Verificacion de Turbo ✅
- [x] Silbido del turbo (se escucha)
- [x] RPM de entrada en boost: ~1600 RPM (normal)
- [x] Presion de boost a plena carga: 1.5 bar de sobrepresion (NORMAL)
- [x] Tipo de turbo confirmado: wastegate mecanica, no pilotado

**Resultado:** Turbo funciona correctamente. 1.5 bar de boost es valor nominal.

## Paso 7: Verificacion de Distribucion ✅
- [x] Marcas de puesta a punto ciguenal/arbol de levas (correctas)

**Resultado:** Timing correcto.

## Paso 8: Verificacion de Transmision ✅
- [x] Embrague reparado, no patina
- [x] Caja funciona en todas las marchas

**Resultado:** Transmision OK.

## Paso 9: Verificacion de Sistema de Escape ⏳ PENDIENTE
- [ ] **Identificar componentes del escape** ✅ (2 tachos: catalizador + silenciador)
- [ ] **PRUEBA: Desconectar escape antes del catalizador**
- [ ] Probar camioneta con escape libre
- [ ] Evaluar resultado

### Procedimiento para la prueba de escape

**Herramientas necesarias:**
- Llave de boca/tubo (tamaño segun bulones de la brida, tipicamente 13mm o 15mm)
- WD-40 o similar (aplicar la noche anterior a los bulones)
- Proteccion auditiva (va a hacer mucho ruido)

**Pasos:**
1. **Preparacion (noche anterior):**
   - Rociar WD-40 generosamente en los bulones/abrazadera de la union entre downpipe del turbo y catalizador
   - Dejar actuar toda la noche

2. **Desconexion:**
   - Motor FRIO (importante: el escape se calienta mucho)
   - Ubicar la brida/union entre la bajada del turbo y el catalizador (tacho corto)
   - Aflojar los bulones o la abrazadera
   - No es necesario sacarlos del todo, solo separar lo suficiente para que los gases salgan

3. **Prueba de ruta:**
   - ⚠️ Usar proteccion auditiva — el ruido sera muy fuerte
   - ⚠️ Probar en zona sin vecinos
   - Hacer la misma prueba que siempre: salir en 1ra, subir marchas, llegar a 5ta
   - **Prestar atencion a:**
     - ¿La salida en 1ra es mas rapida?
     - ¿El motor sube mas de RPM bajo carga?
     - ¿En 5ta supera los 120 km/h?
     - ¿Cuantas RPM maximas alcanza en 3ra a fondo?

4. **Evaluacion:**

   **SI MEJORA NOTABLEMENTE:**
   - Catalizador tapado CONFIRMADO
   - Solucion: reemplazar catalizador o vaciarlo (eliminar el sustrato interno)
   - Opcion: instalar un caño recto en lugar del catalizador

   **SI NO MEJORA:**
   - Repetir la prueba desconectando DESPUES del silenciador (tacho grande)
   - Si con silenciador desconectado tampoco mejora → escape descartado
   - Ir a Paso 10 (diagnostico alternativo)

5. **Reconexion:**
   - Volver a ajustar los bulones/abrazadera
   - Verificar que no haya fugas audibles en ralenti

## Paso 10: Diagnostico Alternativo (solo si falla test de escape)

Si la prueba del escape NO muestra mejora, las siguientes verificaciones son:

- [ ] Medir retorno individual de inyectores (Paso 4 completo)
- [ ] Verificar cableado del T-MAP con multimetro (5V referencia, senal en ralenti y acelerando)
- [ ] Verificar presion de rail NOMINAL vs REAL en scanner (si la real esta por debajo de la nominal, hay fuga/restriccion)
- [ ] Verificar que el sensor de posicion del acelerador (TPS/APP) llegue a 100% a fondo
- [ ] Considerar reprogramacion/actualizacion del PCM

---

## Registro de Pruebas

### 2026-03-29 — Diagnostico Inicial
- Recopilacion de sintomas y datos de scanner
- Descarte sistematico de todos los sistemas verificables
- Conclusion: unica variable sin verificar = sistema de escape
- Identificacion de catalizador (tacho corto antes del puente de la caja)
- Programada prueba de escape para 2026-03-30

### 2026-03-30 — Prueba de Escape (PENDIENTE)
- [ ] Resultado:
- [ ] Observaciones:
- [ ] Conclusion:
- [ ] Siguiente paso:

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
