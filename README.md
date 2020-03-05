> El siguiente contenido fue elaborado por [@_nhsz](https://twitter.com/_nhsz) como guía para las clases de [undefined school](https://twitter.com/undefinedSchool)
> Son bienvenidos los _issues_ y _PRs_ para mejorar el contenido, corregir errores, etc. 

> 👉 Si te resultó útil, **se agradece que lo compartas para que le llegue a más gente!**

# ![Redux](https://i.imgur.com/3Y4n7hz.png)

## Notas relacionadas

### `react`

- [**Principios**](https://github.com/undefinedschool/notes-react-principles/)
- [**Conceptos Básicos**](https://github.com/undefinedschool/notes-react-basics)

## Contenido

- [Intro](https://github.com/undefinedschool/notes-redux#intro)
- [Por qué usar Redux?](https://github.com/undefinedschool/notes-redux#por-qu%C3%A9-usar-redux)
- [Conceptos](https://github.com/undefinedschool/notes-redux#conceptos)
  - [Inmutabilidad](https://github.com/undefinedschool/notes-redux#inmutabilidad)
  - [Actions](https://github.com/undefinedschool/notes-redux#actions)
    - [Utilizar _Action_ `types` constantes](https://github.com/undefinedschool/notes-redux#utilizar-action-types-constantes)
    - [Action creators](https://github.com/undefinedschool/notes-redux#action-creators)
  - [Reducer](https://github.com/undefinedschool/notes-redux#reducer)
  - [Store](https://github.com/undefinedschool/notes-redux#store)
    - [Accediendo al _state_](https://github.com/undefinedschool/notes-redux#accediendo-al-state)
    - [Actualizando el _state_](https://github.com/undefinedschool/notes-redux#actualizando-el-state)
    - [Escuchando cambios en el _state_](https://github.com/undefinedschool/notes-redux#escuchando-cambios-en-el-state)
- [Flujo de datos unidireccional (one-way data flow)](https://github.com/undefinedschool/notes-redux#flujo-de-datos-unidireccional-one-way-data-flow)  
- [Redux Toolkit](https://github.com/undefinedschool/notes-redux#redux-toolkit)
- [Redux vs Context API](https://github.com/undefinedschool/notes-redux#redux-vs-context-api)
- [Redux vs Hooks](https://github.com/undefinedschool/notes-redux#redux-vs-hooks)

---

## Intro

[Redux](https://redux.js.org/) es una librería (biblioteca) que funciona como [_State_](https://github.com/undefinedschool/notes-react-basics#state) _Container_ o _State Manager_ (nos permite manejar el estado de los componentes) para nuestras aplicaciones, que funciona independientemente del framework o librería que utilicemos para manejar la _vista_<sup id="cite_ref-1"><a href="#cite_note-1">[1]</a></sup>.

Lo que hace básicamente Redux es proveernos de **un gran objeto que contiene el estado de cada componente de nuestra aplicación** (nos permite lidiar con el estado de toda la aplicación de una forma centralizada), al cual cada componente puede acceder.

**Redux nos garantiza que este objeto es [_inmutable_](https://github.com/undefinedschool/notes-redux#inmutabilidad), es decir, no va a cambiar**, ya que no modifica el _state_ actual cuando se produce algún cambio, sino que retorna una nueva copia de este objeto con los cambios requeridos, haciendo que el _state_ de nuestra aplicación sea más fácil de manejar, entender, debuggear y predecible<sup id="cite_ref-2"><a href="#cite_note-2">[2]</a></sup><sup id="cite_ref-3"><a href="#cite_note-3">[3]</a></sup>. 

> 👉 En este sentido, Redux se comporta como una _función pura_, según el paradigma funcional.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Por qué usar Redux?

Recordemos que React ya nos provee una forma de manejar el [_state_](https://github.com/undefinedschool/notes-react-basics#state) de cada componente, de forma local.

**De hecho, la mayoría de las veces, [probablemente no necesitemos una solución como Redux](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)**, ya que podemos estar agregando complejidad innecesaria. 

Qué beneficio nos trae entonces utilizar Redux por sobre el _local state_?

_Levantar_ el _state_ en el árbol de [componentes](https://github.com/undefinedschool/notes-react-basics#react-component) funciona en casos simples, pero **en aplicaciones más complejas podemos terminar encontrándonos moviendo el state continuamente entre componentes, a través de las [_props_](https://github.com/undefinedschool/notes-react-basics#props), dificultando el mantenimiento y seguimiento del flujo de datos en nuestra aplicación**. 

**Un mejor enfoque podría ser utilizar un _store_ externo, global** (un gran objeto que funcione algo así como una variable global, al que cualquier componente pueda acceder, con la diferencia de que en este caso, es [_inmutable_](https://github.com/undefinedschool/notes-redux#inmutabilidad)) y esto es justamente lo que propone Redux.

Por lo tanto, sólo deberíamos usar Redux si manejar el state local de los componentes de React se vuelve lo suficientemente tedioso<sup id="cite_ref-4"><a href="#cite_note-4">[4]</a></sup>. 

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Conceptos

### Inmutabilidad

El estado completo de la aplicación se encuentra representado por un gran objeto de JavaScript, conocido como _state_ o _state tree_.

Decimos que **el _state_ es _inmutable_ porque se trata de un objeto de _sólo lectura_**: no se puede modificar directamente, sino sólo a través del _dispatch_ de una [acción](https://github.com/undefinedschool/notes-redux#actions).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

### Actions

**Una _acción_ es un objeto JavaScript que describe un cambio y cuenta con la información mínima necesaria para representarlo (es minimal)**.

El único requisito de este tipo de objetos es tener una propiedad `type`, cuyo valor suele ser un _string_.

Ejemplo sólo con `type`

```js
{ type: 'CLICKED_SIDEBAR' };
```

Ejemplo con más propiedades

```js
{
  type: 'SELECTED_USER', 
  userId: 232 
};
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

#### Utilizar _Action_ `types` constantes

Un _Action_ `type` puede definirse como un simple _string_, pero se recomienda utilizar constantes y modularizarlos.

```js
const ADD_ITEM = 'ADD_ITEM';
const action = { 
  type: ADD_ITEM, 
  title: 'Third item' 
};
```

Ejemplo importando _Actions_

```js
import { ADD_ITEM, REMOVE_ITEM } from './actions';
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

#### Action creators

Son funciones que crean [_Actions_](https://github.com/undefinedschool/notes-redux#actions) (por lo tanto siempre retornan un objeto).

```js
function addItem(t) {
  return { 
    type: ADD_ITEM,     
    title: t  
  } 
};
```

Generalmente ejecutamos _Action creators_ junto con el _dispatch_

```js
dispatch(addItem('Water bottle'));
```

También pueden combinarse, definiendo un _Action dispatcher_

```js
function dispatchAddItem(i) {
  dispatch(addItem(i));
}

dispatchAddItem('Water bottle');
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

### Reducer

**Cuando una [acción](https://github.com/undefinedschool/notes-redux#actions) se dispara, el _state_ de la aplicación debe cambiar y son los _reducers_ quienes se encargan de realizar esta tarea**.

Un _reducer_ es una [_función pura_](https://ericelliottjs.com/premium-content/lesson-pure-functions) que calcula el siguiente _state_ basado en el estado previo y la acción despachada.

![Reducer](https://css-tricks.com/wp-content/uploads/2016/03/redux-article-3-04.svg)

> 👉 **Una _función pura_ recibe un input y retorna un output generado a partir de este input, sin modificarlo ni depender de ningún otro factor. Un _reducer_ returna un objeto (_state_) nuevo que reemplaza al anterior**.

Un _reducer_ es una función pura, por lo tanto no debería

- _mutar_ (modificar) sus argumentos.
- _mutar_ el estado (debe crear uno nuevo).
- generar algún tipo de _side-effect_.
- invocar funciones que no sean puras, es decir, funciones cuyo output depende no sólo del input sino también de otros factores.

> 👉 **Dado que el estado de una aplicación compleja puede ser, valga la redundancia, complejo, suele haber múltiples _reducers_, para diferentes tipos de acciones.**

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

### Store

El _Store_ es un objeto de JavaScript con las siguientes características:

- contiene el _state_ (entero) de la aplicación.
- permite acceder (leer) el _state_ a través del método `getState()`.
- permite actualizar el _state_ a través del método `dispatch()`.
- permite suscribir (o cancelar la suscripción) a cambios del _state_ a través de un _listener_, con el método `subscribe()`.
- Hay 1 _store_ (único) por aplicación.

Por ejemplo, si queremos crear un _store_ para `listManager`, podemos hacer

```js
import { createStore } from 'redux';
import listManager from './reducers';

const store = createStore(listManager);
```

Podemos inicializar el _store_ con datos pre-existentes (por ejemplo que vienen del backend), pasándole un parámetro extra

```js
const store = createStore(listManager, preexistingState);
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

#### Accediendo al _state_

```js
store.getState();
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

#### Actualizando el _state_

```js
store.dispatch(addItem('Something'));
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

#### Escuchando cambios en el _state_

```js
const unsubscribe = store.subscribe(() => const newState = store.getState());
```

También podemos cancelar la suscripción

```js
unsubscribe();
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Flujo de datos unidireccional (one-way data flow)

Al igual que en React, en Redux [el flujo de datos es siempre _unidireccional_](https://github.com/undefinedschool/notes-react-principles#flujo-de-datos-unidireccional-one-way-data-flow).

![Redux Flow](https://www.datocms-assets.com/639/1556116473-1.png)

1. Llamamos al método `dispatch()` del _Store_, pasándole una acción. 
2. El Store se encarga de pasar la acción al _reducer_, generando así el nuevo estado.
3. El Store actualiza el _state_ y le avisa a todos los _listeners_ suscriptos.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Redux Toolkit

(WIP)

> 👉 **Ver [Redux Toolkit](https://redux-toolkit.js.org/)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Redux vs Context API

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Redux vs Hooks

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

---

<sup id="cite_note-1"><a href="#cite_ref-1">1</a></sup> Si bien se popularizó mucho su uso junto con React, Redux puede utilizarse con Angular, Vue, Svelte o cualquier otro framework o librería de frontend que maneje el concepto de [_state_](https://github.com/undefinedschool/notes-react-basics#state) (incluso con [HTML/JS vanilla](https://www.youtube.com/watch?v=SV_reBvGKPE)!).

<sup id="cite_note-2"><a href="#cite_ref-2">2</a></sup> Si estamos usando React, es conveniente utilizar [_React Redux_](https://react-redux.js.org/) para simplificar la integración.

<sup id="cite_note-3"><a href="#cite_ref-3">3</a></sup> Es por esto último que se define como _un contenedor predecible del estado de aplicaciones JavaScript._

<sup id="cite_note-4"><a href="#cite_ref-4">4</a></sup> Actualmente existe [_Context API_](https://reactjs.org/docs/context.html) como una solución más simple a este problema.
