# 🧭 Primeros pasos: del dato a la decisión

**Actividad introductoria guiada de Data Analytics para personas sin experiencia previa en tecnología.**

En esta actividad vas a recorrer, con un caso real, el viaje completo de un dato: **cargarlo, limpiarlo, hacerle preguntas, dibujarlo y reflexionar sobre lo que nos dice y lo que no**.

No necesitas saber programar. Todo el código está escrito y explicado. Tu papel es ejecutarlo, observar qué ocurre y pensar.

---

## 📚 Índice

1. [Antes de empezar: prepárate en 10 minutos](#-antes-de-empezar-prepárate-en-10-minutos)
2. [Qué vas a aprender](#-qué-vas-a-aprender)
3. [Los datos](#-los-datos)
4. [Estructura del proyecto](#-estructura-del-proyecto)
5. [Paso a paso: cómo ejecutar el proyecto](#-paso-a-paso-cómo-ejecutar-el-proyecto)
6. [Un concepto para el primer día: agrupar y resumir](#-un-concepto-para-el-primer-día-agrupar-y-resumir-group-by)
7. [Errores frecuentes y cómo resolverlos](#-errores-frecuentes-y-cómo-resolverlos)
8. [Resumen del análisis](#-resumen-del-análisis)
9. [Conclusiones y limitaciones](#-conclusiones-y-limitaciones)

---

## ☕ Antes de empezar: prepárate en 10 minutos

Lee esta sección **antes de la sesión práctica**. Así, cuando abras el notebook, ya sabrás de qué va todo y podrás dedicar la sesión a hacer, no a escuchar.

### La pregunta que vamos a explorar

> 🤔 Si tuvieras que puntuar tu vida del 0 al 10, donde 0 es la peor vida posible y 10 la mejor, ¿qué número darías? ¿Qué has tenido en cuenta: el dinero, la salud, tu gente, tu libertad…?

Cada año se hace esa misma pregunta a miles de personas en todo el mundo. Con las respuestas se publica el **Informe Mundial de la Felicidad** (*World Happiness Report*). Vamos a usar sus datos de **2016** para responder a una pregunta sencilla:

**¿Qué tienen en común los países donde la gente valora mejor su vida? ¿Es solo cuestión de dinero?**

### Seis palabras que vas a encontrar

| Palabra | Qué significa | Ejemplo cotidiano |
|---|---|---|
| **Dataset** | Un conjunto de datos sobre un mismo tema | Un fichero de clientes de una tienda |
| **Fila** | Un registro: aquí, **un país** | Una ficha del fichero |
| **Columna** | Una característica que se apunta en cada fila | El campo «teléfono» de cada ficha |
| **DataFrame** | Una tabla dentro de Python, con filas y columnas | Una hoja de Excel que manejamos con código |
| **Valor nulo** | Una casilla vacía: no sabemos el dato. **No es un cero** | Una pregunta de un formulario que alguien dejó en blanco |
| **SQL** | Un lenguaje para hacer preguntas precisas a una base de datos | Pedirle a un bibliotecario «los libros de cocina posteriores a 2010» |

### Las herramientas

- **Google Colab:** una página web de Google donde se puede abrir y ejecutar el notebook **sin instalar nada**, solo con una cuenta de Google. **Es lo que usaremos en clase.**
- **Visual Studio Code (VS Code):** un programa que se instala en el ordenador para trabajar con código. **Este proyecto se desarrolló aquí**, y es la opción para quien quiera trabajar sin conexión o seguir practicando por su cuenta.
- **Python:** el lenguaje de programación.
- **Jupyter Notebook (`.ipynb`):** un cuaderno que mezcla explicaciones y trozos de código que puedes ejecutar uno a uno.
- **Pandas y NumPy:** cajas de herramientas de Python para trabajar con tablas y números.
- **SQLite:** una pequeña base de datos que viene incluida con Python.
- **Matplotlib:** una caja de herramientas para dibujar gráficos.

### Qué tendrás al terminar

- Una tabla revisada y guardada (`data/clean_data.csv`).
- Las respuestas a tres preguntas hechas con SQL.
- Tres gráficos que podrás interpretar y explicar.
- Tus propias conclusiones… y una lista de lo que estos datos **no** pueden decir.

> 🤔 **Para pensar antes de la sesión:** ¿crees que los países más ricos son siempre los más felices? Apunta tu respuesta. Al final la compararemos con lo que digan los datos.

---

## 🎯 Qué vas a aprender

Al terminar la actividad serás capaz de:

1. **Cargar** una tabla de datos con Python y describir qué contiene.
2. **Revisar su calidad**: buscar casillas vacías, filas repetidas y valores extraños, y **justificar** cada decisión.
3. **Hacer preguntas** a los datos con SQL usando `JOIN`, `GROUP BY`, `WHERE` y `HAVING`.
4. **Elegir el gráfico adecuado** para cada pregunta y leerlo con espíritu crítico.
5. **Contar lo que has descubierto** en lenguaje sencillo, sin confundir «van juntos» con «uno causa el otro».

---

## 🌍 Los datos

| | |
|---|---|
| **Nombre** | World Happiness Report 2016 |
| **Publicado por** | Red de Soluciones para el Desarrollo Sostenible de Naciones Unidas (UN SDSN), en Kaggle |
| **Enlace** | [kaggle.com/datasets/unsdsn/world-happiness](https://www.kaggle.com/datasets/unsdsn/world-happiness) (archivo `2016.csv`) |
| **Origen de las respuestas** | Encuesta Gallup World Poll |
| **Licencia** | CC0: dominio público, según la ficha del dataset en Kaggle |
| **Copia en este proyecto** | `data/raw_data.csv` (sin modificar) |

### Qué sabemos por la documentación

- La **puntuación de felicidad** es la media de lo que responden las personas de cada país cuando se les pide valorar su vida del 0 al 10. En la mayoría de países se encuesta a unas 1.000 personas al año.
- El informe intenta **explicar** esa puntuación con seis factores: economía, apoyo social, salud, libertad, confianza (ausencia de corrupción) y generosidad.
- Los valores de esos factores **no son medidas directas**. Indican cuánto ayuda cada factor a explicar la puntuación, comparando con **Distopía**, un país imaginario que tiene los valores más bajos observados en cada factor.

### Qué hemos comprobado nosotras en el archivo

- **157 filas** (una por país) y **13 columnas**.
- **0 casillas vacías** y **0 filas repetidas**.
- **6 ceros**, uno en cada factor. No son errores: corresponden al país que coincide con Distopía en ese factor.
- **3 empates** en el ranking (países con la misma puntuación).

---

## 🗂️ Estructura del proyecto

```
primeros-pasos-dato-decision/
├── README.md              ← esta guía
├── requirements.txt       ← lista de librerías necesarias (con sus versiones)
├── .gitignore             ← archivos que no se suben a GitHub
├── data/
│   ├── raw_data.csv       ← datos originales, sin tocar
│   └── clean_data.csv     ← datos revisados (los genera el notebook)
└── notebooks/
    ├── 01_primeros_pasos_del_dato_a_la_decision.ipynb         ← actividad para VS Code
    └── 01_primeros_pasos_del_dato_a_la_decision_colab.ipynb   ← la misma actividad, para Google Colab
```

El notebook está organizado en cuatro etapas:

| Etapa | Qué haces | Qué aprendes |
|---|---|---|
| **A · Cargar y limpiar** | Abrir la tabla y revisarla paso a paso | Que limpiar es comprobar, entender y decidir |
| **B · Preguntar con SQL** | Crear una base de datos y hacerle 3 preguntas | `JOIN`, `GROUP BY`, `WHERE` y `HAVING` |
| **C · Visualizar** | Dibujar 3 gráficos | Qué gráfico usar para cada pregunta |
| **D · Reflexionar** | Leer y debatir las conclusiones | Separar lo que los datos dicen de lo que no |

---

## 🛠️ Paso a paso: cómo ejecutar el proyecto

Puedes hacer la actividad de dos formas. Hay **un notebook para cada una**, con el mismo contenido. Solo cambia de dónde lee el archivo de datos.

| | 🌐 Opción 1 · Google Colab | 💻 Opción 2 · Visual Studio Code |
|---|---|---|
| **Cuándo usarla** | En clase | En tu ordenador, sin depender de internet |
| **Qué necesitas** | Navegador y cuenta de Google | Instalar Python, VS Code y las librerías |
| **Notebook** | `…_colab.ipynb` | `01_primeros_pasos_del_dato_a_la_decision.ipynb` |
| **Preparación** | Baja: abrir un enlace y subir el CSV | Media: unos 15 minutos la primera vez |
| **Dónde se guardan tus cambios** | En tu Google Drive, si guardas una copia | En tu ordenador |

> Este proyecto se **desarrolló y probó en Visual Studio Code**. En clase usaremos **Google Colab**, porque no exige instalar nada y todo el grupo empieza en las mismas condiciones.

### 🌐 Opción 1 · Google Colab (la que usaremos en clase)

Usa el notebook **`01_primeros_pasos_del_dato_a_la_decision_colab.ipynb`**. Es igual que el de VS Code, pero preparado para leer el CSV que tú subes a Colab. Viene **sin resultados**, para que los descubras tú al ejecutar cada celda. La versión de VS Code se guarda con los resultados visibles, como referencia para comprobar los tuyos.

1. Abre el notebook con tu cuenta de Google:
   **[Abrir la versión Colab](https://colab.research.google.com/github/MariaIsaDurango/primeros-pasos-dato-decision/blob/main/notebooks/01_primeros_pasos_del_dato_a_la_decision_colab.ipynb)**
2. Pulsa **Archivo → Guardar una copia en Drive**. Así trabajas sobre tu propia copia y no pierdes los cambios.
3. Descarga a tu ordenador el archivo [`data/raw_data.csv`](data/raw_data.csv) de este repositorio (botón **Download raw file**).
4. En Colab, pulsa el icono de carpeta 📁 de la barra izquierda y arrastra ahí `raw_data.csv`.
5. Ejecuta las celdas con **Shift + Enter**, una a una y en orden.

> 💡 Si Colab avisa de que el notebook no lo ha creado Google, pulsa **Ejecutar de todos modos**. Ese aviso aparece siempre con los notebooks que vienen de GitHub.

> ⚠️ Los archivos que subes a Colab **se borran al cerrar la sesión**. Si vuelves otro día, repite el paso 4.

### 💻 Opción 2 · Visual Studio Code (como se desarrolló el proyecto)

#### Lo que necesitas instalado

- [Python 3.12](https://www.python.org/downloads/) o una versión superior. En Windows, marca la casilla **«Add Python to PATH»** durante la instalación.
- [Visual Studio Code](https://code.visualstudio.com/), con las extensiones **Python** y **Jupyter** (búscalas en el icono de cuadraditos de la barra izquierda).
- [Git](https://git-scm.com/downloads), solo si vas a descargar el proyecto con `git clone`.

Para comprobar qué tienes, abre una terminal y escribe:

```bash
python --version
git --version
```

Si aparece un número de versión, está instalado.

#### 1. Descargar el proyecto

**Opción A (sin Git):** en la página del repositorio en GitHub, pulsa el botón verde **Code → Download ZIP**. Descomprime el archivo en tu Escritorio.

**Opción B (con Git):** abre una terminal y escribe:

```bash
git clone https://github.com/MariaIsaDurango/primeros-pasos-dato-decision.git
```

#### 2. Abrir la carpeta en VS Code

Abre VS Code y ve a **File → Open Folder…** (Archivo → Abrir carpeta). Elige la carpeta `primeros-pasos-dato-decision`.

> ⚠️ Abre la **carpeta del proyecto completa**, no el notebook suelto. Así verás toda la estructura en el panel izquierdo y la terminal se abrirá en el sitio correcto.

#### 3. Crear tu entorno virtual e instalar las librerías

Un **entorno virtual** es como una mochila exclusiva para este proyecto: lo que instales dentro no se mezcla con otros proyectos de tu ordenador.

En VS Code, abre la terminal con **Terminal → New Terminal** y ejecuta, línea a línea:

```bash
python -m venv .venv
```

Después activa la mochila. El comando depende de tu terminal:

| Terminal | Comando |
|---|---|
| Git Bash (Windows) | `source .venv/Scripts/activate` |
| PowerShell (Windows) | `.venv\Scripts\Activate.ps1` |
| macOS / Linux | `source .venv/bin/activate` |

Sabrás que ha funcionado porque la línea de la terminal empezará por `(.venv)`. Por último, instala las librerías de la lista:

```bash
python -m pip install -r requirements.txt
```

Tardará uno o dos minutos y terminará con `Successfully installed …`.

#### 4. Abrir y ejecutar el notebook

1. En el panel izquierdo, abre `notebooks/01_primeros_pasos_del_dato_a_la_decision.ipynb` (la versión **sin** `_colab`).
2. Arriba a la derecha, pulsa **Select Kernel → Python Environments** y elige **`.venv`**.
3. Haz clic en la primera celda de código y pulsa **Shift + Enter**. La celda se ejecuta y pasas a la siguiente.
4. Avanza **en orden, de arriba abajo**, leyendo cada explicación antes de ejecutar.

### ✅ Cómo saber que ha funcionado (en las dos opciones)

Verás la tabla de países en el Paso 1, tres tablas de resultados en la Etapa B y tres gráficos en la Etapa C. La última celda dirá `Fin de la actividad 🎉`.

---

## 💡 Un concepto para el primer día: agrupar y resumir (`GROUP BY`)

Imagina que al final del mes vacías la cartera y tienes **un montón de tiques de compra** mezclados. Quieres saber cuánto has gastado en comida, en transporte y en ocio.

¿Qué haces? Seguramente esto:

1. **Separas los tiques en montones**, uno por cada tipo de gasto.
2. **Sumas** cada montón por separado.
3. Te queda **una línea por montón**: «Comida: 230 €, Transporte: 45 €, Ocio: 60 €».

Eso es exactamente lo que hace `GROUP BY` en SQL. En nuestro proyecto, los «tiques» son 157 países y los «montones» son las regiones del mundo:

```sql
SELECT region,
       COUNT(*)         AS num_paises,      -- ¿cuántos tiques hay en cada montón?
       AVG(puntuacion)  AS felicidad_media  -- ¿cuál es la media de cada montón?
FROM felicidad
GROUP BY region;                            -- separa los países en montones por región
```

El resultado ya no tiene 157 filas, sino **una por región**. A esto se le llama **agregación**: resumir muchos datos en uno solo por grupo (contar, sumar, hacer la media…).

> ⚠️ **El límite de la analogía:** al agrupar, los detalles individuales desaparecen. Igual que el total de «Comida» no te dice si compraste fruta o pasteles, la felicidad media de una región no te dice nada de cada país por separado.

> 🤔 **Pruébalo:** en tu vida diaria, ¿qué otra cosa agrupas para resumirla? (Tus horas de la semana por actividad, tus fotos por mes…)

---

## 🚑 Errores frecuentes y cómo resolverlos

Equivocarse es parte de aprender. Estos dos errores son muy habituales al empezar. Si te pasan, no has roto nada.

### Error 1 · «No encuentro el archivo» (`FileNotFoundError`)

**Lo que verás:**

```
FileNotFoundError: [Errno 2] No such file or directory: 'data/raw_data.csv'
```

**Qué significa:** Python ha buscado el archivo en un sitio y no estaba allí. Es como si le dices a alguien «las llaves están en el cajón de la cocina» y las tienes en el del dormitorio: las llaves existen, pero la indicación es incorrecta.

**Por qué ocurre en este proyecto (VS Code):** el notebook vive en la carpeta `notebooks/` y los datos en `data/`. Por eso la ruta empieza por `../`, que significa «sal primero de esta carpeta». Si escribes `data/raw_data.csv` sin el `../`, Python busca una carpeta `data` **dentro** de `notebooks`, y no existe.

**Cómo resolverlo:**

1. **En Google Colab:** comprueba que estás usando la versión `_colab` y que `raw_data.csv` aparece en el panel 📁. Si cerraste la sesión, vuelve a subirlo.
2. **En VS Code:** comprueba que la ruta del código es `"../data/raw_data.csv"`.
3. Comprueba que el archivo está realmente en la carpeta `data`, con ese nombre exacto (mira el panel izquierdo de VS Code o el icono de carpeta 📁 de Colab).
4. **En VS Code:** comprueba que abriste la **carpeta del proyecto** (Paso 2) y que el notebook está dentro de `notebooks/`.

### Error 2 · Olvidar las comillas en SQL

**Lo que verás**, si escribes `WHERE region = Latin America and Caribbean`:

```
DatabaseError: Execution failed on sql '...': near "America": syntax error
```

**Qué significa:** para SQL, una palabra sin comillas es el **nombre de una columna** o una **instrucción**. Lee `Latin`, después `America`… y se pierde. Las comillas le dicen «esto es un texto literal, búscalo tal cual». Es como al buscar en Google: si quieres la frase exacta, la pones entre comillas.

**Cómo resolverlo:**

1. Escribe los textos **entre comillas simples**: `WHERE region = 'Latin America and Caribbean'`.
2. Revisa que el texto coincida **exactamente** con el de la tabla: mayúsculas, espacios y la palabra `and` incluidos.
3. Los **números no llevan comillas**: `WHERE puntuacion > 6`.

> 💡 **Consejo de formadora:** cuando aparezca un error, lee primero la **última línea** del mensaje en rojo. Casi siempre dice qué ha pasado.

---

## 📊 Resumen del análisis

### Tres preguntas en SQL

| # | Pregunta | Qué se practica | Respuesta corta |
|---|---|---|---|
| 1 | ¿Qué regiones del mundo son, de media, más felices? | `JOIN` + `GROUP BY` | Australia y Nueva Zelanda y América del Norte encabezan, pero con solo 2 países cada una. África subsahariana tiene la media más baja (4,14) |
| 2 | ¿Qué países de América Latina y el Caribe superan la media mundial (5,38)? | `WHERE` | 21 de 24. Costa Rica es la primera (puesto 14 del mundo) |
| 3 | En las regiones con al menos 5 países, ¿más economía significa más felicidad? | `GROUP BY` + `HAVING` | En general sí, pero América Latina y el Caribe es 5.ª en aporte económico y 2.ª en felicidad |

Para practicar el `JOIN` se crea una tabla auxiliar, `regiones`, que traduce al español el nombre de cada región. Las dos tablas se unen por la columna `region`.

### Tres gráficos

| # | Gráfico | Pregunta que responde | Por qué este tipo |
|---|---|---|---|
| 1 | Barras horizontales | ¿Qué regiones son más felices de media? | Compara categorías con nombres largos, que se leen mejor en horizontal |
| 2 | Dispersión (puntos) | ¿Van juntas la economía y la felicidad? | Muestra la relación entre dos números, país a país |
| 3 | Histograma | ¿Cómo se reparten las puntuaciones? | Agrupa 157 países en tramos y enseña dónde se concentran |

---

## 💬 Conclusiones y limitaciones

### Lo que hemos descubierto

1. **Hay grandes diferencias entre regiones.** Entre la región con mayor media y la de menor media hay más de 3 puntos sobre 10.
2. **La economía y la felicidad suelen ir de la mano** (correlación de 0,79)… **pero el dinero no lo explica todo.** América Latina y el Caribe es la segunda región más feliz entre las de al menos 5 países, aunque la economía le aporte menos que a otras.
3. **América Latina y el Caribe destaca en positivo:** 21 de sus 24 países superan la media mundial. También es la región donde los seis factores del informe dejan **más parte sin explicar**.

### ¿A quién le puede servir?

- A **organizaciones sociales y de cooperación**, para recordar que el bienestar no depende solo del dinero.
- A **responsables de políticas públicas**, como punto de partida para preguntarse qué mejora la vida de las personas además del crecimiento económico.
- A **docentes y estudiantes**, como un caso real para aprender a analizar datos con espíritu crítico.

### ⚠️ Lo que estos datos NO dicen

- **Es una foto de un solo año** (el informe de 2016). No sabemos si las diferencias se mantienen hoy.
- **Una media por país esconde desigualdades** entre zonas, edades o niveles de ingresos dentro del mismo país.
- **Que dos cosas vayan juntas no significa que una cause la otra.** El propio informe advierte de que sus factores muestran relaciones, no causas.
- **«Felicidad» aquí es una sola pregunta de encuesta**: cómo valora la gente su vida del 0 al 10, respondida por una muestra de personas. No mide todo lo que es una vida plena.

> 🤔 **Vuelve a tu respuesta del principio:** ¿creías que los países más ricos son siempre los más felices? ¿Ha cambiado tu opinión?

---

*Proyecto realizado como prueba técnica para el puesto de Formador/a Asistente de Data Analytics en Somos F5.*
