![https://timasterbox.googlecode.com/svn/trunk/Web/Header.png](https://timasterbox.googlecode.com/svn/trunk/Web/Header.png)

# Descripción #

Kit de herramientas para la construcción de interfaces gráficas para las calculadoras Ti-Nspire. Una colección de componentes (widgets), foco y sistema de eventos para crear aplicaciones para las calculadoras, programada en Lua. Es una versión inicial y puede contener muchos errores.


# Description #

Toolkit for building graphical interfaces for the TI-Nspire. A collection of widgets, focus and system events to create applications for calculators, programmed in Lua. It is an early version and can contain many errors.


---


# Autor del kit de herramientas #

  * José David Abad García (Granveoduendes)

Como buen software de licencia GPL, será bienvenido aquel autor que aporte elementos y mejoras al proyecto.

# Toolkit author #

  * José David Abad García (Granveoduendes)

As a good GPL software, you are welcome, those that contribute elements and improvements to the project.


---


# Licencia #

  * GPL Versión 3.0.
![https://timasterbox.googlecode.com/svn/trunk/Web/License.png](https://timasterbox.googlecode.com/svn/trunk/Web/License.png)


---


# Estado del Kit de Herramientas #

Versión 0.4 Beta 1
(27 de Enero del 2013) El Kit de Herramientas TiMasterBox incluye las siguientes características:


---


# Código Fuente #

El código está a vuestra disposición mediante SVN. Dentro de un archivo .lua y dentro de un archivo .tns

# Dudas y Preguntas #

Podéis dirigiros a la dirección del proyecto timasterbox@gmail.com

# Capturas de pantalla #

![https://timasterbox.googlecode.com/svn/trunk/Web/Screen00.png](https://timasterbox.googlecode.com/svn/trunk/Web/Screen00.png)
![https://timasterbox.googlecode.com/svn/trunk/Web/Screen01.png](https://timasterbox.googlecode.com/svn/trunk/Web/Screen01.png)
![https://timasterbox.googlecode.com/svn/trunk/Web/Screen02.png](https://timasterbox.googlecode.com/svn/trunk/Web/Screen02.png)
![https://timasterbox.googlecode.com/svn/trunk/Web/Screen03.png](https://timasterbox.googlecode.com/svn/trunk/Web/Screen03.png)
![https://timasterbox.googlecode.com/svn/trunk/Web/Screen04.png](https://timasterbox.googlecode.com/svn/trunk/Web/Screen04.png)
![https://timasterbox.googlecode.com/svn/trunk/Web/Screen05.png](https://timasterbox.googlecode.com/svn/trunk/Web/Screen05.png)


---


# Guía rápida de los componentes (Widgets) #

Este kit de herramientas tiene un funcionamiento básico usando líneas. Se crea una clase main de entrada. Pero la magia es la clase MASTERBOX que se encarga de realizar el trabajo engorroso. Esta se encarga de buscar eventos, almacenar los componentes (widgets), manejar el foco y otras operaciones. Mis lenguajes cotidianos son C++ y Java, y Lua, no es un lenguaje donde me encuentre cómodo y es probable que no haya sido, lo estricto al lenguaje que debería ser. Pero he buscado, ante todo, que sea un toolkit limpio y con una mecánica de uso simple. Si sigue este orden le será muy sencillo realizar sus aplicaciones:

  * Declarar la clase main.
  * Crear los widgets a usar.
  * Crear una clase MASTERBOX y añadir los widgets anteriores.
  * Añadir los eventos.

![https://timasterbox.googlecode.com/svn/trunk/Web/Explanation.png](https://timasterbox.googlecode.com/svn/trunk/Web/Explanation.png)

Un ejemplo completo sería este, insertando su código en medio de estos dos bloques, que usted antes deberá copiar del archivo TiMasterBox.lua:

![https://timasterbox.googlecode.com/svn/trunk/Web/ExampleScreen01.png](https://timasterbox.googlecode.com/svn/trunk/Web/ExampleScreen01.png)

```
Main = class()

function Main:init()
    -- Creamos los widgets.
    buttonBox01 = ButtonBox(160, "Launch a Bubble dialog 1")
    buttonBox02 = ButtonBox(160, "Launch a Bubble dialog 2")
   
    -- Añadimos los widgets a la caja maestra.
    MASTERBOX = MasterBox("Example")
    MASTERBOX:addWidget(buttonBox01)
    MASTERBOX:addNewLine()
    MASTERBOX:addWidget(buttonBox02)
    MASTERBOX:addNewLine()
    
    -- Añadimos los eventos.
    MASTERBOX:addEvent(buttonBox01, "ENTER", Main.LaunchBubble1)
    MASTERBOX:addEvent(buttonBox02, "ENTER", Main.LaunchBubble2)
     
    -- Mostramos la pantalla de inicio.
    MASTERBOX:showSplash()
end

function Main:LaunchBubble1()
    MASTERBOX:showBubble("This is a dialogue 1 bubble type", "With his explanations 1.")
end

function Main:LaunchBubble2()
    MASTERBOX:showBubble("This is a dialogue 2 bubble type", "With his explanations 2.")
end

```

![https://timasterbox.googlecode.com/svn/trunk/Web/ExampleScreen02.png](https://timasterbox.googlecode.com/svn/trunk/Web/ExampleScreen02.png)

El sistema de eventos es muy sencillo. Se trata de emparejar un metodo con un tipo de evento. Estos son los eventos que se pueden usar:

| KEY\_PRESS | Se presiona una tecla alfanumérica. Este evento es el que captura la tecla de los LetterComboBox. |
|:-----------|:--------------------------------------------------------------------------------------------------|
| TEXT\_CHANGE | Cambia el texto. Es muy útil para los NumberBox.                                                  |
| ARROWKEYS  | Nos desplazamos con la tecla de cursor. Es muy útil para el TableBox.                             |
| ENTER      | Presionamos la tecla "Enter".                                                                     |

Un ejemplo sería:

```
    MASTERBOX:addEvent(buttonBox01, "ENTER", Example.LaunchBubble)
```

Tenga en cuenta que al haber un widget tipo tabla valoré que era mejor pasar el foco de uno a otro usando la tecla "tab" en vez de usar la tecla de cursor.

También proporciona un diálogo de aviso o alerta que he llamado bubble.

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_Bubble.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_Bubble.png)

### Ejemplo de código ###

```
    MASTERBOX:showBubble("This is a dialogue bubble type", "With his explanations.")
```

### Parámetros ###

| title | Título del diálogo |
|:------|:-------------------|
| description | Descripción del diálogo |


---


## LabelBox ##

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_LabelBox.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_LabelBox.png)

Etiqueta de texto simple.

### Ejemplo de código ###

```
    labelBox01 = LabelBox("LabelBox:")
```

### Parámetros ###

| text | Texto a mostrar en la etiqueta. |
|:-----|:--------------------------------|

## NumberBox ##

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_NumberBox.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_NumberBox.png)

Caja de entrada de números. Únicamente admite números, si por el contrario no es un número la caja cambiará de color a rojo e indicará a la clase maestra de TIMASTERBOX que hay un error de entrada. Esto es muy útil para detectar un fallo, si la caja esta enlazada a un evento de cambio de texto y evitar que produzca un error consultando a TIMASTERBOX si hay un error en algún widget.

### Ejemplo de código ###

```
    numberBox02 = NumberBox(70, "RIGHT")
```

### Parámetros ###

| width | Ancho del componente en píxeles. |
|:------|:---------------------------------|
| align | Alineación del contenido del widget. Siendo: "LEFT", "CENTER" y "RIGHT" |

## LetterComboBox ##

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_LetterComboBox.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_LetterComboBox.png)

Botón de selección de opciones. Se asigna una tecla para el botón y de esta manera evitamos tener el foco del widget y ganamos en velocidad de uso.

### Ejemplo de código ###

```
    letterComboBox04 = LetterComboBox(78, 2, {"Option A", "Option B"}, "A")
```

### Parámetros ###

| width | Ancho del componente en píxeles. |
|:------|:---------------------------------|
| valuesCount | Número de opciones.              |
| values | Lista con las opciones.          |
| handleLetter | Letra asignada para cambiar de opción. |

## CheckBox ##

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_CheckBox.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_CheckBox.png)

Botón de validación.

### Ejemplo de código ###

```
    checkBox05 = CheckBox("Checkbox", true)
```

### Parámetros ###

| text | Texto a mostrar en la caja de validación. |
|:-----|:------------------------------------------|
| checked | Valor de la caja. Siendo: true o false.   |

## ButtonBox ##

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_ButtonBox.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_ButtonBox.png)

Botón. Este botón necesita tener el foco de la aplicación.

### Ejemplo de código ###

```
    buttonBox03 = ButtonBox(68, "ButtonBox")
```

### Parámetros ###

| width | Ancho del componente en píxeles. |
|:------|:---------------------------------|
| text  | Texto a mostrar en la caja de validación. |

## TableBox ##

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_TableBox.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_TableBox.png)

Tabla de resultados. Esta tabla permite mostrar una matriz de resultados y desplazarse por ella.

### Ejemplo de código ###

```
    tableBox06 = TableBox(18, 6, 250, 90, {80, 80, 80, 80, 80, 80}, {"Column A", "Column B", "Column C", "Column D", "Column E", "Column F"}, {"LEFT", "CENTER", "RIGHT", "LEFT", "CENTER", "RIGHT"})
```

### Parámetros ###

| rows | Número de filas de la tabla. |
|:-----|:-----------------------------|
| columns | Número de columnas de la tabla. |
| width | Ancho del componente en píxeles. |
| height | Alto del componente en píxeles. |
| headerWidth | Lista con los anchos de la cabecera. (Debe coincidir al número de columnas) |
| headerText | Lista con los títulos de las cabecera. Si este valor es nulo (nil) no se dibujará la cabecera. |
| headerAlign | Lista con la alineación del contenido de las columnas. Siendo: "LEFT", "CENTER" y "RIGHT" |
| borderless | Por razones estéticas podemos evitar que se dibuje el indicador de foco. Siendo: true o false |

## EscapeKeyBox ##

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_EscapeKeyBox.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_EscapeKeyBox.png)

Botón de la tecla escape. Este widget no necesita tener el foco y es muy útil para salir de un diálogo. Se puede ocultar el widget para ganar limpieza en la pantalla.

### Ejemplo de código ###

```
    escapeKeyBox01 = EscapeKeyBox("Press the escape key to return to the main menu", false)
```

### Parámetros ###

| text | Texto indicativo a mostrar. |
|:-----|:----------------------------|
| visible | Si el widget es visible.    |

## ArrowBox ##

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_ArrowBox.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_ArrowBox.png)

Dibuja una flecha con punta en la izquierda, derecha, ambas o ninguna.

### Ejemplo de código ###

```
    arrowBox01 = ArrowBox("100", true, false)
```

### Parámetros ###

| width | Ancho del componente en píxeles. |
|:------|:---------------------------------|
| leftArrow | Dibujar la punta de la flecha izquierda. Siendo: true o false |
| rightArrow | Dibujar la punta de la flecha derecha. Siendo: true o false |

## LineBox ##

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_LineBox.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_LineBox.png)

Dibuja una linea horizontal con efecto rehundido. A diferencia de un ArrowBox este componente consume el mínimo de altura.

### Ejemplo de código ###

```
    lineBox01 = LineBox("180")
```

### Parámetros ###

| width | Ancho del componente en píxeles. |
|:------|:---------------------------------|

## ParBox ##

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_ParBox.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_ParBox.png)

Es un componente para dibujar textos que ocupen mucho. Este componente divide las palabras y las muestra en un párrafo, siendo esto último transparente al usuario solo especificando el ancho del componente.

### Ejemplo de código ###

```
    parBox01 = ParBox("This is a widget type ParBox, is used for long texts.", 150)
```

### Parámetros ###

| text | Texto a mostrar como párrafo. |
|:-----|:------------------------------|
| width | Ancho del componente en píxeles. |

## CornerButtonBox ##

![https://timasterbox.googlecode.com/svn/trunk/Web/Widget_CornerButtonBox.png](https://timasterbox.googlecode.com/svn/trunk/Web/Widget_CornerButtonBox.png)

Es un botón con foco que se aloja siempre en la esquina. Este componente es muy útil cuando necesitamos crear varios diálogos consecutivos.

### Ejemplo de código ###

```
    cornerButtonBox01 = CornerButtonBox()
```

### Parámetros ###

(Sin parámetros)