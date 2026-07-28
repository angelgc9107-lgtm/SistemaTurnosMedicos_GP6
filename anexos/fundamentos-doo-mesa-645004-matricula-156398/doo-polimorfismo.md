# Polimorfismo

---

El **polimorfismo** permite que objetos pertenecientes a una misma jerarquía respondan de manera diferente ante una misma operación. Gracias a este principio es posible escribir código genérico que funcione con distintos tipos de objetos, favoreciendo la flexibilidad y la posibilidad de extender el sistema sin modificar el código existente. 

---

## Ejemplo en el proyecto

Las clases `Paciente` y `Medico` pueden redefinir una operación heredada desde `Persona`, ejecutando un comportamiento diferente según el tipo de objeto.

![Polimorfismo — Ejemplo 1: Persona](../../diagramas/01-diagrama-clases/capturas-pilares/poo-polimorfismo-ejemplo-1.png)

> Ver diagrama completo en: [polimorfismo-ejemplo](../../diagramas/01-diagrama-clases/capturas-pilares/poo-polimorfismo-ejemplo-1.png)

**Descripción del diagrama:**

Las clases derivadas comparten una misma estructura heredada, pero cada una puede implementar determinados comportamientos de forma diferente.

**Justificación técnica:**

El polimorfismo permite trabajar con referencias del tipo `Persona` sin importar si el objeto concreto corresponde a un `Paciente` o una `Medico`, ya que cada uno responderá según su propia implementación.

---

## Ejemplo de Código

```java
public class Persona {

    public void mostrarRol() {
        System.out.println("Persona del sistema");
    }
}

public class Paciente extends Persona {

    @Override
    public void mostrarRol() {
        System.out.println("Paciente");
    }
}

public class Medico extends Persona {

    @Override
    public void mostrarRol() {
        System.out.println("Medico");
    }
}
```

**Justificación técnica del código:**

Aunque las clases heredan el mismo método, cada una proporciona una implementación diferente. Esto demuestra cómo un mismo mensaje puede producir comportamientos distintos según el objeto que lo reciba, representando el principio de polimorfismo.
