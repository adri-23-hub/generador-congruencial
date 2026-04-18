## Context

Aplicación web para el curso de Modelación y Simulación que implementa el Método Congruencial Lineal (LCG). El usuario ingresa parámetros (X0, a, m, c) y la aplicación:
1. Valida los parámetros
2. Detecta errores y explica por qué ocurren
3. Clasifica como binario/decimal según m
4. Genera la secuencia de números pseudoaleatorios
5. Detecta el período (primera repetición)
6. Exporta a PDF

## Goals / Non-Goals

**Goals:**
- Validar todos los parámetros antes de ejecutar
- Mostrar mensajes de error claros y explicativos
- Clasificar representación numérica (binario/decimal)
- Exportar a PDF con parámetros y secuencia completa
- Detectar período automáticamente

**Non-Goals:**
- Tests estadísticos de aleatoriedad
- Visualización gráfica
- Persistencia de datos

## Decisions

### Tech Stack

| Decisión | Alternativas | Justificación |
|----------|--------------|----------------|
| HTML/JS puro | React, Vue | Simplicidad, cero dependencias, archivo único |
| jsPDF | PDFKit, html2pdf | Mejor soporte para generar PDF desde cliente |

### Algoritmo LCG

| Decisión | Alternativas | Justificación |
|----------|--------------|----------------|
| Implementación iterativa | Recursiva | Evitar stack overflow en secuencias largas |
| Detección de período con Set | Comparación array | Búsqueda O(1) vs O(n) |

### Validación de Parámetros

| Decisión | Alternativas | Justificación |
|----------|--------------|----------------|
| Validar antes de calcular | Validar durante | Feedback inmediato al usuario |

**Reglas de validación:**
- m > 0 (obligatorio)
- X0, a < m (para período máximo)
- Si modo multiplicativo → c debe ser 0
- Si m = 2^k → Representación binaria
- Si m ≠ 2^k y es primo → Representación decimal óptima

### Arquitectura

```
┌─────────────────────────────────────┐
│         Interfaz HTML               │
├─────────────────────────────────────┤
│  Formulario de Parámetros          │
│  - Tipo: Mixto/Multiplicativo       │
│  - X0, a, m, c                      │
├─────────────────────────────────────┤
│  Módulo de Validación               │
│  - Verificar parámetros             │
│  - Clasificar binario/decimal      │
├─────────────────────────────────────┤
│  Motor LCG                         │
│  - Generar secuencia               │
│  - Detectar período                 │
├─────────────────────────────────────┤
│  Exportador PDF                    │
│  - jsPDF para generar documento   │
└─────────────────────────────────────┘
```

## Risks / Trade-offs

| Riesgo | Mitigación |
|--------|------------|
| Números muy grandes | Usar BigInt para operaciones |
| Período infinito | Limitar iteraciones máx. (10000) |
| Errores sin explicación | Mensajes claros por tipo de error |

## Open Questions

- ¿Cuál debe ser el límite máximo de iteraciones?
- ¿Necesita permitir configurar el límite?