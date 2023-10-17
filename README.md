# 📋 Primer Parcial SPD
![Logo de GitHub](https://github.com/ErikLujan/proyecto/blob/main/Imagen/arduino.jpeg)

# <h2>👥 Integrantes del grupo</h2>
- Lucio Belloni
- Ciro Luongo
- Erik Lujan
# <h2>📌 Proyecto: Contador de 0 a 99 con Display de 7 segmentos y multiplexación</h2>
![Logo de GitHub](https://github.com/ErikLujan/proyecto/blob/main/Imagen/Contador%20de%200%20a%2099%20Arduino.png)

# <h2>📎 Descripcion del proyecto</h2>
Este circuito cumple con la funcion de, mediante displays de 7 segmentos, mostrarnos numeros desde el 0 hasta el 99. Este contador se maneja mediante 3 pulsadores y cada uno tiene su respectiva funcion: Uno para subir el numero en el contador, otro para bajarlo y el ultimo para reiniciar el contador e inicializarlo en 0.

# <h2>Funcion principal (loop)</h2>
Esta funcion cumple con las siguientes caracteristicas:
- Lee el estado de los botones para determinar si se presionó alguno.
- Actualiza el contador en función de los botones presionados.
- Llama a MostrarContador() para mostrar el valor actual en los displays.
-  No toma parámetros y no retorna ningún valor.
```
void loop()
{
  int presionado = botonPresionado();
  if (presionado == botonSubir) 
  {
    contador++;
    if (contador > 99)
    {
      contador = 0;
    } 
  }
  else if(presionado == botonBajar)
  {
    contador--;
    if (contador < 0)
    {
      contador = 99;
    }
  }
  else if(presionado == botonReset)
  {
    contador = 0;
  }
  MostrarContador(contador);
}
```
# <h2>Funcion ApagarDisplay()</h2>
Esta funcion se encarga de apagar todos los leds de los displays, apagando los pines A, B, C, D, E, F y G. No toma parámetros ni retorna ningún valor.
```
void ApagarDisplay()
{
  apagarLeds(A);
  apagarLeds(B);
  apagarLeds(C);
  apagarLeds(D);
  apagarLeds(E);
  apagarLeds(F);
  apagarLeds(G);
}
```

# <h2>Funcion MostrarDigito()</h2>
- Muestra un dígito específico en los displays. Toma un parámetro digito que es el número a mostrar (0-9).
- Enciende los leds correspondientes para mostrar el dígito.
```
void MostrarDigito(int digito)
{
  ApagarDisplay();
  switch(digito)
  {
    case 0:
      numeroCero();
      break;
    case 1:
      numeroUno();
      break;
    case 2:
      numeroDos();
      break;
    case 3:
      numeroTres();
      break;
    case 4:
      numeroCuatro();
      break;
    case 5:
      numeroCinco();
      break;
    case 6:
      numeroSeis();
      break;
    case 7:
      numeroSiete();
      break;
    case 8:
      numeroOcho();
      break;
    case 9:
      numeroNueve();
      break;
  }
}
```

# <h2>Funcion prenderDigito()</h2>
Controla cuál de los dos displays (UNIDAD o DECENA) debe estar encendido y cuál apagado. Toma como un parámetro digito que indica qué display se debe prender.
```
void prenderDigito(int digito)
{
  if (digito == UNIDAD)
  {
    digitalWrite(UNIDAD, LOW);
    digitalWrite(DECENA, HIGH);
  }
  else if (digito == DECENA)
  {
    digitalWrite(UNIDAD, HIGH);
    digitalWrite(DECENA, LOW);
  }
  else
  {
    digitalWrite(UNIDAD, HIGH);
    digitalWrite(DECENA, HIGH);
  }
}
```

# <h2>Funcion MostrarContador()</h2>
- Muestra el valor del contador en los displays. Toma un parámetro contador que es el número que se mostrará en los displays.
- Divide el número en unidades y decenas y muestra ambos dígitos en los displays.

```
void MostrarContador(int contador)
{
  ApagarDisplay();
  prenderDigito(UNIDAD);
  MostrarDigito(contador % 10);
  delay(5);
  ApagarDisplay();
  prenderDigito(DECENA);
  MostrarDigito(contador / 10);
  delay(tiempo);
}
```

# <h2>Funcion botonPresionado()</h2>
- Lee el estado de los botones y detecta si alguno de ellos ha sido presionado desde la última llamada.
- No toma parámetros.
- Retorna un valor que representa el botón presionado (botonSubir, botonBajar, botonReset) o 0, en caso de que ningún botón sea presionado.
```
int botonPresionado(void)
{
  sube = digitalRead(botonSubir);
  baja = digitalRead(botonBajar);
  reset = digitalRead(botonReset);
  
  if(sube)
    subePrevia = 1;
  if(baja)
    bajaPrevia = 1;
  if(reset)
    resetPrevia = 1;
  
    if(sube == 0 && sube != subePrevia)
    {
      subePrevia = sube;
      return botonSubir;
    }
    if(baja == 0 && baja != bajaPrevia)
    {
      bajaPrevia = baja;
      return botonBajar;
    }
    if(reset == 0 && reset != resetPrevia)
    {
      resetPrevia = reset;
      return botonReset;
    }
 return 0;
}
```

# <h2>Funcion encenderLeds()</h2>
Enciende el led conectado al pin correspondiente. Toma como parámetro un pin que es el número del pin al que se debe aplicar la señal de encendido.
```
void encenderLeds(int pin)
{
  digitalWrite(pin, HIGH);
}
```

# <h2>Funcion apagarLeds()</h2>
Apaga el led conectado al pin correspondiente. Toma como parámetro un pin que es el número del pin al que se debe aplicar la señal de apagado.
```
void apagarLeds(int pin)
{
  digitalWrite(pin, LOW);
}
```

# <h2>Funciones de numeroCero() a numeroNueve()</h2>
- Son funciones que encienden los leds en patrones específicos para mostrar los números del 0 al 9 en los displays.
- No toman parámetros ni retornan valores. Cada función está diseñada para mostrar un número específico en los displays.
```
void numeroUno(void){
    apagarLeds(A);
  	apagarLeds(D);
  	apagarLeds(E);
  	apagarLeds(F);
    apagarLeds(G);
	encenderLeds(B);
    encenderLeds(C);
}

void numeroDos(void){
	apagarLeds(C);
  	apagarLeds(F);
  	encenderLeds(A);
	encenderLeds(B);
  	encenderLeds(D);
  	encenderLeds(E);
  	encenderLeds(G); 	
}

void numeroTres(void){
  	apagarLeds(E);
  	apagarLeds(F);	
  	encenderLeds(A);
  	encenderLeds(B);
  	encenderLeds(C);
  	encenderLeds(D);
  	encenderLeds(G);
}

void numeroCuatro(void){
  	apagarLeds(A);
  	apagarLeds(D);
  	apagarLeds(E);
  	encenderLeds(B);
  	encenderLeds(C);
  	encenderLeds(F);
  	encenderLeds(G);
}

void numeroCinco(void) {
  apagarLeds(B);
  apagarLeds(E);
  encenderLeds(A);
  encenderLeds(C);
  encenderLeds(D);
  encenderLeds(F);
  encenderLeds(G);
}

void numeroSeis(void) {
  apagarLeds(B);
  encenderLeds(A);
  encenderLeds(C);
  encenderLeds(D);
  encenderLeds(E);
  encenderLeds(F);
  encenderLeds(G);
}

void numeroSiete(void){
  apagarLeds(D);
  apagarLeds(E);
  apagarLeds(F);
  apagarLeds(G);
  encenderLeds(A);
  encenderLeds(B);
  encenderLeds(C);
}

void numeroOcho(void){
  encenderLeds(A);
  encenderLeds(B);
  encenderLeds(C);
  encenderLeds(D);
  encenderLeds(E);
  encenderLeds(F);
  encenderLeds(G);
}

void numeroNueve(void) {
  apagarLeds(E);
  encenderLeds(A);
  encenderLeds(B);
  encenderLeds(C);
  encenderLeds(D);
  encenderLeds(F);
  encenderLeds(G);
}
```

# 👾 Link al Proyecto
- [Proyecto](https://www.tinkercad.com/things/kzC52jqYoI3)
