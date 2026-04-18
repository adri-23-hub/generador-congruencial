## ADDED Requirements

### Requirement: Mostrar mensaje de error preciso
El sistema SHALL mostrar un mensaje de error claro que indique exactamente qué parámetro es inválido.

#### Scenario: Error en m negativo
- **WHEN** usuario ingresa m = -5
- **THEN** sistema muestra "Error: m debe ser mayor que 0"

#### Scenario: Error en X0
- **WHEN** usuario ingresa X0 = 10 y m = 10
- **THEN** sistema muestra "Error: X0 debe ser menor que m"

#### Scenario: Error en a
- **WHEN** usuario ingresa a = 10 y m = 10
- **THEN** sistema muestra "Error: a debe ser menor que m"

#### Scenario: Error en c para modo multiplicativo
- **WHEN** usuario selecciona modo multiplicativo y c = 5
- **THEN** sistema muestra "Error: en modo multiplicativo, c debe ser 0"

### Requirement: Explicar causa del error
El sistema SHALL explicar por qué el error ocurre para que el usuario pueda corregirlo.

#### Scenario: Explicación de error en m
- **WHEN** usuario ingresa m = -5
- **THEN** sistema muestra "Error: m debe ser mayor que 0. Justificación: el módulo debe ser positivo para que la operación módulo esté definida."

#### Scenario: Explicación de período máximo
- **WHEN** usuario ingresa X0 = 10 y m = 10
- **THEN** sistema muestra mensaje explicando que para período máximo, X0 y a deben ser menores que m