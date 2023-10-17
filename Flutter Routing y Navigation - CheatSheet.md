# Flutter Routing y Navegación

Flutter ofrece una amplia flexibilidad para la navegación y el routing en tus aplicaciones. Estas son algunas de las técnicas fundamentales para crear una experiencia de navegación efectiva en Flutter.

## Introducción a Navigator [↗](https://github.com/ies-rincon/3_damna_23_24-pgl-ut3-flutter-router)

Flutter proporciona un sistema completo para la navegación entre pantallas y la gestión de enlaces profundos. Las aplicaciones pequeñas sin enlaces profundos complejos pueden utilizar [Navigator](https://api.flutter.dev/flutter/widgets/Navigator-class.html), mientras que las aplicaciones con requisitos específicos de navegación y enlaces profundos también deben utilizar el [Router](https://api.flutter.dev/flutter/widgets/Router-class.html) para gestionar correctamente los enlaces profundos en Android e iOS, y para mantenerse sincronizadas con la barra de direcciones cuando la aplicación se ejecuta en la web

### Navegación Básica

La navegación en Flutter se gestiona utilizando un sistema de rutas. El widget central para la navegación es `Navigator`. Aquí tienes algunos conceptos clave:

- **Navigator**: El `Navigator` de Flutter es una herramienta poderosa para gestionar la pila de rutas. Permite la navegación hacia adelante y hacia atrás, así como la gestión de rutas.

- **Rutas**: Cada pantalla o página en tu aplicación Flutter se representa como una "ruta" en el `Navigator`. Puedes utilizar `Navigator.push()` para ir a una nueva página y `Navigator.pop()` para volver a la página anterior.

### Navegación con Argumentos

Puedes pasar argumentos entre rutas en Flutter. Esto es útil para compartir datos entre diferentes pantallas. Algunos detalles importantes:

- **Navigator.push()**: Puedes pasar argumentos a la siguiente página mediante la propiedad `arguments`. Por ejemplo:

```dart
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => SecondPage(data: 'Información importante'),
  ),
);
```

- **Recuperar Argumentos**: En la página de destino, puedes recuperar los argumentos utilizando `ModalRoute.of(context)`. Ejemplo:

```dart
final args = ModalRoute.of(context)!.settings.arguments as String;
```

### Rutas con Nombres

En Flutter, también puedes utilizar rutas con nombres para simplificar la navegación. Aquí está cómo se hace:

- **Definición de Rutas con Nombres**: Define rutas con nombres en la configuración de `MaterialApp`. Por ejemplo:

```dart
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => HomePage(),
    '/second': (context) => SecondPage(),
    '/detail': (context) => DetailPage(),
  },
);
```

- **Navegación con Rutas con Nombres**: Utiliza `Navigator.pushNamed()` para navegar utilizando rutas con nombres. Por ejemplo:

```dart
Navigator.pushNamed(context, '/second');
```

### Argumentos con Rutas con Nombres

Puedes pasar argumentos utilizando rutas con nombres en Flutter:

- **Navegación con Argumentos**: Al utilizar rutas con nombres, también puedes pasar argumentos. Ejemplo:

```dart
Navigator.pushNamed(context, '/detail', arguments: 'Información importante');
```

- **Recuperar Argumentos**: En la página de destino, puedes recuperar los argumentos de la misma manera que con la navegación básica.

## Introducción a Router [↗](https://github.com/ies-rincon/3_damna_23_24-pgl-ut3-flutter-go_router)

En Flutter, [GoRouter](https://pub.dev/packages/go_router) es una solución de enrutamiento que proporciona una forma flexible y potente de gestionar la navegación en tu aplicación. A diferencia de la navegación básica de Flutter, GoRouter ofrece una mayor personalización y estructura para tus rutas.

- **GoRouter**: GoRouter es una librería de enrutamiento de alto rendimiento para Flutter. Te permite definir y gestionar rutas de manera eficiente.

- **Definición de Rutas**: Con GoRouter, puedes definir rutas de manera más detallada y estructurada. Puedes asignar funciones de controlador a cada ruta para manejar la navegación y realizar acciones específicas.

- **Argumentos de Ruta**: GoRouter facilita el paso de argumentos entre rutas. Puedes enviar datos entre páginas a través de argumentos de ruta y personalizar cómo se manejan.

- **Navegación Personalizada**: GoRouter te permite personalizar la navegación de tu aplicación. Puedes definir transiciones de pantalla personalizadas y diseñar la experiencia de navegación según tus necesidades.

### Definición de Rutas

Primero, definimos nuestras rutas utilizando GoRouter. Cada ruta está asociada a una función de controlador.

```dart
final GoRouter _router = GoRouter(
  routes: <RouteBase>[
    GoRoute(
      path: '/',
      builder: (BuildContext context, GoRouterState state) {
        return const HomeScreen();
      },
      routes: <RouteBase>[
        GoRoute(
          path: 'details',
          builder: (BuildContext context, GoRouterState state) {
            return const DetailsScreen();
          },
        ),
      ],
    ),
  ],
);
```

### Inicialización de GoRouter

Luego, inicializamos GoRouter con nuestras rutas definidas y configuramos el enrutador:

```dart
/// The main app.
class MyApp extends StatelessWidget {
  /// Constructs a [MyApp]
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp.router(
      routerConfig: _router,
    );
  }
}
```

### Navegación

Podemos navegar entre las rutas de la siguiente manera:

```dart
/// The home screen
class HomeScreen extends StatelessWidget {
  /// Constructs a [HomeScreen]
  const HomeScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Home Screen')),
      body: Center(
        child: ElevatedButton(
          onPressed: () => context.go('/details'),
          child: const Text('Go to the Details screen'),
        ),
      ),
    );
  }
}

/// The details screen
class DetailsScreen extends StatelessWidget {
  /// Constructs a [DetailsScreen]
  const DetailsScreen({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('Details Screen')),
      body: Center(
        child: ElevatedButton(
          onPressed: () => context.go('/'),
          child: const Text('Go back to the Home screen'),
        ),
      ),
    );
  }
}
```

GoRouter te brinda un mayor control y personalización en la gestión de rutas y la navegación en tus aplicaciones Flutter. Puedes personalizar las transiciones de pantalla y manejar argumentos de manera efectiva.

Para obtener más detalles y ejemplos, consulta la documentación completa en [la página de GoRouter en Pub.dev](https://pub.dev/documentation/go_router/latest/topics/Get%20started-topic.html).

---

Para obtener más detalles y ejemplos, consulta la documentación completa en [Flutter Documentation](https://docs.flutter.dev/ui/navigation).
