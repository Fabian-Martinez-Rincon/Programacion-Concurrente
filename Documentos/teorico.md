### Modelo-Vista-Controlador (MVC)
El patrón Modelo-Vista-Controlador (MVC) es una arquitectura de software que divide una aplicación en tres componentes interconectados para mejorar la flexibilidad y la organización del código:

**Modelo (Model):**

Representa la estructura de datos y lógica de negocio de la aplicación.
Responde a consultas sobre su estado y puede modificarlo
No sabe nada sobre la interfaz de usuario.

**Vista (View):**

Presenta los datos al usuario y gestiona la interacción.
Recupera información del modelo y la muestra de una manera adecuada.
No realiza cambios en los datos, solo presenta la información.

**Controlador (Controller):**

Actúa como intermediario entre el modelo y la vista.
Interpreta las acciones del usuario, procesa las entradas y coordina la actualización del modelo y la vista.

### **Relación con HTML y CSS**
**HTML (HyperText Markup Language):**

Representa la estructura básica de la página web y el contenido.
Encaja principalmente en la capa de Vista (View) del patrón MVC.
Define cómo se deben mostrar los datos y cómo interactuar con ellos en la interfaz del usuario.

**CSS (Cascading Style Sheets):**

Controla la presentación y el estilo de los elementos HTML.
Complementa a HTML y permite definir el diseño, colores, fuentes, tamaños y aspecto general de la interfaz.
Encaja dentro de la capa de Vista (View) para garantizar que la presentación de la interfaz de usuario sea atractiva y coherente.

Usando lo trabajado en la práctica explicá algún código asociado  a la vista (5 pts.)

---

Claro, este código es un ejemplo de un archivo de plantilla en Jinja2, un motor de plantillas utilizado comúnmente en aplicaciones web con Flask u otros frameworks similares. Aquí está una breve explicación:

1. **`{% extends "layout.html" %}`**:
   - Indica que esta plantilla extiende otra plantilla llamada "layout.html". Hereda su estructura y contenido, permitiendo agregar contenido específico en bloques.

2. **`{% import "_macros/form.html" as Form %}`**:
   - Importa un conjunto de macros (fragmentos de código reutilizables) definidos en "_macros/form.html" y los nombra como "Form", para su uso en esta plantilla.

3. **`{% block head %} ... {% endblock %}`**:
   - Define un bloque llamado "head". Los bloques son áreas en los que la plantilla hija puede agregar contenido adicional que se insertará en la plantilla padre en el mismo bloque.

4. **`{% block content %} ... {% endblock %}`**:
   - Define un bloque llamado "content". Aquí es donde se espera que la plantilla hija agregue su contenido específico.

5. **`<main class="flex-1 flex flex-col"> ... </main>`**:
   - Define un bloque `<main>` con ciertas clases CSS aplicadas. Dentro de este bloque, se coloca el contenido principal de la página.

6. **`<h1 class="text-3xl font-semibold mt-[1em] ml-2">Creación de Servicio</h1>`**:
   - Es un encabezado HTML que muestra "Creación de Servicio" con estilos CSS aplicados.

7. **`{% call Form.render_form(form) %} ... {% endcall %}`**:
   - Llama a un macro llamado "render_form" definido en "_macros/form.html", pasando el objeto "form" como argumento. Este macro probablemente renderiza un formulario.

8. **`{{ Form.button_submit("Crear") }}`**:
   - Renderiza un botón "Crear" utilizando el macro "button_submit" del objeto "Form".

En resumen, la plantilla extiende otra, define bloques para agregar contenido específico, y utiliza macros para renderizar formularios y botones. Es una forma eficiente de estructurar la presentación en aplicaciones web.


---

Respondé: ¿qué herramientas tuviste que instalar para lograr este código?  (3 pts.)

Instalamos poetry, flask y todas las dependencias necesarias para el proyecto. 

---

Mostrar el codigo en ejecucion