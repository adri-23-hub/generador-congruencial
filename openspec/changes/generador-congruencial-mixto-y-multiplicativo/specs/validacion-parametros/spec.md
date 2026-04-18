## ADDED Requirements

### Requirement: Validar que m sea mayor que cero
El sistema SHALL verificar que el parámetro m (módulo) sea mayor que cero antes de ejecutar el algoritmo.

#### Scenario: m positivo válido
- **WHEN** usuario ingresa m = 10
- **THEN** sistema permite continuar la ejecución

#### Scenario: m negativoinválido
- **WHEN** usuario ingresa m = -5
- **THEN** sistema muestra error "Error: m debe ser mayor que 0"

#### Scenario: m cero inválido
- **WHEN** usuario ingresa m = 0
- **THEN** sistema muestra error "Error: m debe ser mayor que 0"

### Requirement: Validar que X0 sea menor que m
El sistema SHALL verificar que la semilla X0 sea menor que m.

#### Scenario: X0 válido
- **WHEN** usuario ingresa X0 = 5 y m = 10
- **THEN** sistema permite continuar la ejecución

#### Scenario: X0 mayor o igual a m inválido
- **WHEN** usuario ingresa X0 = 10 y m = 10
- **THEN** sistema muestra error "Error: X0 debe ser menor que m"

### Requirement: Validar que a sea menor que m
El sistema SHALL verificar que el multiplicador a sea menor que m.

#### Scenario: a válido
- **WHEN** usuario ingresa a = 3 y m = 10
- **THEN** sistema permite continuar la ejecución

#### Scenario: a mayor o igual a m inválido
- **WHEN** usuario ingresa a = 10 y m = 10
- **THEN** sistema muestra error "Error: a debe ser menor que m"

### Requirement: Validar modo multiplicativo
El sistema SHALL verificar que c sea 0 cuando se selecciona modo multiplicativo.

#### Scenario: Modo mixto con c distinto de cero
- **WHEN** usuario selecciona modo mixto y ingresa c = 3
- **THEN** sistema permite continuar la ejecución

#### Scenario: Modo multiplicativo con c distinto de cero
- **WHEN** usuario selecciona modo multiplicativo y ingresa c = 3
- **THEN** sistema muestra error "Error: en modo multiplicativo, c debe ser 0"