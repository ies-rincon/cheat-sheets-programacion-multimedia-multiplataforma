# Flutter State Management & Persistence

Los gestores de estado son una parte esencial en el desarrollo de aplicaciones Flutter, ya que permiten administrar la lógica de la aplicación y la gestión de datos de manera eficiente. A continuación, exploraremos algunos de los gestores de estado más comunes en Flutter.

## Gestores de Estados

### Provider [↗](https://github.com/ies-rincon/3_damna_23_24-pgl-ut3-flutter-counter-app-with-multiple-providers)

**Provider** es una [biblioteca ampliamente utilizada](https://pub.dev/packages/provider) en el ecosistema de Flutter para la gestión de estados. Proporciona un mecanismo para compartir y acceder a datos entre widgets de manera eficiente. Algunas características clave de Provider incluyen:

- **Inyección de Dependencias**: Provider permite inyectar dependencias y acceder a instancias compartidas de objetos o modelos de datos en toda la aplicación.

- **Notifier y ChangeNotifier**: Provider utiliza el concepto de **ChangeNotifier** para notificar a los widgets cuando los datos cambian. Los widgets pueden escuchar cambios en los datos y actualizar su interfaz de usuario en consecuencia.

- **Múltiples Niveles de Provider**: Puedes anidar múltiples proveedores para manejar diferentes partes de la aplicación. Esto permite un control fino sobre el estado en función de su alcance.

#### Ejemplo de Provider [↗](https://github.com/ies-rincon/3_damna_23_24-pgl-ut3-flutter-counter-app-with-provider)

```dart
// Definir un Modelo (ChangeNotifier)
class CounterModel extends ChangeNotifier {
  int _count = 0;
  
  int get count => _count;
  
  void increment() {
    _count++;
    notifyListeners(); // Notifica a los oyentes sobre el cambio.
  }
}

// Inicializar Provider
void main() {
  runApp(
    ChangeNotifierProvider(
      create: (context) => CounterModel(), // Crear una instancia del modelo.
      child: MyApp(),
    ),
  );
}

// Acceder al Modelo en un Widget
class MyWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    final counter = Provider.of<CounterModel>(context);
    
    return Text('Contador: ${counter.count}');
  }
}
```

#### Riverpod

**Riverpod** es otra biblioteca de gestión de estados que se basa en los conceptos de Provider. Ofrece un enfoque más avanzado y una sintaxis mejorada. Con Riverpod, se pueden definir proveedores sin necesidad de un widget raíz y proporciona una gestión de dependencias más robusta.

#### Bloc Pattern

El **Bloc Pattern** es un patrón de gestión de estados que se centra en la separación de la lógica de negocio y la interfaz de usuario. Utiliza **cubit** y **bloc** para gestionar los eventos y estados de la aplicación de manera clara y predecible. Este patrón es especialmente útil para aplicaciones con lógica compleja.

[Ver más sobre gestores de estado en Flutter](https://docs.flutter.dev/data-and-backend/state-mgmt/options)

## Persistencia de Datos [↗](https://github.com/ies-rincon/3_damna_23_24-pgl-ut3-flutter-counter-app-provider-persist)

Flutter ofrece varias opciones para persistir datos en la aplicación, lo que permite almacenar y recuperar información de manera eficiente. Una de las bibliotecas más populares para lograr esto es `shared_preferences`.

### shared_preferences

`shared_preferences` es una [biblioteca](https://pub.dev/packages/shared_preferences) que proporciona una forma sencilla de [almacenar datos clave-valor](https://docs.flutter.dev/cookbook/persistence/key-value) de manera persistente. Es especialmente útil para guardar configuraciones de la aplicación o pequeñas cantidades de datos que deben sobrevivir a los reinicios de la aplicación.

### Ejemplo de uso

Para utilizar `shared_preferences`, primero debes agregarlo como una dependencia en tu archivo `pubspec.yaml`:

```yaml
dependencies:
  shared_preferences: ^2.2.2
```

Luego, puedes usarlo en tu código de la siguiente manera:

```dart
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State<MyHomePage> {
  final key = 'counter';
  int counter = 0;

  @override
  void initState() {
    super.initState();
    _loadCounter();
  }

  void _loadCounter() async {
    final prefs = await SharedPreferences.getInstance();
    setState(() {
      counter = prefs.getInt(key) ?? 0;
    });
  }

  void _incrementCounter() async {
    final prefs = await SharedPreferences.getInstance();
    setState(() {
      counter = (prefs.getInt(key) ?? 0) + 1;
      prefs.setInt(key, counter);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Persistencia de Datos con shared_preferences'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Text('Contador: $counter'),
          ],
        ),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: _incrementCounter,
        tooltip: 'Incrementar',
        child: Icon(Icons.add),
      ),
    );
  }
}
```

Además de `shared_preferences`, Flutter ofrece [otras opciones de persistencia de datos](https://docs.flutter.dev/cookbook/persistence).
