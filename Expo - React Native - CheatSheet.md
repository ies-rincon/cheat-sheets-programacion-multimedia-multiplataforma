# Expo - React Native Cheat Sheet

Este Cheat Sheet proporciona una guía rápida para desarrollar aplicaciones móviles con Expo en React Native.

## Componentes más habituales [↗](https://reactnative.dev/docs/components-and-apis#basic-components)

- **`View`**: Un componente contenedor que se utiliza para agrupar otros componentes.

- **`Text`**: Utilizado para mostrar texto en la aplicación.

- **`Image`**: Para mostrar imágenes.

- **`Button`**: Crea botones interactivos.

- **`TextInput`**: Permite a los usuarios ingresar texto.

- **`ScrollView`**: Para desplazarse por contenido más grande que la pantalla.

- **`FlatList`**: Muestra una lista de elementos con alto rendimiento.

```jsx
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function App() {
  return (
    <View style={styles.container}>
      <View style={styles.box1}>
        <Text style={styles.text}>Caja 1</Text>
      </View>
      <View style={styles.box2}>
        <Text style={styles.text}>Caja 2</Text>
      </View>
      <View style={styles.box3}>
        <Text style={styles.text}>Caja 3</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
  },
  box1: {
    flex: 1,
    backgroundColor: '#3498db',
    height: 100,
    alignItems: 'center',
    justifyContent: 'center',
  },
  box2: {
    flex: 1,
    backgroundColor: '#e74c3c',
    height: 100,
    alignItems: 'center',
    justifyContent: 'center',
  },
  box3: {
    flex: 1,
    backgroundColor: '#27ae60',
    height: 100,
    alignItems: 'center',
    justifyContent: 'center',
  },
  text: {
    color: '#fff',
    fontSize: 20,
  },
});
```

## Conceptos Comunes de Expo

- **Expo CLI**: Herramienta de línea de comandos para crear, desarrollar y publicar aplicaciones Expo. [↗](https://docs.expo.dev/more/expo-cli/)

- **Expo Go**: La aplicación Expo Go te permite previsualizar tus aplicaciones en dispositivos móviles. [↗](https://docs.expo.dev/get-started/expo-go/)

- **Expo SDK**: API y bibliotecas específicas de Expo para acceder a características como cámara, ubicación y notificaciones. [↗](https://docs.expo.dev/versions/latest/#each-expo-sdk-version-depends-on-a-react-native-version)

- **Expo Client**: Una aplicación que permite a los usuarios acceder a aplicaciones Expo publicadas.

- **Expo Bare Workflow**: Configuración personalizada para proyectos React Native que utilizan características nativas junto con Expo.

```unix
Usage
  $ npx expo <command>

Commands
  start, export, export:web
  run:ios, run:android, prebuild
  install, customize, config
  login, logout, whoami, register

Options
  --version, -v   Version number
  --help, -h      Usage info
```

## Estilos

En React Native, los estilos se manejan principalmente con propiedades de estilo.

Puedes aplicar estilos en línea a tus componentes:

```jsx
<View style={{ flex: 1, backgroundColor: 'lightblue', alignItems: 'center', justifyContent: 'center' }}>
  <Text style={{ fontSize: 24, color: 'white' }}>¡Hola, Expo!</Text>
</View>
```

Otra forma común de definir estilos es utilizando [`StyleSheet`](https://reactnative.dev/docs/stylesheet). Es una API que proporciona un enfoque más eficiente para definir estilos. Puedes crear un objeto `StyleSheet` para definir estilos reutilizables.

```jsx
const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: 'lightblue',
    alignItems: 'center',
    justifyContent: 'center',
  },
  text: {
    fontSize: 24,
    color: 'white',
  },
});

<View style={styles.container}>
  <Text style={styles.text}>¡Hola, Expo!</Text>
</View>
```

Flexbox (Flexible Box) es un modelo de diseño que permite organizar y alinear elementos en una interfaz web o aplicación móvil de manera eficiente y flexible. Con Flexbox, puedes diseñar diseños complejos y alinear elementos en varias direcciones, como horizontal y vertical, con relativa facilidad.

- **`yogalayout.com`**: [YogaLayout](https://yogalayout.com/) es un recurso en línea que proporciona una experiencia interactiva para aprender Flexbox. Te permite experimentar y visualizar cómo se comportan los elementos en un diseño Flexbox a medida que ajustas las propiedades.

- **`Flex-Direction, Justify-Content, Align-Items`**: [Este artículo de Medium](https://medium.com/@pateldhara248/flex-direction-justify-content-align-items-71d65bec1e95) ofrece una explicación detallada sobre propiedades y conceptos clave de Flexbox, como `flex-direction`, `justify-content`, y `align-items`. Es útil para comprender cómo funcionan estas propiedades y cómo aplicarlas en tus proyectos de diseño web y aplicaciones móviles.


Más información sobre estilos y diseño se encuentra en la [documentación](https://reactnative.dev/docs/style) de React Native y Expo.

## `app.json` y `app.config.js` [↗](https://docs.expo.dev/workflow/configuration/)

El [archivo](https://docs.expo.dev/versions/latest/config/app/#properties) `app.json` o `app.config.js` en una aplicación Expo es un archivo de configuración que permite definir diversas propiedades y configuraciones relacionadas con tu proyecto de Expo. Expo utiliza este archivo para personalizar la experiencia de construcción y ejecución de tu aplicación móvil.

## Bibliotecas de Componentes de Interfaz de Usuario (UI)

Una lista de bibliotecas de componentes de interfaz de usuario para aplicaciones Expo y React Native.

La Interfaz de Usuario (UI) es una parte fundamental de cualquier aplicación. Si el ícono es la puerta principal, la UI es el diseño interior. Puedes optar por diseñar completamente tu UI desde cero; sin embargo, si deseas ponerlo en funcionamiento rápidamente manteniendo un acabado pulido, existen muchas bibliotecas ya disponibles para ayudarte a llevar tu aplicación donde deseas.

- [React Native Elements](https://reactnativeelements.com/)
- [React Native Paper](https://reactnativepaper.com/)

Para obtener más información sobre estas bibliotecas de componentes de interfaz de usuario, puedes consultar la [documentación de Expo sobre bibliotecas de interfaz de usuario](https://docs.expo.dev/ui-programming/user-interface-libraries/).

## Recursos Adicionales

- [Documentación oficial de Expo](https://docs.expo.dev/)
- [Tutorial: Introducción de Expo](https://docs.expo.dev/tutorial/introduction/)
- [Documentación oficial de React Native](https://reactnative.dev/)
- [Recursos Adicionales de Expo](https://docs.expo.dev/additional-resources/)
- [React Native Cheat Sheet para Principiantes en dev.to](https://dev.to/codemaker2015/react-native-cheatsheet-for-beginners-28oa)
