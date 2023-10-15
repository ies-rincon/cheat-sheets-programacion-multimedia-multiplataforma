# Flutter Cheat Sheet

Este Cheat Sheet proporciona una guía rápida para desarrollar aplicaciones móviles con el framework Flutter.

## Introducción a Flutter

- **¿Qué es Flutter?**: Flutter es un framework de código abierto creado por Google para desarrollar aplicaciones móviles nativas tanto para Android como para iOS desde una sola base de código.

- **Lenguaje de Programación**: Flutter utiliza el lenguaje de programación [Dart](Dart%20-%20CheatSheet.md), que es rápido, orientado a objetos y fácil de aprender.

- [Sitio web oficial de Flutter](https://flutter.dev/)

## Widgets en Flutter

Flutter utiliza una amplia variedad de widgets para construir interfaces de usuario. Algunos de los widgets más comunes incluyen:

- [`Container`](https://api.flutter.dev/flutter/widgets/Container-class.html)
- [`Text`](https://api.flutter.dev/flutter/widgets/Text-class.html)
- [`Image`](https://api.flutter.dev/flutter/widgets/Image-class.html)
- [`Row`](https://api.flutter.dev/flutter/widgets/Row-class.html) y [`Column`](https://api.flutter.dev/flutter/widgets/Column-class.html)
- [`ListView`](https://api.flutter.dev/flutter/widgets/ListView-class.html)
- [`AppBar`](https://api.flutter.dev/flutter/material/AppBar-class.html)
- [`Scaffold`](https://api.flutter.dev/flutter/material/Scaffold-class.html)
- `Button`, `IconButton`, `TextField`, o `Card`, de [Material](https://api.flutter.dev/flutter/material/material-library.html)

## StatelessWidget vs StatefulWidget

En Flutter, existen dos tipos principales de widgets: `StatelessWidget` y `StatefulWidget`.

- **StatelessWidget**: Los widgets [`Stateless`](https://api.flutter.dev/flutter/widgets/StatelessWidget/build.html) son inmutables y no pueden cambiar su estado una vez creados. Se utilizan para representar partes de la interfaz de usuario que no cambian con el tiempo.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Saludo App'),
        ),
        body: Center(
          child: Text('¡Hola, Mundo!'),
        ),
      ),
    );
  }
}
```

- **StatefulWidget**: Los widgets [`Stateful`](https://api.flutter.dev/flutter/widgets/StatefulWidget-class.html) pueden cambiar su estado durante la vida de la aplicación. Se utilizan para representar partes de la interfaz de usuario que pueden cambiar con el tiempo.

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  int contador = 0;

  void _incrementarContador() {
    setState(() {
      contador++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Contador App'),
        ),
        body: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              Text('Contador: $contador'),
              RaisedButton(
                onPressed: _incrementarContador,
                child: Text('Incrementar'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

## BuildContext

El [`BuildContext`](https://api.flutter.dev/flutter/widgets/BuildContext-class.html) es un objeto que proporciona información sobre la ubicación de un widget en el árbol de widgets de Flutter. Se utiliza para buscar widgets, obtener información sobre el tema de la aplicación y más.

## Estilos en Flutter

En Flutter, los estilos y la apariencia se gestionan mediante propiedades de widgets y objetos de tema. Algunos de los widgets de estilo más comunes son:

- `Text`: Para estilizar el texto.
- `Container`: Para definir el diseño y el estilo del contenedor que puede contener otros widgets.
- `AppBar`: Para personalizar la barra de aplicación en la parte superior de la pantalla.
- `Button`: Para estilizar botones y acciones interactivas.
- `Card`: Para crear tarjetas con contenido estilizado.

Puedes definir colores, fuentes, márgenes, rellenos y más utilizando propiedades específicas de estos widgets.

### Ejemplo de Estilo en Flutter

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: Scaffold(
        appBar: AppBar(
          title: Text('Ejemplo de Estilo'),
        ),
        body: Center(
          child: Text(
            '¡Hola, Flutter!',
            style: TextStyle(
              fontSize: 24,  // Tamaño de fuente
              color: Colors.blue,  // Color de texto
              fontWeight: FontWeight.bold,  // Negrita
              fontStyle: FontStyle.italic,  // Cursiva
            ),
          ),
        ),
      ),
    );
  }
}
```

## Gestión de Paquetes con pub.dev

[pub.dev](https://pub.dev/) es el repositorio oficial de paquetes para Flutter, y es una parte esencial del ecosistema de desarrollo de Flutter. Aquí hay algunas razones por las que [pub.dev](https://pub.dev/) es importante:

- **Repositorio de Paquetes Flutter**: [pub.dev](https://pub.dev/) es el lugar donde se encuentran todos los paquetes y bibliotecas de código abierto para Flutter. Los desarrolladores pueden buscar y encontrar paquetes que se adapten a sus necesidades específicas.

- **Instalación Sencilla de Paquetes**: Para utilizar un paquete en tu proyecto Flutter, simplemente agrega una referencia a ese paquete en el archivo `pubspec.yaml` de tu proyecto. Luego, puedes ejecutar `flutter pub get` para descargar e instalar automáticamente el paquete.

- **Documentación Detallada**: La mayoría de los paquetes disponibles en [pub.dev](https://pub.dev/) están bien documentados. Esto significa que puedes encontrar información detallada sobre cómo usar el paquete y ejemplos de código para ayudarte a integrarlo en tu proyecto.

- **Versión y Compatibilidad**: [pub.dev](https://pub.dev/) proporciona información sobre las versiones de los paquetes, sus dependencias y su compatibilidad con las versiones de Flutter. Esto es importante para asegurarse de que los paquetes utilizados sean compatibles con tu proyecto.

- **Calificaciones y Comentarios**: Los usuarios pueden calificar y dejar comentarios en los paquetes que han utilizado. Esto puede ser útil para tomar decisiones informadas sobre qué paquetes utilizar en tu proyecto.

- **Herramientas de Búsqueda Avanzada**: [pub.dev](https://pub.dev/) ofrece herramientas de búsqueda avanzada que permiten a los desarrolladores encontrar paquetes específicos según sus necesidades. Puedes filtrar los resultados por popularidad, relevancia y más.

[pub.dev](https://pub.dev/) es una fuente invaluable de paquetes y bibliotecas para desarrolladores de Flutter. Te permite acceder a una amplia gama de recursos que pueden acelerar el desarrollo de tus aplicaciones, mejorar la funcionalidad y la apariencia de tus proyectos, y simplificar tareas comunes.

## Flutter CLI

El Command Line Interface (CLI) de Flutter es una herramienta poderosa para desarrolladores que permite realizar tareas como crear proyectos, ejecutar aplicaciones en dispositivos emulados o reales, gestionar paquetes, y más.

1. **Crear un Nuevo Proyecto Flutter**:

   ```unix
   flutter create nombre_del_proyecto
   ```

   Esto generará un nuevo proyecto con la estructura y archivos básicos.

2. **Ejecutar la Aplicación en un Emulador o Dispositivo Físico**:

   ```unix
   flutter run
   ```

   Asegúrate de tener un emulador en ejecución o un dispositivo físico conectado.

3. **Actualizar las Dependencias del Proyecto**:

   Para asegurarte de que todas las dependencias estén actualizadas, ejecuta:

   ```unix
   flutter pub get
   ```

   Esto actualizará las dependencias definidas en el archivo `pubspec.yaml`.

4. **Crear un APK o IPA (para Android o iOS)**:

   ```unix
   flutter build apk
   ```

   o

   ```unix
   flutter build ios
   ```

   Esto generará un archivo de instalación de la aplicación para la plataforma correspondiente.

5. **Verificar Dependencias y Configuraciones del Proyecto**:

   Para verificar si el proyecto tiene dependencias faltantes o problemas de configuración, puedes usar:

   ```unix
   flutter doctor
   ```

   Este comando mostrará una lista de recomendaciones y soluciones para problemas comunes.

6. **Ejecutar Pruebas Unitarias o de Widget**:

   Para ejecutar pruebas unitarias o de widget en tu proyecto, puedes utilizar:

   ```unix
   flutter test
   ```

   Esto ejecutará todas las pruebas definidas en tu proyecto.

## Recursos Adicionales

- [Documentación de Flutter](https://docs.flutter.dev/)
- [Flutter en GitHub](https://github.com/flutter/flutter)
- [Flutter Cheat Sheet (PDF)](https://devtalles.com/files/flutter-cheat-sheet.pdf) by [Fernando Herrera](https://fernando-herrera.com/#/about)
- [Cheat Sheet de Flutter en Gist](https://gist.github.com/jb0gie/ed298ac37f3e5c6d147688a176e67546)
- [Flutter For Dummies Cheat Sheet](https://www.dummies.com/article/technology/programming-web-design/app-development/flutter-for-dummies-cheat-sheet-271270/)
