# UML_y_Markdown

```mermaid
classDiagram
    direction TB

    %% ─────────────── PUNTO DE ENTRADA ───────────────
    class Main {
        +main(args: String[]) void
    }

    %% ─────────────── CONTROLADOR ───────────────
    class ControladorCalculadora {
        -vista: VistaCalculadora
        -gestorOperaciones: GestorOperaciones
        +ControladorCalculadora(vista: VistaCalculadora)
        +ejecutar() void
    }

    %% ─────────────── LÓGICA ───────────────
    class GestorOperaciones {
        -calculadora: Calculadora
        +GestorOperaciones()
        +calcularResultado(operacion: Operacion) double
        +esOperadorValido(operador: char) boolean
    }

    %% ─────────────── MODELO ───────────────
    class Calculadora {
        +sumar(a: double, b: double) double
        +restar(a: double, b: double) double
        +multiplicar(a: double, b: double) double
        +dividir(a: double, b: double) double
    }

    class Operacion {
        -operandoA: double
        -operandoB: double
        -operador: char
        +Operacion(a: double, b: double, op: char)
        +getOperandoA() double
        +getOperandoB() double
        +getOperador() char
        +toString() String
    }

    %% ─────────────── VISTA ───────────────
    class VistaCalculadora {
        <<interface>>
        +pedirPrimerNumero() double
        +pedirSegundoNumero() double
        +pedirOperador() char
        +mostrarResultado(op: Operacion, resultado: double) void
        +mostrarError(mensaje: String) void
    }

    class VistaConsola {
        -scanner: Scanner
        +pedirPrimerNumero() double
        +pedirSegundoNumero() double
        +pedirOperador() char
        +mostrarResultado(op: Operacion, resultado: double) void
        +mostrarError(mensaje: String) void
    }

    class VistaGrafica {
        <<future>>
        +pedirPrimerNumero() double
        +pedirSegundoNumero() double
        +pedirOperador() char
        +mostrarResultado(op: Operacion, resultado: double) void
        +mostrarError(mensaje: String) void
    }

    %% ─────────────── RELACIONES ───────────────
    Main --> ControladorCalculadora : crea y lanza

    ControladorCalculadora --> VistaCalculadora : usa (interfaz)
    ControladorCalculadora --> GestorOperaciones : delega cálculo
    ControladorCalculadora ..> Operacion : construye

    GestorOperaciones --> Calculadora : delega operación
    GestorOperaciones ..> Operacion : lee datos de

    VistaConsola ..|> VistaCalculadora : implementa
    VistaGrafica ..|> VistaCalculadora : implementará
```
