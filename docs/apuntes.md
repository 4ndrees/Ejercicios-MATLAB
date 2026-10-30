# MATLAB Onramp - Apuntes

## Fundamentos de MATLAB

### 1.1. Operaciones básicas

| Operación | Sintáxis |
|---|---|
| Suma | `x + y` |
| Resta | `x - y` |
| Multiplicación | `x * y` |
| División | `x / y` |
| Potencia | `x^y` |
| Asignación | `x = y` |

- `;` → Suprime la visualización del resultado.
- `ans` → Almacena el último resultado no asignado.
- `pi` → Constante matemática integrada.
- `format short / long` → Cambia el formato de visualización, no el tipo de dato.

**Ejemplo ejecutable:**

```matlab
x = 5;
y = 2;

suma = x + y
potencia = x^y
division = x/y;

sqrt(16)      % ans = 4
format long   % Más decimales
```

**Funciones integradas:** `abs(x)` (valor absoluto), `sqrt(x)` (raíz cuadrada), `eig(A)` (valores propios).

### 1.2. Operadores relacionales y lógicos

Los operadores de comparación devuelven valores lógicos: `1` (true) o `0` (false).

| Operador | Significado |
|---|---|
| `<` | Menor que |
| `>` | Mayor que |
| `<=` | Menor o igual |
| `>=` | Mayor o igual |
| `==` | Igual a |
| `~=` | Distinto de |
| `&` | AND lógico (Y) |
| `\|` | OR lógico (O) |
| `~` | NOT lógico (negación) |

**Ejemplo ejecutable:**

```matlab
x = 5;
y = 10;

a = x < y           % true
b = x == y          % false
c = (x < 8) & (y > 5)  % true
d = (x > 8) | (y > 5)  % true
```

Los operadores pueden aplicarse directamente a vectores, realizando las comparaciones elemento a elemento.

### 1.3. Indexación lógica

Permite extraer elementos de un array que cumplen una condición mediante un vector lógico.

**Ejemplo ejecutable:**

```matlab
x = [3 8 1 7 5];

mask = x < 5
resultado = x(mask)
```

Resultado:

```matlab
mask = [1 0 1 0 0]
resultado = [3 1]
```

**Combinación de condiciones:**

```matlab
x = [3 8 1 7 5];

resultado = x((x > 2) & (x < 8))
% [3 7 5]
```

**Importante:** al indexar un vector con una máscara lógica, ambos deben tener el mismo número de elementos. MATLAB selecciona únicamente las posiciones cuyo valor lógico es `true`.

### 1.4. Variables y archivos

Los nombres de las variables deben comenzar por una letra y pueden contener letras, números y `_`. MATLAB distingue mayúsculas y minúsculas.

| Comando | Función |
|---|---|
| `save datos.mat` | Guarda todas las variables |
| `save datos.mat x y` | Guarda únicamente x e y |
| `load datos.mat` | Carga las variables guardadas |
| `load datos.mat x` | Carga únicamente x |
| `clear` | Elimina las variables |
| `clc` | Limpia la ventana de comandos |

**Ejemplo ejecutable:**

```matlab
x = 10;
y = 20;

save datos.mat x y
clear x y
load datos.mat x

disp(x)       % Muestra 10
```

### 1.5. Entorno de trabajo

| Panel | Función |
|---|---|
| Command Window | Ejecutar comandos |
| Workspace | Consultar variables |
| Files | Explorar archivos |
| Script | Ejecutar secuencias de comandos |
| Output | Visualizar resultados del script |

Los scripts (`.m`) permiten ejecutar varios comandos consecutivamente y dividirlos en secciones independientes mediante `%%`.

**Ejemplo ejecutable:**

```matlab
%% Sección 1: Variables
a = 5;
b = 10;

%% Sección 2: Cálculo
resultado = a + b
```

**Restaurar interfaz:** `Layout` → diseño predeterminado.

---

## 2. Vectores y matrices

### 2.1. Creación de arrays

| Tipo | Sintaxis |
|---|---|
| Vector fila | `x = [1 2 3]` |
| Vector columna | `x = [1; 2; 3]` |
| Matriz | `A = [1 2; 3 4]` |
| Trasposición | `x'` |

**Separadores:** espacios o comas separan columnas; puntos y coma separan filas.

**Ejemplo ejecutable:**

```matlab
fila = [1 2 3];
columna = fila';

A = [1 2 3;
     4 5 6];

disp(A)
```

