# Ionic Cheat Sheet

Este Cheat Sheet proporciona una guía rápida para el desarrollo de aplicaciones móviles con el framework Ionic.

## Introducción a Ionic

[Ionic es un framework](https://ionicframework.com/) de código abierto que te permite desarrollar aplicaciones móviles y web de alta calidad utilizando tecnologías web estándar como HTML, CSS y JavaScript. Ionic facilita la creación de aplicaciones con una apariencia y funcionalidad nativas, lo que lo convierte en una elección popular para el desarrollo de aplicaciones móviles multiplataforma.

## Componentes más habituales [↗](https://ionicframework.com/docs/components)

- **`<ion-button>`**: Un componente de botón.

- **`<ion-list>`**: Utilizado para mostrar una lista de elementos.

- **`<ion-input>`**: Para ingresar texto.

- **`<ion-card>`**: Crea tarjetas con contenido.

- **`<ion-modal>`**: Muestra ventanas modales.

- **`<ion-grid>`**: Muestra ventanas modales.

- **`<ion-tab-bar>`**: Una barra de pestañas para navegación.

- **`<ion-header>` y `<ion-footer>`**: Componentes para encabezados y pies de página.

## Ionic CLI [↗](https://ionicframework.com/docs/cli)

- **`ionic start`**: Inicia un nuevo proyecto de Ionic.

- **`ionic serve`**: Inicia un servidor de desarrollo local.

- **`ionic build`**: Compila la aplicación para producción.

- **`ionic generate`**: Genera componentes y páginas.

- **`ionic capacitor add`**: Agrega Capacitor a tu proyecto.

## Capacitor [↗](https://ionicframework.com/docs/native)

- [Capacitor](https://capacitorjs.com/docs/) es una plataforma para construir aplicaciones web, móviles y de escritorio con HTML, CSS y JavaScript.

- Permite acceder a características nativas en aplicaciones web.

- Puedes [instalar plugins de Capacitor](https://capacitorjs.com/docs/plugins) para acceder a características como la cámara, geolocalización y notificaciones.

## Estilos

- Utiliza CSS y los estilos de Ionic para [personalizar la apariencia de tu aplicación](https://ionicframework.com/docs/theming/themes).

- Puedes aplicar estilos en línea a elementos individuales o utilizar [hojas de estilo globales](https://ionicframework.com/docs/layout/global-stylesheets).

- Aprovecha las clases de CSS predefinidas de Ionic para darle un aspecto pulido a tu aplicación.

```jsx
import React, { useState } from 'react';
import { IonContent, IonHeader, IonTitle, IonToolbar, IonList, IonItem, IonInput, IonButton } from '@ionic/react';

function App() {
  const [tareas, setTareas] = useState(['Tarea 1', 'Tarea 2', 'Tarea 3']);
  const [nuevaTarea, setNuevaTarea] = useState('');

  const agregarTarea = () => {
    if (nuevaTarea) {
      setTareas([...tareas, nuevaTarea]);
      setNuevaTarea('');
    }
  };

  return (
    <>
      <IonHeader>
        <IonToolbar style={styles.toolbar}>
          <IonTitle style={styles.title}>Lista de Tareas</IonTitle>
        </IonToolbar>
      </IonHeader>
      <IonContent>
        <IonList style={styles.list}>
          {tareas.map((tarea, index) => (
            <IonItem key={index} style={styles.listItem}>{tarea}</IonItem>
          ))}
        </IonList>
        <IonInput
          value={nuevaTarea}
          onIonChange={(e) => setNuevaTarea(e.detail.value!)}
          placeholder="Nueva Tarea"
          style={styles.input}
        />
        <IonButton expand="full" onClick={agregarTarea} style={styles.button}>
          Agregar Tarea
        </IonButton>
      </IonContent>
    </>
  );
}

const styles = {
  toolbar: {
    backgroundColor: '#3498db',
  },
  title: {
    fontSize: '24px',
    fontWeight: 'bold',
    color: '#fff',
  },
  list: {
    listStyleType: 'none',
  },
  listItem: {
    fontSize: '18px',
    marginBottom: '10px',
  },
  input: {
    width: '80%',
    padding: '5px',
    margin: '10px 0',
  },
  button: {
    backgroundColor: '#3498db',
    color: '#fff',
    padding: '10px 20px',
  },
};

export default App;
```

## Recursos Adicionales

- [Documentación oficial de Ionic](https://ionicframework.com/docs/)
- [Documentación de Capacitor](https://capacitorjs.com/)
- [Ionic Framework en GitHub](https://github.com/ionic-team/ionic-framework)
- [Ion-Cheat-Sheet](https://ioncheatsheet.com/)
