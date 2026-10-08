# Casos de Prueba — Olimpiadas de Informática Chuquisaca

> **Guía de uso para HackerRank:** Por cada problema existe una carpeta en `casos_de_prueba/`. Dentro de cada carpeta se encuentran 10 pares de archivos `inputXX.txt` / `outputXX.txt` listos para subir. Los casos `00` y `01` son los **visibles** (los mismos que aparecen en el enunciado); el resto son **ocultos**.

---

## Categoría A

---

### A1 — El Misterio de la Campana de la Libertad

**Lógica:** Sumar divisores propios de N (1 ≤ d < N, donde N % d == 0) y comparar con N.

| # | Tipo | `input.txt` | `output.txt` | Justificación |
|---|------|-------------|--------------|---------------|
| 00 | Ejemplo visible | `6` | `PERFECTO` | Divisores: {1,2,3} → suma = 6 = N |
| 01 | Ejemplo visible | `12` | `ABUNDANTE` | Divisores: {1,2,3,4,6} → suma = 16 > 12 |
| 02 | Ejemplo visible | `15` | `DEFICIENTE` | Divisores: {1,3,5} → suma = 9 < 15 |
| 03 | Borde mínimo | `2` | `DEFICIENTE` | Solo divisor propio: {1} → suma = 1 < 2 |
| 04 | Perfecto conocido | `28` | `PERFECTO` | 1+2+4+7+14 = 28 = N |
| 05 | Perfecto grande | `496` | `PERFECTO` | 3er número perfecto |
| 06 | Perfecto grande | `8128` | `PERFECTO` | 4to número perfecto |
| 07 | Abundante medio | `945` | `ABUNDANTE` | Primer abundante impar |
| 08 | Abundante grande | `720` | `ABUNDANTE` | Muy factorizable; suma divisores >> 720 |
| 09 | Estrés máximo | `999999999989` | `DEFICIENTE` | Número primo grande → suma div = 1 |

---

### A2 — El Núcleo de Energía

**Lógica:** Hallar el mayor factor primo de N.

| # | Tipo | `input.txt` | `output.txt` | Justificación |
|---|------|-------------|--------------|---------------|
| 00 | Ejemplo visible | `84` | `7` | 84 = 2²×3×7 → mayor primo = 7 |
| 01 | Ejemplo visible | `17` | `17` | 17 es primo → mayor primo = sí mismo |
| 02 | Potencia de 5 | `100` | `5` | 100 = 2²×5² → mayor primo = 5 |
| 03 | Borde mínimo | `2` | `2` | 2 es primo |
| 04 | Primo simple | `13` | `13` | 13 es primo |
| 05 | Múltiple factores | `60` | `5` | 60 = 2²×3×5 → mayor primo = 5 |
| 06 | Primo grande | `999983` | `999983` | Primo en rango moderado |
| 07 | Múltiplos pequeños | `1000000000000` | `5` | 10¹² = 2¹²×5¹² → mayor primo = 5 |
| 08 | Primo de Mersenne | `2147483647` | `2147483647` | Primo (2³¹ − 1) |
| 09 | Caso clásico ICPC | `600851475143` | `6857` | Mayor factor primo = 6857 |

---

### A3 — Los Dígitos Capicúa

**Lógica:** Contar palíndromos en el rango [A, B]. Entrada: dos enteros en la misma línea separados por espacio.

| # | Tipo | `input.txt` | `output.txt` | Justificación |
|---|------|-------------|--------------|---------------|
| 00 | Ejemplo visible | `1 9` | `4` | Palíndromos primos de 1 dígito: 2,3,5,7 |
| 01 | Ejemplo visible | `10 30` | `2` | Palíndromos: 11 y ningún otro primo palíndromo de 2 dígitos en ese rango |
| 02 | Rango pequeño | `100 115` | `1` | Solo 101 es palíndromo primo |
| 03 | Sin resultado | `1 1` | `0` | 1 no es primo |
| 04 | Rango amplio 1 | `1 100` | `18` | Todos los palíndromos en [1,100] |
| 05 | Rango 4 dígitos | `1000 9999` | `45` | Palíndromos de 4 dígitos en el rango |
| 06 | Rango [1,1000] | `1 1000` | `108` | Total de palíndromos en [1,1000] |
| 07 | Rango [500,600] | `500 600` | `4` | Palíndromos: 505,515,525,535,545,555,565,575,585,595 — contar los 10 |
| 08 | Sin palíndromos | `99999 100000` | `0` | Ningún número en ese rango es palíndromo |
| 09 | Estrés | `1 1000000` | `1998` | Total palíndromos en [1, 10⁶] |