El operador `'` realiza la trasposición conjugada. Para trasponer sin conjugar números complejos se utiliza `.'`.

### 2.2. Vectores equiespaciados

| Sintaxis | Resultado |
|---|---|
| `1:5` | `[1 2 3 4 5]` |
| `1:2:9` | `[1 3 5 7 9]` |
| `linspace(1,9,5)` | `[1 3 5 7 9]` |

- `inicio:paso:fin` → Define el incremento entre elementos (por defecto, 1).
- `linspace(inicio,fin,n)` → Genera `n` elementos equiespaciados.

**Ejemplo ejecutable:**

```matlab
a = 0:2:10
b = linspace(0, 10, 6)
```

Ambos generan `[0 2 4 6 8 10]`.

### 2.3. Matrices predefinidas y aleatorias

| Función | Descripción |
|---|---|
| `zeros(m,n)` | Matriz de ceros |
| `ones(m,n)` | Matriz de unos |
| `rand(m,n)` | Valores aleatorios entre 0 y 1 |
| `rand(n)` | Matriz aleatoria n × n |
| `randi([a b],m,n)` | Enteros aleatorios entre a y b |

**Ejemplo ejecutable:**

```matlab
A = zeros(2,3);
B = ones(2,3);
C = rand(2,3);
D = randi([1 10],2,3);

disp(D)
```

---

## 3. Dimensiones e indexación

### 3.1. Dimensiones

- `size(A)` → Devuelve las dimensiones del array.
- `[filas,columnas] = size(A)` → Guarda ambas dimensiones en variables independientes.

**Ejemplo ejecutable:**

```matlab
A = [1 2 3;
     4 5 6];

[filas, columnas] = size(A)
```

Resultado: `filas = 2`, `columnas = 3`.

### 3.2. Acceso a elementos

**MATLAB comienza a indexar desde 1.**

| Sintaxis | Función |
|---|---|
| `A(i,j)` | Elemento de fila i, columna j |
| `A(i,:)` | Fila completa i |
| `A(:,j)` | Columna completa j |
| `A(2:4,:)` | Filas 2, 3 y 4 |
| `A(end,:)` | Última fila |
| `A(:,end)` | Última columna |
| `x([1 3 5])` | Elementos en posiciones indicadas |

`end` representa el último índice de la dimensión correspondiente.

**Ejemplo ejecutable:**

```matlab
A = [10 20 30;
     40 50 60;
     70 80 90];

elemento = A(2,3)    % 60
fila = A(1,:)        % [10 20 30]
columna = A(:,2)     % [20; 50; 80]
ultimo = A(end,end)  % 90
```

---

## 4. Operaciones con arrays

### 4.1. Operaciones básicas

MATLAB permite operar escalares sobre todos los elementos de un array y sumar o restar arrays de dimensiones compatibles.

**Ejemplo ejecutable:**

```matlab
A = [1 2 3];
B = [4 5 6];

C = A + 2     % [3 4 5]
D = A * 3     % [3 6 9]
E = A + B     % [5 7 9]
```

### 4.2. Operaciones matriciales y elemento a elemento

| Operador | Operación |
|---|---|
| `A * B` | Multiplicación matricial |
| `A .* B` | Multiplicación elemento a elemento |
| `A / B` | División matricial por la derecha |
| `A ./ B` | División elemento a elemento |
| `A ^ n` | Potencia matricial |
| `A .^ n` | Potencia elemento a elemento |

**Ejemplo ejecutable:**

```matlab
A = [1 2;
     3 4];

B = [2 0;
     1 2];

C = A * B      % Multiplicación matricial
D = A .* B     % Elemento a elemento
E = A .^ 2     % Cuadrado de cada elemento
```

**Expansión implícita:** MATLAB puede operar arrays de diferentes tamaños si sus dimensiones son compatibles.

```matlab
A = [1 2;
     3 4;
     5 6];

b = [10; 20; 30];

C = A .* b
```

Resultado:

```matlab
C =
    10    20
    60    80
   150   180
```

Cada fila de `A` se multiplica por su elemento correspondiente de `b`.

---

## 5. Funciones sobre arrays

Las funciones matemáticas y estadísticas pueden aplicarse directamente sobre arrays.

| Función | Resultado |
|---|---|
| `sqrt(A)` | Raíz cuadrada de cada elemento |
| `max(x)` | Máximo de un vector |
| `[valor,idx] = max(x)` | Máximo y su posición |
| `size(A)` | Dimensiones del array |

En matrices, `max(A)` obtiene el máximo de cada columna.

