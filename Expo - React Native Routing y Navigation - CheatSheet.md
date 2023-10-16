# Expo - React Native Routing y Navegación [↗](https://github.com/ies-rincon/3_damna_23_24-pgl-expo-router-v2)

En Expo y React Native, la navegación y el enrutamiento son aspectos fundamentales para crear una experiencia de usuario fluida en tus aplicaciones móviles. Expo ofrece un enfoque basado en stacks de navegación, que permite gestionar las transiciones entre pantallas y la organización de la navegación de manera eficiente.

## Introducción a Expo Router

Expo Router es una biblioteca de enrutamiento de código abierto diseñada para aplicaciones React Native universales creadas con Expo. Cuando un archivo se agrega al directorio de la aplicación, automáticamente se convierte en una ruta en tu navegación.

### Características

- **Nativo**: Expo Router se basa en la potente suite de React Navigation y ofrece navegación verdaderamente nativa y optimizada por plataforma de manera predeterminada.

- **Compartible**: Cada pantalla de tu aplicación es automáticamente vinculable mediante enlaces profundos, lo que hace que cualquier ruta en tu aplicación sea compartible con enlaces.

- **Offline-first**: Las aplicaciones se almacenan en caché y se ejecutan en modo offline primero, con actualizaciones automáticas al publicar una nueva versión. También gestiona todas las URL nativas entrantes sin necesidad de una conexión de red o servidor.

- **Optimizado**: Las rutas se optimizan automáticamente con evaluación diferida en producción y bundling diferido en desarrollo.

- **Iteración**: Ofrece un refresco rápido universal en Android, iOS y web, junto con la memorización de artefactos en el bundler para mantener la eficiencia incluso a gran escala.

- **Universal**: Android, iOS y web comparten una estructura de navegación unificada, con la capacidad de acceder a las API específicas de la plataforma a nivel de ruta.

- **Descubrible**: Expo Router permite la representación estática en tiempo de compilación en web y la vinculación universal a nativa. Esto significa que el contenido de tu aplicación puede ser indexado por motores de búsqueda.

