## Why

El Método Congruencial Lineal (LCG) es un algoritmo clásico para generar números pseudoaleatorios utilizado en simulación y computación. Se necesita una herramienta web que permita parametrizar, ejecutar y visualizar los resultados de los métodos congruenciales mixto y multiplicativo, con capacidad de exportar los resultados a PDF.

## What Changes

- Crear aplicación web para cálculo de generadores congruenciales
- Implementar algoritmo mixto: X(n+1) = (a·X(n) + c) mod m
- Implementar algoritmo multiplicativo: X(n+1) = (a·X(n)) mod m
- Interfaz para ingresar parámetros: X0 (semilla), a (multiplicador), m (módulo), c (constante aditiva)
- Validar parámetros antes de ejecutar
- Detectar errores: Mostrar explicación clara cuando los parámetros sean inválidos
- Clasificar representación: Determinar si es binario (m=2^k) o decimal (otros casos)
- Mostrar secuencia de números pseudoaleatorios generados
- Detectar punto de repetición (período)
- Exportar resultados a PDF con parámetros y secuencia completa

## Capabilities

### New Capabilities

- `generador-lcg`: Aplicación web que implementa generadores congruenciales lineales (mixto y multiplicativo) con interfaz de usuario y exportación PDF
- `validacion-parametros`: Validar parámetros X0, a, m, c antes de ejecutar
- `gestion-errores`: Explicar por qué los parámetros son inválidos con mensajes claros
- `analisis-representacion`: Clasificar como binario (m=2^k) o decimal
- `exportacion-pdf`: Generación de documento PDF con parámetros y resultados

## Impact

- Nueva aplicación web standalone
- Biblioteca para generación de números pseudoaleatorios
- Dependencias: framework web (cliente), biblioteca PDF