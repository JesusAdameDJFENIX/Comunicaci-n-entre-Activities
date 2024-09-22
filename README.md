Objetivo:
Dominar el uso de ConstraintLayout para crear pantallas con múltiples vistas.
Implementar una transición de vistas mediante cambios de visibilidad y animaciones.
Manejar la entrada de datos y su visualización en la misma actividad.

1. XML de Diseño (activity_main.xml)
Este archivo define la interfaz gráfica de la aplicación, es decir, lo que el usuario verá.

Paso 1: Definir el ConstraintLayout
El ConstraintLayout es el contenedor principal donde se colocan todos los elementos de la pantalla.
Este contenedor te permite posicionar los elementos de manera flexible, usando restricciones para alinearlos entre sí o con los bordes de la pantalla.
Paso 2: Añadir los campos de texto
Dos campos de texto (para el nombre y la edad) se añaden para que el usuario pueda escribir.
Estos campos tienen un "hint" o sugerencia (como "Nombre" y "Edad") que indica qué información debe ingresar el usuario.
Paso 3: Añadir el botón de envío
Se coloca un botón que el usuario presionará para enviar los datos ingresados.
El botón está ubicado debajo de los campos de texto y su función será procesar la información cuando se presione.
Paso 4: Añadir las vistas para mostrar los datos
Se añaden dos etiquetas (TextView) que inicialmente están ocultas. Estas etiquetas se usarán para mostrar el nombre y la edad que el usuario ingrese después de presionar el botón de envío.
Las etiquetas se mostrarán cuando el usuario haya enviado los datos.
Paso 5: Añadir el botón para regresar al formulario
También se coloca un botón que permite al usuario regresar al formulario después de haber enviado los datos.
Este botón está inicialmente oculto y solo aparece cuando el usuario ha enviado la información.

Asi es como se ve el codigo .xml

<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/constraintLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <!-- Formulario -->
    <EditText
        android:id="@+id/editTextName"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:hint="Nombre"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:layout_marginTop="32dp" />

    <EditText
        android:id="@+id/editTextAge"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:hint="Edad"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@id/editTextName"
        android:layout_marginTop="16dp" />

    <Button
        android:id="@+id/buttonSubmit"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Enviar"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@id/editTextAge"
        android:layout_marginTop="16dp" />

    <!-- Pantalla Principal (inicialmente oculta) -->
    <TextView
        android:id="@+id/textViewName"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Nombre: "
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        android:visibility="gone"
        android:layout_marginTop="32dp" />

    <TextView
        android:id="@+id/textViewAge"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Edad: "
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@id/textViewName"
        android:visibility="gone" />

    <Button
        android:id="@+id/buttonBack"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Regresar"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintTop_toBottomOf="@id/textViewAge"
        android:visibility="gone"
        android:layout_marginTop="16dp" />

</androidx.constraintlayout.widget.ConstraintLayout>


![Captura de pantalla 2024-09-22 131350](https://github.com/user-attachments/assets/12594fe4-c10c-4749-bd13-fa6a6a942ee1)

![Captura de pantalla 2024-09-22 132006](https://github.com/user-attachments/assets/3a09cf8d-60b9-488e-b12c-c75e9618f8f2)


![Captura de pantalla 2024-09-22 132059](https://github.com/user-attachments/assets/a16fd171-ee4d-4bb1-9763-47ef9acc0b64)


2. Código Kotlin (MainActivity.kt)
Este archivo contiene la lógica de la aplicación. Aquí es donde se controla qué sucede cuando el usuario interactúa con la interfaz.

Paso 1: Inicializar la actividad
La actividad principal se configura cuando la aplicación se abre. Aquí se vincula el diseño visual que creaste en el archivo XML con el código.
En este paso, también se hace referencia a cada componente de la interfaz (como los campos de texto, botones, y etiquetas) para poder interactuar con ellos desde el código.
Paso 2: Configurar el botón de envío
Cuando el usuario presiona el botón de envío, se verifica si los campos de texto (nombre y edad) están completos.
Si faltan datos, se muestra un mensaje (con un Toast) indicando que todos los campos deben completarse.
Si los campos están completos, los datos ingresados se muestran en las etiquetas de la pantalla principal, ocultando el formulario y mostrando los datos.
Paso 3: Transiciones suaves
Cuando los datos se envían y se muestran, el cambio de pantalla (ocultar el formulario y mostrar los datos) se realiza con una animación suave para hacer la transición más agradable para el usuario.
Esto mejora la experiencia visual, haciendo que los cambios no sean abruptos.
Paso 4: Configurar el botón para regresar al formulario
Al presionar el botón de regreso, se revierte la transición: el formulario vuelve a aparecer para que el usuario pueda ingresar nuevos datos, y las etiquetas y el botón de regreso se ocultan nuevamente.
Se usa la misma animación suave para esta transición.

Asi es como se ve el código .kt

package com.example.comunicacinentreactivities

import android.os.Bundle
import android.view.View
import android.widget.Button
import android.widget.EditText
import android.widget.TextView
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity
import androidx.transition.TransitionManager
import androidx.constraintlayout.widget.ConstraintLayout

class MainActivity : AppCompatActivity() {

    private lateinit var constraintLayout: ConstraintLayout

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        constraintLayout = findViewById(R.id.constraintLayout) // Asegúrate de que tu ConstraintLayout tenga este ID

        val editTextName = findViewById<EditText>(R.id.editTextName)
        val editTextAge = findViewById<EditText>(R.id.editTextAge)
        val buttonSubmit = findViewById<Button>(R.id.buttonSubmit)
        val textViewName = findViewById<TextView>(R.id.textViewName)
        val textViewAge = findViewById<TextView>(R.id.textViewAge)
        val buttonBack = findViewById<Button>(R.id.buttonBack)

        buttonSubmit.setOnClickListener {
            val name = editTextName.text.toString()
            val age = editTextAge.text.toString()

            if (name.isEmpty() || age.isEmpty()) {
                Toast.makeText(this, "Todos los campos deben ser completados", Toast.LENGTH_SHORT).show()
            } else {
                // Mostrar datos en la pantalla principal
                textViewName.text = "Nombre: $name"
                textViewAge.text = "Edad: $age"

                // Cambiar la visibilidad con animación
                TransitionManager.beginDelayedTransition(constraintLayout)
                editTextName.visibility = View.GONE
                editTextAge.visibility = View.GONE
                buttonSubmit.visibility = View.GONE
                textViewName.visibility = View.VISIBLE
                textViewAge.visibility = View.VISIBLE
                buttonBack.visibility = View.VISIBLE
            }
        }

        buttonBack.setOnClickListener {
            // Regresar al formulario
            TransitionManager.beginDelayedTransition(constraintLayout)
            editTextName.visibility = View.VISIBLE
            editTextAge.visibility = View.VISIBLE
            buttonSubmit.visibility = View.VISIBLE
            textViewName.visibility = View.GONE
            textViewAge.visibility = View.GONE
            buttonBack.visibility = View.GONE
        }
    }
}


![image](https://github.com/user-attachments/assets/fac89ffd-26c8-4c23-b423-d0ed3d0fb653)

![image](https://github.com/user-attachments/assets/b9f2d54a-c2dd-49d7-8914-e4a390349140)


Y por ultimo este es el resultado final 


![Video-de-WhatsApp-2024-09-22-a-las-00 00 44_fc3bb10a](https://github.com/user-attachments/assets/e8485aff-7d54-4c7c-867f-0d6c5d540fde)

