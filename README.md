# Proyecto-I-Mecatronica

## Manufactura: 

Para la fabricacion de las articulaciones de los dedos, se utilizó una cadena genérica de bicicleta:

<div>
<p style = 'text-align:center;'>
<img src="Photos/Cadena.jpg" width="500px">
</p>
</div>

Para separar los eslabones de la cadena en medidas regulares para los dedos, se utilizó la siguiente herramienta (corta cadenas):

<div>
<p style = 'text-align:center;'>
<img src="Photos/Herramienta.jpg" width="500px">
</p>
</div>


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
