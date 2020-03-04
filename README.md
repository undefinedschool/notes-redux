> El siguiente contenido fue elaborado por [@_nhsz](https://twitter.com/_nhsz) como guía para las clases de [undefined school](https://twitter.com/undefinedSchool)
> Son bienvenidos los _issues_ y _PRs_ para mejorar el contenido, corregir errores, etc. 

> 👉 Si te resultó útil, **se agradece que lo compartas para que le llegue a más gente!**

# ![Redux](https://i.imgur.com/3Y4n7hz.png)

## Notas relacionadas

### `react`

- [**Principios**](https://github.com/undefinedschool/notes-react-principles/)
- [**Conceptos Básicos**](https://github.com/undefinedschool/notes-react-basics)

## Contenido

- [Intro](https://github.com/undefinedschool/redux#intro)
- [Inmutabilidad]()
- [Redux vs Context API]()
- [Redux vs Hooks]()

---

## Intro

[Redux](https://redux.js.org/) es una librería (biblioteca) que funciona como [_State_](https://github.com/undefinedschool/notes-react-basics#state) _Container_ (es decir, nos permite manejar el estado de los componentes) para nuestras aplicaciones, independientemente del framework o librería que utilicemos para manejar la _vista_ de nuestra aplicación<sup id="cite_ref-1"><a href="#cite_note-1">[1]</a></sup>.

Lo que hace básicamente Redux es proveernos de **un gran objeto que contiene el estado de cada componente de nuestra aplicación** (nos permite lidiar con el estado de toda la aplicación de una forma centralizada), al cual cada componente puede acceder.

Y por qué no utilizamos simplemente un objeto común, el _state_ del componente principal y ya?

Porque aparte de este gran objeto, **Redux nos garantiza que este objeto es [_inmutable_](), es decir, no va a cambiar**, ya que no modifica el _state_ actual cuando se produce algún cambio, sino que retorna una nueva copia de este objeto, con los cambios requeridos, haciendo que el _state_ de nuestra aplicación sea más fácil de manejar, entender, debuggear y predecible<sup id="cite_ref-2"><a href="#cite_note-2">[2]</a></sup>. 

> 👉 En este sentido, Redux se comporta como una _función pura_, según el paradigma funcional.

[↑ Ir al inicio](https://github.com/undefinedschool/redux#contenido)

## Inmutabilidad

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/redux#contenido)

## Redux vs Context API

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/redux#contenido)

## Redux vs Hooks

(WIP)

[↑ Ir al inicio](https://github.com/undefinedschool/redux#contenido)

---

<sup id="cite_note-1"><a href="#cite_ref-1">1</a></sup> Si bien se popularizó mucho su uso junto con React, Redux puede utilizarse con Angular, Vue, Svelte o cualquier otro framework o librería de frontend que maneje el concepto de [_state_](https://github.com/undefinedschool/notes-react-basics#state) (incluso con [HTML/JS vanilla](https://www.youtube.com/watch?v=SV_reBvGKPE)!).

<sup id="cite_note-2"><a href="#cite_ref-2">2</a></sup> Es por esto último que se define como _un contenedor predecible del estado de aplicaciones JavaScript._
