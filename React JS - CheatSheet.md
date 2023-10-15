# React JS Cheat Sheet

## Introducción a React

- [Sitio web oficial de react](https://es.react.dev/)
- Este Cheat Sheet proporciona una guía rápida de React JS, un popular framework de JavaScript para la construcción de interfaces de usuario.

## Componentes en React

React se basa en la creación de componentes reutilizables. Un componente es una parte de la interfaz de usuario que se puede componer y reutilizar en toda la aplicación.

### Crear un Componente

```jsx
class MiComponente extends React.Component {
  render() {
    return <div>Mi componente React</div>;
  }
}
```

#### Uso de Componentes Funcionales

Los componentes funcionales son una forma más concisa y moderna de crear componentes en React.

### Usando Funciones Normales

```jsx
function MiComponenteFuncional() {
  return <div>Mi componente funcional</div>;
}
```

### Usando Arrow Functions

```jsx
const MiComponenteFuncional = () => (
  <div>Mi componente funcional (usando Arrow Function)</div>
);
```

## Propiedades (Props)

Las propiedades permiten que los componentes reciban datos de su componente padre.

```jsx
function Saludo(props) {
  return <h1>Hola, {props.nombre}</h1>;
}
```

### Spreading

```jsx
function ComponentePadre() {
  const datos = { nombre: 'Juan', edad: 30 };
  return <ComponenteHijo {...datos} />;
}

const ComponenteHijo = (props) => {
  return (
    <div>
      <p>Nombre: {props.nombre}</p>
      <p>Edad: {props.edad}</p>
    </div>
  );
}
```

### Children

```jsx
function Boton(props) {
  return <button>{props.children}</button>;
}

function App() {
  return (
    <Boton>
      Haga clic aquí
    </Boton>
  );
}

```

### Conditional operator & Template Literals

Puedes utilizar el operador condicional (?:) y Template Literals para mostrar contenido condicional en tu componente.

```jsx
function Saludo(props) {
  return (
    <div>
      <p>{props.nombre ? `Hola, ${props.nombre}` : 'Hola, Invitado'}</p>
    </div>
  );
}
```

## Estado (State)

El estado se utiliza para almacenar datos que pueden cambiar a lo largo del tiempo y afectar la representación del componente.

```jsx
class Contador extends React.Component {
  constructor(props) {
    super(props);
    this.state = { contador: 0 };
  }

  render() {
    return (
      <div>
        <p>Contador: {this.state.contador}</p>
        <button onClick={() => this.setState({ contador: this.state.contador + 1 })}>Incrementar</button>
      </div>
    );
  }
}
```

## Hook `useState`

El hook `useState` es una función que te permite añadir estado a los componentes funcionales en React.

```jsx
import React, { useState } from 'react';

function Contador() {
  // Declara una variable de estado llamada "contador" con un valor inicial de 0.
  const [contador, setContador] = useState(0);

  return (
    <div>
      <p>Contador: {contador}</p>
      <button onClick={() => setContador(contador + 1)}>Incrementar</button>
    </div>
  );
}
```

## Hook `useEffect`

El hook `useEffect` es una parte fundamental de React que te permite realizar efectos secundarios en componentes funcionales. Puedes utilizarlo para gestionar tareas como el acceso a API, la suscripción a eventos, la actualización del DOM y más.

### Uso Básico

```jsx
import React, { useState, useEffect } from 'react';

function Temporizador() {
  const [segundos, setSegundos] = useState(0);

  // El efecto se ejecutará cada vez que 'segundos' cambie.
  useEffect(() => {
    const interval = setInterval(() => {
      setSegundos(segundos + 1);
    }, 1000);

    // Limpieza del efecto: detén el intervalo cuando el componente se desmonta.
    return () => clearInterval(interval);
  }, [segundos]);

  return (
    <div>
      Segundos: {segundos}
    </div>
  );
}
```

Puedes utilizar un efecto para realizar una carga inicial de datos cuando el componente se monta.

```jsx
useEffect(() => {
  // Lógica para cargar datos iniciales.
}, []); // Sin dependencias, se ejecuta solamente una vez al montar el componente.
```

Puedes controlar cuándo se ejecuta un efecto utilizando los "dependencias" pasadas como segundo argumento al useEffect.

```jsx
const valor = 42;

useEffect(() => {
  // Este efecto se ejecuta cuando 'valor' cambia.
}, [valor]);
```

Si no proporcionas dependencias, el efecto se ejecutará cada vez que se renderice el componente.

```jsx
useEffect(() => {
  // Este efecto se ejecuta en cada render.
});
```

## Styles

La estilización de componentes es esencial para el diseño de interfaces de usuario en React. Puedes aplicar estilos utilizando diferentes enfoques.

### Inline Styles

Los estilos en línea son útiles cuando deseas aplicar estilos de manera directa a un elemento en React.

```jsx
function EstiloEnLinea() {
  const estilo = {
    backgroundColor: 'lightblue',
    color: 'darkblue',
    padding: '10px',
    border: '1px solid blue',
    borderRadius: '5px',
  };

  return (
    <div style={estilo}>
      Estilo en línea
    </div>
  );
}
```

### Hojas de Estilo CSS

También puedes utilizar hojas de estilo CSS para aplicar estilos a tus componentes React.

```jsx
// Archivo Estilo.css
.estilo-css {
  background-color: lightblue;
  color: darkblue;
  padding: 10px;
  border: 1px solid blue;
  border-radius: 5px;
}

```

```jsx
import React from 'react';
import './Estilo.css'; // Importa la hoja de estilo CSS

function EstiloCSS() {
  return (
    <div className="estilo-css">
      Estilo CSS
    </div>
  );
}

```

## JavaScript Básico

A continuación, algunos conceptos básicos de JavaScript que son esenciales al trabajar con React:

### Variables y Declaración

```javascript
const nombre = 'Juan';
let edad = 30;
var pi = 3.14159;
```

### Listas

```jsx
const frutas = ['manzana', 'banana', 'naranja'];

const listaDeFrutas = frutas.map((fruta) => (
  <li key={fruta}>{fruta}</li>
));

const numeros = [1, 2, 3, 4, 5];

const numerosPares = numeros.filter((numero) => numero % 2 === 0);
```

### Eventos

```jsx
<button onClick={miFuncion}>Haz clic</button>
```

### Promises

```jsx
const miPromesa = new Promise((resolve, reject) => {
  setTimeout(() => {
    const exito = Math.random() >= 0.5;
    if (exito) {
      resolve('¡La promesa se resolvió con éxito!');
    } else {
      reject('Hubo un error en la promesa.');
    }
  }, 2000);
});

miPromesa
  .then((resultado) => {
    console.log(resultado);
  })
  .catch((error) => {
    console.error(error);
  });

async function miFuncionAsincrona() {
  try {
    const miPromesa = new Promise((resolve, reject) => {
      setTimeout(() => {
        const exito = Math.random() >= 0.5;
        if (exito) {
          resolve('¡La promesa se resolvió con éxito!');
        } else {
          reject('Hubo un error en la promesa.');
        }
      }, 2000);
    });

    const resultado = await miPromesa;
    console.log(resultado);
  } catch (error) {
    console.error(error);
  }
}

miFuncionAsincrona();
```

## Recursos Adicionales

- [Documentación oficial de React](https://es.react.dev/reference/react)
- [Aprende React](https://es.react.dev/learn)
- [React en GitHub](https://github.com/facebook/react)
- [Ultimate ReactJS Cheat Sheet](https://upmostly.com/ultimate-reactjs-cheat-sheet)
- [React TypeScript Cheatsheet](https://react-typescript-cheatsheet.netlify.app/) con *TypeScript*
- [React DevHints](https://devhints.io/react)
