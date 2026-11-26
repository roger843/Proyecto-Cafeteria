# Sistema de pedidos para cafetería

Aplicación de escritorio desarrollada en Java para gestionar el menú, los pedidos y las ventas de una cafetería. Cuenta con una interfaz gráfica en Swing y una versión por consola. Ambas utilizan los mismos servicios y pueden acceder a los mismos datos locales.

**Integrantes:** Roger Barros, Andres Rodriguez y Juan Gaitan.

## Funcionalidades

- Crear, consultar, editar y eliminar bebidas, platos y adiciones.
- Personalizar productos y calcular automáticamente su descripción y precio.
- Armar combos paso a paso, guardarlos en el menú y reutilizarlos en pedidos.
- Registrar pedidos con cantidades, personalizaciones y descuentos.
- Cambiar el estado de un pedido de pendiente a en preparación, listo y entregado.
- Generar avisos para cocina, caja y mesero cuando cambia el estado de un pedido.
- Configurar promociones por día de la semana y aplicar automáticamente la de mayor descuento cuando coinciden varias.
- Registrar pagos, ingresos y egresos, realizar cierres de caja y consultar reportes de ventas.
- Consultar el historial de pedidos y crear o restaurar copias de seguridad.

## Requisitos

- Java 21 o posterior para ejecutar el programa.
- JDK 21 o posterior para compilar el código o abrirlo en NetBeans.
- Git si vas a clonar el repositorio.

Puedes verificar tu versión de Java con `java -version`.

## Descargar el proyecto

Desde GitHub, selecciona **Code → Download ZIP**, extrae el archivo y abre la carpeta que contiene este README. También puedes copiar la URL HTTPS desde **Code** y clonar el repositorio con:

```bash
git clone "URL_DEL_REPOSITORIO"
```

Reemplaza `URL_DEL_REPOSITORIO` por la URL copiada. Si tienes el archivo de entrega `Cafeteria_Java.zip`, extráelo y abre la carpeta `Cafeteria`.

## Compilar y ejecutar

Si la carpeta ya contiene `cafeteria.jar`, puedes ir directamente a la tabla de ejecución. Si descargaste el código desde GitHub, abre una terminal en la raíz del proyecto y usa el comando de tu sistema:

| Sistema | Comando de compilación |
| --- | --- |
| Windows PowerShell | `.\compilar.bat` |
| Linux o macOS | `sh compilar.sh` |

El script compila el código, ejecuta las pruebas automatizadas y genera `cafeteria.jar` al finalizar correctamente.

| Modo | Desde la terminal, en la raíz del proyecto | En Windows |
| --- | --- | --- |
| Interfaz gráfica | `java -jar cafeteria.jar --gui` | Doble clic en `iniciar-grafica.bat` |
| Consola | `java -jar cafeteria.jar --consola` | Doble clic en `iniciar-consola.bat` |

## Usuarios de demostración

| Usuario | Contraseña | Funciones principales |
| --- | --- | --- |
| `admin` | `admin123` | Acceso a todas las funciones. |
| `mesero` | `mesero123` | Registra pedidos, arma combos y marca como entregados los pedidos listos. |
| `cocina` | `cocina123` | Cambia los pedidos a en preparación y listo. |
| `caja` | `caja123` | Registra pagos y movimientos, realiza cierres y consulta ventas. |

Para probar todas las funciones desde una sola sesión, inicia como `admin`.

## Abrir el código en NetBeans

1. Crea un proyecto de **Java con Ant a partir de código existente**.
2. Agrega `src/main/java` como carpeta de código fuente. También puedes agregar `src/test/java` como carpeta de pruebas.
3. Configura el **JDK 21** como plataforma del proyecto y **`cafeteria.Main`** como clase principal.
4. Ejecuta el proyecto para abrir la interfaz gráfica. Para usar la versión por consola, ejecuta el JAR desde una terminal con el argumento `--consola`.
5. Para compartir los datos con el JAR, configura como directorio de trabajo la carpeta que contiene este README.

## Arquitectura y patrones de diseño

El proyecto usa una arquitectura en capas. La consola y la interfaz gráfica invocan los servicios de aplicación, que coordinan las reglas del dominio y acceden a los datos mediante interfaces de repositorio.

| Patrón | Clases principales | Aplicación |
| --- | --- | --- |
| **Decorator** | `Producto`, `ProductoDecorador`, `Adicion` | Una adición envuelve un producto y actualiza su descripción y precio. |
| **Builder** | `ComboBuilder`, `ConstructorCombo`, `Combo` | Construye un combo paso a paso y valida sus componentes antes de terminarlo. |
| **Observer** | `Pedido`, `ObservadorPedido`, `ObservadorCocina`, `ObservadorCaja`, `ObservadorMesero` | Notifica a las tres áreas después de guardar un cambio de estado. |

Las pruebas se encuentran en `src/test/java`. Cubren los tres patrones, los permisos, las promociones, el flujo de caja y la recuperación de datos.

## Datos y respaldos

La aplicación crea automáticamente la carpeta `datos/` en su directorio de trabajo y guarda la información en `datos/cafeteria.dat`. Para pasar de la versión gráfica a la consola usando los mismos datos, cierra primero la instancia abierta.

Desde **Administración**, el usuario `admin` puede crear un respaldo o restaurar uno existente.
