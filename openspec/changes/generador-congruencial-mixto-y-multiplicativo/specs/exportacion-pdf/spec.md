## ADDED Requirements

### Requirement: Exportar resultados a PDF
El sistema SHALL permitir exportar los parámetros y la secuencia generada a un archivo PDF.

#### Scenario: Exportar con параметros válidos
- **WHEN** usuario completa la generación y hace clic en "Exportar PDF"
- **THEN** sistema descarga un archivo PDF con los parámetros y la secuencia

#### Scenario: Exportar sin haber generado
- **WHEN** usuario hace clic en "Exportar PDF" sin ejecutar el algoritmo
- **THEN** sistema muestra mensaje "Debe ejecutar el algoritmo primero"

### Requirement: Incluir parámetros en PDF
El sistema SHALL incluir los parámetros ingresados en el documento PDF.

#### Scenario: PDF con parámetros
- **WHEN** usuario exporta a PDF
- **THEN** el PDF incluye:
  - Tipo de algoritmo (mixto/multiplicativo)
  - Valores de X0, a, m, c
  - Clasificación binario/decimal

### Requirement: Incluir secuencia en PDF
El sistema SHALL incluir la secuencia completa de números generados en el PDF.

#### Scenario: PDF con secuencia
- **WHEN** usuario exporta a PDF
- **THEN** el PDF incluye:
  - Número de iteraciones realizadas
  - Lista completa de valores X(n)
  - Punto de repetición (si se detectó)
  - Período (si aplica)

### Requirement: Incluir período en PDF
El sistema SHALL incluir información sobre el período detectado en el PDF.

#### Scenario: Período detectado
- **WHEN** se detecta repetición en la iteración 15
- **THEN** el PDF indica "Período: 15 (desde iteración 1)"