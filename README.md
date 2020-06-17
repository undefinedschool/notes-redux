# ![Redux](https://i.imgur.com/3Y4n7hz.png)

### 👉 Ver [todas las notas](https://github.com/undefinedschool/notes)

## Contenido

- [Intro](https://github.com/undefinedschool/notes-redux#intro)
- [Por qué usar Redux?](https://github.com/undefinedschool/notes-redux#por-qu%C3%A9-usar-redux)
  - [Beneficios](https://github.com/undefinedschool/notes-redux#beneficios)
- [Conceptos](https://github.com/undefinedschool/notes-redux#conceptos)
  - [Inmutabilidad](https://github.com/undefinedschool/notes-redux#inmutabilidad)
  - [Actions](https://github.com/undefinedschool/notes-redux#actions)
    - [Utilizar _Action_ `types` constantes](https://github.com/undefinedschool/notes-redux#utilizar-action-types-constantes)
    - [Action creators](https://github.com/undefinedschool/notes-redux#action-creators)
  - [Reducer](https://github.com/undefinedschool/notes-redux#reducer)
    - [_Reducers_ y _Actions_](https://github.com/undefinedschool/notes-redux#reducers-y-actions)
  - [Store](https://github.com/undefinedschool/notes-redux#store)
    - [Accediendo al _state_](https://github.com/undefinedschool/notes-redux#accediendo-al-state)
    - [Actualizando el _state_](https://github.com/undefinedschool/notes-redux#actualizando-el-state)
    - [Escuchando cambios en el _state_](https://github.com/undefinedschool/notes-redux#escuchando-cambios-en-el-state)
- [Flujo de datos unidireccional (one-way data flow)](https://github.com/undefinedschool/notes-redux#flujo-de-datos-unidireccional-one-way-data-flow)
- [Redux vs React Local State](https://github.com/undefinedschool/notes-redux#redux-vs-react-local-state)
- [Redux Developer Tools](https://github.com/undefinedschool/notes-redux#redux-developer-tools)
- [React Redux](https://github.com/undefinedschool/notes-redux#react-redux)
- [Redux vs Context API](https://github.com/undefinedschool/notes-redux#redux-vs-context-api)
- [Redux vs Hooks](https://github.com/undefinedschool/notes-redux#redux-vs-hooks)
- [Redux Toolkit](https://github.com/undefinedschool/notes-redux#redux-toolkit)
- [Testing](https://github.com/undefinedschool/notes-redux#testing)

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

### Beneficios

Algunas de las ventajas que implica utilizar Redux incluyen

- manejo centralizado del _state_.
- flujo de datos unidireccional, transparente y predecible.
- más fácil de debuggear.
- más fácil de testear.
- posibilidad de rehacer/deshacer cambios y movernos entre diferentes _states_ a través del tiempo (_time travelling_).
- _state_ inmutable.
- ecosistema bastante desarrollado y maduro (mucha documentación, extensiones, herramientas de desarrollo, etc).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Conceptos

### Inmutabilidad

El estado completo de la aplicación se encuentra representado por un gran objeto de JavaScript, conocido como _state_ o _state tree_.

Decimos que **el _state_ es _inmutable_ porque se trata de un objeto de _sólo lectura_**: no se puede modificar directamente, sino sólo a través del _dispatch_ de una [acción](https://github.com/undefinedschool/notes-redux#actions).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

### Actions

**Una _acción_ es un objeto JavaScript que describe un cambio y cuenta con la información mínima necesaria para representarlo (es minimal)**.

> 👉 **El único requisito de este tipo de objetos es tener una propiedad `type`, cuyo valor suele ser un _string_**.

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

> 👉 **En Redux, la única forma de actualizar el _state_ es disparando una acción**, la cual se pasa al [_reducer_](https://github.com/undefinedschool/notes-redux#reducer), que se encargará de generar un nuevo _state_.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

#### Utilizar _Action_ `types` constantes

Un _Action_ `type` puede definirse como un simple _string_, pero se recomienda utilizar constantes y modularizarlos, para de esta forma poder reutilizarlos y evitar errores de tipeo.

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

Son funciones que crean [_acciones_](https://github.com/undefinedschool/notes-redux#actions) (por lo tanto siempre retornan un objeto).

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

> 👉 **Estas funciones van a _despachar_ acciones cada vez que querramos realizar cambios al _state_**.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

### Reducer

**Cuando una [acción](https://github.com/undefinedschool/notes-redux#actions) se dispara, el _state_ de la aplicación debe cambiar y son los _reducers_ quienes se encargan de realizar esta tarea**.

**Un _reducer_ es una [_función pura_](https://ericelliottjs.com/premium-content/lesson-pure-functions) que recibe un _state_ (el actual) y una acción y retorna un nuevo estado, basándose únicamente en estos parámetros**. Por lo tanto, si no hay acción, retornamos el mismo estado.

![Reducer](https://css-tricks.com/wp-content/uploads/2016/03/redux-article-3-04.svg)

> 👉 **En una _función pura_, el output depende únicamente del input y dado el mismo input, genera el mismo output**, sin modificarlo ni depender de ningún otro factor. Además, **no tiene _side-effects_**, es decir, la función no modifica el entorno externo de ninguna forma (no muta los argumentos que recibe ni accede a variables por fuera de su scope). Esto hace que el comportamiento de la función sea _predecible_ y por lo tanto, más fácil de razonar, debuggear y testear.

**Un _reducer_ retorna un objeto (_state_) nuevo que reemplaza al anterior, basándose únicamente en el _state_ previo y las _actions_ generadas**. 

⚠️ Al tratarse un _reducer_ de una función pura, no debería

- _mutar_ (modificar) sus argumentos.
- _mutar_ el estado (debe crear uno nuevo).
- generar algún tipo de _side-effect_.
- invocar funciones que no sean puras, es decir, funciones cuyo output depende no sólo del input sino también de otros factores.

> 👉 **Dado que el estado de una aplicación compleja puede ser, valga la redundancia, complejo, suele haber múltiples _reducers_, para diferentes tipos de acciones y un _reducer principal_ (root) que los combina.** Para hacer esto último, Redux nos provee la función [`combineReducers`](https://redux.js.org/api/combinereducers/).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

#### _Reducers_ y _Actions_

Los _reducers_ no se llaman directamente, sino que primero debe dispararse una [acción](https://github.com/undefinedschool/notes-redux#actions), que va a ser interceptada y procesada por un reducer.

> 👉 **En Redux, las acciones son simplemente instrucciones que le dicen al _Reducer_ cómo modificar el estado actual**.

Estas acciones vienen en forma de objeto, siempre con una propiedad `type` (que por convención es un _string_ en UPPER_SNAKE_CASE) y un _payload_ opcional, para indicar nuevos datos que queremos agregar al _state_.

Por ejemplo, si queremos indicarle al _reducer_ que agregue a `'Jimmy'` a una lista de nombres del _state_, podemos hacer

```js
{
  type: 'ADD_NAME',
  payload: 'Jimmy'
}
```

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

### Store

El _Store_ es un objeto de JavaScript con las siguientes características:

- contiene el _state_ (entero) de la aplicación.
- permite acceder (leer) el _state_ a través del método `getState()`.
- permite actualizar el _state_ a través del método `dispatch()`.
- permite suscribirse (o cancelar la suscripción) a cambios del _state_ a través de un _listener_, con el método `subscribe()`.
- hay 1 solo _store_ por aplicación.

> 👉 **Notar que _Store_ y _state_ no son lo mismo: el [_state_](https://github.com/undefinedschool/notes-react-basics#state) está conformado por los datos con los que opera nuestra aplicación, mientras que el _Store_ contiene al _state_ y nos provee de ciertos métodos (una API) para interactuar con este**.

Ejemplo de Store:

```js
import { createStore } from 'redux';

const store = createStore(firstReducer);

// we can now dispatch actions and get state from the store

const initialState = store.getState();

console.log(initialState); // this will be an array

store.dispatch(addName('Elie'));
store.dispatch(addName('Matt'));
store.dispatch(addName('Tim'));

console.log(store.getState()); // this object will have an array with three values

store.dispatch(removeName('Elie'));

console.log(store.getState()); // this array will have 2 values
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

El flujo o _lifecycle_ en Redux entonces es el siguiente:

1. Invocamos el método `dispatch()` del _Store_, pasándole una acción que representa un cambio en el _state_: `store.dispatch(action)`. 
2. El Store se encarga de pasarle la acción al _reducer_ (e invocar a este último), generando así el nuevo estado.
3. Puede haber un _Reducer_ principal que combine el output de múltiples funciones reducers.
4. El Store actualiza el _state_ y le avisa a todos los _listeners_ suscriptos.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Redux vs React Local State

En React, el _state_

- es [_local_](https://github.com/undefinedschool/notes-react-basics#state) (por lo tanto, descentralizado), propio de cada componente.
- si necesitamos compartir el _state_ de un componente con otros, se pasa por [_props_](https://github.com/undefinedschool/notes-react-basics#props) (siempre hacia _child components_).
- es _mutable_.

En Redux, el _state_

- es _global_ (por lo tanto, centralizado) y está contenido en el [Store](https://github.com/undefinedschool/notes-redux#store).
- si un componente necesita tener acceso a algún valor del _state_, puede simplemente _suscribirse_ al _Store_ para obtenerlo, sin tener que pasar _props_ innecesariamente entre componentes.
- es [_inmutable_](https://github.com/undefinedschool/notes-redux#inmutabilidad).

> 👉 Algo importante a tener en cuenta es que **utilizar Redux no implica pasar a manejar todo el _state_ con esta solución**. Necesitamos determinar qué partes del _state_ pasarán a estar almacenadas en el Store de Redux y qué partes continuarán en el state local de cada [React Component](https://github.com/undefinedschool/notes-react-basics#react-component).

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Redux Developer Tools

Tener un único store inmutable nos permite acceder a features como _time traveling_, _hot module reloading_ y simplifica el debugging. 

Como el _Store_ está al tanto de las acciones que se disparan (por el _dispatch_), podemos ver los cambios en el _state_ y revertirlos (aka [_time travelling_](https://medium.com/the-web-tub/time-travel-in-react-redux-apps-using-the-redux-devtools-5e94eba5e7c0))! No sólo eso, también podemos reproducir y repetir series de acciones que suceden en nuestra aplicación, a través de las _Developer Tools_ para Redux.

> 👉 Descargar [Redux Developer Tools para Chrome](https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd)

> 👉 Descargar [Redux Developer Tools para Firefox](https://addons.mozilla.org/en-US/firefox/addon/reduxdevtools/)

Además de instalar la extensión, tenemos que agregar el siguiente código a nuestra aplicación

```js
import { createStore, compose } from 'redux';
import rootReducer from './reducers';

const store = createStore(rootReducer, compose(
  typeof window === 'object' && typeof window.devToolsExtension !== 'undefined' ? window.devToolsExtension() : (f) => f
));

export default store;
```

Algunas de las acciones de _time travelling_ que podemos realizar incluyen

- `commit`: toma cualquier cambio que le hagamos al _state_ y lo setea como el estado inicial. Podemos hacer esto tantas veces como querramos.
- `revert`: retroceder a un estado anterior (un commit previo).
- `reset`: deshacer todos los commits y volver al _state_ original.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## React Redux

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Redux vs Context API

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Redux vs Hooks

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Redux Toolkit

(WIP)

> 👉 **Ver [Redux Toolkit](https://redux-toolkit.js.org/)**.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Testing

[notas aparte]

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

---

<sup id="cite_note-1"><a href="#cite_ref-1">1</a></sup> Si bien se popularizó mucho su uso junto con React, Redux puede utilizarse con Angular, Vue, Svelte o cualquier otro framework o librería de frontend que maneje el concepto de [_state_](https://github.com/undefinedschool/notes-react-basics#state) (incluso con [HTML/JS vanilla](https://www.youtube.com/watch?v=SV_reBvGKPE)!).

<sup id="cite_note-2"><a href="#cite_ref-2">2</a></sup> Si estamos usando React, es conveniente utilizar [_React Redux_](https://react-redux.js.org/) para simplificar la integración.

<sup id="cite_note-3"><a href="#cite_ref-3">3</a></sup> Es por esto último que se define como _un contenedor predecible del estado de aplicaciones JavaScript._

<sup id="cite_note-4"><a href="#cite_ref-4">4</a></sup> Actualmente existe [_Context API_](https://reactjs.org/docs/context.html) como una solución más simple a este problema.