---

### A4 — Los Faroles de la Plaza

**Lógica:** Suma de todos los enteros positivos menores a N que sean múltiplos de 3 o de 5.

| # | Tipo | `input.txt` | `output.txt` | Justificación |
|---|------|-------------|--------------|---------------|
| 00 | Ejemplo visible | `10` | `23` | Múltiplos de 3 o 5 menores a 10: {3,5,6,9} → 3+5+6+9 = 23 |
| 01 | Ejemplo visible | `15` | `60` | Múltiplos de 3 o 5 menores a 15: suma = 60 |
| 02 | Caso medio | `100` | `2418` | Suma en [1,99] |
| 03 | Borde mínimo | `1` | `0` | Sin múltiplos positivos menores a 1 |
| 04 | Borde mínimo+1 | `4` | `3` | Solo el 3 es múltiplo de 3 o 5 menor a 4 |
| 05 | Borde N=6 | `6` | `8` | Múltiplos menores a 6: {3,5} → 3+5 = 8 |
| 06 | Caso grande | `1000` | `234168` | Suma usando fórmula de inclusión-exclusión |
| 07 | Caso grande-1 | `999` | `233168` | Un valor menos que el anterior |
| 08 | Estrés máximo | `1000000000` | `233333333166666668` | Requiere `long long` |
| 09 | Estrés doble | `2000000000` | `933333333666666668` | Límite superior del rango |

---

### A5 — Los Ríos Gemelos

**Lógica:** Contar números en [A, B] que sean palíndromos **y** primos simultáneamente.

| # | Tipo | `input.txt` | `output.txt` | Justificación |
|---|------|-------------|--------------|---------------|
| 00 | Ejemplo visible | `1 10` | `4` | Primos palíndromos: 2,3,5,7 |
| 01 | Ejemplo visible | `10 100` | `1` | Solo 11 es primo palíndromo en ese rango |
| 02 | Sin resultado | `24 28` | `0` | Ningún primo palíndromo en ese rango |
| 03 | Borde bajo | `1 5` | `3` | Primos palíndromos: 2, 3, 5 |
| 04 | Borde mínimo | `4 6` | `0` | Solo 5 es primo en [4,6] y sí es palíndromo → 1 |
| 05 | Rango [1,100] | `1 100` | `5` | Primos palíndromos: 2,3,5,7,11 |
| 06 | Rango [100,200] | `100 200` | `5` | Primos palíndromos: 101,131,151,181,191 |
| 07 | Rango [1,1000] | `1 1000` | `20` | Todos los primos palíndromos hasta 1000 |
| 08 | Estrés | `1 10000000` | `1224` | Contar todos en el rango |
| 09 | Sin resultado | `9999990 10000000` | `0` | No hay primos palíndromos en ese rango |

---

## Categoría B

---

### B1 — El Carácter Solitario

**Lógica:** Encontrar el primer carácter que aparece exactamente una vez. Entrada: N (longitud) en primera línea, cadena en segunda línea.

| # | Tipo | `input.txt` | `output.txt` | Justificación |
|---|------|-------------|--------------|---------------|
| 00 | Ejemplo visible | `8` / `sucresuc` | `r` | 'e' y 'r' aparecen 1 vez; 'r' tiene posición anterior |
| 01 | Ejemplo visible | `6` / `bonobo` | `n` | 'n' aparece 1 sola vez (posición 2) |
| 02 | Sin solitario | `6` / `cancan` | `-1` | Todos los caracteres se repiten |
| 03 | Longitud 1 | `1` / `a` | `a` | Único carácter → es solitario |
| 04 | Dos distintos | `2` / `ab` | `a` | Ambos únicos; 'a' es el primero |
| 05 | Todos repetidos | `4` / `aabb` | `-1` | 'a'×2, 'b'×2 → sin solitario |
| 06 | Solitario central | `7` / `abcbdbd` | `a` | 'a'×1 primero; verificar secuencia |
| 07 | Solitario al final | `6` / `aabbcz` | `c` | 'a'×2,'b'×2,'c'×1,'z'×1 → 'c' primero |
| 08 | Alfabeto completo | `26` / `abcdefghijklmnopqrstuvwxyz` | `a` | Todos únicos → primero = 'a' |
| 09 | Repetición parcial | `10` / `cochabamba` | `h` | c×2,o×2,h×1,a×3,b×2,m×1 → 'h' primero |

