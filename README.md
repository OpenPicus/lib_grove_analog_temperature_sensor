lib_grove_analog_temperature_sensor
===================================

Flyport library for Grove analog temperature sensor, released under GPL v.3.<br>
This library allows to interface the Grove analog temperature sensor with OpenPicus Flyport wifi/ethernet or GPRS, returning a value for temperature directly expressed in °C. <BR>
For complete documentation go to wiki.openpicus.com, here's an easy to use example:
<br>1) import files inside Flyport IDE using the external libs button.<br>
2) add following code example in FlyportTask.c:

<pre>
#include "taskFlyport.h"
#include "grovelib.h"
#include "analog_temp.h"

void FlyportTask()
{  
	char msg[100];

	vTaskDelay(50);
	UARTWrite(1,"Welcome to GROVE NEST example!\r\n");

	// GROVE board
	void *board = new(GroveNest);

	// GROVE devices	
	// Analog Temperature Sensor
	void *tempAn = new(An_Temp);
	
	// Attach devices
	attachToBoard(board, tempAn, AN1);
	
	while(1)
	{
		// since the "analog_temp" library automatically converts the value
		// using the "get" methods we have the temperature in °C
		sprintf(msg, "temperature: %3.2f\r\n", (double)(get(tempAn)));
		UARTWrite(1, msg);
		vTaskDelay(50);		
	}
}
</pre>
