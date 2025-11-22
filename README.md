# REPORTE-2
Se implementa el uso de un ```LCD 16x2 I2C``` que cumple la función de visualizar valores obtenidos de una entrada.
## Descripción
```LCD 16x2 I2C``` hará visual los valores obtenidos de un sensor ```DHT22``` el cual hará lecturas de humedad y temperatur y a su vez pormedio de la misma LCD se agregara datos generales delautor, con el fin de entender el código para imprimir los valores de una entrada a un ```LCD 16x2 I2C``` 
(https://wokwi.com/projects/new/esp32)
## Materiales
1. Simulador WOKWI, dentro del simulador se hará uso de lossiguientes componentes:
- Cableado
- Tarjeta ```ESP32```
- Sensor ```DHT22```
- ```LCD 16x2 I2C```
- Libreria ```DHT sensor library for ESPx```
- Libreria ```LiquidCrystal I2C```
## Instrucciones
1. Abrir el simulador WOKWI en el navegador ![](https://wokwi.com/projects/new/esp32)

![](https://github.com/EfrenQA/Reporte-1/blob/main/wokwi.png?raw=true)

3. Elegir la tarjeta ```ESP32```

 ![](https://github.com/EfrenQA/Reporte-1/blob/main/ESP32.png?raw=true)

4. Selección del sketch

![](https://github.com/EfrenQA/Reporte-1/blob/main/ESP32-2.png?raw=true)

5. Al seleccionar el skecth se mostrara una interfas como se muestra en la imagen

![](https://github.com/EfrenQA/Reporte-1/blob/main/INTERFAS.png?raw=true)

6. Se hará la selección de la libreria para el sensor ```DHT22``` y ```LCD 16x2 I2C```, para esto se tiene que dirigir Library Manager

![](https://github.com/EfrenQA/Reporte-1/blob/main/AGREGAR%20LIBRERIA.png?raw=true)

7. Una ves en la pestaña de librerias, se tiene que clickear sobre el botón de "+", seguido de esto se abrira un cuadro de busqueda donde se buscara la libreria "DHT sensor library for ESPX" y "LiquidCrystal I2C"

![](https://github.com/EfrenQA/Reporte-1/blob/main/BUSQUEDA%20DE%20LIBRERIA%20.png?raw=true)
![](https://github.com/EfrenQA/REPORTE-2/blob/main/libreria%20liquid%20crystal.png?raw=true)

8. Para colocar el sensor y el LCD en el espacio de simulación se tiene que clickear en el botón de "+" que esta en el cuadro de simuación.

![](https://github.com/EfrenQA/Reporte-1/blob/main/AGREGAR%20COMPONENTES.png?raw=true)

9. Para la selección del sensor y del LCD, podemos escribir su nombre en la barra de buscador o desplazarnos en las opciones.

![](https://github.com/EfrenQA/Reporte-1/blob/main/BUSCAR%20COMPONENTE.png?raw=true)
![](https://github.com/EfrenQA/REPORTE-2/blob/main/sleccion%20de%20lcd.png?raw=true)

10. Una vez que se tengan los tres componentes en el cuadro de simulación, se procede a la conección entre la tarjeta y los dos componentes de la siguiente forma:
- Primer pin del sensor se conecta al pin GND de la tarjeta.
- Segundo pin del sensor se conecta al pin 15 de la tarjeta.
- Cuarto pin del sensor se conecta al pin de 5V de la tarjeta.

- PIN GND del LCD al PIN GND de la tarjeta.
- PIN VCC del LCD al PIN VCC de la tarjeta.
- PIN SDA del LCD al PIN 21 de la tarjeta.
- PIN SCL del LCD al PIN 22 de la tarjeta.


![](https://github.com/EfrenQA/REPORTE-2/blob/main/layout2.png?raw=true)
10. En el lado de "SKETCH" se debe colocar el siguiente código:
```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int DHT_PIN = 15;

DHTesp dhtSensor;

LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);

void setup() {

  Serial.begin(115200);
  dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
  lcd.init();
  lcd.backlight();

}

void loop() {

  TempAndHumidity  data = dhtSensor.getTempAndHumidity();
  Serial.println("Temp: " + String(data.temperature, 1) + "°C");
  Serial.println("Humidity: " + String(data.humidity, 1) + "%");
  Serial.println("---");
    lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("BIENVENIDOS");
  lcd.setCursor(0, 1);
  lcd.print("MODULO 5");

delay(1500);
 lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("EFREN QUIROZ");
  lcd.setCursor(0, 1);
  lcd.print("ING.INDUSTRIAL");
 
delay(1500);
lcd.clear();
lcd.setCursor(0, 0);
  lcd.print("  Temp: " + String(data.temperature, 1) + "\xDF"+"C  ");
  lcd.setCursor(0, 1);
  lcd.print(" Humidity: " + String(data.humidity, 1) + "% ");

  delay(1500);
}
```
11. como último paso se inicia el simulador con el botón de "play" y se podra visualizar las lecturas del sensor.
![](https://github.com/EfrenQA/Reporte-1/blob/main/SIMULACI%C3%93N.png?raw=true)
## Instrucciones de operación
1. Iniciar simulación con el botón de "PLAY"
2. Visualizar los datos que se mostrarán en LCD
3. Descargar valores
![](https://github.com/EfrenQA/REPORTE-2/blob/main/simulacion%202.png?raw=true)
## Resultados
Al finalizar cada paso se podrá obtener datos desde la simulación del LCD
![](https://github.com/EfrenQA/REPORTE-2/blob/main/simulacion%202.png?raw=true)
## Créditos
Autor Ing. Efren David Quiroz Ayala 
