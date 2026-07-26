# Herencia
---

La **herencia** es el mecanismo mediante el cual una clase (subclase) hereda de otra (superclase), reutilizando sus atributos y métodos y especializando su comportamiento según el rol concreto que representa en el dominio.

En la programación orientada a objetos, la herencia cumple dos funciones principales. La primera es la reutilización de código: los atributos y métodos comunes se definen una sola vez en la superclase y son heredados por las subclases. La segunda es la creación de una jerarquía de tipos que permite aplicar el polimorfismo, ya que las subclases pueden utilizarse donde se espere una instancia de la superclase.

La herencia está directamente ligada al principio de Sustitución de Liskov (LSP), que establece que una subclase debe poder reemplazar a su superclase sin alterar el comportamiento esperado.También favorece el principio Open/Closed (OCP), ya que permite incorporar nuevas especializaciones mediante nuevas subclases sin modificar la superclase ni las clases que dependen de ella.

En cuanto a los patrones del proyecto, el Factory Method aprovecha la jerarquía de herencia para devolver instancias concretas, como Medico o Paciente, a través del tipo base Persona, sin que el cliente conozca la subclase exacta.

---

## Ejemplo en el proyecto

La clase abstracta `Persona` define la identidad y el comportamiento común a todos los actores del sistema. `Medico` hereda esa base y la especializa con atributos y operaciones propias de su rol clínico.

![Herencia — Ejemplo 1: Persona → Medico](../../diagramas/01-diagrama-clases/capturas-pilares/poo-herencia-ejemplo-1.png)

> Ver diagrama completo en: [herencia-ejemplo](../../diagramas/01-diagrama-clases/capturas-pilares/poo-herencia-ejemplo-1.png)

**Descripción del diagrama:** `Persona` define los atributos protegidos `nombre`, `apellido`, `dni`, `telefono`, `email`, `rol` y `estadoActivo`, y los métodos `getDatos()`, `getContacto()` y `notificar()`. `Medico` hereda todos esos atributos y métodos, y agrega `matricula` y `especialidad` como propios, junto con `definirDisponibilidad()`, `autorizarSobreturno()` y `obtenerAgenda()`.

**Justificación técnica:** La relación es semánticamente válida porque un médico *es* una persona del sistema con datos de identidad y contacto compartidos. La herencia evita duplicar esos atributos en `Medico`, `Paciente` y `Secretaria`, y garantiza que cualquier código que opere sobre `Persona` —como un módulo de notificaciones— funcione automáticamente con cualquier subclase sin modificación. La jerarquía respeta **LSP**: `Medico` cumple el contrato completo de `Persona` y lo extiende con capacidades clínicas sin contradecirlo.

---

## Ejemplo de Código

El siguiente fragmento en Java ilustra la jerarquía de herencia entre `Persona` y `Medico`, mostrando la reutilización de atributos y la especialización de comportamiento.

```java
public abstract class Persona {

    protected String  nombre;
    protected String  apellido;
    protected String  dni;
    protected String  telefono;
    protected String  email;
    protected boolean estadoActivo;

    public Persona(String nombre, String apellido, String dni,
                   String telefono, String email) {
        this.nombre      = nombre;
        this.apellido    = apellido;
        this.dni         = dni;
        this.telefono    = telefono;
        this.email       = email;
        this.estadoActivo = true;
    }

    public String getDatos() {
        return apellido + ", " + nombre + " [DNI: " + dni + "]";
    }

    public String getContacto() {
        return "Tel: " + telefono + " | Email: " + email;
    }

    public abstract void notificar(String mensaje);
}

public class Medico extends Persona {

    private String matricula;
    private String especialidad;

    public Medico(String nombre, String apellido, String dni,
                  String telefono, String email,
                  String matricula, String especialidad) {
        super(nombre, apellido, dni, telefono, email);
        this.matricula    = matricula;
        this.especialidad = especialidad;
    }

    @Override
    public void notificar(String mensaje) {
        System.out.println("[PANEL MÉDICO] " + getDatos() + ": " + mensaje);
    }

    public void definirDisponibilidad(Date fecha, String horario) {
        // Lógica de disponibilidad clínica
    }
}
```

**Justificación técnica del código:**

Medico hereda de Persona los atributos y métodos comunes, como nombre, apellido, dni, getDatos() y getContacto(). Su constructor utiliza super(...) para inicializar la parte común del objeto, evitando repetir esa lógica. Además, Medico especializa el comportamiento heredado mediante la implementación de notificar() y agrega operaciones propias, como definirDisponibilidad(). La jerarquía permite tratar una instancia de Medico como una Persona, siempre que la subclase mantenga el comportamiento esperado por el contrato de la superclase, respetando así el principio de Sustitución de Liskov.