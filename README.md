# Laboratorio #2 · Limpieza y transformación de datos

**SINF-633 Análisis Exploratorio de Datos · Universidad Cenfotec**  
**Grupo 3 · Carnet P000021441**

## Caso
El Gerente Comercial de **Comercial del Pacífico S.A.** reporta que los datos "se ven sucios" y que los totales de los reportes no cuadran. Este repositorio contiene el proceso completo de limpieza, imputación, escalado y enriquecimiento de dos archivos fuente:
- `ventas_productos.csv` (1 530 × 7)
- `empleados_rrhh.csv` (600 × 10)

## Proceso aplicado (orden estricto)
| # | Etapa | Decisión principal |
|---|-------|--------------------|
| 1 | Diagnóstico | Tabla resumen, mapa de calor de nulos, valores imposibles |
| 2 | Limpieza de texto | `strip` + `title` + quitar tildes (unifica "María"/"Maria") |
| 3 | Anomalías | Precios < 0 y cantidades ≤ 0 → `NaN` (no se borra la fila) |
| 4 | Duplicados | Absolutos eliminados antes de imputar (conserva el 1.º) |
| 5 | Imputación | Numéricas → mediana; salario → **mediana por cargo**; categóricas → sentinela |
| 6 | Escalado | Robust o Standard según skew / % outliers por columna |
| 7 | Variables nuevas | `total_venta`, `segmento_venta`, `riesgo_fuga`, dummies, etc. |
| 8 | Pipeline | `limpiar_dataset()` **idempotente** que reproduce todo el proceso |
| 9 | Verificación | 8 checks sobre los archivos **exportados** desde disco |

## Resultado
| Métrica | Ventas | Empleados |
|---------|--------|-----------|
| Filas | 1 530 → **1 500** | 600 → 600 |
| Columnas | 7 → **20** | 10 → **33** |
| Nulos | 179 → **0** | 80 → **0** |
| Duplicados | 30 → **0** | 0 → 0 |
| Verificaciones | 8/8 | ✅ |

## Cómo reproducir
```bash
# 1) Clonar y entrar
git clone <URL_DE_TU_REPO>
cd cenfotec-Comercial-del-Pac-fico-S.A.

# 2) Instalar dependencias
pip install pandas numpy scikit-learn matplotlib seaborn jupyter

# 3) Abrir el notebook
jupyter notebook
