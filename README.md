# Analizador Interactivo de Parábolas

> Herramienta didáctica e interactiva para el estudio de la parábola en su forma de vértice $y = a(x-h)^2 + k$, implementada íntegramente en un único archivo HTML, sin dependencias externas.

---

## Índice

1. [Descripción general](#1-descripción-general)
2. [Objetivos](#2-objetivos)
3. [Fundamento matemático](#3-fundamento-matemático)
   - 3.1 [Forma de vértice y forma general](#31-forma-de-vértice-y-forma-general)
   - 3.2 [Interpretación de los parámetros](#32-interpretación-de-los-parámetros)
   - 3.3 [Elementos notables de la parábola](#33-elementos-notables-de-la-parábola)
   - 3.4 [Fórmulas utilizadas](#34-fórmulas-utilizadas)
4. [Características de la aplicación](#4-características-de-la-aplicación)
5. [Guía de uso](#5-guía-de-uso)
   - 5.1 [Sintaxis admitida para la ecuación](#51-sintaxis-admitida-para-la-ecuación)
   - 5.2 [Controles interactivos](#52-controles-interactivos)
   - 5.3 [Ejemplo canónico](#53-ejemplo-canónico)
6. [Arquitectura del código](#6-arquitectura-del-código)
7. [Interfaz y salidas visuales](#7-interfaz-y-salidas-visuales)
8. [Instalación y ejecución](#8-instalación-y-ejecución)
9. [Compatibilidad](#9-compatibilidad)
10. [Limitaciones conocidas](#10-limitaciones-conocidas)
11. [Posibles extensiones](#11-posibles-extensiones)
12. [Referencias](#12-referencias)
13. [Licencia](#13-licencia)

---

## 1. Descripción general

**Analizador Interactivo de Parábolas** es una aplicación web autocontenida que permite al estudiante o docente introducir la ecuación de una parábola vertical en forma de vértice o en forma general, y obtener de forma **síncrona y visual** todos los elementos que la caracterizan: vértice, eje de simetría, dirección de apertura, foco, directriz, parámetro $p$, lado recto con sus extremos, raíces reales (si existen) y tabla de valores.

La aplicación está pensada como recurso pedagógico para los temas de **geometría analítica** y **funciones cuadráticas** en educación media superior o universitaria introductoria. No depende de ninguna biblioteca externa: todo el motor matemático, el parser y el renderizado en `<canvas>` están escritos en JavaScript puro.

---

## 2. Objetivos

- **Comprender** la relación entre la forma algebraica $y=a(x-h)^2+k$ y la geometría de la parábola.
- **Visualizar** el efecto de los parámetros $a$, $h$, $k$ sobre el vértice, la apertura y la posición de la curva.
- **Identificar** los elementos notables (foco, directriz, lado recto, raíces) y sus coordenadas exactas.
- **Relacionar** la representación gráfica con la tabla numérica de valores.
- **Servir** como material complementario en clases presenciales o virtuales, tareas dirigidas y autoestudio.

---

## 3. Fundamento matemático

### 3.1 Forma de vértice y forma general

La ecuación de una parábola con eje vertical puede escribirse en dos formas equivalentes:

**Forma de vértice:**

$$
y = a(x - h)^2 + k, \qquad a \neq 0
$$

**Forma general (o desarrollada):**

$$
y = ax^2 + bx + c, \qquad a \neq 0
$$

La conversión entre ambas se logra completando el cuadrado. Partiendo de la forma general:

$$
h = -\frac{b}{2a}, \qquad k = c - \frac{b^2}{4a}
$$

La aplicación implementa ambas rutas de lectura: si el usuario introduce la forma de vértice, los parámetros se extraen directamente; si introduce la forma general, se aplican las fórmulas anteriores.

### 3.2 Interpretación de los parámetros

| Parámetro | Efecto geométrico |
|-----------|-------------------|
| $a > 0$ | La parábola abre **hacia arriba** (∪). El vértice es un mínimo. |
| $a < 0$ | La parábola abre **hacia abajo** (∩). El vértice es un máximo. |
| $\vert a \vert > 1$ | Apertura más **estrecha** que $y = x^2$. |
| $\vert a \vert < 1$ | Apertura más **ancha** que $y = x^2$. |
| $h$ | **Desplazamiento horizontal** del vértice. El signo dentro del paréntesis es opuesto al desplazamiento: $x+3$ desplaza 3 unidades a la izquierda. |
| $k$ | **Desplazamiento vertical** del vértice. Signo igual al movimiento: $+2$ desplaza 2 unidades hacia arriba. |

> **Observación pedagógica.** El error más frecuente entre estudiantes es interpretar $(x+3)^2$ como un desplazamiento hacia la derecha. La aplicación explica explícitamente esta inversión del signo en el panel *Interpretación de la traslación*.

### 3.3 Elementos notables de la parábola

Sea $V(h,k)$ el vértice y $p = \dfrac{1}{4a}$ el parámetro focal.

| Elemento | Expresión |
|----------|-----------|
| **Vértice** | $V(h, k)$ |
| **Eje de simetría** | $x = h$ |
| **Foco** | $F\left(h,\; k + \dfrac{1}{4a}\right)$ |
| **Directriz** | $y = k - \dfrac{1}{4a}$ |
| **Parámetro focal** | $p = \dfrac{1}{4a}$ |
| **Longitud del lado recto** | $\vert 4p \vert = \dfrac{1}{\vert a \vert}$ |
| **Extremos del lado recto** | $\left(h \pm \dfrac{1}{2a},\; k + \dfrac{1}{4a}\right)$ |
| **Raíces reales** | $x = h \pm \sqrt{-\dfrac{k}{a}}$, si $-\dfrac{k}{a} \geq 0$ |

### 3.4 Fórmulas utilizadas

**Definición focal de la parábola.** El conjunto de puntos $Q(x,y)$ que equidistan del foco $F$ y de la directriz $d$:

$$
\sqrt{(x-h)^2 + \left(y - k - \frac{1}{4a}\right)^2} \;=\; \left|\, y - k + \frac{1}{4a} \,\right|
$$

Al elevar al cuadrado y simplificar se recupera la ecuación $y = a(x-h)^2 + k$.

**Raíces.** Resolviendo $a(x-h)^2 + k = 0$:

$$
(x-h)^2 = -\frac{k}{a} \;\Longrightarrow\; x = h \pm \sqrt{-\frac{k}{a}}
$$

Existen raíces reales si y solo si $\dfrac{k}{a} \leq 0$, es decir, si el vértice está en el eje $X$ o si $a$ y $k$ tienen signos opuestos.

---

## 4. Características de la aplicación

- ✅ Entrada de ecuaciones en **forma de vértice** y **forma general**.
- ✅ Identificación automática de $a$, $h$ y $k$.
- ✅ **Gráfica cartesiana** en `<canvas>` con zoom (rueda del ratón), paneo (arrastre) y rejilla adaptativa.
- ✅ **Auto-encuadre** centrado en los elementos notables, de modo que vértice, foco, directriz y extremos del lado recto siempre son visibles.
- ✅ **Vértice** marcado y etiquetado.
- ✅ **Eje de simetría** como línea punteada.
- ✅ **Foco** y **directriz** con colores diferenciados.
- ✅ **Raíces** resaltadas con halos y etiquetas verdes cuando existen.
- ✅ **Lado recto** dibujado como segmento horizontal que pasa por el foco, con sus **extremos** marcados.
- ✅ **Deslizadores** para modificar $a$, $h$ y $k$ en tiempo real.
- ✅ Panel de **interpretación pedagógica** de la traslación horizontal y vertical.
- ✅ **Tabla de valores** alrededor del vértice (11 puntos).
- ✅ **Sin dependencias externas**: un solo archivo `.html`.

---

## 5. Guía de uso

### 5.1 Sintaxis admitida para la ecuación

| Entrada | Interpretación |
|---------|----------------|
| `(x+3)^2+2` | $y = (x+3)^2 + 2$ |
| `2(x-1)^2-4` | $y = 2(x-1)^2 - 4$ |
| `-(x-2)^2+3` | $y = -(x-2)^2 + 3$ |
| `1/2(x+1)^2-2` | $y = \tfrac{1}{2}(x+1)^2 - 2$ |
| `x^2` | $y = x^2$ |
| `x^2-4x+1` | $y = x^2 - 4x + 1$ (forma general) |
| `-3x^2+6x+1` | $y = -3x^2 + 6x + 1$ (forma general) |

Se aceptan indistintamente `^2` y `²`, así como los signos menos tipográficos `−`, `–`, `—`.

### 5.2 Controles interactivos

| Acción | Efecto |
|--------|--------|
| **Escribir en el campo de ecuación + Enter** | Recalcula y redibuja todo. |
| **Botón «Analizar parábola»** | Igual que Enter. |
| **Deslizadores $a$, $h$, $k$** | Modifican la parábola en tiempo real. |
| **Botón «Reajustar vista»** | Reencuadra la gráfica sobre los puntos clave. |
| **Rueda del ratón sobre la gráfica** | Zoom centrado en el cursor. |
| **Arrastrar sobre la gráfica** | Paneo libre. |
| **Campos «X mínimo / X máximo»** | Fijan el rango horizontal; el vertical se ajusta automáticamente. |

### 5.3 Ejemplo canónico

Introduciendo:

$$
y = (x+3)^2 + 2
$$

la aplicación identifica:

$$
a = 1, \qquad h = -3, \qquad k = 2
$$

y deduce:

- **Vértice:** $V(-3, 2)$
- **Eje de simetría:** $x = -3$
- **Apertura:** hacia arriba, misma que $y = x^2$
- **Foco:** $F\left(-3, \tfrac{9}{4}\right) = (-3, 2.25)$
- **Directriz:** $y = \tfrac{7}{4} = 1.75$
- **Parámetro focal:** $p = \tfrac{1}{4}$
- **Longitud del lado recto:** $\vert 4p \vert = 1$
- **Extremos del lado recto:** $(-3.5,\; 2.25)$ y $(-2.5,\; 2.25)$
- **Raíces:** no existen (la parábola no corta al eje $X$, pues $k/a = 2 > 0$)

La explicación mostrada es:

> Dentro del paréntesis aparece $x + 3$, que es lo mismo que $x - (-3)$. Por eso $h = -3$: el vértice se desplaza **3 unidades hacia la izquierda**. Fuera del paréntesis aparece $+2$, es decir $k = +2$: el vértice se desplaza **2 unidades hacia arriba**.

---

## 6. Arquitectura del código

El archivo `Analizador_Interactivo_Parabolas.html` está organizado en 13 secciones numeradas dentro del bloque `<script>`.

<!-- Aquí puedes agregar la lista de las 13 secciones, por ejemplo:
1. Constantes y utilidades
2. Parser
...
-->

**Decisiones de diseño relevantes:**

- **Parser basado en expresiones regulares** construidas dinámicamente a partir de una constante `NUM` que describe números enteros, decimales o fraccionarios. Se admiten dos gramáticas: forma de vértice y forma general.
- **Auto-encuadre focalizado.** `autoFitView()` no muestrea toda la parábola (lo que dispararía el rango vertical en parábolas muy abiertas), sino que construye una caja a partir de los puntos clave y aplica mitades mínimas para garantizar la visibilidad de los elementos.
- **Banderas `autoX` / `autoY` independientes.** Permiten que el usuario fije el rango horizontal sin perder el autoajuste vertical.
- **Renderizado con `requestAnimationFrame` implícito.** Cada llamada a `render()` ejecuta `draw()` de forma sincrónica; el redibujado por `resize` se limita con un *debounce* de 80 ms.
- **Alta densidad (HiDPI).** El canvas escala por `window.devicePixelRatio` para evitar borrosidad en pantallas Retina.

---

## 7. Interfaz y salidas visuales

La interfaz se divide en ocho bloques:

1. **Barra de entrada** — ecuación, rango $X$, botón *Analizar*.
2. **Deslizadores** — $a$, $h$, $k$ con etiquetas numéricas en vivo.
3. **Gráfica** — canvas de 640 px de alto, con rejilla, ejes, etiquetas y todos los elementos notables.
4. **Forma de vértice** — ecuación reescrita de forma canónica.
5. **Interpretación de la traslación** — texto explicativo dinámico.
6. **Elementos principales** — tarjetas con vértice, eje, apertura, $p$, foco, directriz, raíces, lado recto y extremos.
7. **Tabla de valores** — 11 filas centradas en el vértice, con resaltado de la fila del vértice.
8. **Interpretación geométrica** — definiciones del foco, directriz y lado recto.

**Convenciones de color:**

| Color | Elemento |
|-------|----------|
| 🔵 Azul `#1769aa` | Parábola |
| 🔴 Rojo `#c62828` | Vértice |
| 🟠 Naranja `#d97706` | Foco y directriz |
| 🟣 Púrpura `#8b5cf6` | Eje de simetría |
| 🟢 Verde `#2e7d32` | Raíces |
| 🟡 Ámbar `#f59e0b` | Lado recto y sus extremos |

---

## 8. Instalación y ejecución

No requiere instalación. Basta con descargar el archivo y abrirlo en un navegador:

```bash
git clone https://github.com/jcteacher-lab/analizadordeparabolas.git
cd analizadordeparabolas
# Abrir el archivo con el navegador predeterminado
xdg-open Analizador_Interactivo_Parabolas.html    # Linux
open Analizador_Interactivo_Parabolas.html        # macOS
start Analizador_Interactivo_Parabolas.html       # Windows
```

---

## 9. Compatibilidad

| Navegador | Versión mínima |
|-----------|----------------|
| Chrome / Edge | 88+ |
| Firefox | 85+ |
| Safari | 14+ |
| Opera | 74+ |

El código utiliza `const`, `let`, funciones flecha, template literals, `Math.log10` y `<canvas>` con `getBoundingClientRect()`, todas disponibles en navegadores modernos. No se emplean módulos ES ni *features* experimentales.

---

## 10. Limitaciones conocidas

- Solo se admiten **parábolas con eje vertical** (de la forma $y = f(x)$). Las parábolas con eje horizontal $x = a(y-k)^2 + h$ no están soportadas.
- El parser no admite paréntesis anidados arbitrarios ni expresiones simbólicas (por ejemplo `(x+(1+2))^2`).
- La tabla de valores muestra 11 puntos simétricos alrededor del vértice. No es configurable desde la UI.
- El zoom con la rueda desactiva el auto-encuadre; para recuperarlo hay que pulsar *Reajustar vista*.
- La escala vertical y horizontal son independientes, por lo que la curvatura visual no preserva necesariamente la proporción $1:1$ de la forma geométrica real.

---

## 11. Posibles extensiones

- [ ] Soporte para parábolas horizontales $x = a(y-k)^2 + h$.
- [ ] Exportación de la gráfica a PNG o SVG.
- [ ] Modo «paso a paso» con la transformación $y = x^2 \to y = ax^2 \to y = a(x-h)^2 \to y = a(x-h)^2 + k$.
- [ ] Trazado dinámico de la recta focal y de la directriz con un punto móvil que cumpla la propiedad focal.
- [ ] Internacionalización (ES / EN).
- [ ] Ejercicios autoevaluables generados aleatoriamente.
- [ ] Modo oscuro.

---

## 12. Referencias

- Larson, R., & Edwards, B. (2018). *Cálculo* (10.ª ed.). Cengage Learning. Capítulo sobre secciones cónicas.
- Stewart, J. (2018). *Precálculo: Matemáticas para el cálculo* (7.ª ed.). Cengage Learning.
- Swokowski, E. W., & Cole, J. A. (2011). *Álgebra y trigonometría con geometría analítica* (13.ª ed.). Cengage Learning.
- Apostol, T. M. (1967). *Calculus, Vol. I*. John Wiley & Sons.

---

## 13. Licencia

Este proyecto se distribuye bajo la **Licencia Pública General de GNU v3.0 (GPL-3.0)**.

This program is free software: you can redistribute it and/or modify it under the terms of the GNU General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU General Public License for more details.

You should have received a copy of the GNU General Public License along with this program. If not, see <https://www.gnu.org/licenses/>.
