# Dart Cheat Sheet

## Introducción a Dart

- [Sitio web oficial de Dart](https://dart.dev/)
- Dart es un lenguaje de programación de código abierto desarrollado por Google.

## Variables

### Declaración de variables

```dart
var nombre = 'Juan';
int edad = 30;
final pi = 3.14159;
```

### Tipos de variables

- `var`: Inferencia de tipo.
- `int`: Números enteros.
- `double`: Números de punto flotante.
- `String`: Cadenas de texto.
- `bool`: Valores booleanos.

### Interpolación de Strings

```dart
var nombre = 'Juan';
print('Hola, $nombre'); // Imprime 'Hola, Juan'
```

## Funciones

### Funciones de flecha (Arrow Functions)

```dart
int multiplicar(int a, int b) => a * b;
```

## Estructuras de control

### If Statement

```dart
if (condición) {
  // Código a ejecutar si la condición es verdadera
} else {
  // Código a ejecutar si la condición es falsa
}
```

### Switch Statement

```dart
switch (valor) {
  case 1:
    // Código si valor es 1
    break;
  case 2:
    // Código si valor es 2
    break;
  default:
    // Código si no coincide con ningún caso
}
```

## Listas

### Declaración de listas

```dart
var frutas = ['manzana', 'banana', 'naranja'];
```

### Lista de Objetos, Sets y Maps

```dart
var personas = [
  {'nombre': 'Juan', 'edad': 30},
  {'nombre': 'María', 'edad': 25},
];

var conjunto = Set.from([1, 2, 3]);

var mapa = {
  'clave1': 'valor1',
  'clave2': 'valor2',
};
```

## Operación de Cascades

```dart
class Persona {
  String nombre;
  int edad;

  Persona(this.nombre, this.edad);

  void presentarse() {
    print('Me llamo $nombre y tengo $edad años.');
  }
}

void main() {
  var juan = Persona('Juan', 30)
    ..presentarse()
    ..edad = 31
    ..presentarse();
}
```

## Clases y Objetos

### Declaración de una clase

```dart
class Persona {
  String _nombre; // Propiedad privada
  int _edad;       // Propiedad privada

  Persona(this._nombre, this._edad);

  void _metodoPrivado() {
    // Método privado
  }
}
```

### Creación de objetos

```dart
var persona = Persona('Juan', 30);
```

## Programación Asíncrona (Future, Async, Await)

```dart
Future<void> tareaAsincrona() async {
  print('Comenzando la tarea...');
  await Future.delayed(Duration(seconds: 2));
  print('Tarea completada.');
}

void main() {
  tareaAsincrona();
  print('La ejecución continúa mientras se realiza la tarea asincrónica.');
}
```

## Excepciones

### Try-Catch

```dart
try {
  // Código que puede lanzar una excepción
} catch (e) {
  print('Ocurrió una excepción: $e');
}
```

## Recursos Adicionales

- [Documentación oficial de Dart](https://dart.dev/guides)
- [Dart en GitHub](https://github.com/dart-lang)
- [Dart Quick Reference](https://quickref.me/dart.html)
- [Dart Cheat Sheet en Español (PDF)](https://devtalles.com/files/dart-cheat-sheet.pdf) by [Fernando Herrera](https://fernando-herrera.com/#/about)
- [Dart Cheat Sheet - Codelabs](https://dart.dev/codelabs/dart-cheatsheet)
