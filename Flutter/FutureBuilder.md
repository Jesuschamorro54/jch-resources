# ¿Qué es un Future Builder en Flutter?

Los **Future Builder** están diseñados para manejar tareas **asíncronas** (es decir, que toman tiempo en completarse).

---

## 🕒 ¿Qué es un `Future`?

Un **`Future`** en Dart representa una **tarea que se ejecutará en el futuro**, como:

- Consultar una API en internet.
- Leer un archivo del dispositivo.
- Esperar un temporizador.

### Ejemplo:

```dart
Future<String> obtenerNombre() async {
  await Future.delayed(Duration(seconds: 2));
  return "Sergio";
}

```

### Ejemplo completo
```dart
FutureBuilder<String>(
  future: obtenerNombre(), // función que devuelve un Future
  builder: (context, snapshot) {
    if (snapshot.connectionState == ConnectionState.waiting) {
      return CircularProgressIndicator(); // Mientras se carga
    } else if (snapshot.hasError) {
      return Text('Error: ${snapshot.error}'); // Si hay error
    } else {
      return Text('Hola, ${snapshot.data}'); // Cuando tiene el dato
    }
  },
)

```
