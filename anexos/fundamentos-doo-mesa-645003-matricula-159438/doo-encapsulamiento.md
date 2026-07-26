# Encapsulamiento
---

El **encapsulamiento** agrupa datos y comportamiento dentro de una clase, ocultando los detalles de su estado interno y exponiendo solo lo necesario mediante una interfaz pública controlada. En la práctica, significa que los atributos de una clase tienen visibilidad restringida —privada o protegida— y que el acceso o la modificación de esos atributos solo es posible a través de métodos explícitamente diseñados para ese fin.

En la programación orientada a objetos, el encapsulamiento protege la integridad del estado interno: si cualquier clase pudiera modificar directamente los atributos de otra, sería imposible garantizar que ese estado se mantenga coherente.

El encapsulamiento favorece la aplicación del principio de Responsabilidad Única (SRP), ya que permite exponer únicamente las operaciones relacionadas con la responsabilidad de una clase y ocultar los detalles de su implementación. También favorece el principio Open/Closed (OCP), ya que la implementación interna puede modificarse sin afectar a las clases que utilizan su interfaz pública.

En cuanto a los patrones del proyecto, los tres aplican el encapsulamiento como base. El Factory Method encapsula la lógica de creación dentro del método de fábrica, de modo que el cliente no conoce qué clase concreta se instancia ni cómo se configura. El Strategy encapsula cada algoritmo en una clase independiente, ocultando su implementación al contexto que lo utiliza. El Adapter encapsula la traducción entre la interfaz INotificadorCanal y la API del proveedor externo, permitiendo que ServicioNotificacion interactúe con una interfaz uniforme sin conocer los detalles de cada canal.

---

## Ejemplo en el proyecto

La clase `Turno` encapsula su estado interno con visibilidad privada y controla cualquier modificación a través de métodos específicos, que son los únicos puntos de acceso válidos para cambiar su ciclo de vida.

![Encapsulamiento — Ejemplo 1: Turno](../../diagramas/01-diagrama-clases/capturas-pilares/poo-encapsulamiento-ejemplo-1.png)

> Ver diagrama completo en: [encapsulamiento-ejemplo](../../diagramas/01-diagrama-clases/capturas-pilares/poo-encapsulamiento-ejemplo-1.png)

**Descripción del diagrama:** El fragmento muestra que `fecha`, `hora`, `estado` y `tipoConsulta` tienen visibilidad privada (`-`). La única forma de cambiar el estado de un turno es invocar `establecerEstado(nuevoEstado)` o `cambiarEstado(nuevoEstado)`.

**Justificación técnica:** Un turno médico tiene invariantes de dominio estrictas: el estado solo puede transitar de *Pendiente* a *Presente* o *Cancelado*; no puede pasar de *Cancelado* a *Presente*. Si `estado` fuera un campo público, cualquier clase podría asignar un valor inválido y corromper el historial y los registros de presencia. El encapsulamiento garantiza que `cambiarEstado()` sea el único punto donde esa transición ocurre, permitiendo centralizar la validación en un solo lugar. Esto cumple **SRP**: la responsabilidad de validar y aplicar transiciones de estado pertenece exclusivamente a `Turno`.

---

## Ejemplo de Código

El siguiente fragmento en Java muestra cómo `Turno` encapsula su estado interno y solo permite modificarlo a través de métodos que validan la transición.

```java
public class Turno {

    private String estado;
    private Date   fecha;
    private Time   hora;

    public Turno(Date fecha, Time hora) {
        this.fecha  = fecha;
        this.hora   = hora;
        this.estado = "Pendiente";
    }

    public String getEstado() {
        return estado;
    }

    public void cambiarEstado(String nuevoEstado) {
        Map<String, Set<String>> transiciones = Map.of(
            "Pendiente",    Set.of("Presente", "Cancelado", "Reprogramado"),
            "Reprogramado", Set.of("Presente", "Cancelado")
        );

        if (!transiciones.getOrDefault(this.estado, Set.of()).contains(nuevoEstado)) {
            throw new IllegalStateException(
                "Transición inválida: " + this.estado + " → " + nuevoEstado);
        }
        this.estado = nuevoEstado;
    }
}
```

**Justificación técnica del código:**

Turno no expone un setter directo para estado. La única forma de modificarlo es mediante cambiarEstado(), que comprueba si la transición solicitada es válida antes de aplicarla. De esta manera, clases como Agenda, ControlSistema o Secretaria no pueden modificar directamente el estado del turno ni dejarlo en una situación incoherente. Las reglas de transición permanecen centralizadas dentro de Turno, lo que facilita su mantenimiento y protege la consistencia del objeto.
