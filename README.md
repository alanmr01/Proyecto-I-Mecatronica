# Proyecto-I-Mecatrónica

## Fabricación: 

### Materiales:

Para la fabricación de las articulaciones de los dedos, se utilizó una cadena genérica de bicicleta:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Cadena.jpg" width="400px">
</p>
</div>

Como base para la muñeca de la mano, se utilizó un resorte de tracción lineal (Zugfedern), con largo 17 cm, diámetro interno 2 cm y diámetro externo 2.5 cm:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Resorte.jpg" width="300px">
</p>
</div>

Como base de los demas componentes se utilizo cartón compacto gris:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Carton.jpg" width="300px">
</p>
</div>


Para articular los dedos, se utilizan tuercas y tornillos:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Tornillos.jpg" width="300px">
</p>
</div>

Se utilizan gomas elásticas para movilizar los dedos a una posición inicial:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Elasticos.jpg" width="300px">
</p>
</div>

Para la union de componentes, se utilizó principalmente cinta aislante eléctrica:
<div>
<p style = 'text-align:center;'>
<img src="Photos/Cinta.jpg" width="300px">
</p>
</div>

### Componentes electrónicos:

Para el accionamiento de la mano, se utiliza un microservomotor MG90 de engranajes plásticos:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Servo.jpg" width="300px">
</p>
</div>

Para accionar el servomotor, se utiliza un pulsador se tamaño pequeño:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Pulsador.jpg" width="300px">
</p>
</div>

Para la alimentación eléctrica del Arduino UNO, se utilizan 6 pilas AA recargables montadas sobre un portapilas, entregando aproximadamente 7.8 V:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Pilas.jpg" width="300px">
</p>
</div>

Para cableado que requiera soldadura, se utilizó cable de audio duplex calibre 12:

<div>
<p style = 'text-align:center;'>
<img src="Photos/CableAudio.jpg" width="300px">
</p>
</div>

### Herramientas:

Para separar los eslabones de la cadena en medidas regulares para los dedos, se utilizó una herramienta corta cadenas:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Herramienta.jpg" width="300px">
</p>
</div>

Para el pegado de los componentes, se utilizó silicona caliente suministrada mediante una pistola dispensadora de tamaño pequeño (potencia de 75 W).

<div>
<p style = 'text-align:center;'>
<img src="Photos/Silicona.jpg" width="300px">
</p>
</div>

### Procedimiento:

Dividir la cadena en 5 partes de similar tamaño, en este caso, se hicieron con dedos cercanos a 16 cm. 

<div>
<p style = 'text-align:center;'>
<img src="Photos/Dedos.jpg" width="400px">
</p>
<div>

Dado que todos los eslabones de la cadena son partes móviles, se hace necesario volver rígidos aquellos que no requieran moverse. Para ello, es posible fijar los eslabones inmóviles con algún material que los sostengan, utilizar pegamento para fijar los ejes, o siguiendo la metodología utilizada en este proyecto, convertir el eje de cada eslabón en un pasador fijo golpeando cada eje con un martillo hasta que llegue al tope el eslabon, realizando entonces ajuste mecánico impidiendo el movimiento. En la siguiente imagen se muestran los únicos ejes que no fueron endurecidos, a fin de que estos actuen como articulaciones de la mano:

<div>
<p style = 'text-align:center;'>
<img src="Photos/DedosR.jpg" width="400px">
</p>
<div>

Se ensabambla la base de cartón rígido con el interior del resorte, adhiriendo los dedos al cartón con silicona caliente, tal como se muestra en la siguiente imagen:

<div>
<p style = 'text-align:center;'>
<img src="Photos/ManoPt1.jpg" width="400px">
</p>
<div>

Para evitar desensambles entre los dedos y la base, se aseguran los dedos con cinta aislante: 
<div>
<p style = 'text-align:center;'>
<img src="Photos/Encintado.jpg" width="400px">
</p>
<div>

Se utilizan gomas elásticas entre los eslabones de cadena a articular para permitir el regreso a su posición inicial. Estos van unidos a los tornillos encajados en los eslabones y fijados a través de tuercas:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Art1.jpg" width="400px">
</p>
<div>

Las fijaciones entre tornillo, tuerca y goma elástica se realizaron de la siguiente forma:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Art2.jpg" width="400px">
</p>
<div>


## Programación en Arduino:

```C++
#include <Servo.h>

// C++ code
//

Servo servomotor;  // Nombrar el servo

int pinServo = 9;     // Definir el pin de señal para el servo
int angulo=100;       // Definir un angulo inicial en el servo
int pinPulsador1 = 8; // Definir el pin de señal para el pulsador
int Pulsador1 = 0;    // Definir el estado inicial en el pulsador
  
void setup()
{
  pinMode(LED_BUILTIN, OUTPUT);
  servomotor.attach(pinServo);  // Definir el pin de donde el servo recibirá la señal
  pinMode(pinPulsador1,INPUT);  // Definir como entrada de señal el pin definido para el pulsador
  servomotor.write(angulo);     // Posicionar el servo en el ángulo inicial
}

void loop()
{
  Pulsador1 = digitalRead(pinPulsador1); // Leer el estado en el pulsador
  if(Pulsador1 == HIGH){                 // Si está sin pulsar:
    angulo=100;                          // Mantiene/vuelve al ángulo inicial
  }
  if(Pulsador1 == LOW){                  // Si está pulsado:
    angulo=20 ;                          // Se define un nuevo angulo deseado
  }
servomotor.write(angulo);                // Se posiciona el servo en el angulo definido
delay(25);                               // Se añade una pequeña latencia para evitar errores
}
```
