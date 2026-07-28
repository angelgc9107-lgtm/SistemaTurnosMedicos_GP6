# Encapsulamiento

---

El **encapsulamiento** es un principio de la programación orientada a objetos que consiste en proteger el estado interno de una clase, evitando que otras clases accedan directamente a sus datos. Para ello, la información se mantiene privada y solamente puede consultarse o modificarse mediante métodos definidos por la propia clase. De esta manera se controla cómo se utilizan los datos y se preserva la consistencia del objeto.

Aplicar encapsulamiento mejora la organización del código, reduce errores y permite que la implementación interna de una clase pueda modificarse sin afectar al resto del sistema, siempre que se mantenga la misma interfaz pública. Este principio también favorece la modularidad y el mantenimiento del software. 

---

## Ejemplo en el proyecto

La clase `Turno` almacena información importante sobre un turno médico, como su estado, fecha y horario. Estos datos permanecen protegidos dentro de la clase y solo pueden modificarse utilizando los métodos definidos para ese propósito.

![Encapsulamiento — Ejemplo 1: Turno](../../diagramas/01-diagrama-clases/capturas-pilares/poo-encapsulamiento-ejemplo-1.png)

> Ver diagrama completo en: [encapsulamiento-ejemplo](../../diagramas/01-diagrama-clases/capturas-pilares/poo-encapsulamiento-ejemplo-1.png)

**Descripción del diagrama:**

La clase `Turno` mantiene sus atributos con visibilidad privada y expone únicamente los métodos necesarios para consultar o modificar su estado. De esta manera, la información queda protegida y las modificaciones se realizan de forma controlada.

**Justificación técnica:**

El encapsulamiento evita que otras clases alteren directamente los datos internos de `Turno`. Todas las modificaciones pasan por los métodos de la clase, permitiendo validar la información y mantener la coherencia del objeto durante todo su ciclo de vida.

---

## Ejemplo de Código

```java
public class Turno {

    private EstadoTurno estado;

    public EstadoTurno getEstado() {
        return estado;
    }

    public void actualizarEstado(EstadoTurno nuevoEstado) {
        this.estado = nuevoEstado;
    }
}

public class ControlSistema {

    public void confirmarTurno(Turno turno) {
        turno.actualizarEstado(EstadoTurno.CONFIRMADO);
    }
}
```

**Justificación técnica del código:**

En este ejemplo, el atributo `estado` posee acceso privado, por lo que ninguna clase puede modificarlo directamente. La única forma de cambiar su valor es mediante el método `actualizarEstado()`, definido por la propia clase `Turno`. Esto permite controlar el acceso a la información interna, proteger el estado del objeto y garantizar que los cambios se realicen de manera controlada, aplicando el principio de encapsulamiento.