---

### B2 — El Stand de la FEXPO

**Lógica:** Encontrar el elemento que aparece un número impar de veces (operación XOR sobre todos los elementos). Entrada: N en primera línea, N números en segunda línea.

| # | Tipo | `input.txt` | `output.txt` | Justificación |
|---|------|-------------|--------------|---------------|
| 00 | Ejemplo visible | `7` / `12 5 12 8 5 12 8` | `12` | 12 aparece 3 veces (impar); 5 y 8 aparecen 2 (par) |
| 01 | Ejemplo visible | `5` / `7 3 7 3 9` | `9` | 9 aparece 1 sola vez |
| 02 | Un elemento | `1` / `99` | `99` | Único elemento → frecuencia impar |
| 03 | Todos iguales | `5` / `1 1 1 1 1` | `1` | Aparece 5 veces (impar) |
| 04 | Clásico XOR | `5` / `4 1 2 1 2` | `4` | 4 aparece 1 vez; 1 y 2 dos veces cada uno |
| 05 | Solitario al inicio | `7` / `9 3 3 5 5 7 7` | `9` | 9 aparece 1 vez al inicio |
| 06 | Solitario al final | `7` / `3 3 5 5 7 7 9` | `9` | 9 aparece 1 vez al final |
| 07 | Valores grandes | `5` / `999999999 1 999999999 1 999999999` | `999999999` | Aparece 3 veces (impar) |
| 08 | Triple igual | `3` / `7 7 7` | `7` | 7 aparece 3 veces (impar) |
| 09 | Cinco ocurrencias | `9` / `2 3 2 3 2 3 2 3 2` | `2` | 2 aparece 5 veces; 3 aparece 4 veces |

---

### B3 — Las Notas Secretas

**Lógica:** Determinar si dos palabras son anagramas. Entrada: dos cadenas en líneas separadas.

| # | Tipo | `input.txt` | `output.txt` | Justificación |
|---|------|-------------|--------------|---------------|
| 00 | Ejemplo visible | `bolivia` / `alivibo` | `SI` | Mismas letras reordenadas |
| 01 | Diferente longitud | `chuquisaca` / `sucre` | `NO` | Distinto número de caracteres |
| 02 | Longitud extra | `perro` / `perros` | `NO` | 'perros' tiene una 's' extra |
| 03 | Idénticas | `a` / `a` | `SI` | Misma palabra = anagrama trivial |
| 04 | Dos letras | `ab` / `ba` | `SI` | Intercambio simple |
| 05 | Anagrama clásico | `roma` / `amor` | `SI` | Par conocido |
| 06 | Anagrama inglés | `listen` / `silent` | `SI` | Par famoso |
| 07 | No anagrama | `hello` / `world` | `NO` | Letras completamente distintas |
| 08 | Inversa | `abc` / `cba` | `SI` | Reversión = anagrama |
| 09 | Cadena larga | `abcdefghij` / `jihgfedcba` | `SI` | Reversa de 10 letras |

---

### B4 — La Compra Exacta

**Lógica:** Determinar si existe algún par de precios que sume exactamente T. Entrada: `N T` en primera línea, N números en segunda línea.

