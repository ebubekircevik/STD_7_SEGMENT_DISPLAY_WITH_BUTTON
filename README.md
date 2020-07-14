# STD_7_SEGMENT_DISPLAY_WITH_BUTTON
This project is seven segment display control with button and used Std Library with Stm32f407-Discovery Kit. This project was created on Atollic TrueSTUDIO
//CODES

#include "stm32f4xx.h"
#include "stm32f4_discovery.h"

GPIO_InitTypeDef GPIO_InitStruct;

int count=0;

void delay(uint32_t time)
{
	while(time--);
}

void GPIO_Config(){
	RCC_AHB1PeriphClockCmd(RCC_AHB1Periph_GPIOA, ENABLE);
	RCC_AHB1PeriphClockCmd(RCC_AHB1Periph_GPIOD, ENABLE);

	GPIO_InitStruct.GPIO_Mode = GPIO_Mode_IN;
	GPIO_InitStruct.GPIO_OType = GPIO_OType_PP;
	GPIO_InitStruct.GPIO_Pin = GPIO_Pin_0;
	GPIO_InitStruct.GPIO_PuPd = GPIO_PuPd_DOWN;
	GPIO_InitStruct.GPIO_Speed = GPIO_Speed_100MHz;
	GPIO_Init(GPIOA, &GPIO_InitStruct);

	GPIO_InitStruct.GPIO_Mode = GPIO_Mode_OUT;
	GPIO_InitStruct.GPIO_OType = GPIO_OType_PP;
	GPIO_InitStruct.GPIO_Pin = GPIO_Pin_0 | GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3
			| GPIO_Pin_4 | GPIO_Pin_5 | GPIO_Pin_6 ;
	GPIO_InitStruct.GPIO_PuPd = GPIO_PuPd_NOPULL;
	GPIO_InitStruct.GPIO_Speed = GPIO_Speed_100MHz;
	GPIO_Init(GPIOD, &GPIO_InitStruct);

}

int main(void)
{
	GPIO_Config();
  while (1)
  {
	if(GPIO_ReadInputDataBit(GPIOA, GPIO_Pin_0))
	{
		while(GPIO_ReadInputDataBit(GPIOA, GPIO_Pin_0));
		delay(1680000);
		count++;
	}

	switch(count)
	{
		case 0:
		{
			GPIO_SetBits(GPIOD, GPIO_Pin_0 | GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3
					| GPIO_Pin_4 | GPIO_Pin_6);
			GPIO_ResetBits(GPIOD, GPIO_Pin_5);
			break;
		}
		case 1:
		{
			GPIO_SetBits(GPIOD,  GPIO_Pin_1 | GPIO_Pin_2 );
			GPIO_ResetBits(GPIOD,GPIO_Pin_0 | GPIO_Pin_3
							| GPIO_Pin_4 | GPIO_Pin_5| GPIO_Pin_6);
			break;
		}
		case 2:
		{
			GPIO_SetBits(GPIOD, GPIO_Pin_0|GPIO_Pin_1 |GPIO_Pin_2 | GPIO_Pin_3
							| GPIO_Pin_4 | GPIO_Pin_5| GPIO_Pin_6  );
			GPIO_ResetBits(GPIOD,GPIO_Pin_2 | GPIO_Pin_6);
			break;
		}
		case 3:
		{
			GPIO_SetBits(GPIOD, GPIO_Pin_0 | GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_3
							| GPIO_Pin_5);
			GPIO_ResetBits(GPIOD, GPIO_Pin_4 | GPIO_Pin_6);
			break;
		}
		case 4:
		{
			GPIO_SetBits(GPIOD,  GPIO_Pin_1 | GPIO_Pin_2 | GPIO_Pin_5| GPIO_Pin_6);
			GPIO_ResetBits(GPIOD,GPIO_Pin_0 | GPIO_Pin_3
									| GPIO_Pin_4 );
			break;
		}
		case 5:
		{
			GPIO_SetBits(GPIOD,  GPIO_Pin_0 | GPIO_Pin_2 | GPIO_Pin_3| GPIO_Pin_5| GPIO_Pin_6 );
			GPIO_ResetBits(GPIOD,GPIO_Pin_1 | GPIO_Pin_4 );
			break;
		}
		case 6:
		{
			GPIO_SetBits(GPIOD,  GPIO_Pin_0 | GPIO_Pin_2| GPIO_Pin_3
							| GPIO_Pin_4 | GPIO_Pin_5| GPIO_Pin_6 );
			GPIO_ResetBits(GPIOD,GPIO_Pin_1 );
			break;
		}
		case 7:
		{
			GPIO_SetBits(GPIOD,  GPIO_Pin_0 |GPIO_Pin_1 | GPIO_Pin_2 );
			GPIO_ResetBits(GPIOD, GPIO_Pin_3| GPIO_Pin_4 | GPIO_Pin_5| GPIO_Pin_6);
			break;
		}
		case 8:
		{
			GPIO_SetBits(GPIOD,  GPIO_Pin_All);
			break;
		}
		case 9:
		{
			GPIO_SetBits(GPIOD,  GPIO_Pin_0 |GPIO_Pin_1 | GPIO_Pin_2| GPIO_Pin_3| GPIO_Pin_5| GPIO_Pin_6 );
			GPIO_ResetBits(GPIOD, GPIO_Pin_4 );
			break;
		}
		default:
		{
			count=0;
			break;
		}
	}
  }
}



void EVAL_AUDIO_TransferComplete_CallBack(uint32_t pBuffer, uint32_t Size){
  /* TODO, implement your code here */
  return;
}

uint16_t EVAL_AUDIO_GetSampleCallBack(void){
  /* TODO, implement your code here */
  return -1;
}
