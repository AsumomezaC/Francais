
> [!warning] Solo para Math Blocks
> Estos comandos solo funcionan si están contenido por algo que inda que es una expresión matemática, es decir están contenidos por '\$' '\$'.


> [!NOTE] [[Sintaxis]] de [[Latex]]
> Obsidian utiliza como base para sus 'Math blocks', la sintaxis de Latex.
# Generales
## Poner un subíndice
Se escribe de la siguiente forma: a_b $\leftrightarrow a_b$ 

## Fracciones[^1]
Se utiliza la forma: "\frac{elem1}{elem2}". Obteniendo el siguiente resultado:
$$
\frac{elem1}{elem2}
$$
## Raíz cuadrada[^1]
Se utiliza la forma "\sqrt{elem}", que da como resultado lo siguiente:
$$
\sqrt{elem}
$$
## Raíz 'n'[^1]
Se utiliza la forma "\sqrt\[n]{elem}", que da como resultado lo siguiente:
$$
\sqrt[n]{elem}
$$
## Exponente de varios elementos[^1]
Se utiliza la forma "a^{exp}", permitiendo hacer que la expresión sea tan compleja como se guste.
$$
a^{exp}
$$
## Símbolo $\pm$[^2]
Se escribe poniendo el comando "\pm".
## Símbolo $\mp$[^2]
El símbolo contrario a [[#Símbolo $ pm$]], se escribe curiosamente al contrario que este símbolo, así: "\mp".
## No igual (diferente) o $\neq$
Se escribe poniendo "\neq"
## Aproximadamente o $\approx$
Se escribe poniendo el comando "\approx"
# Formato
## Texto
Para ingresar texto dentro de una ecuación se utiliza "\text{texto a escribir}"
## Saltos de línea
Si quieres escribir varias líneas dentro de un mismo bloque `$$ ... $$`, usa los siguientes comandos de LaTeX:

#### a) **`\\` (doble barra invertida)**  
Funciona en entornos de ecuaciones multilínea (como `align`, `gather`, o `multline`).

**Ejemplo**:
```latex
$$
\begin{align}
x &= y + 1 \\
y &= z^2 \\
\end{align}
$$
```
Ejemplo:
$$
\begin{align}
x &= y + 1 \\
y &= z^2 \\
\end{align}
$$
#### b) **`\newline` o `\linebreak`**  
Funciona en modo texto dentro de ecuaciones:
```latex
$$
\text{Línea 1} \newline \text{Línea 2}
$$
```
### 2. **Entornos específicos para multilínea**
- **`align`**: Para ecuaciones alineadas (usa `&` para marcar el punto de alineación).
  ```latex
  $$
  \begin{align}
  f(x) &= x^2 \\
  g(x) &= \sin(x)
  \end{align}
  $$
  ```

- **`gather`**: Para ecuaciones centradas sin alineación:
  ```latex
  $$
  \begin{gather}
  a = b \\
  c = d
  \end{gather}
  $$
  ```

- **`multline`**: Para ecuaciones largas que ocupan varias líneas:
  ```latex
  $$
  \begin{multline}
  p(x) = 3x^6 + 2x^5 \\ 
  - x^4 + 4x^3 \\
  - 2x^2 + x - 1
  \end{multline}
  $$
  ```

---

### 3. **En modo texto dentro de LaTeX**
Si necesitas escribir texto con saltos de línea dentro de un bloque matemático, usa `\text{}` combinado con `\\`:
```latex
$$
\text{Esto es la línea 1} \\
\text{Esto es la línea 2}
$$
```

---

### Resumen rápido:
| Qué necesitas       | Sintaxis LaTeX                     |
| ------------------- | ---------------------------------- |
| Salto en ecuaciones | `\\` o `\newline`                  |
| Alinear ecuaciones  | `align` + `&`                      |
| Texto con saltos    | `\text{Línea 1} \\ \text{Línea 2}` |

# Conectores lógicos
## Equivalente o $\equiv$
Se pone escribiendo el comando "\equiv"
## Divisor o $\mid$
Se consigue poniendo el comando "\mid"
## Poner $\leftrightarrow$
Puedes utilizar "\leftrightarrow" para obtener $\leftrightarrow$

>Sin se trata de una implicación doble se suele poner "\iff" que da $\iff$
## Implica o $\implies$
Se pone poniendo el comando "\implies"
## '$\therefore$' o por lo tanto
Para poner el signo de por lo tanto se utiliza **"\therefore"** y da como resultado: $\therefore$

## '$\because$' o porque (dado que)
Para poner el signo contario a [[#'$ therefore$' o por lo tanto]] se utiliza el comando "\because", que da como resultado: $\because$
## Pertenece o $\in$
Se escribe poniendo el comando **"\in"**
## No pertenece (no está contenido) o $\notin$
Se escribe poniendo el comando **"\notin"**
## Unión o $\cup$
Se escribe usando el comando **"\cup"**
## Intersección o $\cap$
Se escribe usando el comando **"\cap"**
## Conjunto nulo o $\emptyset$
Se escribe usando el comando **"\emptyset"**
# Constantes
## Pi o $\pi$
Se escribe poniendo el comando "\pi"
## Infinito o $\infty$
Se escribe poniendo el comando "\infty"

>Para el [[Números irracionales Y Constantes#Número de Euler (e)|número de Euler]] basta con poner una 'e'
## Nulo o $\varnothing$
Se escribe poniendo el comando **"\varnothing"**

# Integrales
## Integral simple
## Integral definida
## Integral doble y triple
## Integral cerrada (contorno)
# Sumatorias
### 1. **Sintaxis básica de LaTeX para sumatorias**
Para una sumatoria con límites inferior y superior, usa el siguiente formato:

```latex
\sum_{límite\ inferior}^{límite\ superior} expresión
```

Por ejemplo:
```latex
\sum_{i=1}^{n} i^2
```
Se verá como:  
$\sum_{i=1}^{n} i^2$

---

### 2. **Cómo escribirlo en Obsidian**
- **En una línea** (inline): Encierra la expresión entre `$`:
  ```
  La sumatoria es $\sum_{i=1}^{n} i^2$.
  ```
  Resultado:  
  La sumatoria es $\sum_{i=1}^{n} i^2$.

- **En modo bloque** (centrado): Encierra la expresión entre `$$`:
  ```latex
  $$
  \sum_{i=1}^{n} i^2
  $$
  ```
  Resultado:  
  $$
  \sum_{i=1}^{n} i^2
  $$
---

### 3. **Ejemplos avanzados**
- **Con fracciones o funciones**:
  ```latex
  $$
  \sum_{k=0}^{\infty} \frac{(-1)^k}{k+1}
  $$
  ```
  Resultado:  
  $$
  \sum_{k=0}^{\infty} \frac{(-1)^k}{k+1}
  $$

- **Con condiciones (usando `\substack`)**:
  ```latex
  $$
  \sum_{\substack{0 < i < m \\ 0 < j < n}} A_{ij}
  $$
  ```
  Resultado:  
$$
\sum_{\substack{0 < i < m \\ 0 < j < n}} A_{ij}
$$
### Resumen rápido
| Tipo         | Sintaxis                              | Ejemplo Visualizado                 |
| ------------ | ------------------------------------- | ----------------------------------- |
| Inline       | `$\sum_{i=1}^{n} i^2$`                | $\sum_{i=1}^{n} i^2$                |
| Bloque       | `$$\sum_{i=1}^{n} i^2$$`              | $$\sum_{i=1}^{n} i^2$$              |
| Con fracción | `$$\sum_{k=0}^\infty \frac{1}{k^2}$$` | $$\sum_{k=0}^\infty \frac{1}{k^2}$$ |


[^1]: Se pueden anidar y combinar con otras funciones.
[^2]: Se debe de poner un espacio luego de escribir este comando.