# Vue.js 3

<br>
<br>

## Creando nuestro primer proyecto

1. Ejecutamos el comando: npm create vite@latest
2. Asignamos nombre al proyecto
3. Seleccionados vue
4. Seleccionamos la opción de preferencia, en este caso JavaScript
5. La forma corta para crear un proyecto y asi evitar los pasos anteriores es: `npm create vite@latest veterinaria -- --template vue`
6. Nos movemos a la carpeta del proyecto desde la terminal
7. Ejecutamos el comando npm install, para instalar las dependencias
8. Ejecutamos el comando npm run dev, para iniciar el ambiente de desarrollo

<br>
<br>

## Single File Components

- Básicamente es el HTML, CSS y JS en un solo archivo.

- Un componente debe tener la extension de .vue

- Un componente usualmente tiene 2 propósitos: <br>
  ser re-utilizable o separar la funcionalidad; si se cumplen ambos es mejor

- Single File Components (SFC) es una convención en la cual un Componente contiene 3 partes:

  ```
  <script>
    Lógica de la aplicación
  </script>
  ```

  ```
  <template>
    Código html que se muestra en pantalla
  <template>
  ```

  ```
  <style>
     Estilos de la pagina
  </style>`
  ```

  <br>
  <br>

## API Styles

- Los componentes de Vue.js se pueden escribir en 2 API'S diferentes: Options API y Composition API

Options API esta disponible desde Vue.js 2 mientras que Composition API desde la version 2.7 y es la recomendada para proyecto con Vue 3

#### Options API

- Se define la lógica de un componente utilizando una sintaxis de objecto

Ejemplo de código usando Options API:

```
export default ({
    components: { Productos },
    data() {
        return {
            productos: [],
            carrito: []
        }
    },
    mounted() {
        fetch('http://fakeurl.com/api')
            .then(res => res.json())
            .then(data => this.productos = data.data)
    },
    methods() {
        agregarCarrito(producto){
            this.carrito.push(producto)
        }
    }
})
```

#### Composition API

- Se definen los componentes utilizando imports (Tanto para funciones de Vue como librerías)
- Se define Composition API añadiendo setup al `<script setup>`
- Composition API tiene dos funciones para reactivada: reactive y ref

Ejemplo de código usando Composition API:

```
import { ref } from 'vue'

const productos = ref([]);
const carrito = ref([]);

const consultarAPI = () => {
  fetch('http://fakeurl.com/api')
    .then(res => res.json())
    .then(data => this.productos = data.data)
};

consultarAPI();

const agregarCarrito(producto){
  this.carrito.push(producto)
}
```

### Cual API utilizar?

- Composition API permitirá tener código mas re-utilizable
- Options API es recomendado si tu proyecto utilizara pequeñas piezas de Vue o escenarios no tan complejos, también si prefieres el estilo orientado a objectos
- Composition API es recomendado si todo tu proyecto sera hecho con Vue.js
- Composition API es recomendado si tu proyecto usa la version 3 en adelante de Vue.js

<br>
<br>

## State en Vue.js

- El state determina la situación actual de nuestra aplicación
- El State no es siempre igual; tienda a cambiar en base a las interacciones del usuarios(clicks, formularios, navegar en diferentes paginas)
- Debido a que el state tiende a cambiar; Vue.js tiene un par de funciones que nos permitirán declararlo y sobretodo identificar cuando el state ha cambiado. Las dos son funciones son `ref` y `reactive`; ambas se importan de vue.
- Una vez que el state cambie el DOM se actualizara automáticamente

### State con Reactive

- Es un objecto
- Para acceder a las propiedades de reactive se utiliza .
- Para modificar un objecto de reactive, se accede por el punto a la variable y se iguala al valor asignado `libro.nombre = 'Go desde cero';`
- la diferencia entre reactive y ref, es que reactive siempre sera un objecto mientras que ref, podrá ser lo que tu desees.

Ejemplo de código con Reactive

```
import { reactive } from 'vue';

const libro = reactive({
    disponible: true,
    nombre: 'Cuentos Macabros',
    precio: 189.000,
    ISBN: '0-7645-2641-3'
})

console.log(libro.disponible);
console.log(libro.nombre);
console.log(libro.precio);
```

### State con Ref

- Cuando declaras un Ref deberás color un valor inicial
- Te permite usar arreglos, objectos, booleanos, strings
- Para acceder a las propiedades de ref se usa .value
- Ref usa Proxy, un proxy es un intermediario para otro objecto, ee cual puede interceptar y redefinir operaciones que se permiten o se pueden usar en ese objecto, arreglo. por ejm, push, filter ...etc
- Para modificar un ref, se debe escribir .value y se iguala al valor asignado por ejm: libros.value = `"Cuentos Macabros"`.

```
import { ref } from 'vue';

