# Ionic con React Routing y Navigation

Este Cheat Sheet te proporciona una guía rápida para configurar la navegación en una aplicación Ionic con React. Aprenderás a aprovechar IonReactRouter junto con [React Router](https://github.com/remix-run/react-router) para crear una navegación efectiva en tu aplicación.

## Introducción a la Navegación en Ionic con React [↗](https://ionicframework.com/docs/react/navigation)

La navegación es un componente esencial en las aplicaciones móviles, y en una aplicación Ionic con React, no es una excepción. Proporciona una manera efectiva de moverse entre diferentes secciones y páginas de tu aplicación.

## Instalación y Configuración de IonReactRouter

Para habilitar la navegación en tu proyecto React con Ionic, primero debes configurar `IonReactRouter`. Esta biblioteca está diseñada para proporcionar una integración perfecta entre la potente biblioteca de enrutamiento de React, react-router, y los componentes de navegación de Ionic.

```jsx
const App: React.FC = () => (
  <IonApp>
    <IonReactRouter>
      <IonRouterOutlet>
        <Route path="/dashboard" component={DashboardPage} />
        <Redirect exact from="/" to="/dashboard" />
      </IonRouterOutlet>
    </IonReactRouter>
  </IonApp>
);
```

## Configuración de Rutas

Las rutas definen las diferentes páginas y secciones de tu aplicación. `IonRouterOutlet` es un componente fundamental en Ionic que se utiliza para gestionar la visualización y navegación entre las diferentes páginas o componentes de una aplicación. Este componente está diseñado específicamente para trabajar con el enrutamiento de React y la biblioteca IonReactRouter en aplicaciones Ionic construidas con React.

Un `IonRouterOutlet` solo debe contener `Route`s o `Redirect`s. Cualquier otro componente debe renderizarse ya sea como resultado de una `Route` o fuera del `IonRouterOutlet`.

## Páginas

`IonPage` es un componente clave en Ionic que se utiliza para definir y estructurar páginas individuales en una aplicación. Este componente se utiliza principalmente en aplicaciones Ionic con React para crear páginas con una estructura específica y proporcionar una forma organizada de mostrar contenido en la pantalla.

```jsx
import { IonContent, IonHeader, IonPage, IonTitle, IonToolbar } from '@ionic/react';
import React from 'react';

const Home: React.FC = () => {
  return (
    <IonPage>
      <IonHeader>
        <IonToolbar>
          <IonTitle>Home</IonTitle>
        </IonToolbar>
      </IonHeader>
      <IonContent className="ion-padding">Hello World</IonContent>
    </IonPage>
  );
};
export default Home;
```

## Navegación entre Páginas

Existen varias opciones disponibles al enrutarse hacia diferentes vistas en una aplicación Ionic React. Aquí, la página UsersListPage utiliza la propiedad routerLink de IonItem para especificar la ruta a la que ir cuando se toca/hace clic en el elemento:

```jsx
const UsersListPage: React.FC = () => {
  return (
    <IonPage>
      <IonHeader>
        <IonToolbar>
          <IonTitle>Users</IonTitle>
        </IonToolbar>
      </IonHeader>
      <IonContent>
        <IonList>
          <IonItem routerLink="/dashboard/users/1">
            <IonLabel>User 1</IonLabel>
          </IonItem>
          <IonItem routerLink="/dashboard/users/2">
            <IonLabel>User 2</IonLabel>
          </IonItem>
        </IonList>
      </IonContent>
    </IonPage>
  );
};
```

- Otros componentes que tienen la propiedad `routerLink` incluyen `IonButton`, `IonCard`, `IonRouterLink`, `IonFabButton` y `IonItemOption`.

- Cada uno de estos componentes también tiene una propiedad `routerDirection` para establecer explícitamente el tipo de transición de página a utilizar ("back", "forward" o "none").

- Fuera de estos componentes que tienen la propiedad `routerLink`, también puedes utilizar el componente `Link` de React Router para navegar entre vistas.

```jsx
<Link to="/dashboard/users/1">User 1</Link>
```

## Navegación Programática

La navegación programática es útil para moverte entre páginas en respuesta a eventos o acciones del usuario. Una opción programática para la navegación es utilizar la propiedad `history` que React Router proporciona a los componentes que renderiza a través de las rutas.

```jsx
<IonButton
  onClick={(e) => {
    e.preventDefault();
    history.push('/dashboard/users/1');
  }}
>
  Go to User 1
</IonButton>
```

### Navegar utilizando history.go​

React Router utiliza el paquete `history` que tiene un método [history.go](https://github.com/remix-run/history/blob/dev/docs/api-reference.md#history.go) que permite a los desarrolladores avanzar o retroceder en el historial de la aplicación.

## Paso de Parámetros y Datos

```jsx
interface UserDetailPageProps
  extends RouteComponentProps<{
    id: string;
  }> {}

const UserDetailPage: React.FC<UserDetailPageProps> = ({ match }) => {
  return (
    <IonPage>
      <IonHeader>
        <IonToolbar>
          <IonTitle>User Detail</IonTitle>
        </IonToolbar>
      </IonHeader>
      <IonContent>User {match.params.id}</IonContent>
    </IonPage>
  );
};
```

La propiedad [match](https://v5.reactrouter.com/web/api/match) contiene información sobre la ruta coincidente, incluidos los parámetros de la URL. Aquí obtenemos el parámetro id y lo mostramos en la pantalla.

## Rutas Anidadas

Las Rutas Anidadas son una configuración de rutas en la que las rutas se enumeran como hijos de otras rutas. El siguiente es un ejemplo de una configuración de rutas anidadas:

```jsx
const App: React.FC = () => (
  <IonApp>
    <IonReactRouter>
      <IonRouterOutlet>
        <Route path="/dashboard/:id">
          <DashboardRouterOutlet />
        </Route>
      </IonRouterOutlet>
    </IonReactRouter>
  </IonApp>
);

const DashboardRouterOutlet: React.FC = () => (
  <IonRouterOutlet>
    <Route path="/dashboard" exact={true}>
      <DashboardMainPage />
    </Route>
    <Route path="/dashboard/stats" exact={true}>
      <DashboardStatsPage />
    </Route>
  </IonRouterOutlet>
);
```

Las rutas anteriores están anidadas porque se encuentran en el arreglo de hijos de la ruta principal. Observa que la ruta principal renderiza el componente `DashboardRouterOutlet`. Cuando anidas rutas, necesitas renderizar otra instancia de `IonRouterOutlet`.

## Tabs

Cuando trabajamos con pestañas, Ionic necesita saber a qué vista pertenece cada pestaña. El componente IonTabs resulta útil en este caso. Veamos cómo se configura el enrutamiento:

```jsx
<IonApp>
  <IonReactRouter>
    <IonRouterOutlet>
      <Route path="/tabs" render={() => <Tabs />} />
      <Route exact path="/">
        <Redirect to="/tabs" />
      </Route>
    </IonRouterOutlet>
  </IonReactRouter>
</IonApp>
```

En este ejemplo, la ruta `tabs` carga un componente `Tabs`. Proporcionamos cada pestaña como un objeto de ruta dentro de este componente. En este caso, llamamos a la ruta `tabs`, pero esto se puede personalizar.

Echemos un vistazo al componente `Tabs`:

```jsx
import { Redirect, Route } from 'react-router-dom';
import { IonIcon, IonLabel, IonRouterOutlet, IonTabBar, IonTabButton, IonTabs } from '@ionic/react';
import { IonReactRouter } from '@ionic/react-router';
import { ellipse, square, triangle } from 'ionicons/icons';
import Tab1 from './pages/Tab1';
import Tab2 from './pages/Tab2';
import Tab3 from './pages/Tab3';

const Tabs: React.FC = () => (
  <IonTabs>
    <IonRouterOutlet>
      <Redirect exact path="/tabs" to="/tabs/tab1" />
      <Route exact path="/tabs/tab1">
        <Tab1 />
      </Route>
      <Route exact path="/tabs/tab2">
        <Tab2 />
      </Route>
      <Route path="/tabs/tab3">
        <Tab3 />
      </Route>
      <Route exact path="/tabs">
        <Redirect to="/tabs/tab1" />
      </Route>
    </IonRouterOutlet>
    <IonTabBar slot="bottom">
      <IonTabButton tab="tab1" href="/tabs/tab1">
        <IonIcon icon={triangle} />
        <IonLabel>Tab 1</IonLabel>
      </IonTabButton>
      <IonTabButton tab="tab2" href="/tabs/tab2">
        <IonIcon icon={ellipse} />
        <IonLabel>Tab 2</IonLabel>
      </IonTabButton>
      <IonTabButton tab="tab3" href="/tabs/tab3">
        <IonIcon icon={square} />
        <IonLabel>Tab 3</IonLabel>
      </IonTabButton>
    </IonTabBar>
  </IonTabs>
);

export default Tabs;
```

En este ejemplo, cada pestaña se define como una ruta individual. Esto facilita la navegación entre las pestañas y las vistas correspondientes.

Cada pestaña en Ionic se trata como una pila de navegación individual. Esto significa que si tienes tres pestañas en tu aplicación, cada pestaña tiene su propia pila de navegación. Dentro de cada pila, puedes navegar hacia adelante (agregar una vista) y hacia atrás (quitar una vista).

Para obtener más información sobre la navegación en React Router, puedes consultar la documentación oficial en [este enlace](https://v5.reactrouter.com/web).
