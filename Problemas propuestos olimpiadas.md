# Propuesta de Problemas para Olimpiadas de Informática

## Categoría A (3º y 4º de Secundaria)

---

### Problema 1: El Misterio de la Campana de la Libertad

* **Área temática:** Aritmética, Divisibilidad y Control de Flujo.
* **Límite de tiempo:** 1.0 segundo
* **Límite de memoria:** 64 MB

#### Enunciado

En la Basílica de San Francisco de la ciudad de Sucre se custodia la legendaria Campana de la Libertad. Un estudio histórico clasifica a los números enteros positivos $N$ según la suma de sus **divisores propios** (todos los divisores positivos del número $N$, excluyendo al propio $N$):

* **PERFECTO:** Si la suma de sus divisores propios es exactamente igual a $N$.
* **ABUNDANTE:** Si la suma de sus divisores propios es estrictamente mayor que $N$.
* **DEFICIENTE:** Si la suma de sus divisores propios es estrictamente menor que $N$.

Se requiere escribir un programa en C++ que reciba un número entero $N$ y determine su categoría correspondiente.

#### Ilustración de Referencia

```text
         / \
        /   \
       /_____\
       |  _  |
       | | | |      [Campana de la Libertad]
      /  |_|  \
     /    o    \
    (___________)

  Ejemplo con N = 12:
  Divisores propios: {1, 2, 3, 4, 6}
  Suma acumulada:    1 + 2 + 3 + 4 + 6 = 16
  Evaluación:        16 > 12  -->  ABUNDANTE
```

#### Entrada

Una única línea con un número entero $N$ ($2 \le N \le 10^{12}$).

*(Nota: El valor de $N$ excede el rango de un entero de 32 bits, por lo que requiere el uso de tipos de datos de 64 bits).*

#### Salida

Imprimir una sola palabra en mayúsculas: `PERFECTO`, `ABUNDANTE` o `DEFICIENTE`.

#### Ejemplos de Entrada y Salida

| Entrada | Salida | Explicación |
| --- | --- | --- |
| `6` | `PERFECTO` | Divisores propios de 6: $1, 2, 3$. Suma = $1 + 2 + 3 = 6$. Como la suma es igual a $N$, es perfecto. |
| `12` | `ABUNDANTE` | Divisores propios de 12: $1, 2, 3, 4, 6$. Suma = $1 + 2 + 3 + 4 + 6 = 16$. Como $16 > 12$, es abundante. |
| `15` | `DEFICIENTE` | Divisores propios de 15: $1, 3, 5$. Suma = $1 + 3 + 5 = 9$. Como $9 < 15$, es deficiente. |

---

#### Solución Subóptima (Fuerza Bruta)

Este enfoque evalúa literalmente la definición de divisor iterando desde $1$ hasta $N - 1$ mediante un bucle lineal.

```cpp
#include <iostream>

using namespace std;

int main() {
    long long n;
    cin >> n;

    long long suma = 0;

    // Recorre todos los números desde 1 hasta n - 1
    for (long long i = 1; i < n; i++) {
        if (n % i == 0) {
            suma += i;
        }
    }

    if (suma == n) {
        cout << "PERFECTO" << endl;
    } else if (suma > n) {
        cout << "ABUNDANTE" << endl;
    } else {
        cout << "DEFICIENTE" << endl;
    }

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(N)$. Para un límite de $N = 10^{12}$, el bucle requiere $10^{12}$ iteraciones.
* **Resultado:** Excede el tiempo límite de ejecución (*Time Limit Exceeded - TLE*).

---

#### Solución Óptima

Aprovechando la propiedad matemática de que los divisores ocurren en pares (si $d$ divide a $N$, entonces $\frac{N}{d}$ también es divisor de $N$), es suficiente evaluar los divisores únicamente hasta $\sqrt{N}$.

```cpp
#include <iostream>

using namespace std;

