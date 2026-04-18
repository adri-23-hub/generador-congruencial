# Tasks: Generador Congruencial Mixto y Multiplicativo

## Implementation Tasks

### Phase 1: Estructura HTML

- [x] **1.1** Crear archivo HTML principal con estructura base
- [x] **1.2** Agregar formulario con campos:
  - Selector: Mixto / Multiplicativo
  - Input: X0 (semilla)
  - Input: a (multiplicador)
  - Input: m (módulo)
  - Input: c (constante aditiva)
  - Botón: "Generar"
  - Botón: "Exportar PDF"

### Phase 2: Validación de Parámetros

- [x] **2.1** Implementar función de validación de m > 0
- [x] **2.2** Implementar validación X0 < m
- [x] **2.3** Implementar validación a < m
- [x] **2.4** Validar c = 0 en modo multiplicativo
- [x] **2.5** Mostrar mensajes de error con explicaciones

### Phase 3: Análisis de Representación

- [x] **3.1** Detectar si m es potencia de 2
- [x] **3.2** Clasificar como binario/decimal
- [x] **3.3** Mostrar explicación de la clasificación
- [x] **3.4** Mostrar advertencia cuando período no será máximo

### Phase 4: Motor LCG

- [x] **4.1** Implementar algoritmo mixto: X(n+1) = (a·X(n) + c) mod m
- [x] **4.2** Implementar algoritmo multiplicativo: X(n+1) = (a·X(n)) mod m
- [x] **4.3** Generar secuencia de números pseudoaleatorios
- [x] **4.4** Detectar período (primera repetición)
- [x] **4.5** Limitar máximo de iteraciones (10000)

### Phase 5: Interfaz de Resultados

- [x] **5.1** Mostrar secuencia generada en tabla
- [x] **5.2** Mostrar clasificación binario/decimal
- [x] **5.3** Mostrar período detectado
- [x] **5.4** Resaltar primera repetición

### Phase 6: Exportación PDF

- [x] **6.1** Integrar jsPDF
- [x] **6.2** Generar PDF con parámetros
- [x] **6.3** Incluir secuencia en PDF
- [x] **6.4** Incluir período en PDF

### Phase 7: Pruebas y Validación

- [x] **7.1** Probar con parámetros válidos
- [x] **7.2** Probar validación de errores
- [x] **7.3** Probar clasificación binario/decimal
- [x] **7.4** Probar exportación PDF
- [x] **7.5** Verificar detección de período

## Dependencies

- jsPDF (biblioteca para PDF)

## Notes

- Usar BigInt para operaciones con números grandes
- Limitar iteraciones a 10000 para evitar loops infinitos
- Validar antes de ejecutar para mejor UX