Para obtener más detalles y recursos, consulta la [documentación oficial de Expo Router](https://docs.expo.dev/routing/introduction/).

### Compatibilidad de Versiones

Asegúrate de que la versión de Expo Router sea compatible con la versión de Expo SDK que utiliza tu proyecto. La siguiente tabla muestra las combinaciones de versiones recomendadas:

| Expo SDK | Expo Router | Configuración del Punto de Entrada `package.json` |
|----------|------------|-------------------|
| 49.0.0 y superior | 2.0.0 | `"main": "expo-router/entry"` |
| 48.0.0 | 1.0.0 | `"main": "index.js"` |

### Creación de Páginas con Expo Router [↗](https://docs.expo.dev/routing/create-pages/)

Expo Router utiliza una convención de enrutamiento basada en archivos que simplifica la creación de páginas en tu aplicación React Native. Cuando creas un archivo en el directorio de la aplicación `app/`, este automáticamente se convierte en una ruta en la aplicación. Por ejemplo, los siguientes archivos generan las siguientes rutas:

- `app/index.js` coincide con `/`
- `app/home.js` coincide con `/home`
- `app/settings/index.js` coincide con `/settings`
- `app/[user].js` coincide con rutas dinámicas como `/expo` o `/evanbacon`

#### Páginas

Las páginas se definen exportando un componente React como el valor predeterminado desde un archivo en el directorio de la aplicación. El archivo del que se exportan debe usar una de las extensiones `.js`, `.jsx`, `.tsx` o `.ts`.

Por ejemplo, crea el directorio de la aplicación en tu proyecto y luego crea un archivo `index.js` en su interior. Luego, agrega el siguiente fragmento:

```jsx
// app/index.js
import { Text } from 'react-native';

export default function Page() {
  return <Text>Página de inicio</Text>;
}
```

El ejemplo anterior coincide con la ruta / en la aplicación y en el navegador. Los archivos con el nombre index coinciden con el directorio principal y no agregan un segmento de ruta adicional. Por ejemplo, app/settings/index.js coincide con /settings en la aplicación.

#### Rutas Dinámicas

Las rutas dinámicas permiten que cualquier ruta no coincidente en un nivel de segmento dado se empareje.

| Ruta                  | URL Coincidente        |
|-----------------------|------------------------|
| `app/blog/[slug].js`  | `/blog/123`            |
| `app/blog/[...rest].js` | `/blog/123/settings` |

Las rutas con mayor especificidad se emparejarán antes que una ruta dinámica. Por ejemplo, `/blog/bacon` coincidirá con `blog/bacon.js` antes que `blog/[id].js`.

Múltiples segmentos pueden coincidir en una sola ruta mediante el uso de la sintaxis de "rest" (`...`). Por ejemplo, `app/blog/[...id].js` coincide con `/blog/123/settings`.

Los segmentos dinámicos son accesibles como parámetros de búsqueda en el componente de la página.

```javascript
// app/blog/[slug].js
import { useLocalSearchParams } from 'expo-router';
import { Text } from 'react-native';

export default function Page() {
  const { slug } = useLocalSearchParams();

  return <Text>Entrada de blog: {slug}</Text>;
}
```

Este ejemplo muestra cómo crear y utilizar una ruta dinámica para mostrar una entrada de blog basada en el valor de slug. Puedes personalizar este código y la información según sea necesario.

### Navegar entre Páginas con Expo Router [↗](https://docs.expo.dev/routing/navigating-pages/)

Crea enlaces para moverte entre las páginas de tu aplicación.

Expo Router utiliza "enlaces" para navegar entre páginas en la aplicación. Esto es conceptualmente similar a cómo funciona la web con las etiquetas `<a>` y el atributo `href`.

```plaintext
app
├─ index.js
├─ about.js
└─ user
   ├─ [id].js
```

La estructura de directorio anterior muestra cómo se organizan las páginas en la aplicación. Cada archivo representa una página y se pueden crear enlaces para moverte entre ellas.

#### Ejemplo de Uso de Enlaces `<Link>`

```jsx
// app/index.js
import { View } from 'react-native';
import { Link } from 'expo-router';

export default function Page() {
  return (
    <View>
      <Link href="/about">Acerca de</Link>

      <Link href="/user/bacon">Ver usuario</Link>
    </View>
  );
}
```

Aquí tienes la nueva sección "Navegación Imperativa" y el texto correspondiente para agregar al archivo:

#### Navegación Imperativa

En ocasiones, es posible que desees navegar desde un almacén global cuando un usuario inicia o cierra sesión. Puedes utilizar el objeto del enrutador para navegar de manera imperativa (fuera de React).

```jsx
import { router } from 'expo-router';

export function logout() {
  router.replace('/login');
}
```

El objeto del enrutador es inmutable y contiene las siguientes funciones:

- `push: (href: Href) => void`: Navega a una ruta. Puedes proporcionar una ruta completa como `/perfil/configuracion` o una ruta relativa como `../configuracion`. También puedes navegar a rutas dinámicas pasando un objeto como `{ pathname: 'perfil', params: { id: '123' } }`.

- `replace: (href: Href) => void`: Misma API que `push`, pero reemplaza la ruta actual en el historial en lugar de agregar una nueva. Esto es útil para redireccionamientos.

- `back: () => void`: Navega hacia la ruta anterior.

- `canGoBack: () => boolean`: Devuelve `true` si existe una pila de historial válida y la función `back()` puede retroceder.

- `setParams: (params: Record<string, string>) => void`: Actualiza los parámetros de consulta para la ruta actualmente seleccionada.

La navegación imperativa te permite realizar acciones de navegación fuera del flujo de React, lo que puede ser útil en situaciones específicas.

### Rutas de Diseño en Expo Router [↗](https://docs.expo.dev/routing/layouts/)

Aprende a definir elementos de interfaz de usuario compartidos, como barras de pestañas y encabezados.

Por defecto, las rutas llenan toda la pantalla. El movimiento entre ellas es una transición de pantalla completa sin animación. En las aplicaciones nativas, los usuarios esperan que los elementos compartidos, como encabezados y barras de pestañas, persistan entre las páginas. Estos elementos se crean utilizando rutas de diseño (**layout routes**).

#### Crear una Ruta de Diseño (*Layout*)

Para crear una ruta de diseño para un directorio, crea un archivo llamado `_layout.js` en el directorio y exporta un componente React como predeterminado.

```jsx
// app/home/_layout.js
import { Slot } from 'expo-router';

export default function HomeLayout() {
  return <Slot />;
}
```

En el ejemplo anterior, Slot renderizará la ruta secundaria actual, similar al uso del prop "children" en React. Este componente se puede envolver con otros componentes para crear un diseño.

```jsx
// app/home/_layout.js
import { Slot } from 'expo-router';

export default function HomeLayout() {
  return (
    <>
      <Header />
      <Slot />
      <Footer />
    </>
  );
}
```

Expo Router admite la adición de una sola ruta de diseño para un directorio determinado. Si deseas usar múltiples rutas de diseño, agrega varios directorios:

```plaintext
app
├─ _layout.js
├─ home
    ├─ _layout.js
    ├─ index.js
```

```jsx
// app/_layout.js
import { Tabs } from 'expo-router';

export default function Layout() {
  return <Tabs />;
}

// app/home/_layout.js
import { Stack } from 'expo-router';

export default function Layout() {
  return <Stack />;
}
```

Si deseas utilizar múltiples rutas de diseño sin modificar la URL, puedes usar grupos.

Aquí tienes la nueva sección "Grupos" y el texto correspondiente para agregar al archivo:

#### Grupos

Puedes evitar que un segmento aparezca en la URL utilizando la sintaxis de grupo `()`.

- `app/root/home.js` coincide con `/root/home`
- `app/(root)/home.js` coincide con `/home`

Esto es útil para agregar diseños sin agregar segmentos adicionales a la URL. Puedes agregar tantos grupos como desees.

Los grupos también son útiles para organizar secciones de la aplicación. En el siguiente ejemplo, tenemos `app/(app)`, que es donde vive la aplicación principal, y `app/(aux)`, que es donde se encuentran las páginas auxiliares. Esto es útil para agregar páginas a las que deseas vincular externamente, pero que no necesitas que formen parte de la aplicación principal.

```plaintext
app
├─ (app)
│   ├─ index.js
│   ├─ user.js
├─ (aux)
    ├─ terms-of-service.js
    ├─ privacy-policy.js
```

Este enfoque te permite organizar y estructurar tu aplicación de manera más eficiente, evitando la inclusión innecesaria de segmentos en la URL.

### Stack de Navegación [↗](https://docs.expo.dev/router/advanced/stack/)

Un "stack" de navegación es una pila de pantallas que se gestionan de manera LIFO (Last In, First Out). Esto significa que la última pantalla agregada al stack es la primera en mostrarse y la primera en desaparecer cuando el usuario navega hacia atrás.

Aquí tienes la nueva sección "El Diseño de Pila en Expo Router" y el texto correspondiente para agregar al archivo:

#### El Diseño de Pila en Expo Router `Stack`

El Diseño de Pila en Expo Router envuelve el Navegador de Pila Nativa de React Navigation, no debe confundirse con el antiguo Navegador de Pila en JavaScript.

### Estructura de Directorio de Ejemplo

```plaintext
app
├─ _layout.js
├─ index.js
├─ detail.js
```

Para crear un diseño de pila con dos pantallas como se muestra en la estructura de archivos anterior:

```jsx
// app/_layout.js
import { Stack } from 'expo-router/stack';

export default function Layout() {
  return <Stack />;
}
```

Este diseño de pila permite crear una navegación en pila con varias pantallas, lo que es útil para organizar y estructurar la navegación en tu aplicación.

### Tabs de Navegación [↗](https://docs.expo.dev/router/advanced/tabs/)

El Diseño de Pestañas en Expo Router envuelve las `Bottom Tabs` de [React Navigation](https://reactnavigation.org/docs/bottom-tab-navigator).

Ejemplo de Directorio de Tabs:

```plaintext
app
├─ (tabs)
    ├─ _layout.js
    ├─ pestaña1.js
    ├─ pestaña2.js
    ├─ pestaña3.js
```

```jsx
// app/(pestañas)/_layout.js
import { Slot, Tabs } from "expo-router";
// export default Slot;
export default Tabs;
```

Considera la siguiente estructura de archivos, que se utiliza como ejemplo en esta guía:

```plaintext
app
├─ _layout.js
├─ index.js
├─ home
    ├─ _layout.js
    ├─ feed.js
    ├─ messages.js
```

En el ejemplo anterior, `app/home/feed.js` coincide con `/home/feed`, y `app/home/messages.js` coincide con `/home/messages`.

```jsx
// app/_layout.js
import { Stack } from 'expo-router';
export default Stack;
```

Tanto `app/home/_layout.js` como `app/index.js` están anidados en el diseño de `app/_layout.js` para que se representen como una pila.

```jsx
// app/home/_layout.js
import { Tabs } from 'expo-router';
export default Tabs;

// app/index.js
import { Link } from 'expo-router';
export default function Root() {
  return <Link href="/home/messages">Navegar a la ruta anidada</Link>;
}
```

Tanto `app/home/feed.js` como `app/home/messages.js` están anidados en el diseño de `home/_layout.js`, por lo que se representarán como una pestaña.

```jsx
import { View, Text } from 'react-native';
export default function Feed() {
  return (
    <View>
      <Text>Pantalla de Feed</Text>
    </View>
  );
}

import { View, Text } from 'react-native';
export default function Messages() {
  return (
    <View>
      <Text>Pantalla de Mensajes</Text>
    </View>
  );
}
```

Este ejemplo ilustra cómo organizar y estructurar tus rutas y diseños en Expo Router para crear una navegación más eficiente y organizada en tu aplicación.

### Drawer de Navegación [↗](https://docs.expo.dev/router/advanced/drawer/)

Un Drawer, en el contexto de la navegación de aplicaciones móviles y de React Native, es un componente de interfaz de usuario que se utiliza comúnmente para mostrar un menú de navegación lateral oculto. Este menú se encuentra fuera de la pantalla principal y se puede deslizar hacia adentro desde un borde de la pantalla (generalmente el borde izquierdo) o se puede activar tocando un botón o un icono en la pantalla. El término "Drawer" proviene de la idea de que este menú se "extrae" o "abre" desde un espacio oculto.

## Personalización y Navegación Avanzada

React Navigation ofrecen muchas opciones de personalización y navegación avanzada. Puedes explorar las posibilidades para crear una experiencia de usuario única en tus aplicaciones.

Para obtener más información y recursos detallados sobre el enrutamiento y la navegación en Expo con react navigation, consulta la [documentación oficial de React Navigation](https://reactnavigation.org/).

Este es solo un vistazo rápido al enrutamiento y la navegación en Expo y React Native. Puedes expandir y personalizar tu enfoque de navegación según tus necesidades específicas.
