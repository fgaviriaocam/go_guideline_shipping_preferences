<!--

Como editar este documento:

- Comenta todos los cambios primero creando una issue de Github.
- Actualice la tabla de contenido a medida que se agreguen o eliminen nuevas secciones.
- Usa tablas, una al lado de la otra para ejemplos de código. Como se explica a continuación.

Ejemplos de código:

Usar 2 espacios para indentar. Debes mantener un estado horizontal en las tablas una al lado de la otra.

Para el código de ejemplo, usar tablas una al lado de la otra, siguiendo el siguiente snippet.

~~~
<table>
<thead><tr><th>Bad</th><th>Good</th></tr></thead>
<tbody>
<tr><td>

```go
CÓDIGO INCORRECTO AQUÍ
```

</td><td>

```go
CÓDIGO CORRECTO AQUÍ
```

</td></tr>
</tbody></table>
~~~

(Necesitas dejar líneas vacías entre los <td> y los ejemplos de códigos para que Markdown pueda interpretarlo correctamente.)

Si necesitas añadir etiquetas o descripciones debajo de los ejemplos de código, debes añadir otra fila antes de la línea </tbody></table>.

~~~
<tr>
<td>DESCRIPCIÓN DE CÓDIGO INCORRECTO</td>
<td>DESCRIPCIÖN DE CÓDIGO CORRECTO</td>
</tr>
~~~

-->

# Guía de estilo de Go en MELI en shipping & preferences


## Índice

