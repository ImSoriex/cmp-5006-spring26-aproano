# Sección 1: Investigación – Cifrados Clásicos Históricos y Avanzados  

# 1. Cifrado Vigenère  

## 1.1 Mecanismo  

El cifrado Vigenère es un sistema de sustitución polialfabética que utiliza la llamada Tabula Recta, una matriz de 26 × 26 donde cada fila contiene el alfabeto desplazado una posición respecto a la anterior.

Proceso de cifrado:

1. Se elige una palabra clave.
2. La clave se repite hasta igualar la longitud del mensaje.
3. Cada letra del texto plano se cifra usando la letra correspondiente de la clave.

Si representamos las letras como números (A = 0, B = 1, ..., Z = 25), el cifrado se define como:

Cᵢ = (Pᵢ + Kᵢ) mod 26  

donde:  
Pᵢ = letra del texto plano  
Kᵢ = letra de la clave  
Cᵢ = letra cifrada  

### Ejemplo  

Texto plano:  
ATTACKATDAWN  

Clave:  
LEMONLEMONLE  

Convertimos las primeras letras:

A (0) + L (11) = 11 → L  
T (19) + E (4) = 23 → X  
T (19) + M (12) = 31 mod 26 = 5 → F  

El texto cifrado comienza como: LXF…

Este ejemplo muestra cómo el alfabeto de sustitución cambia en cada posición.

## 1.2 ¿Por qué dificulta el análisis de frecuencia?  

En un cifrado por sustitución simple, cada letra del texto plano siempre se transforma en la misma letra cifrada. En Vigenère, una misma letra puede cifrarse de distintas maneras según la posición dentro del ciclo de la clave.

Por ejemplo, la letra “E” puede transformarse en distintos símbolos a lo largo del mensaje. Esto dispersa las frecuencias estadísticas y elimina los picos claros que permiten romper fácilmente un cifrado monoalfabético.

Sin embargo, si la clave es corta, el patrón se repite periódicamente. En ese caso, el texto puede dividirse en subconjuntos, cada uno equivalente a un cifrado César independiente, lo que permite aplicar análisis de frecuencia por separado.

## 1.3 Ruptura del cifrado: Examen de Kasiski  

El examen de Kasiski permite estimar la longitud de la clave.

Procedimiento:

1. Buscar secuencias repetidas en el texto cifrado.
2. Medir las distancias entre repeticiones.
3. Calcular el máximo común divisor (mcd) de esas distancias.
4. Los divisores más frecuentes sugieren la longitud probable de la clave.

Ejemplo:  
Si una secuencia repetida aparece a 12 y 18 posiciones de distancia:

mcd(12, 18) = 6  

Esto sugiere que la clave podría tener longitud 6.

Una vez conocida la longitud, el texto se divide en grupos según la posición en la clave, reduciendo el problema a varios cifrados César independientes.

---

# 2. Cifrado Hill  

## 2.1 Base matemática  

El cifrado Hill, propuesto por Lester Hill en 1929, aplica conceptos de álgebra lineal a la criptografía.

Procedimiento:

1. Convertir letras a números (A = 0, ..., Z = 25).
2. Dividir el texto plano en bloques de tamaño n.
3. Representar cada bloque como un vector columna P.
4. Definir una matriz clave K de tamaño n × n.
5. Calcular:

C = K × P mod 26  

Este método cifra múltiples letras simultáneamente, generando mayor difusión que una sustitución simple.

### Ejemplo (caso 2 × 2)

Sea la matriz clave:

K =  
[3  3]  
[2  5]  

Texto plano: HE  

H = 7, E = 4  

Vector P = (7, 4)

Multiplicación:

Primera fila: (3·7 + 3·4) = 33  
Segunda fila: (2·7 + 5·4) = 34  

Aplicando módulo 26:

33 mod 26 = 7  
34 mod 26 = 8  

Resultado: HI  

Este ejemplo muestra cómo varias letras se transforman simultáneamente mediante operaciones matriciales.

## 2.2 Requisitos matemáticos  

Para que el cifrado sea reversible, la matriz K debe ser invertible módulo 26.

Condiciones necesarias:

1. det(K) ≠ 0  
2. mcd(det(K), 26) = 1  

Como 26 = 2 × 13, el determinante no debe compartir factores con 2 ni con 13. Si los comparte, la matriz no tendrá inversa modular y el mensaje no podrá descifrarse.

