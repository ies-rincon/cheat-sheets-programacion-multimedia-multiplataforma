# Expo - React Native State Management & Persistence

En Expo - React Native, la gestión de estados y la persistencia de datos son componentes esenciales para el desarrollo de aplicaciones móviles.

## Gestores de Estados

Expo - React Native utiliza el sistema de estado de React para administrar los datos que cambian con el tiempo en una aplicación. Puedes usar el estado local con `useState` en componentes o el estado global en combinación con bibliotecas como `Zustand`, `Redux`, `Mobx` o `Recoil`. Estos son algunos ejemplos:

- **Zustand**: Una [biblioteca simple y liviana](https://github.com/pmndrs/zustand) que se integra de manera eficiente con React. Es adecuada para administrar estados locales en componentes.

- **React Context API**: Puedes aprovechar el [Context API](https://react.dev/learn/passing-data-deeply-with-context) de React para crear contextos y proporcionar estados a componentes específicos de tu aplicación. Esto facilita el intercambio de estados entre componentes sin necesidad de pasarlos manualmente a través de las propiedades. [↗](https://github.com/ies-rincon/3_damna_23_24-pgl-ut3-expo-rn-counter-app-with-state-management-context-api)

- **Redux**: Una [biblioteca](https://redux.js.org/) popular que implementa la arquitectura de almacenamiento de aplicaciones basada en un único árbol de estados. Permite administrar de manera eficiente el estado global de la aplicación. [Redux Toolkit (RTK)](https://redux-toolkit.js.org/) es una biblioteca que simplifica la gestión del estado en aplicaciones React y React Native que utilizan Redux. Esta herramienta integra características clave que hacen que trabajar con Redux sea más eficiente.

- **Mobx**: Una biblioteca que utiliza observables y reacciones para administrar el estado global y local. Es conocida por su simplicidad y capacidad de reactividad.

- **Recoil**: Una biblioteca experimental de Facebook que simplifica la administración de estados compartidos. Se integra bien con React y React Native.

### Ejemplo de Uso de Zustand [↗](https://github.com/ies-rincon/3_damna_23_24-pgl-ut3-expo-rn-counter-app-zustand-persist)

```javascript
import create from 'zustand';

// Define el store y sus métodos
const useCounterStore = create((set) => ({
  count: 0,
  increment: () => set((state) => ({ count: state.count + 1 })),
  decrement: () => set((state) => ({ count: state.count - 1 })),
}));

export default useCounterStore;
```

```javascript
import React from 'react';
import { View, Text, Button } from 'react-native';
import useCounterStore from './useCounterStore'; // Importa el store

const CounterComponent = () => {
  const { count, increment, decrement } = useCounterStore(); // Usa el store

  return (
    <View>
      <Text>Contador: {count}</Text>
      <Button title="Incrementar" onPress={increment} />
      <Button title="Decrementar" onPress={decrement} />
    </View>
  );
};

export default CounterComponent;
```

### Ejemplo de Uso de Redux con RTK

```javascript
import React from 'react';
import { View, Text, Button } from 'react-native';
import { useDispatch, useSelector, Provider } from 'react-redux';
import { configureStore, createSlice } from '@reduxjs/toolkit';

// Define un slice
const counterSlice = createSlice({
  name: 'counter',
  initialState: 0,
  reducers: {
    increment: (state) => state + 1,
    decrement: (state) => state - 1,
  },
});

// Configure el almacenamiento
const store = configureStore({
  reducer: {
    counter: counterSlice.reducer,
  },
});

// Acceso a acciones y estado
const { increment, decrement } = counterSlice.actions;

// Utilización en un componente
const CounterComponent = () => {
  const count = useSelector((state) => state.counter);
  const dispatch = useDispatch();

  return (
    <View>
      <Text>Contador: {count}</Text>
      <Button title="Incrementar" onPress={() => dispatch(increment())} />
      <Button title="Decrementar" onPress={() => dispatch(decrement())} />
    </View>
  );
};

export default function App() {
  return (
    <Provider store={store}>
      <CounterComponent />
    </Provider>
  );
}

```

## Persistencia de Datos

### AsyncStorage

`AsyncStorage` [es una API](https://react-native-async-storage.github.io/async-storage/) incorporada en React Native que permite almacenar datos de forma asíncrona en el dispositivo del usuario. Es útil para guardar configuraciones de la aplicación, tokens de autenticación y otros datos pequeños.

```javascript
import React, { useState, useEffect } from 'react';
import { View, Text, Button } from 'react-native';
import AsyncStorage from '@react-native-async-storage/async-storage';

const App = () => {
  const [data, setData] = useState('');

  useEffect(() => {
    (async () => {
      const storedData = await AsyncStorage.getItem('myData');
      setData(storedData || 'No data found');
    })();
  }, []);

  const saveData = async () => {
    await AsyncStorage.setItem('myData', 'Hello, AsyncStorage!');
    setData('Data saved!');
  };

  return (
    <View>
      <Text>{data}</Text>
      <Button title="Guardar Datos" onPress={saveData} />
    </View>
  );
};

export default App;
```

### Otras Opciones de Persistencia de Datos

Además de `AsyncStorage`, existen [otras opciones para la persistencia de datos en React Native](https://docs.expo.dev/develop/user-interface/store-data/):

- **Expo SQLite**: diseñado para trabajar con bases de datos SQLite en aplicaciones móviles desarrolladas con React Native y Expo.

- **Expo SecureStore**: permite a los desarrolladores almacenar datos sensibles y cifrados de forma segura en dispositivos móviles en aplicaciones desarrolladas con React Native y Expo
