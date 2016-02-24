# TIMER AND COUNTER 
## Timer Base Interrupt
- Prescale: range from 0 to 65535
- Counter mode: can be count-down and count-up
- Counter period: the value that the count to or count from.
- (clock / prescale) * period = timer value

		void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim)
			{
				if (htim->Instance == TIM3)
					HAL_GPIO_TogglePin(GPIOA, GPIO_PIN_5);
			}
When timer value elapsed, Callback function is called. 
## External Input Counter
 - The counter clock can be provided by the following clock source:
 	- Internal clock (CK_INT)
 	- External clock mode1: external input pin
 	- external clock mode2: external trigger input ETR
 	- Internal trigger inputs (ITRx): using one timer as prescaler for another timer, for example, you can configure Timer 1 to act as a prescaler for Timer 2. 

- Get counter with the clock source is external input pin. Because broad Nucleo-F411RE haven't connect external pin PC13, so clock source in here internal clock source.

		count = __HAL_TIM_GetCounter(&htim1)
## PWM Generation
PWM uses pins which has TIMx_CH1 to CH4 function, it means that one Timer can generate maximum 4 PWM outputs.

- timer tick frequency = clock / (prescaller + 1)
- PWM frequency = timer tick frequency / TM_period + 1
- TIM period = timer tick frequency / PWM frequency - 1
- pulse length = ((TM_period + 1) * DutyCycle) / 100 - 1

		HAL_TIM_PWM_Start (&htim3, TIM_CHANNEL_1);
		HAL_TIM_PWM_Start (&htim3, TIM_CHANNEL_2);
Enable PWM of Timer 3, channel 1 and channel 2.
