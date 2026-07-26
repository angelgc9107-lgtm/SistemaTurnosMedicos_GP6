# Polimorfismo
---

El **polimorfismo** permite que distintas clases respondan al mismo mensaje de forma diferente según su propia implementación, y que objetos de distintos tipos concretos sean tratados de manera uniforme a través de su tipo base.

En la programación orientada a objetos, el polimorfismo se expresa principalmente mediante la sobreescritura de métodos en subclases. Cuando una superclase declara un método y sus subclases lo implementan de forma diferente, el lenguaje resuelve en tiempo de ejecución cuál de esas implementaciones invocar, según el tipo concreto del objeto.

El polimorfismo está directamente ligado al principio de Sustitución de Liskov (**LSP**), que garantiza que cualquier subclase puede reemplazar a su superclase sin alterar el comportamiento esperado desde afuera. También habilita el principio Open/Closed (**OCP**): agregar una nueva subclase con comportamiento diferenciado no requiere modificar el código que la usa a través del tipo base.

En cuanto a los patrones del proyecto, los tres se apoyan en el polimorfismo. El **Strategy** lo utiliza como mecanismo central: el contexto invoca el método de la estrategia y cada implementación concreta resuelve el algoritmo de forma diferente, sin que el contexto lo sepa. El **Factory Method** retorna un tipo base y el cliente usa polimorfismo para trabajar con el objeto retornado sin conocer su tipo concreto. El **Adapter** permite que `ServicioNotificacion` invoque `enviarConfirmacion()` sobre cualquier canal —`AdaptadorWhatsApp`, `AdaptadorEmail`, `AdaptadorSMS`— de forma intercambiable, gracias a que todos implementan `INotificadorCanal`.

---

## Ejemplo en el proyecto

El método `notificar(mensaje: String)` está definido en `Persona` y sobreescrito en `Paciente` y `Medico` con comportamiento diferente. Ambas subclases responden al mismo mensaje, pero cada una lo resuelve a través de su canal específico.

![Polimorfismo — Ejemplo 1: Paciente y Medico](../../diagramas/01-diagrama-clases/capturas-pilares/poo-polimorfismo-ejemplo-1.png)

> Ver diagrama completo en: [polimorfismo-ejemplo](../../diagramas/01-diagrama-clases/capturas-pilares/poo-polimorfismo-ejemplo-1.png)

**Descripción del diagrama:** `Persona` declara `notificar(mensaje: String): void`. `Paciente` sobreescribe ese método para enviar la notificación por WhatsApp a través de `ServicioNotificacion`. `Medico` sobreescribe el mismo método para publicar una alerta en el panel médico del sistema. Desde afuera, ambos responden a la misma firma: `persona.notificar(mensaje)`.

**Justificación técnica:** `ServicioNotificacion` puede invocar `persona.notificar(mensaje)` de forma uniforme sobre cualquier subclase de `Persona`. El despacho dinámico resuelve en tiempo de ejecución qué implementación ejecutar según el tipo concreto del objeto. Si se agrega un nuevo rol con su propio canal de notificación, basta con crear una nueva subclase y sobreescribir `notificar()`: el código que la invoca no necesita modificarse.

---

## Ejemplo de Código

El siguiente fragmento en Java ilustra el polimorfismo en acción: `ServicioNotificacion` invoca `notificar()` sobre referencias de tipo `Persona` y el despacho dinámico resuelve la implementación correcta en tiempo de ejecución.

```java
public abstract class Persona {

    protected String nombre;
    protected String apellido;
    protected String telefono;

    public abstract void notificar(String mensaje);
}

public class Paciente extends Persona {

    @Override
    public void notificar(String mensaje) {
        System.out.println("[WHATSAPP → " + telefono + "] " + mensaje);
    }
}

public class Medico extends Persona {

    @Override
    public void notificar(String mensaje) {
        System.out.println("[PANEL MÉDICO → " + nombre + " " + apellido + "] " + mensaje);
    }
}

public class ServicioNotificacion {

    public void notificarCambioTurno(List<Persona> destinatarios, String mensaje) {
        for (Persona destinatario : destinatarios) {
            destinatario.notificar(mensaje);
        }
    }
}
```

**Justificación técnica del código:**

notificarCambioTurno() recorre una lista de Persona e invoca notificar() en cada iteración sin conocer si el objeto es un Paciente, Medico o Secretaria. La JVM resuelve en tiempo de ejecución qué implementación ejecutar según el tipo concreto del objeto. Esto elimina la necesidad de utilizar bloques if/else para distinguir tipos y permite incorporar nuevas subclases con su propio mecanismo de notificación sin modificar ServicioNotificacion, favoreciendo así el principio Open/Closed (OCP) gracias al uso del polimorfismo.
