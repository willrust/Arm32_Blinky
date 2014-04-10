
/* Includes ------------------------------------------------------------------*/
#include <__cross_studio_io.h>

#include "stm32l1xx.h"
#include "discover_board.h"
#include <stm32l1xx_rcc.h>
#include <stm32l1xx_gpio.h>

void TimingDelay_Decrement(void);  // used in SysTick_Handler function
void Delay(__IO uint32_t nTime);
static __IO uint32_t TimingDelay;


/* Private typedef -----------------------------------------------------------*/
//GPIO_InitTypeDef    GPIO_InitStructure;

/* Private define ------------------------------------------------------------*/
/* Private macro -------------------------------------------------------------*/
/* Private variables ---------------------------------------------------------*/
/* Private function prototypes -----------------------------------------------*/
/* Private functions ---------------------------------------------------------*/

int main(void)
{

debug_printf("hello world\n");

/* At this stage the micro-controller clock setting is already configured,
this is done through SystemInit() function which is called from startup
file (startup_stm32l1xx_md.S) before to branch to application main.
To reconfigure the default setting of SystemInit() function, refer to
system_stm32l1xx.c file
*/
    GPIO_InitTypeDef GPIO_InitStructure;

    // Enable Peripheral Clocks
    RCC_AHBPeriphClockCmd(RCC_AHBPeriph_GPIOB, ENABLE);

    // Configure GPIO Pins
    GPIO_InitStructure.GPIO_Pin = GPIO_Pin_6 | GPIO_Pin_7;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_OUT;
    GPIO_InitStructure.GPIO_OType = GPIO_OType_PP;
    GPIO_InitStructure.GPIO_PuPd = GPIO_PuPd_NOPULL;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_2MHz;
    GPIO_Init(GPIOB, &GPIO_InitStructure);

    GPIO_WriteBit(GPIOB, GPIO_Pin_6, Bit_RESET);
    GPIO_WriteBit(GPIOB, GPIO_Pin_7, Bit_RESET);

    debug_printf("RESET pin 6 & pin 7 \n");

    SysTick_Config(SystemCoreClock / 1000);  // SysTick for every  1-miliSec

    GPIO_WriteBit(GPIOB, GPIO_Pin_6, Bit_SET);
    debug_printf("SET pin 6 \n");

    // toggle LEDs
    while(1) {

        debug_printf("toggle \n");

    	GPIO_TOGGLE(GPIOB,GPIO_Pin_6);
    	GPIO_TOGGLE(GPIOB,GPIO_Pin_7);

    	Delay(100);
    }
}


/**
  * @brief  Decrements the TimingDelay variable.
  * @param  None
  * @retval None
  */
void TimingDelay_Decrement(void)
{
    if( TimingDelay != 0x00 ) {
        TimingDelay--;
    }
}


/**
  * @brief  Inserts a delay time.
  * @param  nTime: specifies the delay time length.
  * @retval None
  */
void Delay(__IO uint32_t nTime)
{
    TimingDelay = nTime;
    while(TimingDelay != 0);
}


#ifdef  USE_FULL_ASSERT

/**
  * @brief  Reports the name of the source file and the source line number
  *         where the assert_param error has occurred.
  * @param  file: pointer to the source file name
  * @param  line: assert_param error line source number
  * @retval None
  */

void assert_failed(uint8_t* file, uint32_t line)
{ 
  /* User can add his own implementation to report the file name and line number,
     ex: printf("Wrong parameters value: file %s on line %d\r\n", file, line) */
  /* Infinite loop */
  while (1){

  }
}

#endif