# 🧠 Antipatrones fuera de GoF
## 🏗️ Diseño de Software, Arquitectura, Bases de Datos y Colaboración

---

## 🏗️ Diseño de Software

### 🔹 1. God Object
**Comprensión:**  
Ocurre cuando una sola clase asume demasiadas responsabilidades. Viola el principio de *Responsabilidad Única (SRP)*.  
**Ejemplo Técnico:**  
```java
class Sistema {
    void gestionarUsuarios() { }
    void generarReportes() { }
    void procesarPagos() { }
    void manejarInventario() { }
}
````

**Consecuencias:**
Dificultad para mantener, probar y escalar el sistema; cualquier cambio puede afectar todo el proyecto.
**Solución Correctiva:**
Aplicar descomposición modular, usar *Facade* o dividir en servicios especializados.

---

### 🔹 2. Shotgun Surgery

**Comprensión:**
Un cambio pequeño requiere modificaciones en muchas clases diferentes.
**Ejemplo Técnico:**
Actualizar el formato de fecha en 10 clases distintas.
**Consecuencias:**
Aumenta el riesgo de errores y el tiempo de mantenimiento.
**Solución Correctiva:**
Centralizar la lógica repetida en una clase común o módulo de utilidades.

---

### 🔹 3. Lava Flow

**Comprensión:**
Fragmentos de código obsoleto o experimental que permanecen sin uso.
**Ejemplo Técnico:**
Funciones antiguas sin referencia pero aún compiladas.
**Consecuencias:**
Incrementa la complejidad y confunde a los desarrolladores.
**Solución Correctiva:**
Refactorizar periódicamente y eliminar código muerto con control de versiones.

---

### 🔹 4. Golden Hammer

**Comprensión:**
Usar siempre la misma tecnología o patrón para todos los problemas.
**Ejemplo Técnico:**
Usar bases de datos relacionales para almacenar imágenes o logs.
**Consecuencias:**
Baja eficiencia y rigidez tecnológica.
**Solución Correctiva:**
Elegir herramientas según el contexto y aplicar *Polyglot Programming*.

---

### 🔹 5. Poltergeist Classes

**Comprensión:**
Clases temporales que solo delegan llamadas a otras clases.
**Ejemplo Técnico:**

```java
class PedidoController {
    void crear() { new PedidoService().crear(); }
}
```

**Consecuencias:**
Aumenta la complejidad y acoplamiento innecesario.
**Solución Correctiva:**
Eliminar intermediarios o integrar la lógica directamente en la clase responsable.

---

### 🔹 6. Hard-Coded Constants / Magic Numbers

**Comprensión:**
Valores fijos sin contexto dentro del código.
**Ejemplo Técnico:**

```python
if velocidad > 255:
    print("Demasiado rápido")
```

**Consecuencias:**
Dificultad para modificar y entender el significado del valor.
**Solución Correctiva:**
Usar constantes con nombre o variables de configuración.

---

### 🔹 7. Circular Dependency

**Comprensión:**
Dos o más módulos se importan entre sí.
**Ejemplo Técnico:**
`ClaseA` depende de `ClaseB` y viceversa.
**Consecuencias:**
Problemas de compilación, carga y acoplamiento.
**Solución Correctiva:**
Romper dependencias mediante interfaces o inversión de dependencias (DIP).

---

### 🔹 8. Premature Optimization

**Comprensión:**
Optimizar sin haber identificado cuellos de botella reales.
**Ejemplo Técnico:**
Implementar hilos o caching antes de medir rendimiento.
**Consecuencias:**
Código complejo, poco legible y difícil de mantener.
**Solución Correctiva:**
Primero medir (profiling), luego optimizar con evidencia.

---

### 🔹 9. Feature Envy

**Comprensión:**
Una clase depende excesivamente de los datos o métodos de otra clase.
**Ejemplo Técnico:**

```java
if(cliente.getEdad() > 18 && cliente.getSaldo() > 1000)
    descuento = cliente.getSaldo() * 0.05;