---

# 3. Cifrado Playfair  

## 3.1 Mecanismo  

El cifrado Playfair utiliza una matriz de 5 × 5 construida a partir de una palabra clave.

Construcción:

1. Escribir la palabra clave eliminando letras repetidas.
2. Completar con el resto del alfabeto.
3. Generalmente se combinan I y J en una sola celda.

El mensaje se divide en digrafos (pares de letras).  
Si un par contiene letras iguales, se inserta una “X” entre ellas.

Reglas de cifrado:

1. Misma fila → sustituir cada letra por la situada a su derecha.
2. Misma columna → sustituir cada letra por la situada debajo.
3. Regla del rectángulo → cada letra se reemplaza por la letra en su misma fila pero en la columna de la otra.

Al cifrar pares de letras en lugar de letras individuales, el análisis estadístico se vuelve más complejo, ya que deben considerarse hasta 26² = 676 posibles combinaciones.

## 3.2 Contexto histórico  

El cifrado Playfair fue utilizado por fuerzas británicas durante la Primera y Segunda Guerra Mundial para comunicaciones tácticas.

Se consideraba adecuado para el campo porque:

- No requería dispositivos mecánicos.
- Podía ejecutarse con papel y lápiz.
- Era relativamente rápido.
- Proporcionaba seguridad suficiente para información de validez temporal.

---

# 4. Máquina Enigma  

## 4.1 Lógica de los rotores  

La máquina Enigma utilizaba rotores con cableado interno fijo que realizaban sustituciones monoalfabéticas.

Cada vez que se presionaba una tecla:

- El rotor derecho avanzaba una posición.
- Tras completar una vuelta, hacía avanzar el siguiente rotor.
- Esto producía un cambio constante en el alfabeto de sustitución.

Cada pulsación generaba una transformación distinta, creando un sistema polialfabético mecánico con un período extremadamente largo.

## 4.2 El reflector  

El reflector redirigía la corriente eléctrica de vuelta a través de los rotores.

Consecuencias fundamentales:

1. La misma configuración servía para cifrar y descifrar.
2. Ninguna letra podía cifrarse como ella misma.

Esta propiedad estructural fue explotada por los criptoanalistas aliados.

## 4.3 El panel de conexiones (Plugboard)  

Antes de entrar en los rotores, las letras podían intercambiarse en pares mediante cables.

Con 10 pares conectados, el número de configuraciones superaba los 150 billones de posibilidades.

Si se combinan:

- Orden y selección de rotores  
- Posiciones iniciales  
- Tipo de reflector  
- Configuración del plugboard  

El espacio total de claves en versiones militares superaba 10¹¹⁴ configuraciones posibles.

---

# Conclusión  

Estos sistemas muestran una evolución progresiva en el diseño criptográfico:

- Vigenère introduce polialfabetismo estructurado.  
- Hill incorpora formalmente el álgebra lineal.  
- Playfair amplía la unidad de cifrado de letras individuales a digrafos.  
- Enigma mecaniza la sustitución variable mediante ingeniería electromecánica.  

En conjunto, representan la transición desde métodos simbólicos hacia sistemas matemáticamente estructurados y posteriormente hacia criptografía basada en máquinas. Esta evolución sentó bases conceptuales para la criptografía moderna, que depende profundamente de estructuras algebraicas, teoría de números y complejidad computacional.

---

# Referencias  

Britannica. (2023). Vigenère cipher. Encyclopedia Britannica.  

Britannica. (2023). Playfair cipher. Encyclopedia Britannica.  

Hill, L. S. (1929). Cryptography in an Algebraic Alphabet. The American Mathematical Monthly, 36(6), 306–312.  

Kahn, D. (1996). The Codebreakers: The Comprehensive History of Secret Communication. Scribner.  

Rejewski, M. (1981). How Polish Mathematicians Deciphered the Enigma. Annals of the History of Computing.  

Singh, S. (1999). The Code Book: The Science of Secrecy from Ancient Egypt to Quantum Cryptography. Anchor Books.  

Stinson, D. R., & Paterson, M. B. (2019). Cryptography: Theory and Practice (4th ed.). CRC Press.  

Welchman, G. (1982). The Hut Six Story: Breaking the Enigma Codes. McGraw-Hill.  