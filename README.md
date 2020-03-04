> El siguiente contenido fue elaborado por [@_nhsz](https://twitter.com/_nhsz) como guía para las clases de [undefined school](https://twitter.com/undefinedSchool)
> Son bienvenidos los _issues_ y _PRs_ para mejorar el contenido, corregir errores, etc. 

> 👉 Si te resultó útil, **se agradece que lo compartas para que le llegue a más gente!**

# ![Redux](https://i.imgur.com/3Y4n7hz.png)

## Notas relacionadas

### `react`

- [**Principios**](https://github.com/undefinedschool/notes-react-principles/)
- [**Conceptos Básicos**]()

## Contenido

- [Intro]()
- [Inmutabilidad]()

---

## Intro

[Redux](https://redux.js.org/) es una librería (biblioteca) que funciona como [_State_](https://github.com/undefinedschool/notes-react-basics#state) _Container_ para nuestras aplicaciones, independientemente del framework o librería que utilicemos para manejar la _vista_ de nuestra aplicación (por ejemplo React).

Lo que hace básicamente Redux es proveernos de **un gran objeto que contiene el estado de cada componente de nuestra aplicación**, al cual cada componente puede acceder.

Y por qué no utilizamos simplemente un objeto común, el _state_ del componente principal y ya?

Aparte de este gran objeto, **Redux nos garantiza que este objeto es [_inmutable_](), es decir, no va a cambiar**, ya que no modifica el _state_ actual cuando se produce algún cambio, sino que retorna una nueva copia de este objeto, con los cambios requeridos, haciendo que nuestra aplicación sea más fácil de entender, debuggear y predecible<sup id="cite_ref-1"><a href="#cite_note-1">[1]</a></sup>. 

> 👉 En este sentido, Redux se comporta como una _función pura_, según el paradigma funcional.

## Inmutabilidad

---

<sup id="cite_note-1"><a href="#cite_ref-1">1</a></sup>Es por esto último que se define como _un contenedor predecible del estado de aplicaciones JavaScript._