int main() {
    long long n;
    cin >> n;

    // El 1 siempre es divisor propio de cualquier n > 1
    long long suma = 1;

    // Se evalúan divisores solo hasta la raíz cuadrada de n
    for (long long i = 2; i * i <= n; i++) {
        if (n % i == 0) {
            suma += i;
            
            // Si no es un cuadrado perfecto, se agrega la pareja de divisores
            if (i * i != n) {
                suma += (n / i);
            }
        }
    }

    if (suma == n) {
        cout << "PERFECTO" << endl;
    } else if (suma > n) {
        cout << "ABUNDANTE" << endl;
    } else {
        cout << "DEFICIENTE" << endl;
    }

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(\sqrt{N})$. Para $N = 10^{12}$, $\sqrt{N} = 10^6$ iteraciones, completando la ejecución en menos de $0.01$ segundos.
* **Manejo de Cuadrados Perfectos:** La condición `i * i != n` evita duplicar la raíz cuadrada cuando el número es un cuadrado exacto.
* **Tipos de Datos:** Se emplea `long long` para prevenir desbordamiento de entero (*integer overflow*).

---

### Problema 2: El Núcleo de Energía Ancestral

* **Área temática:** Factorización de Enteros y Números Primos.
* **Límite de tiempo:** 1.0 segundo
* **Límite de memoria:** 64 MB

#### Enunciado

Un sistema de control requiere analizar un código numérico entero $N$ para determinar su "frecuencia pura dominante", la cual equivale al **mayor factor primo** que compone al número $N$.

Se requiere escribir un programa en C++ que calcule e imprima dicho mayor factor primo de $N$.

#### Ilustración de Referencia

```text
         .---.
        /     \     [REACTOR ANCESTRAL]
       |  (N)  |    Objetivo: Extraer el mayor factor primo
        \     /
         '---'
        /  |  \

  Ejemplo con N = 84:
  Descomposición: 84 = 2 * 2 * 3 * 7
  Factores primos: {2, 3, 7}
  Frecuencia dominante (mayor primo): 7
```

#### Entrada

Una única línea con un número entero $N$ ($2 \le N \le 10^{12}$).

#### Salida

Imprimir un único número entero: el mayor factor primo del número $N$.

#### Ejemplos de Entrada y Salida

| Entrada | Salida | Explicación |
| --- | --- | --- |
| `84` | `7` | Los factores primos de 84 son 2, 3 y 7. El mayor de ellos es 7. |
| `17` | `17` | Al ser 17 un número primo, su único y mayor factor primo es él mismo. |
| `100` | `5` | Descomposición: $100 = 2^2 \times 5^2$. Los factores primos son 2 y 5. El mayor es 5. |

---

#### Solución Subóptima (Fuerza Bruta)

Este enfoque identifica divisores probando todos los números hasta $N$ y verifica la primalidad de cada divisor encontrado mediante una función auxiliar.

```cpp
#include <iostream>

using namespace std;

// Función auxiliar para verificar primalidad
bool esPrimo(long long x) {
    if (x < 2) return false;
    for (long long i = 2; i * i <= x; i++) {
        if (x % i == 0) {
            return false;
        }
    }
    return true;
}

int main() {
    long long n;
    cin >> n;

    long long mayorPrimo = 1;

    // Prueba todos los divisores desde 2 hasta n
    for (long long i = 2; i <= n; i++) {
        if (n % i == 0 && esPrimo(i)) {
            mayorPrimo = i;
        }
    }

    cout << mayorPrimo << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(N \sqrt{N})$ en el peor caso. El bucle exterior itera hasta $N = 10^{12}$.
* **Resultado:** Excede el tiempo límite de ejecución (*TLE*).

---

#### Solución Óptima

Esta técnica descompone el número dividiéndolo sucesivamente por sus factores primos más pequeños, lo que reduce el valor de $N$ de forma acelerada en cada iteración.

```cpp
#include <iostream>

using namespace std;

int main() {
    long long n;
    cin >> n;

    long long mayorPrimo = 1;

    // Probar posibles factores primos hasta la raíz de n
    for (long long d = 2; d * d <= n; d++) {
        if (n % d == 0) {
            mayorPrimo = d;

            // Extraer por completo el factor d del número n
            while (n % d == 0) {
                n = n / d;
            }
        }
    }

    // Si al finalizar el bucle n > 1, el residuo final es un factor primo
    if (n > 1) {
        mayorPrimo = n;
    }

    cout << mayorPrimo << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(\sqrt{N})$ en el peor de los casos, y sensiblemente menor en promedio debido a la reducción continua de $N$ en la estructura `while`.
* **Garantía Algorítmica:** Al extraer de forma exhaustiva los factores en orden ascendente empezando desde 2, cualquier divisor posterior que divida a $N$ será necesariamente un número primo.
* **Residuo Final:** La condición `if (n > 1)` captura factores primos superiores a $\sqrt{N}$ en tiempo $O(1)$.

---

### Problema 3: El Enigma de los Dígitos Capicúa

* **Área temática:** Descomposición Aritmética, Números Palíndromos y Paridad.
* **Límite de tiempo:** 1.0 segundo
* **Límite de memoria:** 64 MB

#### Enunciado

En el Archivo y Biblioteca Nacionales de Bolivia se realiza la clasificación de manuscritos históricos. Se define un número de página como "secreto" si cumple dos propiedades simultáneas:

1. Es un **número capicúa** (se lee idénticamente de izquierda a derecha y de derecha a izquierda, como $7$, $44$, $121$ o $3553$).
2. La **suma de todos sus dígitos es un número par** (por ejemplo, en $121$ la suma es $1 + 2 + 1 = 4$, que es par; mientras que en $111$ la suma es $1 + 1 + 1 = 3$, que es impar).

Dado un intervalo cerrado $[A, B]$, se requiere determinar la cantidad total de páginas secretas contenidas dentro del rango.

#### Ilustración de Referencia

```text
    Número analizado:           [ 4 ] [ 7 ] [ 7 ] [ 4 ]
                                  ^               ^
                                  |__ ¿Coinciden?_|

    1. Inversión aritmética:     [ 4 ] [ 7 ] [ 7 ] [ 4 ]  --> 4774 == 4774 (¡Es Capicúa!)
    2. Suma de dígitos:          4 + 7 + 7 + 4 = 22       --> 22 % 2 == 0  (¡Es Par!)
    
    Veredicto: Cumple ambas condiciones.
```

#### Entrada

Una única línea con dos números enteros $A$ y $B$ ($1 \le A \le B \le 10^6$) separados por un espacio.

#### Salida

Imprimir un único número entero: la cantidad total de números dentro del rango $[A, B]$ que son capicúa y poseen una suma de dígitos par.

#### Ejemplos de Entrada y Salida

| Entrada | Salida | Explicación |
| --- | --- | --- |
| `1 9` | `4` | Capicúas de un solo dígito con suma par: $2, 4, 6, 8$. Total = 4. |
| `10 30` | `2` | Entre 10 y 30: $11$ ($1+1=2$, par) y $22$ ($2+2=4$, par). Total = 2. |
| `100 115` | `1` | Entre 100 y 115: $101$ ($1+0+1=2$, par) y $111$ ($1+1+1=3$, impar). Cumple solo $101$. Total = 1. |

---

#### Solución Subóptima (Basada en Cadenas de Texto)

Este enfoque convierte cada entero a un objeto `std::string` para invertir su contenido y sumar sus caracteres.

```cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
    int A, B;
    cin >> A >> B;

    int totalValidos = 0;

    for (int i = A; i <= B; i++) {
        string s = to_string(i);

        // Inversión manual de la cadena
        string invertida = "";
        for (int j = s.length() - 1; j >= 0; j--) {
            invertida += s[j];
        }

        // Verificación de número capicúa
        if (s == invertida) {
            int suma = 0;
            for (size_t j = 0; j < s.length(); j++) {
                suma += (s[j] - '0');
            }

            if (suma % 2 == 0) {
                totalValidos++;
            }
        }
    }

    cout << totalValidos << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O((B - A + 1) \cdot L)$, donde $L$ es la cantidad de dígitos. La función `to_string` y las asignaciones sucesivas de memoria en `invertida += s[j]` generan sobrecarga considerable.
* **Límite Práctico:** Con $10^6$ elementos, la asignación dinámica recurrente puede resultar en tiempos cercanos al límite permitido ($1.0\text{ s}$).

---

#### Solución Óptima (Descomposición Aritmética)

Esta solución aplica operaciones aritméticas directas (`% 10` y `/ 10`) dentro de una función modular de una sola pasada.

```cpp
#include <iostream>

using namespace std;

// Evalúa la propiedad capicúa y la paridad de la suma de dígitos en una sola pasada
bool esCapicuaPar(int n) {
    int original = n;
    int invertido = 0;
    int sumaDigitos = 0;

    while (n > 0) {
        int digito = n % 10;
        
        sumaDigitos += digito;
        invertido = (invertido * 10) + digito;
        
        n /= 10;
    }

    return (original == invertido) && (sumaDigitos % 2 == 0);
}

int main() {
    int A, B;
    cin >> A >> B;

    int contador = 0;

    for (int i = A; i <= B; i++) {
        if (esCapicuaPar(i)) {
            contador++;
        }
    }

    cout << contador << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O((B - A + 1) \cdot L)$. Sin reserva de memoria en la memoria dinámica (*heap*), el cálculo requiere menos de $0.05$ segundos para el rango máximo $10^6$.
* **Complejidad Espacial:** $O(1)$ adicional.

---

### Problema 4: Los Faroles de la Plaza 25 de Mayo

* **Área temática:** Series Matemáticas, Múltiplos y Principio de Inclusión-Exclusión.
* **Límite de tiempo:** 1.0 segundo
* **Límite de memoria:** 64 MB

#### Enunciado

Para las fiestas patrias, la Plaza 25 de Mayo de Sucre es decorada con una fila de $N$ faroles numerados secuencialmente del $1$ al $N$. Los organizadores deciden encender únicamente los faroles cuyo número sea **múltiplo de 3 o múltiplo de 5** (o de ambos a la vez).

Cada farol encendido consume una cantidad de energía equivalente a su propio número identificador. Se requiere escribir un programa en C++ que calcule la **energía total** consumida (es decir, la suma de los números de todos los faroles encendidos).

#### Ilustración de Referencia

```text
  Faroles:     1   2  (3)  4  (5) (6)  7   8  (9) (10)
                       |       |   |           |    |
                       v       v   v           v    v
  Encendidos:          3       5   6           9   10

  Ejemplo con N = 10:
  Energía total = 3 + 5 + 6 + 9 + 10 = 33
```

#### Entrada

Una única línea con un número entero $N$ ($1 \le N \le 2 \cdot 10^9$).

*(Nota: El resultado puede exceder el límite de un entero de 32 bits, por lo que requiere tipos de datos de 64 bits).*

#### Salida

Imprimir un único número entero: la energía total consumida.

#### Ejemplos de Entrada y Salida

| Entrada | Salida | Explicación |
| --- | --- | --- |
| `10` | `33` | Se encienden los faroles 3, 5, 6, 9 y 10. Suma = $3 + 5 + 6 + 9 + 10 = 33$. |
| `15` | `60` | Se encienden 3, 5, 6, 9, 10, 12 y 15. Suma = $60$. |
| `100` | `2418` | Suma de todos los múltiplos de 3 o 5 menores o iguales a 100. |

---

#### Solución Subóptima (Recorrido Lineal)

Este enfoque examina cada farol desde $1$ hasta $N$ mediante un bucle iterativo y acumula los números que cumplen la condición.

```cpp
#include <iostream>

using namespace std;

int main() {
    long long n;
    cin >> n;

    long long suma = 0;

    // Recorre todos los faroles uno por uno
    for (long long i = 1; i <= n; i++) {
        if (i % 3 == 0 || i % 5 == 0) {
            suma += i;
        }
    }

    cout << suma << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(N)$. Para $N = 2 \cdot 10^9$, requiere dos mil millones de iteraciones con operaciones aritméticas de módulo.
* **Resultado:** Excede el tiempo límite de ejecución (*TLE*).

---

#### Solución Óptima (Fórmula de Gauss e Inclusión-Exclusión)

La suma de los múltiplos de $k$ hasta $N$ constituye una progresión aritmética: si $m = \lfloor N/k \rfloor$, la suma es $S(k) = k \cdot \frac{m(m+1)}{2}$. Mediante el principio de inclusión-exclusión, se resta $S(15)$ para evitar contar dos veces los múltiplos comunes de 3 y 5:

$$\text{Total} = S(3) + S(5) - S(15)$$

```cpp
#include <iostream>

using namespace std;

// Calcula la suma de todos los múltiplos de k que no superan n
long long sumaMultiplos(long long n, long long k) {
    long long m = n / k;
    return k * (m * (m + 1) / 2);
}

int main() {
    long long n;
    cin >> n;

    long long total = sumaMultiplos(n, 3) + sumaMultiplos(n, 5) - sumaMultiplos(n, 15);

    cout << total << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(1)$. Evalúa directamente las fórmulas aritméticas sin ciclos iterativos.
* **Principio de Inclusión-Exclusión:** Restar $S(15)$ corrige la duplicación de términos divisibles por 3 y 5.
* **Tipos de Datos:** Para $N = 2 \cdot 10^9$, el resultado es aproximadamente $9.3 \cdot 10^{17}$, lo cual requiere el uso de `long long`.

---

### Problema 5: Los Ríos Gemelos del Valle de Sucre

* **Área temática:** Números Primos y Criba de Eratóstenes.
* **Límite de tiempo:** 1.0 segundo
* **Límite de memoria:** 64 MB

#### Enunciado

Dos números primos se consideran **primos gemelos** si su diferencia absoluta es igual a 2 (por ejemplo, $3$ y $5$, o $11$ y $13$).

Dado un intervalo cerrado $[A, B]$, se requiere escribir un programa en C++ que determine la cantidad de pares de primos gemelos $(p, p+2)$ tales que ambos números se encuentran dentro del rango $[A, B]$.

#### Ilustración de Referencia

```text
  Intervalo [1, 20]:

   1  2  [3] 4 [5] 6 [7] 8  9 10 [11] 12 [13] 14 15 16 [17] 18 [19] 20
          \___/ \___/          \______/              \______/
          (3,5) (5,7)          (11,13)               (17,19)

  Total de pares gemelos: 4
```

#### Entrada

Una única línea con dos números enteros $A$ y $B$ ($1 \le A \le B \le 10^7$) separados por un espacio.

#### Salida

Imprimir un único número entero: la cantidad de pares de primos gemelos $(p, p+2)$ tales que $A \le p$ y $p + 2 \le B$.

#### Ejemplos de Entrada y Salida

| Entrada | Salida | Explicación |
| --- | --- | --- |
| `1 10` | `2` | Los pares contenidos son $(3,5)$ y $(5,7)$. |
| `20 50` | `2` | Los pares contenidos son $(29,31)$ y $(41,43)$. |
| `24 28` | `0` | Entre 24 y 28 no existen números primos gemelos. |

---

#### Solución Subóptima (Prueba de Divisibilidad Individual)

Este enfoque verifica la primalidad de cada entero dentro del rango de manera independiente mediante prueba de divisores.

```cpp
#include <iostream>

using namespace std;

bool esPrimo(int x) {
    if (x < 2) return false;
    for (int i = 2; (long long)i * i <= x; i++) {
        if (x % i == 0) return false;
    }
    return true;
}

int main() {
    int a, b;
    cin >> a >> b;

    int contador = 0;

    for (int p = a; p + 2 <= b; p++) {
        if (esPrimo(p) && esPrimo(p + 2)) {
            contador++;
        }
    }

    cout << contador << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O((B - A + 1) \sqrt{B})$ en el peor caso. Revalúa la primalidad repetidamente sin reutilizar cómputos previos.
* **Resultado:** Para $B = 10^7$ excede el tiempo límite de ejecución (*TLE*).

---

#### Solución Óptima (Criba de Eratóstenes)

La Criba de Eratóstenes precalcula la primalidad de todos los números hasta $B+2$ en una sola pasada. Posteriormente, un recorrido lineal cuenta los pares gemelos en el intervalo.

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    int a, b;
    cin >> a >> b;

    // compuesto[i] = true si i NO es un número primo
    vector<bool> compuesto(b + 3, false);
    compuesto[0] = compuesto[1] = true;

    for (int i = 2; (long long)i * i <= b + 2; i++) {
        if (!compuesto[i]) {
            for (int j = i * i; j <= b + 2; j += i) {
                compuesto[j] = true;
            }
        }
    }

    int contador = 0;
    int inicio = (a < 2) ? 2 : a;

    for (int p = inicio; p + 2 <= b; p++) {
        if (!compuesto[p] && !compuesto[p + 2]) {
            contador++;
        }
    }

    cout << contador << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(B \log \log B)$. Para $B = 10^7$, el precálculo requiere pocas centésimas de segundo.
* **Complejidad Espacial:** $O(B)$. El vector de marcas para $10^7$ posiciones consume aproximadamente $1.2\text{ MB}$ de memoria.

---

## Categoría B (5º y 6º de Secundaria)

---

### Problema 1: El Carácter Solitario del Archivo Histórico

* **Área temática:** Cadenas de Texto (`string`) y Arreglos de Frecuencia.
* **Límite de tiempo:** 1.0 segundo
* **Límite de memoria:** 64 MB

#### Enunciado

En el proceso de digitalización de pergaminos coloniales se requiere validar la autenticidad del texto identificando el **primer carácter que no se repita** a lo largo de una cadena de texto codificada.

El texto recibido está compuesto exclusivamente por letras minúsculas del alfabeto inglés (`'a'` a `'z'`). Se requiere escribir un programa que encuentre e imprima ese primer carácter único. Si todos los caracteres aparecen dos o más veces en el texto, el programa debe imprimir `-1`.

#### Ilustración de Referencia

```text
  Texto: " s u c r e s u c "
           | | | | |
           | | | +-+---> 'r' y 'e' aparecen 1 sola vez.
           +-+-+-------> 's', 'u', 'c' se repiten al final.

  El primer carácter no repetido es: 'r'
```

#### Entrada

* La primera línea contiene un número entero $N$ ($1 \le N \le 10^5$), la longitud del texto.
* La segunda línea contiene la cadena de texto de longitud $N$, formada por letras minúsculas.

#### Salida

Imprimir el primer carácter que aparezca exactamente una vez en la cadena. Si no existe ningún carácter sin repetir, imprimir `-1`.

#### Ejemplos de Entrada y Salida

| Entrada | Salida | Explicación |
| --- | --- | --- |
| `8`<br>`sucresuc` | `r` | Las letras 's', 'u' y 'c' se repiten. 'r' y 'e' aparecen una vez; 'r' aparece en una posición previa a 'e'. |
| `6`<br>`bonobo` | `n` | Las letras 'b' y 'o' se repiten; el único carácter único es 'n'. |
| `6`<br>`cancan` | `-1` | Todos los caracteres se repiten al menos dos veces. |

---

#### Solución Subóptima (Doble Bucle)

Este enfoque recorre la cadena caracter por caracter y, para cada posición, vuelve a iterar por todo el texto para contar la cantidad total de apariciones.

```cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
    int n;
    cin >> n;

    string s;
    cin >> s;

    char respuesta = '?';

    // Recorrido anidado O(N^2)
    for (int i = 0; i < n; i++) {
        int conteo = 0;

        for (int j = 0; j < n; j++) {
            if (s[i] == s[j]) {
                conteo++;
            }
        }

        if (conteo == 1) {
            respuesta = s[i];
            break;
        }
    }

    if (respuesta != '?') {
        cout << respuesta << endl;
    } else {
        cout << -1 << endl;
    }

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(N^2)$. Para $N = 10^5$, requiere cerca de $10^{10}$ operaciones.
* **Resultado:** Excede el tiempo límite de ejecución (*TLE*).

---

#### Solución Óptima (Vector de Frecuencias)

Este método realiza dos pasadas lineales utilizando un arreglo de frecuencias de tamaño fijo ($26$ posiciones) para registrar las repeticiones de cada letra del alfabeto.

```cpp
#include <iostream>
#include <string>
#include <vector>

using namespace std;

int main() {
    int n;
    cin >> n;

    string s;
    cin >> s;

    // Arreglo de frecuencia para las 26 letras minúsculas
    vector<int> freq(26, 0);

    // Primera pasada O(N): Conteo de frecuencias
    for (int i = 0; i < n; i++) {
        freq[s[i] - 'a']++;
    }

    // Segunda pasada O(N): Búsqueda del primer carácter con frecuencia 1
    char respuesta = '?';
    for (int i = 0; i < n; i++) {
        if (freq[s[i] - 'a'] == 1) {
            respuesta = s[i];
            break;
        }
    }

    if (respuesta != '?') {
        cout << respuesta << endl;
    } else {
        cout << -1 << endl;
    }

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(N)$. Se realizan exactamente $2N$ operaciones de inspección.
* **Complejidad Espacial:** $O(1)$ memoria adicional (el arreglo `freq` requiere solo 26 enteros).

---

### Problema 2: El Stand Favorito de la Fexpo Sucre

* **Área temática:** Arreglos, Ordenación y Conteo de Frecuencias.
* **Límite de tiempo:** 1.0 segundo
* **Límite de memoria:** 64 MB

#### Enunciado

Durante la feria Fexpo Sucre se realizó una votación popular en la que cada asistente votó por el código numérico de su stand preferido.

Dada la lista de $N$ votos registrados, se requiere determinar el **código del stand más votado** (la moda estadística). Si existe un empate entre dos o más stands con la misma cantidad máxima de votos, se debe seleccionar el stand cuyo **número de código sea menor**.

#### Ilustración de Referencia

```text
  Votos registrados desordenados:  [ 12,  5,  12,  8,  5,  12,  8 ]

  Paso 1: Ordenar el vector:
           [ 5, 5,   8, 8,   12, 12, 12 ]
             \___/   \___/   \________/
             (2)      (2)       (3 votos)
  
  Ganador: Stand 12 (3 votos)
```

#### Entrada

* La primera línea contiene un número entero $N$ ($1 \le N \le 10^5$), la cantidad total de votos.
* La segunda línea contiene $N$ números enteros separados por espacio: los códigos de los stands votados $V_1, V_2, \dots, V_N$ ($1 \le V_i \le 10^9$).

#### Salida

Un único número entero: el código del stand ganador.

#### Ejemplos de Entrada y Salida

| Entrada | Salida | Explicación |
| --- | --- | --- |
| `7`<br>`12 5 12 8 5 12 8` | `12` | El stand 12 acumula 3 votos; los stands 5 y 8 obtienen 2 votos cada uno. |
| `6`<br>`40 10 40 10 20 20` | `10` | Empate a 2 votos entre 10, 20 y 40. Se selecciona el menor código: 10. |

---

#### Solución Subóptima (Búsqueda por Comparación Cruzada)

Este enfoque evalúa la frecuencia de cada elemento realizando un segundo bucle completo por el arreglo.

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    int n;
    cin >> n;

    vector<int> votos(n);
    for (int i = 0; i < n; i++) {
        cin >> votos[i];
    }

    int mejorStand = votos[0];
    int maxRepeticiones = 0;

    // Doble bucle O(N^2)
    for (int i = 0; i < n; i++) {
        int contador = 0;
        for (int j = 0; j < n; j++) {
            if (votos[j] == votos[i]) {
                contador++;
            }
        }

        if (contador > maxRepeticiones) {
            maxRepeticiones = contador;
            mejorStand = votos[i];
        } else if (contador == maxRepeticiones && votos[i] < mejorStand) {
            mejorStand = votos[i];
        }
    }

    cout << mejorStand << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(N^2)$. Inviable para $N = 10^5$.
* **Resultado:** Excede el tiempo límite de ejecución (*TLE*).

---

#### Solución Óptima (Ordenación y Recorrido Lineal)

Al ordenar el arreglo en tiempo $O(N \log N)$, los elementos idénticos quedan contiguos, permitiendo contarlos en un único barrido lineal de tiempo $O(N)$.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    int n;
    cin >> n;

    vector<int> votos(n);
    for (int i = 0; i < n; i++) {
        cin >> votos[i];
    }

    // Ordenación ascendente en O(N log N)
    sort(votos.begin(), votos.end());

    int mejorStand = votos[0];
    int maxVotos = 1;
    int rachaActual = 1;

    // Barrido lineal O(N)
    for (int i = 1; i < n; i++) {
        if (votos[i] == votos[i - 1]) {
            rachaActual++;
        } else {
            rachaActual = 1;
        }

        // Se actualiza únicamente si se encuentra una frecuencia estrictamente mayor
        if (rachaActual > maxVotos) {
            maxVotos = rachaActual;
            mejorStand = votos[i];
        }
    }

    cout << mejorStand << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(N \log N)$ debido a la etapa de ordenación (`std::sort`).
* **Criterio de Desempate:** Al estar ordenado de menor a mayor, el primer elemento en alcanzar la racha máxima retenida será automáticamente el menor entre los empatados en esa frecuencia.

---

### Problema 3: Las Notas Secretas del Callejón de Santa Teresa

* **Área temática:** Cadenas de Texto (`string`), Anagramas y Ordenación.
* **Límite de tiempo:** 1.0 segundo
* **Límite de memoria:** 64 MB

#### Enunciado

Dos mensajes escritos en clave deben ser analizados para confirmar si uno es un **anagrama** del otro; es decir, si ambas palabras contienen exactamente las mismas letras en las mismas cantidades, independientemente de su ordenación.

Dadas dos palabras $S_1$ y $S_2$, se requiere escribir un programa en C++ que determine si son anagramas.

#### Ilustración de Referencia

```text
  Palabra 1: "b o l i v i a"  ---[ordenar letras]--->  "a b i i l o v"
  Palabra 2: "a l i v i b o"  ---[ordenar letras]--->  "a b i i l o v"
                                                             ||
                                           ¿Son idénticas? -> SI
```

#### Entrada

Dos líneas, cada una con una cadena de texto ($S_1$ y $S_2$) formadas por letras minúsculas (`'a'` a `'z'`).

Las longitudes de las cadenas satisfacen: $1 \le |S_1|, |S_2| \le 10^5$.

#### Salida

Imprimir `SI` si las dos palabras son anagramas, o `NO` en caso contrario.

#### Ejemplos de Entrada y Salida

| Entrada | Salida | Explicación |
| --- | --- | --- |
| `bolivia`<br>`alivibo` | `SI` | Ambas contienen una 'a', una 'b', dos 'i', una 'l', una 'o' y una 'v'. |
| `chuquisaca`<br>`sucre` | `NO` | Tienen distintas longitudes y caracteres. |
| `perro`<br>`perros` | `NO` | La segunda cadena contiene un carácter adicional 's'. |

---

#### Solución Subóptima (Búsqueda y Eliminación Dinámica)

Este método busca cada carácter de la primera palabra dentro de la segunda mediante `find` y elimina la coincidencia hallada usando `erase`.

```cpp
#include <iostream>
#include <string>

using namespace std;

int main() {
    string s1, s2;
    cin >> s1 >> s2;

    if (s1.length() != s2.length()) {
        cout << "NO" << endl;
        return 0;
    }

    // Por cada letra de s1, buscar y eliminar en s2
    for (size_t i = 0; i < s1.length(); i++) {
        size_t pos = s2.find(s1[i]);
        if (pos != string::npos) {
            s2.erase(pos, 1); // Desplazamiento dinámico costoso O(L)
        } else {
            cout << "NO" << endl;
            return 0;
        }
    }

    cout << "SI" << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(L^2)$, donde $L = |S_1|$. Cada llamada a `erase` reestructura la memoria de la cadena.
* **Resultado:** Excede el tiempo límite de ejecución (*TLE*).

---

#### Solución Óptima (Ordenación Alfabética)

Si dos cadenas son anagramas, al ordenar alfabéticamente sus caracteres deben dar como resultado secuencias idénticas.

```cpp
#include <iostream>
#include <string>
#include <algorithm>

using namespace std;

int main() {
    string s1, s2;
    cin >> s1 >> s2;

    // Validación de longitud en O(1)
    if (s1.length() != s2.length()) {
        cout << "NO" << endl;
        return 0;
    }

    // Ordenación de caracteres en O(L log L)
    sort(s1.begin(), s1.end());
    sort(s2.begin(), s2.end());

    // Comparación directa de cadenas
    if (s1 == s2) {
        cout << "SI" << endl;
    } else {
        cout << "NO" << endl;
    }

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(L \log L)$, dominada por `std::sort`.
* **Complejidad Espacial:** $O(1)$ adicional.

---

### Problema 4: La Compra Exacta en el Mercado Central

* **Área temática:** Arreglos, Ordenación y Técnica de Dos Punteros.
* **Límite de tiempo:** 1.0 segundo
* **Límite de memoria:** 64 MB

#### Enunciado

En el Mercado Central de Sucre se dispone de un monto total exacto de $M$ bolivianos. Un puesto comercial ofrece $N$ productos diferentes, cada uno con un precio determinado.

Se requiere determinar si es posible adquirir **exactamente dos productos diferentes** cuya suma de precios sea igual al monto $M$.

#### Ilustración de Referencia

```text
  Precios disponibles: [ 3,  7,  12,  15,  20 ]     Monto exacto: M = 22

  Técnica de dos extremos (punteros):
  Paso 1:  3 + 20 = 23  (Suma > 22  --> Retrocede puntero derecho)
  Paso 2:  3 + 15 = 18  (Suma < 22  --> Avanza puntero izquierdo)
  Paso 3:  7 + 15 = 22  (Suma == 22 --> ¡Coincidencia exacta!) --> SI
```

#### Entrada

* La primera línea contiene dos enteros: $N$ ($2 \le N \le 10^5$), la cantidad de productos, y $M$ ($1 \le M \le 2 \cdot 10^9$), el monto total disponible.
* La segunda línea contiene $N$ enteros separados por espacio: los precios de los productos $P_1, P_2, \dots, P_N$ ($1 \le P_i \le 10^9$).

#### Salida

Imprimir `SI` si existe al menos un par de productos distintos cuya suma sea igual a $M$, o `NO` en caso contrario.

#### Ejemplos de Entrada y Salida

| Entrada | Salida | Explicación |
| --- | --- | --- |
| `5 22`<br>`12 3 20 7 15` | `SI` | Se eligen los productos con precios 7 y 15 ($7 + 15 = 22$). |
| `4 10`<br>`3 3 8 2` | `SI` | Se eligen los productos con precios 8 y 2 ($8 + 2 = 10$). |
| `3 10`<br>`5 2 4` | `NO` | Ninguna combinación de 2 productos distintos suma 10 (no se permite reusar el mismo producto). |

---

#### Solución Subóptima (Fuerza Bruta de Pares)

Este algoritmo prueba todas las combinaciones de pares mediante dos bucles anidados.

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    int n;
    long long m;
    cin >> n >> m;

    vector<long long> precios(n);
    for (int i = 0; i < n; i++) {
        cin >> precios[i];
    }

    bool encontrado = false;

    // Evaluación de todas las parejas O(N^2)
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            if (precios[i] + precios[j] == m) {
                encontrado = true;
                break;
            }
        }
        if (encontrado) break;
    }

    if (encontrado) {
        cout << "SI" << endl;
    } else {
        cout << "NO" << endl;
    }

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(N^2)$. Evalúa hasta $\frac{N(N-1)}{2} \approx 5 \cdot 10^9$ pares en el peor caso.
* **Resultado:** Excede el tiempo límite de ejecución (*TLE*).

---

#### Solución Óptima (Ordenación y Dos Punteros)

Tras ordenar los precios en $O(N \log N)$, se posiciona un puntero al inicio (`izq`) y otro al final (`der`) para estrechar el rango de búsqueda en un solo recorrido lineal $O(N)$.

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

using namespace std;

int main() {
    int n;
    long long m;
    cin >> n >> m;

    vector<long long> precios(n);
    for (int i = 0; i < n; i++) {
        cin >> precios[i];
    }

    // Ordenación ascendente O(N log N)
    sort(precios.begin(), precios.end());

    // Algoritmo de dos punteros O(N)
    int izq = 0;
    int der = n - 1;
    bool encontrado = false;

    while (izq < der) {
        long long sumaActual = precios[izq] + precios[der];

        if (sumaActual == m) {
            encontrado = true;
            break;
        } else if (sumaActual < m) {
            izq++; // Se incrementa el valor inferior
        } else {
            der--; // Se decrementa el valor superior
        }
    }

    if (encontrado) {
        cout << "SI" << endl;
    } else {
        cout << "NO" << endl;
    }

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(N \log N)$ debido a `std::sort`, seguido de un barrido de $O(N)$.
* **Complejidad Espacial:** $O(N)$ para almacenar el vector de precios de 64 bits.

---

### Problema 5: Las Luces de la Plaza 25 de Mayo

* **Área temática:** Matrices, Recorridos y Condicionales.
* **Límite de tiempo:** 1.0 segundo
* **Límite de memoria:** 64 MB

#### Enunciado

Durante una actividad cultural en la Plaza 25 de Mayo de Sucre se han instalado varias filas de luces. Cada luz puede encontrarse **encendida** (`1`) o **apagada** (`0`).

La instalación se representa mediante una matriz de $F$ filas y $C$ columnas. Las filas se encuentran numeradas secuencialmente desde `1` hasta `F`.

Se requiere escribir un programa en C++ que determine el número de la fila que contenga la **mayor cantidad de luces encendidas**. En caso de existir un empate entre dos o más filas con la misma cantidad máxima, se debe seleccionar la fila que posea el **menor número de fila**.

#### Ilustración de Referencia

```text
              Columnas
          1   2   3   4   5
        +---+---+---+---+---+
Fila 1  | 0 | 1 | 1 | 0 | 1 |  --> 3 luces
        +---+---+---+---+---+
Fila 2  | 1 | 1 | 0 | 0 | 0 |  --> 2 luces
        +---+---+---+---+---+
Fila 3  | 0 | 1 | 1 | 1 | 0 |  --> 3 luces
        +---+---+---+---+---+

        Fila 1 y Fila 3 tienen 3 luces.

        Como hay empate, se elige la fila
        con el menor número:

                    Fila 1
                    3 luces
```

#### Entrada

* La primera línea contiene dos enteros $F$ y $C$ ($1 \le F, C \le 100$), correspondientes al número de filas y columnas de la matriz.
* Las siguientes $F$ líneas contienen $C$ enteros cada una, representando la matriz de luces (`0` o `1`), separados por espacios.

#### Salida

Imprimir dos enteros separados por un espacio: el número de la fila ganadora y la cantidad de luces encendidas que contiene.

#### Ejemplos de Entrada y Salida

| Entrada | Salida | Explicación |
| --- | --- | --- |
| `3 5`<br>`0 1 1 0 1`<br>`1 1 0 0 0`<br>`0 1 1 1 0` | `1 3` | Las filas 1 y 3 tienen 3 luces encendidas. Se selecciona la fila 1 por tener el menor número. |
| `4 4`<br>`1 0 0 0`<br>`1 1 1 0`<br>`0 0 0 0`<br>`1 1 1 1` | `4 4` | La fila 4 contiene la mayor cantidad de luces encendidas: 4. |
| `3 3`<br>`1 0 1`<br>`0 1 0`<br>`1 0 1` | `1 2` | Las filas 1 y 3 tienen 2 luces encendidas. Se selecciona la fila 1. |

---

#### Solución Subóptima (Almacenamiento en Arreglo Auxiliar)

Este enfoque contabiliza en una primera etapa la cantidad de luces encendidas de cada fila y las almacena en un arreglo `lucesPorFila`. Posteriormente, realiza una segunda pasada sobre dicho arreglo para determinar la fila con la mayor cantidad.

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main() {
    int f, c;
    cin >> f >> c;

    vector<int> lucesPorFila(f, 0);

    // Contar las luces encendidas de cada fila
    for (int i = 0; i < f; i++) {
        for (int j = 0; j < c; j++) {
            int luz;
            cin >> luz;

            if (luz == 1) {
                lucesPorFila[i]++;
            }
        }
    }

    int mejorFila = 0;
    int mayorCantidad = lucesPorFila[0];

    // Buscar la fila con la mayor cantidad de luces
    for (int i = 1; i < f; i++) {
        if (lucesPorFila[i] > mayorCantidad) {
            mayorCantidad = lucesPorFila[i];
            mejorFila = i;
        }
    }

    cout << mejorFila + 1 << " " << mayorCantidad << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(F \cdot C + F)$. Requiere $O(F \cdot C)$ operaciones para la lectura de la matriz y $O(F)$ para la búsqueda del valor máximo.
* **Complejidad Espacial:** $O(F)$ para almacenar las frecuencias por fila en el arreglo auxiliar.

---

#### Solución Óptima (Conteo Directo en Recorrido Lineal)

En lugar de almacenar las frecuencias de todas las filas, este método procesa cada fila de forma secuencial, contando sus luces encendidas y comparando de inmediato el resultado con el máximo registrado hasta el momento.

Al utilizar la comparación estricta (`>`), cualquier empate subsiguiente conservará automáticamente la primera fila que alcanzó dicho valor máximo.

```cpp
#include <iostream>

using namespace std;

int main() {
    int f, c;
    cin >> f >> c;

    int mejorFila = 1;
    int mayorCantidad = -1;

    for (int i = 1; i <= f; i++) {
        int cantidadActual = 0;

        // Contar las luces encendidas de la fila actual
        for (int j = 0; j < c; j++) {
            int luz;
            cin >> luz;

            if (luz == 1) {
                cantidadActual++;
            }
        }

        // Se actualiza únicamente si se encuentra una cantidad estrictamente mayor
        if (cantidadActual > mayorCantidad) {
            mayorCantidad = cantidadActual;
            mejorFila = i;
        }
    }

    cout << mejorFila << " " << mayorCantidad << endl;

    return 0;
}
```

##### Análisis de Complejidad

* **Complejidad Temporal:** $O(F \cdot C)$. Cada elemento de la matriz se procesa exactamente una vez durante la lectura.
* **Complejidad Espacial:** $O(1)$ adicional.