**Ejemplo ejecutable:**

```matlab
x = [4 9 2 7];

[valor, idx] = max(x)
raices = sqrt(x)

A = [1 8 3;
     5 2 9];

maximos = max(A)    % [5 8 9]
```

---

## 6. Representación de gráficas

### 6.1. Función plot()

La función `plot()` representa datos en una gráfica bidimensional.

| Sintaxis | Función |
|---|---|
| `plot(X,Y)` | Representa Y frente a X |
| `plot(Y)` | Representa Y frente a los índices 1:n |
| `plot(X,Y,'r')` | Línea roja |
| `plot(X,Y,'--')` | Línea discontinua |
| `plot(X,Y,'o')` | Marcadores circulares |
| `plot(X,Y,'LineWidth',2)` | Grosor de línea 2 |

**Ejemplo ejecutable:**

```matlab
x = 0:0.1:10;
y = sin(x);

plot(x,y)
```

Si solo se proporciona `Y`, MATLAB utiliza los índices de sus elementos como valores del eje X.

### 6.2. Personalización de líneas

Las opciones de formato se escriben entre comillas y pueden combinarse.

| Propiedad | Opciones |
|---|---|
| Color | `r` rojo, `g` verde, `b` azul, `k` negro |
| Línea | `-` continua, `--` discontinua, `:` punteada |
| Marcador | `o` círculo, `s` cuadrado, `*` asterisco, `+` cruz |
| Grosor | `'LineWidth', valor` |

**Ejemplo ejecutable:**

```matlab
x = 0:0.5:5;
y = x.^2;

plot(x,y,'r--o','LineWidth',2)
```

Representa una línea roja discontinua con marcadores circulares y grosor 2.

### 6.3. Varias curvas en una gráfica

| Comando | Función |
|---|---|
| `hold on` | Mantiene la gráfica actual para añadir nuevas curvas |
| `hold off` | Desactiva la superposición de nuevas curvas |

**Ejemplo ejecutable:**

```matlab
x = 0:0.1:10;

plot(x,sin(x),'b')
hold on
plot(x,cos(x),'r--')
hold off
```

### 6.4. Títulos, ejes y leyendas

| Función | Descripción |
|---|---|
| `title("Título")` | Título de la gráfica |
| `xlabel("Texto")` | Etiqueta del eje X |
| `ylabel("Texto")` | Etiqueta del eje Y |
| `legend("A","B")` | Leyenda de las curvas |
| `grid on` | Muestra la cuadrícula |
| `grid off` | Oculta la cuadrícula |

**Ejemplo ejecutable:**

```matlab
x = 0:0.1:10;

plot(x,sin(x),'b','LineWidth',2)
hold on
plot(x,cos(x),'r--','LineWidth',2)
hold off

title("Funciones trigonométricas")
xlabel("Tiempo (s)")
ylabel("Amplitud")
legend("Seno","Coseno")
grid on
```

### 6.5. Histogramas

La función `histogram()` representa la distribución de frecuencias de un conjunto de datos, agrupándolos en intervalos.

**Ejemplo ejecutable:**

```matlab
datos = randn(1,1000);

histogram(datos,20)

title("Distribución de datos")
xlabel("Valor")
ylabel("Frecuencia")
```

El segundo argumento (`20`) establece el número de intervalos del histograma.

---

## 7. Conceptos clave para repasar

- **Variables:** `=` asigna valores; `;` oculta resultados.
- **Operadores lógicos:** `==`, `~=`, `<`, `>` comparan valores; `&` y `|` combinan condiciones.
- **Indexación lógica:** extrae elementos que cumplen una condición.
- **Scripts:** `%%` divide el código en secciones ejecutables.
- **Arrays:** espacios separan columnas y `;` separa filas.
- **Vectores:** `:` controla el paso; `linspace` controla el número de elementos.
- **Indexación:** comienza en 1 y `end` representa el último índice.
- **Dimensiones:** `size` permite conocer el tamaño de un array.
- **Operaciones:** distinguir entre multiplicación matricial (`*`) y elemento a elemento (`.*`).
- **Expansión implícita:** permite operar arrays con dimensiones compatibles.
- **Gráficas:** `plot(X,Y)` representa Y frente a X; `plot(Y)` utiliza índices automáticos.
- **Personalización:** colores, estilos y marcadores se combinan en una cadena de formato.
- **Superposición:** `hold on` mantiene las curvas existentes.
- **Histogramas:** `histogram()` representa frecuencias en intervalos.

