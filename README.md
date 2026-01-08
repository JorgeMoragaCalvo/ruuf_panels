# calculate_panels()

Calcula el número máximo de paneles que caben en un techo, probando ambas orientaciones (normal y rotada 90 grados).

## Firma

```python
def calculate_panels(panel_width: int, panel_height: int,
                     roof_width: int, roof_height: int) -> int
```

## Parámetros

| Parametro      | Tipo  | Descripcion              |
|----------------|-------|--------------------------|
| `panel_width`  | `int` | Ancho del panel          |
| `panel_height` | `int` | Alto del panel           |
| `roof_width`   | `int` | Ancho del techo          |
| `roof_height`  | `int` | Alto del techo           |

## Valores de Retorno

| Valor  | Significado                        |
|--------|------------------------------------|
| `>= 0` | Numero maximo de paneles           |
| `-1`   | Dimensiones del panel invalidas    |
| `-2`   | Dimensiones del techo invalidas    |

## Algoritmo

### Paso 1: Validación de Entradas

```
Si panel_width <= 0 o panel_height <= 0 -> retorna -1
Si roof_width <= 0 o roof_height <= 0   -> retorna -2
```

### Paso 2: Cálculo de Orientaciones

La función calcula cuantos paneles caben en dos orientaciones:

**Orientación Horizontal (normal):**
```
horizontal_count = (roof_width // panel_width) * (roof_height // panel_height)
```

**Orientación Rotada (90 grados):**
```
rotated_count = (roof_width // panel_height) * (roof_height // panel_width)
```

### Paso 3: Selección del Maximo

```
return max(horizontal_count, rotated_count)
```

## Diagrama Visual

```
Techo: 10 x 8    Panel: 3 x 2

ORIENTACION HORIZONTAL          ORIENTACION ROTADA (90°)
(panel 3x2)                     (panel 2x3)

+----------+                    +----------+
|[3x2][3x2]|[3x2]|              |[2][2][2][2][2]|
|[3x2][3x2]|[3x2]|              |[x][x][x][x][x]|
|[3x2][3x2]|[3x2]|              |[3][3][3][3][3]|
|[3x2][3x2]|[3x2]|              |[2][2][2][2][2]|
+----------+                    |[x][x][x][x][x]|
                                |[3][3][3][3][3]|
Columnas: 10 // 3 = 3           +----------+
Filas:    8 // 2 = 4
Total:    3 * 4 = 12            Columnas: 10 // 2 = 5
                                Filas:    8 // 3 = 2
                                Total:    5 * 2 = 10

Resultado: max(12, 10) = 12 paneles
```

## Ejemplos de Uso

```python
# Caso normal
result = calculate_panels(3, 2, 10, 8)
# Retorna: 12

# Panel cuadrado
result = calculate_panels(2, 2, 10, 10)
# Retorna: 25

# Panel más grande que el techo
result = calculate_panels(5, 5, 4, 4)
# Retorna: 0

# Dimensiones de panel inválidas
result = calculate_panels(0, 2, 10, 8)
# Retorna: -1

# Dimensiones de techo inválidas
result = calculate_panels(3, 2, -5, 8)
# Retorna: -2
```

## Limitaciones

- Solo considera orientaciones de 0 y 90 grados
- No optimiza combinaciones mixtas de orientaciones
- Asume que todos los paneles deben tener la misma orientación