- [Guía de estilo de Go en MELI en shipping & preferences](#guía-de-estilo-de-go-en-meli-en-shipping--preferences)
	- [Índice](#índice)
	- [Estilo](#estilo)
		- [Agrupar importaciones](#agrupar-importaciones)
		- [Ordenamiento de importaciones](#ordenamiento-de-importaciones)
		- [Nombre de paquetes](#nombre-de-paquetes)
		- [Nombres de funciones](#nombres-de-funciones)
		- [Importar alias](#importar-alias)
		- [Reducir el anidamiento](#reducir-el-anidamiento)
		- [Declaraciones de variables locales](#declaraciones-de-variables-locales)
		- [Nil es un segmento válido](#nil-es-un-segmento-válido)



## Estilo
El código consistente es sencillo de mantener, sencillo de comprender. Ser consistente en el código, permitirá que las personas entiendan como funciona el programa;cuando se lee código consistente, subconcientemente uno se forma un número de supuestos y expectativas acerca del funcionamiento del código, de esta forma es más fácil y seguro realizarle modificaciones. 

Alguna de las directrices recogidas en este documento son estandares levantados por el bloque de shipping & preferences

### Agrupar importaciones

Go soporta la agrupación de importaciones.

<table>
<thead><tr><th>Incorrecto</th><th>Correcto</th></tr></thead>
<tbody>
<tr><td>

```go
import "a"
import "b"
```

</td><td>

```go
import (
  "a"
  "b"
)
```

</td></tr>
</tbody></table>

### Ordenamiento de importaciones

El estandar actual que se utiliza en el bloque de shipping:

  1. Librerías estandar.
  2. Biblioteca de terceros.
  3. Paquetes de aplicaciones.

<table>
<thead><tr><th>Incorrecto</th><th>Correcto</th></tr></thead>
<tbody>
<tr><td>

```go
import (

	"github.com/mercadolibre/go-meli-toolkit/godog"
	"context"

	"github.com/mercadolibre/shipping-items-api/src/api/model"
	"net/http"

	"github.com/gin-gonic/gin"

	"github.com/mercadolibre/shipping-items-api/src/api/apperror"
	"github.com/mercadolibre/shipping-items-api/src/api/utils"


	"context"
)
```

</td><td>

```go
import (
	"context"
	"net/http"

	"github.com/gin-gonic/gin"
	"github.com/mercadolibre/go-meli-toolkit/godog"

	"github.com/mercadolibre/shipping-items-api/src/api/apperror"
	"github.com/mercadolibre/shipping-items-api/src/api/model"
	"github.com/mercadolibre/shipping-items-api/src/api/utils"
)
```

</td></tr>
</tbody></table>

También se puede presentar este caso:

  1. Librerías estandar.
  2. Biblioteca de terceros.
  3. Librerías de MELI.
  4. Paquetes de aplicaciones.


<table>
<thead><tr><th>Incorrecto</th><th>Correcto</th></tr></thead>
<tbody>
<tr><td>

```go
import (

	"github.com/mercadolibre/go-meli-toolkit/godog"
	"context"

	"github.com/mercadolibre/shipping-items-api/src/api/model"
	"net/http"

	"github.com/gin-gonic/gin"

	"github.com/mercadolibre/shipping-items-api/src/api/apperror"
	"github.com/mercadolibre/shipping-items-api/src/api/utils"


	"context"
)
```

</td><td>

```go
import (
	"context"
	"net/http"

	"github.com/gin-gonic/gin"

	"github.com/mercadolibre/go-meli-toolkit/godog"

	"github.com/mercadolibre/shipping-items-api/src/api/apperror"
	"github.com/mercadolibre/shipping-items-api/src/api/model"
	"github.com/mercadolibre/shipping-items-api/src/api/utils"
)
```

</td></tr>
</tbody></table>


### Nombre de paquetes

Los buenos nombres de paquetes son breves y claros. Son minúsculas, sin under_score o mixedCaps. A menudo son sustantivos simples.

El estilo de nombres típico de otro idioma puede no ser idiomático en un programa Go. Aquí hay dos ejemplos de nombres que pueden tener un buen estilo en otros idiomas pero que no encajan bien en Go.

<table>
<thead><tr><th>Incorrecto</th><th>Correcto</th></tr></thead>
<tbody>
<tr><td>


```go
package computeServiceClient
```

```go
package priority_queue
```


</td><td>

```go
package time
```

```go
package list
```

```go
package http
```

</td></tr>
</tbody></table>

### Nombres de funciones

Recordes que las funciones que inician en mayuscula son funciones que son publicas, las funciones que inician en minuscula son funciones privadas, sin embargo para escribir el nombre la función esta debe ser muy descriptiva.

<table>
<thead><tr><th>Incorrecto</th><th>Correcto</th></tr></thead>
<tbody>
<tr><td>


```go
func GetA
```

</td><td>

```go
func GetLogisticAttributes
```

</td></tr>
</tbody></table>

### Importar alias

Se deben usar alias de importación si el nombre del paquete no coincide con el último elemento de la ruta de importación.

<table>
<thead><tr><th>Incorrecto</th><th>Correcto</th></tr></thead>
<tbody>
<tr><td>


```go
import (
   "github.com/mercadolibre/shipping-items-api/src/api/apperror56shipping"
)
```

</td><td>

```go
import (
    errors "github.com/mercadolibre/shipping-items-api/src/api/apperror56shipping"
)
```

</td></tr>
</tbody></table>


### Reducir el anidamiento

El código debe reducir el anidamiento cuando sea posible al manejar primero los casos de error/condiciones especiales y regresar temprano o continuar el ciclo. Reduzca la cantidad de código anidado en varios niveles.

<table>
<thead><tr><th>Incorrecto</th><th>Correcto</th></tr></thead>
<tbody>
<tr><td>


```go
for _, v := range data {
  if v.Example == 1 {
    v = execute(v)
    if err := v.Func(); err == nil {
      v.Success()
    } else {
      return err
    }
  } else {
    log.Printf("Invalid v: %v", v)
  }
}
```

</td><td>

```go
for _, v := range data {
  if v.Example != 1 {
    log.Printf("Invalid v: %v", v)
    continue
  }

  v = execute(v)
  if err := v.Func(); err != nil {
    return err
  }
  v.Success()
}
```

</td></tr>
</tbody></table>

### Declaraciones de variables locales

``` := ``` Deben usarse declaraciones de variables cortas ( ) si una variable se establece explícitamente en algún valor.


<table>
<thead><tr><th>Incorrecto</th><th>Correcto</th></tr></thead>
<tbody>
<tr><td>


```go
var s = "foo"
```

</td><td>

```go
s := "foo"
```

</td></tr>
</tbody></table>

### Nil es un segmento válido

``` nil ``` es un segmento válido de longitud 0. Esto significa que, no debe devolver un segmento de longitud cero explicito. Utilicemos nil.

<table>
<thead><tr><th>Incorrecto</th><th>Correcto</th></tr></thead>
<tbody>
<tr><td>


```go
if x == "" {
  return []int{}
}
```

</td><td>

```go
if x == "" {
  return nil
}
```

</td></tr>
</tbody></table>
