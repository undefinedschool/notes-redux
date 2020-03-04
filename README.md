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
  - [Store](https://github.com/undefinedschool/notes-redux#store)
  - [Reducer](https://github.com/undefinedschool/notes-redux#reducer)
  - [Actions](https://github.com/undefinedschool/notes-redux#actions)
  - [Dispatch](https://github.com/undefinedschool/notes-redux#dispatch)
- [Redux vs Context API](https://github.com/undefinedschool/notes-redux#redux-vs-context-api)
- [Redux vs Hooks](https://github.com/undefinedschool/notes-redux#redux-vs-hooks)
- [Redux Toolkit](https://github.com/undefinedschool/notes-redux#redux-toolkit)

---

## Intro

[Redux](https://redux.js.org/) es una librería (biblioteca) que funciona como [_State_](https://github.com/undefinedschool/notes-react-basics#state) _Container_ o _State Manager_ (nos permite manejar el estado de los componentes) para nuestras aplicaciones, que funciona independientemente del framework o librería que utilicemos para manejar la _vista_<sup id="cite_ref-1"><a href="#cite_note-1">[1]</a></sup>.

Lo que hace básicamente Redux es proveernos de **un gran objeto que contiene el estado de cada componente de nuestra aplicación** (nos permite lidiar con el estado de toda la aplicación de una forma centralizada), al cual cada componente puede acceder.

**Redux nos garantiza que este objeto es [_inmutable_](https://github.com/undefinedschool/notes-redux#inmutabilidad), es decir, no va a cambiar**, ya que no modifica el _state_ actual cuando se produce algún cambio, sino que retorna una nueva copia de este objeto con los cambios requeridos, haciendo que el _state_ de nuestra aplicación sea más fácil de manejar, entender, debuggear y predecible<sup id="cite_ref-2"><a href="#cite_note-2">[2]</a></sup><sup id="cite_ref-3"><a href="#cite_note-3">[3]</a></sup>. 

> 👉 En este sentido, Redux se comporta como una _función pura_, según el paradigma funcional.

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

## Por qué usar Redux?

Recordemos que React ya nos provee una forma de manejar el [_state_](https://github.com/undefinedschool/notes-react-basics#state) de cada componente, de forma local.

**De hecho, la mayoría de las veces, [probablemente no necesitemos una solución como Redux](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)**. Qué beneficio nos trae entonces utilizar Redux por sobre el _local state_?

_Levantar_ el _state_ en el árbol de [componentes](https://github.com/undefinedschool/notes-react-basics#react-component) funciona en casos simples, pero en aplicaciones complejas podemos terminar encontrándonos moviendo el state continuamente entre componentes, a través de las [_props_](https://github.com/undefinedschool/notes-react-basics#props). 

Un mejor enfoque podría ser utilizar un _store_ externo, global (un gran objeto que funcione algo así como una variable global, al que cualquier componente pueda acceder) y esto es lo que propone Redux.

## Conceptos

### Inmutabilidad

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

### Store

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

### Reducer

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

### Actions

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

### Dispatch

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

> 👉 **Ver [Redux Toolkit](https://redux-toolkit.js.org/)

[↑ Ir al inicio](https://github.com/undefinedschool/notes-redux#contenido)

---

<sup id="cite_note-1"><a href="#cite_ref-1">1</a></sup> Si bien se popularizó mucho su uso junto con React, Redux puede utilizarse con Angular, Vue, Svelte o cualquier otro framework o librería de frontend que maneje el concepto de [_state_](https://github.com/undefinedschool/notes-react-basics#state) (incluso con [HTML/JS vanilla](https://www.youtube.com/watch?v=SV_reBvGKPE)!).

<sup id="cite_note-2"><a href="#cite_ref-2">2</a></sup> Si estamos usando React, es conveniente utilizar [_React Redux_](https://react-redux.js.org/) para simplificar la integración.

<sup id="cite_note-3"><a href="#cite_ref-3">3</a></sup> Es por esto último que se define como _un contenedor predecible del estado de aplicaciones JavaScript._