---

## 8. Importación y manipulación de tablas

### 8.1. Importación de archivos CSV

MATLAB permite importar archivos `.csv` mediante la herramienta gráfica de importación, que muestra una vista previa de los datos y permite comprobar cómo se interpretan las columnas.

También se pueden importar directamente mediante `readtable()`.

| Comando | Función |
|---|---|
| `readtable("datos.csv")` | Importa un CSV como tabla |
| `data.Variable` | Accede a una columna |
| `data.Variable(i)` | Accede al elemento i de una columna |

**Ejemplo ejecutable:**

```matlab
% Crear CSV de ejemplo
T = table([1;2;3],[10;20;30], ...
    'VariableNames',{'ID','Valor'});
writetable(T,"datos.csv")

% Importar tabla
data = readtable("datos.csv");

valores = data.Valor
elemento = data.Valor(2)  % 20
```

### 8.2. Modificación de tablas

Se pueden añadir nuevas columnas asignando datos a un nombre de variable nuevo.

**Ejemplo ejecutable:**

```matlab
data = table([1;2;3], ...
    'VariableNames',{'ID'});

data.Resultado = [10;20;30];

disp(data)
```

La nueva columna debe tener el mismo número de filas que la tabla.

### 8.3. Indexación de tablas

| Sintaxis | Función |
|---|---|
| `data(i,j)` | Subtabla de una fila y columna |
| `data(x:y,:)` | Filas desde x hasta y |
| `data(:,x:y)` | Columnas desde x hasta y |
| `data(:,end)` | Última columna |
| `data{:,j}` | Extrae los datos de la columna j como array |
| `data.Variable` | Extrae los datos de una columna por nombre |

**Ejemplo ejecutable:**

```matlab
data = table([1;2;3],[10;20;30], ...
    'VariableNames',{'ID','Valor'});

filas = data(1:2,:)
columna = data(:,2)
valores = data{:,2}
```

**Importante:** `()` devuelve una subtabla, mientras que `{}` extrae el contenido de sus variables.

### 8.4. Ordenación y filtrado

La función `sortrows()` permite ordenar una tabla según los valores de una columna.

| Sintaxis | Función |
|---|---|
| `sortrows(data,"Valor")` | Orden ascendente |
| `sortrows(data,"Valor","descend")` | Orden descendente |
| `data(data.Valor > 10,:)` | Filtra las filas que cumplen la condición |

**Ejemplo ejecutable:**

```matlab
data = table([3;1;2],[30;10;20], ...
    'VariableNames',{'ID','Valor'});

ordenada = sortrows(data,"Valor");
filtrada = data(data.Valor > 10,:);
```

La indexación lógica también funciona con tablas, permitiendo seleccionar únicamente las filas que cumplen determinadas condiciones.

---

## 9. Estructuras de control

### 9.1. Condicionales if / else

Permiten ejecutar diferentes bloques de código según se cumpla o no una condición lógica.

**Sintaxis:**

```matlab
if condicion
    % Código si es true
else
    % Código si es false
end
```

- `if` → Evalúa una condición.
- `elseif` → Evalúa otra condición (opcional).
- `else` → Se ejecuta si ninguna condición anterior se cumple (opcional).
- `end` → Finaliza el bloque condicional.

**Ejemplo ejecutable:**

```matlab
x = 8;

if x > 10
    disp("Mayor que 10")
elseif x == 10
    disp("Igual a 10")
else
    disp("Menor que 10")
end
```

Resultado: `Menor que 10`.

### 9.2. Bucles for

Permiten repetir un bloque de código un número determinado de veces.

**Sintaxis:**

```matlab
for i = inicio:fin
    % Código repetido
end
```

Se puede definir el incremento mediante `inicio:paso:fin`.

**Ejemplo ejecutable:**

```matlab
for i = 1:5
    disp(i)
end
```

Muestra los números del 1 al 5.

### 9.3. Recorrer vectores de longitud variable

La función `length()` devuelve la longitud de un vector, permitiendo recorrerlo sin conocer previamente su tamaño.

**Ejemplo ejecutable:**

```matlab
x = [10 20 30 40];

for i = 1:length(x)
    disp(x(i))
end
```

También se puede recorrer directamente el vector:

```matlab
for valor = x
    disp(valor)
end
```

**Importante:** `length()` devuelve la mayor dimensión de un array. Para recorrer vectores es adecuado; para matrices conviene utilizar `size()` según la dimensión deseada.
