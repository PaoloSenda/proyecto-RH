# proyecto-RH (HR Dashboard)

## Objetivo
Dashboard ejecutivo de capital humano/nomina en un solo archivo HTML. Permite cargar CSV o Excel, filtrar, y visualizar KPIs, graficas y tabla de colaboradores.

## Archivos clave
- RH_Dashboard_Capital_Humano.html: contiene HTML, estilos y JS (toda la app).
- AGENTS.md: este contexto para asistentes.

## Uso rapido
1. Abrir `RH_Dashboard_Capital_Humano.html` en el navegador.
2. Cargar un archivo `.csv`, `.xlsx` o `.xls` con datos de nomina.
3. Usar filtros (division, centro de costo, puesto, empresa especialista, antiguedad, salario).

## Librerias externas (CDN)
- Tailwind CSS
- Chart.js
- SheetJS (xlsx)
- Lucide icons

## Mapeo de columnas
El JS incluye `COLUMN_MAP` con aliases en mayusculas. Se soportan variaciones comunes (ej. `PUESTO`, `JOB`).
Para Excel hay overrides por letra:
- job -> CX
- seniority -> CY
- specialistCompany -> DB
Si cambia el layout del Excel, ajustar esos overrides o el `COLUMN_MAP`.

## Logica de datos
- `headcount` usa IDs unicos.
- `gross` usa `totalPerception` si existe; si no, suma percepciones (`PERCEPTION_SUM_KEYS`).
- `deductions` usa `totalDeduction` si existe; si no, suma deducciones (`DEDUCTION_SUM_KEYS`).
- `net` usa `totalNet` si existe; si no, `gross - deductions`.
- Los conteos por division/CC/puesto/empresa son por empleado unico; los montos se suman por fila.
- La tabla muestra maximo `CONFIG.MAX_TABLE_ROWS`.

## Configuracion relevante
En `CONFIG`:
- `MAX_TABLE_ROWS`, `MAX_CHART_ITEMS`, `DEBOUNCE_DELAY`, `DATE_LOCALE`, `TOAST_DURATION`, `DEBUG`.

## Consideraciones para cambios
- Mantener todo en el mismo HTML (no build step).
- Si cambias keys/labels de percepciones o deducciones, actualizar:
  - `PERCEPTION_KEYS` / `DEDUCTION_KEYS`
  - `PERCEPTION_LABELS` / `DEDUCTION_LABELS`
  - `PERCEPTION_SUM_KEYS` / `DEDUCTION_SUM_KEYS`
- Para nuevos campos del archivo, agregar en `COLUMN_MAP`.
