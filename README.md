# XilinxMicroblazeDrivers

Short notes on how to use Xilinx Microblaze drivers for various blocks. A short cheat sheet for myselft. Design goal to get started as fast and simple as possible. Polled mode is prefered for simplicity.


### Very basic GPIO IP

GPIO IP might have 2 channels plus interrupt. This is example how to set output value on the 1st channel.

#include "xgpio.h"

#define GPIO_ID  XPAR_GPIO_1_DEVICE_ID
<br/>XGpio CS_Gpio; /* The Instance of the GPIO Driver */

/* Initialize the GPIO driver */
<br/>Status = XGpio_Initialize(&CS_Gpio, GPIO_ID);
  
/* Set all bits as outputs */
<br/>XGpio_SetDataDirection(&CS_Gpio, 1, 0);
  
/* Set output value */
<br/>XGpio_DiscreteWrite(&CS_Gpio, 1, 0xFFFF0000);


### I2C or IIC as it is called by Xilinx IP 

I2C can be also used as Serial Camera Control Bus. That's how to write and read a register.

#include "xiic.h"

#define IIC_BASE_ADDRESS	XPAR_IIC_0_BASEADDR
#define IIC_ADDR  		    0x3C

u8 txBuffer[4] ;
u8 rxBuffer[4] ;

/* Put command into send buffer */
<br/>txBuffer[0]= 0x31;
<br/>txBuffer[1]= 0x00;

/* Send data: address + 2 bytes */
<br/>SentByteCount = XIic_Send(IIC_BASE_ADDRESS, IIC_ADDR, txBuffer, 2, XIIC_STOP); 

/* Receive data: address + 1 byte */
<br/>ReceivedByteCount = XIic_Recv(IIC_BASE_ADDRESS, IIC_ADDR, rxBuffer, 1, XIIC_STOP);


### Xilisf library and QUAD SPI IP 

tbd
