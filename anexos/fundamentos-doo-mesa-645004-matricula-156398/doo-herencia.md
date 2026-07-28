# Herencia

---

La **herencia** es un mecanismo que permite que una clase adquiera atributos y comportamientos de otra clase. Gracias a este principio es posible construir jerarquías donde las clases más específicas reutilizan características comunes y agregan funcionalidades propias. Esto favorece la reutilización del código y simplifica el mantenimiento del sistema. 

En UML, la herencia también se conoce como una relación de generalización/especialización, donde una clase general sirve como base para otras más específicas. 

---

## Ejemplo en el proyecto

La clase `Medico` hereda de `Persona`, reutilizando los datos comunes como nombre, DNI y teléfono, además de incorporar atributos propios como matrícula y especialidad junto con comportamientos específicos de su rol.

![Herencia — Ejemplo 1: Persona](../../diagramas/01-diagrama-clases/capturas-pilares/poo-herencia-ejemplo-1.png)

> Ver diagrama completo en: [herencia-ejemplo](../../diagramas/01-diagrama-clases/capturas-pilares/poo-herencia-ejemplo-1.png)

### Descripción del diagrama:

`Persona` representa la información común a los distintos participantes del sistema, mientras que `Medico` extiende esa estructura incorporando funciones propias.

### Justificación técnica:

La herencia evita repetir atributos comunes en varias clases y facilita la creación de nuevas especializaciones reutilizando una única definición base.

---

## Ejemplo de Código

```java
public class Persona {

    protected String nombre;
    protected String dni;
    protected String telefono;

    public String getDatos() {
        return nombre + " - " + dni;
    }

    public void notificar(String mensaje) {
        // Lógica de notificación
    }
}

public class Medico extends Persona {

    private String matricula;
    private String especialidad;

    public void definirDisponibilidad(Date fecha, String horario) {
        // Lógica
    }

    public void autorizarSobreturno(Turno turno) {
        // Lógica
    }

    @Override
    public void notificar(String mensaje) {
        // Notificación específica para el médico
    }
}
```

### Justificación técnica del código:

El código refleja el uso de la herencia al definir a **Medico** como una especialización de **Persona** mediante la palabra clave `extends`. De esta manera, `Medico` reutiliza los atributos y métodos comunes (`nombre`, `dni`, `telefono`, `getDatos()` y `notificar()`), incorporando además los atributos `matricula` y `especialidad`, junto con comportamientos propios como `definirDisponibilidad()` y `autorizarSobreturno()`. Esto evita duplicar información y mantiene una jerarquía de clases coherente con el modelo del sistema.