| # | Tipo | `input.txt` | `output.txt` | Justificación |
|---|------|-------------|--------------|---------------|
| 00 | Ejemplo visible | `5 22` / `12 3 20 7 15` | `SI` | 7 + 15 = 22 ✓ |
| 01 | Ejemplo visible | `4 10` / `3 3 8 2` | `SI` | 8 + 2 = 10 ✓ |
| 02 | Sin par | `3 10` / `5 2 4` | `NO` | Ninguna combinación suma 10 |
| 03 | Par exacto | `2 3` / `1 2` | `SI` | 1 + 2 = 3 ✓ |
| 04 | Valores límite | `2 2000000000` / `1000000000 1000000000` | `SI` | Par exacto en el límite del rango |
| 05 | Mínima suma | `5 1` / `1 1 1 1 1` | `NO` | Mínima suma posible = 1+1 = 2 > 1 |
| 06 | Múltiples pares | `6 100` / `10 90 20 80 50 50` | `SI` | 10+90=100 ✓ y 20+80=100 ✓ |
| 07 | Todos iguales sin suma | `4 7` / `3 3 3 3` | `NO` | 3+3=6 ≠ 7 |
| 08 | Par no consecutivo | `5 13` / `1 5 7 6 8` | `SI` | 5+8=13 ✓ |
| 09 | Estrés con valores grandes | `6 999999999` / `1 499999999 500000000 2 999999997 3` | `SI` | 499999999+500000000 = 999999999 ✓ |

---

### B5 — Las Luces de la Plaza

**Lógica:** Contar las luces apagadas (valor 0) en un arreglo. Entrada: N en primera línea, N valores (0 o 1) en segunda línea.

| # | Tipo | `input.txt` | `output.txt` | Justificación |
|---|------|-------------|--------------|---------------|
| 00 | Ejemplo visible | `3` / `0 1 0` | `2` | Dos ceros en posiciones 0 y 2 |
| 01 | Ejemplo visible | `4` / `1 0 0 1` | `2` | Dos apagadas en posiciones 1 y 2 |
| 02 | Todas encendidas | `5` / `1 1 1 1 1` | `0` | Sin apagadas |
| 03 | Una apagada | `1` / `0` | `1` | Única luz apagada |
| 04 | Una encendida | `1` / `1` | `0` | Única luz encendida |
| 05 | Bloque central | `6` / `0 0 1 1 0 0` | `4` | Cuatro apagadas |
| 06 | Alternadas | `8` / `1 0 1 0 1 0 1 0` | `4` | Cuatro apagadas alternas |
| 07 | Todas apagadas | `10` / `0 0 0 0 0 0 0 0 0 0` | `10` | Todas apagadas |
| 08 | Patrón mixto | `7` / `1 1 0 1 1 0 1` | `2` | Dos apagadas internas |
| 09 | Estrés (N=100 000) | `100000` / `0 0 … 0 1` | `1` | 99 999 ceros + 1 encendida final |

---

## Notas de Configuración para HackerRank

### Pasos para subir los casos

1. Ingresar a **HackerRank for Work** → *Create Challenge*.
2. En la sección **Test Cases**, seleccionar **Upload Files** y cargar los pares `inputXX.txt` / `outputXX.txt`.
3. Marcar los casos `00` y `01` como **Sample** (visibles para el participante durante el concurso).
4. Los casos `02`–`09` se dejan como **Hidden** (solo el juez los evalúa).
5. Ajustar los límites de tiempo y memoria según la tabla siguiente.

### Parámetros recomendados por problema

| Problema | Time Limit | Memory Limit | Tipo de dato clave |
|----------|-----------|--------------|-------------------|
| A1 — Campana Libertad | 1.0 s | 64 MB | `long long` |
| A2 — Núcleo Energía | 1.0 s | 64 MB | `long long` |
| A3 — Dígitos Capicúa | 2.0 s | 64 MB | `int` |
| A4 — Faroles Plaza | 1.0 s | 64 MB | `long long` |
| A5 — Ríos Gemelos | 2.0 s | 64 MB | `long long` |
| B1 — Carácter Solitario | 1.0 s | 64 MB | `string` |
| B2 — Stand FEXPO | 1.0 s | 64 MB | `int` |
| B3 — Notas Secretas | 1.0 s | 64 MB | `string` |
| B4 — Compra Exacta | 1.0 s | 64 MB | `long long` |
| B5 — Luces Plaza | 1.0 s | 64 MB | `int` |

---

*Documento generado como material de apoyo para la configuración de la Olimpiada de Informática — Chuquisaca.*