```

**Consecuencias:**
Cohesión baja y alto acoplamiento.
**Solución Correctiva:**
Mover la lógica al objeto que posee los datos (refactor *Move Method*).

---

## 🔁 Arquitectura y Mantenimiento

### 🔹 Big Ball of Mud

**Comprensión:**
Sistema sin estructura ni separación clara de responsabilidades.
**Ejemplo:**
Aplicaciones donde todo el código está mezclado.
**Consecuencias:**
Difícil de mantener, probar o escalar.
**Solución Correctiva:**
Usar arquitectura en capas, MVC o microservicios.

---

### 🔹 Stovepipe System

**Comprensión:**
Subsistemas aislados que no comparten componentes ni comunicación.
**Consecuencias:**
Duplicación de esfuerzo y problemas de integración.
**Solución Correctiva:**
Usar APIs, servicios compartidos y estándares de comunicación.

---

### 🔹 Reinventing the Wheel

**Comprensión:**
Recrear funcionalidades ya existentes.
**Ejemplo:**
Crear tu propio sistema de logs o ORM.
**Consecuencias:**
Tiempo perdido y errores ya resueltos por herramientas existentes.
**Solución Correctiva:**
Reutilizar bibliotecas y frameworks probados.

---

### 🔹 Vendor Lock-In

**Comprensión:**
Dependencia fuerte de un proveedor o plataforma.
**Ejemplo:**
Usar servicios exclusivos de un cloud sin portabilidad.
**Consecuencias:**
Costos altos y dificultad para migrar.
**Solución Correctiva:**
Usar estándares abiertos y capas de abstracción.

---

### 🔹 Design by Committee

**Comprensión:**
Demasiadas personas tomando decisiones de diseño.
**Consecuencias:**
Arquitectura inconsistente y pérdida de enfoque.
**Solución Correctiva:**
Asignar un arquitecto líder y documentar decisiones.

---

### 🔹 Over / Under Engineering

**Comprensión:**
Diseñar demasiado o demasiado poco.
**Consecuencias:**
Complejidad innecesaria o falta de escalabilidad.
**Solución Correctiva:**
Aplicar principios *KISS* y *YAGNI*.

---

### 🔹 Architecture Sinkhole

**Comprensión:**
Mucho diseño pero poca funcionalidad real.
**Consecuencias:**
Retrasos y baja productividad.
**Solución Correctiva:**
Iterar con entregas de valor desde etapas tempranas.

---

### 🔹 Dead Code / Accidental Complexity

**Comprensión:**
Código no utilizado o lógica innecesaria.
**Consecuencias:**
Reduce el rendimiento y confunde al equipo.
**Solución Correctiva:**
Eliminarlo con revisiones periódicas y herramientas de análisis estático.

---

## 🧩 Bases de Datos y Persistencia

### 🔹 One Table to Rule Them All

**Comprensión:**
Todo se almacena en una sola tabla.
**Consecuencias:**
Consultas lentas y datos inconsistentes.
**Solución Correctiva:**
Aplicar normalización y diseño relacional.

---

### 🔹 Impedance Mismatch

**Comprensión:**
Diferencia entre el modelo de objetos y el modelo relacional.
**Consecuencias:**
Dificultad para mapear objetos a tablas.
**Solución Correctiva:**
Usar ORMs o DTOs bien diseñados.

---

### 🔹 No Index Hell

**Comprensión:**
Falta de índices adecuados en la base de datos.
**Consecuencias:**
Consultas lentas y alto consumo de recursos.
**Solución Correctiva:**
Definir índices según patrones de consulta.

---

### 🔹 Hard Deletes sin respaldo

**Comprensión:**
Eliminar registros sin copia o bitácora.
**Consecuencias:**
Pérdida irreversible de información.
**Solución Correctiva:**
Usar *Soft Deletes* o respaldos automáticos.

---

### 🔹 Massive Stored Procedures

**Comprensión:**
Demasiada lógica en procedimientos almacenados.
**Consecuencias:**
Difícil mantenimiento y poca portabilidad.
**Solución Correctiva:**
Equilibrar responsabilidades entre base de datos y backend.

---

## 💬 Comunicación y Colaboración

### 🔹 Not Invented Here (NIH)

**Comprensión:**
Rechazo a usar soluciones externas.
**Consecuencias:**
Duplicación de esfuerzo y retrasos.
**Solución Correctiva:**
Evaluar tecnologías de forma objetiva.

---

### 🔹 Mushroom Management

**Comprensión:**
Mantener al equipo sin información clara.
**Consecuencias:**
Desmotivación y errores de comunicación.
**Solución Correctiva:**
Transparencia y comunicación frecuente.

---

### 🔹 Hero Syndrome

**Comprensión:**
Depender de una sola persona para tareas críticas.
**Consecuencias:**
Riesgo alto si esa persona se ausenta (bajo *Bus Factor*).
**Solución Correctiva:**
Documentar procesos y distribuir conocimientos.

---

### 🔹 Version Chaos

**Comprensión:**
Falta de control de versiones.
**Consecuencias:**
Conflictos, pérdida de trabajo y caos en el código.
**Solución Correctiva:**
Usar sistemas como *Git* y flujos como *GitFlow*.

---

### 🔹 Death by Meetings

**Comprensión:**
Exceso de reuniones improductivas.
**Consecuencias:**
Pérdida de tiempo y productividad.
**Solución Correctiva:**
Reuniones breves con agenda clara.

---

### 🔹 Cargo Cult Programming

**Comprensión:**
Copiar código sin entender su funcionamiento.
**Consecuencias:**
Errores ocultos y dependencia ciega.
**Solución Correctiva:**
Comprender el propósito antes de aplicar soluciones.

---

## 🚀 DevOps, Seguridad y Ciclo de Vida

### 🔹 Continuous Deployment without Testing

**Comprensión:**
Desplegar código sin pruebas automatizadas.
**Consecuencias:**
Errores en producción y pérdida de estabilidad.
**Solución Correctiva:**
Integrar *Testing* y *CI/CD* con validaciones automáticas.

---

### 🔹 Environment Drift

**Comprensión:**
Diferencias entre entornos de desarrollo, pruebas y producción.
**Consecuencias:**
Errores difíciles de reproducir.
**Solución Correctiva:**
Usar *Infraestructura como Código (IaC)* y contenedores.

---

### 🔹 Passwords in Code

**Comprensión:**
Guardar contraseñas directamente en el código.
**Consecuencias:**
Vulnerabilidades graves y filtración de datos.
**Solución Correctiva:**
Usar *Variables de entorno* o *Vaults* seguros.

---

### 🔹 Logging Everything

**Comprensión:**
Registrar toda la información sin filtrado.
**Consecuencias:**
Rendimiento bajo y exposición de datos sensibles.
**Solución Correctiva:**
Definir niveles de log (info, warn, error) y anonimizar datos.

---


**Autor:** Rolando Jassiel Castro Hernandez
**Materia:** Diseño de Software
**Tema:** Antipatrones fuera de GoF

```