const libro = ref("");

libro.value = "Cuentos Macabros";

console.log(libro.value);
```

<br><br>

## Directivas en Vue.js

- Son básicamente atributos HTML con funcionalidad de JavaScript
- Influencias por AngularJs las directivas de Vue.js es lo que llevan a este framework a un nuevo nivel.
- Las directivas en Vue.js siempre inician con v- y se colocan como atributos HTML

Directivas de Vue.js:

```
v-text      v-bind
v-html      v-model
v-show      v-slot
v-if        v-pre
v-else      v-once
v-else-if   v-memo
v-for       v-cloak
v-on
```

<br><br>

## Props en Vue.js

- Los props sirven para pasar información entre componentes; estos pueden ser datos estáticos o reactivos
- En casos de querer pasar funciones se recomienda que sea por medio de un Component Event
- Los Props nunca deben modificar el state en el componente hijo

```
<script setup>
const props = defineProps({
    guitarra: {
        type: Object,
        required: true
    }
});
</script>
```

<br><br>

## Eventos

- Presionar un botón o link; llenar un formulario, son algunos de las acciones del DOM mas comunes
- Vue hace muy sencillo interactuar con ciertos eventos con la directa v-on

### Tipos de eventos

- En Vue.js existen dos tipos de eventos: inline Handlers y Method Handlers.

#### Inline Handlers

- Son para tareas muy sencillas como cambiar a dark o light mode

```
<button
    type="button"
    class="btn btn-dark w-100"
    v-on:click="numero++">
    Agregar al Carrito
</button>
```

#### Method Handlers

- Son muy útiles cuando realizas diferentes acciones como validar los datos de un formulario

```
<button
    type="button"
    class="btn btn-dark w-100"
    v-on:click="incrementar()">
    Agregar al Carrito
</button>
```

<br><br>

## Components Events

- @click y @submit son eventos muy comunes en nuestros proyectos, debido a que el State de un proyecto no puede cambiarse en los Props lo ideal es registro un evento en el componente

- Por default un evento que se asocia a un botón o formulario buscara una función en ese componente; pero para comunicarlo con el componente padre debemos utilizar una sintaxis especial llamada emit y registrar un component event o evento del componente

Para usar una función desde el componente padre:

1. debemos definir el nombre de la función con defineEmits en el archivo del componente
2. El evento a ejecutar(@click) asignamos el nombre la función declarada en defineEmits con el método $emit('');

```
<script setup>

defineEmits(['incrementar']);
</script>


<template>
  <button
      type="button"
      class="btn btn-dark w-100"
      @click="$emit('incrementar')"
      Agregar al Carrito
  </button>
</template>

```

3. Declaramos la función en el componente padre.
4. Para ejecutar la función dentro del componente, ejecutamos el evento con @nombre_de_la_funcion y le asignamos el nombre de la función declarada en el script

```
<script setup>
const incrementar = () => {
    alert("Hola");
}
</script>

<template>
  <Guitarra
    v-for="guitarra in guitarras"
    v-bind:guitarra="guitarra"
    @incrementar="incrementar"
  />
</template>

```

5. Si queremos pasar un dato de un componente hijo a un padre, le agregamos el valor desde el método $emit: `@click="$emit('agregar-carrito', guitarra)"`
   <br><br>

## Computed

- Computed se encarga de mantener la reactivada
- Se utiliza para definir propiedades calculadas en un componente. Las propiedades calculadas son propiedades que se derivan de una o más propiedades existentes y se recalculan automáticamente cada vez que cambian las propiedades de las que dependen. Esto es útil cuando se necesita realizar algún cálculo o transformación en función de los datos existentes en el componente, pero no se desea que el cálculo se realice manualmente en cada cambio de datos.

```
import { computed } from 'vue';

const totalPagar = computed(() => {
    return props.carrito.reduce((total, producto) => total + (producto.cantidad * producto.precio), 0);
});
```

<br><br>

## Watch

- Es una función que le pasamos una dependencia, va a estar escuchando o viendo cierto state y cuando ese cambie va a ejecutar una función

- Watch recibe opciones, el cual es el objecto de configuración, en este tenemos una propiedad deep, que al estar en true, se encargar de validar todos los atributos del objecto, para validar si hay un cambio o no

```
import { watch } from 'vue';

watch(carrito, () => {
    guardarLocalStorage();
}, {
    deep: true
});
```
