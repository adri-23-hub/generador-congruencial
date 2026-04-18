## ADDED Requirements

### Requirement: Clasificar m como potencia de 2
El sistema SHALL verificar si m es una potencia de 2 (representación binaria).

#### Scenario: m es potencia de 2
- **WHEN** usuario ingresa m = 8 (2³)
- **THEN** sistema clasifica como "Representación binaria (m = 2^k)"
- **AND** sistema muestra explicación "m = 8 = 2³ es potencia de 2, lo que permite representación binaria efisien"

#### Scenario: m no es potencia de 2
- **WHEN** usuario ingresa m = 10
- **THEN** sistema clasifica como "Representación decimal"
- **AND** sistema muestra explicación "m = 10 no es potencia de 2"

### Requirement: Detectar representación binaria
El sistema SHALL detectar cuando m = 2^k para clasificación binaria.

#### Scenario: Potencias de 2 comunes
- **WHEN** usuario ingresa m = 2, 4, 8, 16, 32, 64, 128, 256, 512, 1024
- **THEN** sistema clasifica como binaria

#### Scenario: Número primo
- **WHEN** usuario ingresa m = 7 (primo)
- **THEN** sistema clasifica como "Representación decimal óptima"
- **AND** sistema muestra que primos dan período máximo con constantes apropiadas

### Requirement: Mostrar警告 cuando período no será máximo
El sistema SHALL mostrar警告 cuando los parámetros no producirán período máximo.

#### Scenario: m no es primo ni potencia de 2
- **WHEN** usuario ingresa m = 6
- **THEN** sistema muestra "Advertencia: m no es primo ni potencia de 2. El período no será máximo."

#### Scenario: X0 o a no son menores que m
- **WHEN** usuario ingresa X0 = 10, a = 3, m = 10
- **THEN** sistema muestra "Advertencia: X0 y a deben ser menores que m para período máximo."