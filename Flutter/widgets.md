
# Widgets en Flutter

En Flutter, todo es un **widget**. Los widgets son los componentes básicos de una aplicación, y se utilizan para definir la interfaz de usuario (UI). Un widget puede ser cualquier cosa, desde un texto, una imagen, un botón o incluso toda una pantalla. Los widgets pueden ser **stateless** o **stateful**, dependiendo de cómo gestionan los cambios en la interfaz.

## StatelessWidget
Un `StatelessWidget` es un widget que **no tiene estado**. Esto significa que su apariencia no cambia una vez que ha sido construido. Si el contenido o el diseño del widget debe cambiar, entonces tendrás que reconstruir todo el widget. Este tipo de widget es útil cuando la UI es estática y no depende de cambios dinámicos. Por ejemplo:

```dart
class MiWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Text('Hola, Mundo');
  }
}
```

- **build()**: Es el método que se encarga de construir la interfaz del widget. En el caso de `StatelessWidget`, la interfaz no cambia después de la creación.

Si intentas cambiar el texto o cualquier parte de la interfaz en respuesta a una acción del usuario (como presionar un botón) usando un `StatelessWidget`, notarás que **no ocurrirá ningún cambio visible**. Esto se debe a que los `StatelessWidget` no pueden actualizar su contenido después de ser construidos; no tienen un mecanismo para manejar cambios de estado. Por ejemplo, si intentas actualizar un texto al presionar un botón dentro de un `StatelessWidget`, el texto permanecerá igual, ya que el widget no se reconstruye automáticamente.

Por lo tanto, los `StatelessWidget` se utilizan cuando la interfaz es completamente estática y no depende de interacciones del usuario ni de datos que puedan cambiar. Son ideales para mostrar información fija, íconos, imágenes o cualquier elemento que no requiera actualización dinámica.

## StatefulWidget
Un `StatefulWidget` es un widget que **tiene estado**. Esto significa que su apariencia o su contenido pueden cambiar durante la ejecución del programa. Es necesario cuando un widget depende de datos que pueden cambiar, como cuando un usuario interactúa con la interfaz (por ejemplo, presionando un botón). A diferencia de los `StatelessWidget`, los `StatefulWidget` tienen un estado que puede modificarse.

```dart
class MiWidgetEstado extends StatefulWidget {
  @override
  _MiWidgetEstadoState createState() => _MiWidgetEstadoState();
}

class _MiWidgetEstadoState extends State<MiWidgetEstado> {
  int contador = 0;

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Contador: $contador'),
        ElevatedButton(
          onPressed: () {
            setState(() {
              contador++;
            });
          },
          child: Text('Incrementar'),
        ),
      ],
    );
  }
}
```

- **setState()**: Este método se usa para notificar a Flutter que el estado ha cambiado, lo que hace que el widget se vuelva a construir/renderizar con los nuevos valores.

## MaterialApp
`MaterialApp` es un widget que envuelve la estructura básica de una aplicación basada en Material Design, que es un sistema de diseño visual desarrollado por Google. Es un widget que establece el estilo visual y la estructura general de tu aplicación. Es muy importante cuando se trabaja con aplicaciones Flutter que siguen las pautas de diseño de Google.

```dart
MaterialApp(
  title: 'Mi Aplicación',
  home: MiWidget(),
)
```

Algunas propiedades de `MaterialApp`:
- **title**: El título de la aplicación (usado en algunas plataformas).
- **home**: El widget principal que se mostrará cuando la aplicación se inicie.
- **theme**: Permite definir el tema de la aplicación (colores, fuentes, etc.).

## Scaffold
`Scaffold` es otro widget que proporciona la estructura básica de una pantalla en una aplicación Flutter. Es utilizado para agregar características comunes a la UI, como una barra de navegación, un cuerpo, un fondo, entre otros. Generalmente se utiliza con `MaterialApp` para organizar la interfaz de la aplicación.

El uso de `Scaffold` en Flutter es fundamental cuando queremos construir pantallas que sigan las pautas de Material Design y que incluyan elementos visuales comunes como la barra de aplicaciones (`AppBar`), el botón flotante de acción (`FloatingActionButton`), el cajón de navegación (`Drawer`), entre otros. `Scaffold` facilita la organización y el manejo de estos componentes, ya que provee una estructura predefinida y gestiona automáticamente aspectos como el desplazamiento del contenido para evitar que los widgets se oculten detrás del teclado o de la barra de navegación.

**¿Qué sucede si no utilizamos `Scaffold`?**

Si decides no usar `Scaffold`, puedes seguir construyendo interfaces en Flutter, pero perderás muchas de las funcionalidades y facilidades que este widget ofrece. Por ejemplo, si intentas mostrar un `SnackBar` o un `Drawer` sin un `Scaffold`, obtendrás errores o simplemente no funcionarán, ya que estos widgets dependen de la estructura que proporciona el `Scaffold`. Además, tendrías que implementar manualmente la gestión de elementos como la barra de aplicaciones o el botón flotante, lo que puede ser más complejo y propenso a errores.

**¿Existen alternativas a `Scaffold`?**

Sí, puedes construir tu propia estructura personalizada utilizando widgets como `Container`, `Column`, `Stack`, etc. Sin embargo, esto solo es recomendable si necesitas una interfaz muy personalizada que no siga las pautas de Material Design, o si tu aplicación tiene requerimientos visuales muy específicos. En la mayoría de los casos, especialmente en aplicaciones que buscan una apariencia coherente y profesional, es preferible utilizar `Scaffold`.

En resumen, `Scaffold` no es obligatorio, pero es altamente recomendable para aprovechar todas las ventajas y componentes de Material Design en Flutter, facilitando el desarrollo y asegurando una mejor experiencia de usuario.


```dart
Scaffold(
  appBar: AppBar(
    title: Text('Mi App'),
  ),
  body: Center(
    child: Text('Hola Mundo'),
  ),
  floatingActionButton: FloatingActionButton(
    onPressed: () {},
    child: Icon(Icons.add),
  ),
)
```

Algunas propiedades de `Scaffold`:
- **appBar**: La barra de aplicaciones en la parte superior de la pantalla.
- **body**: El área principal donde se muestra el contenido de la pantalla.
- **floatingActionButton**: Un botón flotante que generalmente se usa para acciones importantes, como agregar algo o realizar una acción principal.

## Resumen
- **StatelessWidget**: Widget que no tiene estado y no cambia después de su creación.
- **StatefulWidget**: Widget que tiene estado y puede cambiar durante la ejecución de la app.
- **MaterialApp**: El widget principal que define el estilo visual y la estructura básica de una aplicación.
- **Scaffold**: Widget que proporciona una estructura común para las pantallas, como barra de navegación, contenido y botones flotantes.
