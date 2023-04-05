# Iplament FreeRTOS
Real Time Operating System witch application from this Microcontroller

# What is RTOS Some Operating Systems at home
Real-time operating systems provide support for resource management, communication, precise scheduling, synchronization and planning. RTOS has a deadline associated with the tasks and must complete the tasks before this deadline. RTOS should be deterministic, quality of service (QoS) and deadline driven.
For Example:

1-Deos (DDC-I),

2-embOS (SEGGER), 

3-FreeRTOS (Amazon),

4-Integrity (Green Hills Software), 

5-Keil RTX (ARM), LynxOS (Lynx Software Technologies), 

6-MQX (Philips NXP / Freescale), 

7-Nucleus (Mentor Graphics), 

8-Neutrino (BlackBerry), 

9-PikeOS (Sysgo), 

10-SafeRTOS (Wittenstein), 

11-ThreadX (Microsoft Express Logic), 

12-µC/OS (Micrium), VxWorks (Wind River), 

13-Zephyr (Linux Foundation) are popular real-time processing systems.


In addition to these;

I will explain the operating systems that I want to go into detail on my field and the operating systems I have researched and studied.

# 1) Integrity
Integrity is an operating system product developed by Hewlett-Packard. It is designed for environments with high security requirements. Integrity is widely used in places with high security requirements, such as large enterprises, banks and government agencies.
In addition, it is also used as a reliable operating system, especially in air combat aircraft. 
For example, the operating system product that is part of this family, the Green Hills Software Integrity DO-178B real-time operating system (RTOS), also plays a role in the F35 fighter jet manufactured by Lockheed Martin. In Turkey, the Real-time National Operating System (RTOS), developed by TUBITAK and Havelsan, continues to be actively used.

The Integrity operating system is specifically optimized for applications that require high security and high performance. This operating system can run on multi-processor systems, allowing applications requiring high performance to be run in parallel.

The most widely used version of the Integrity operating system family is HP-UX. HP-UX is optimized for workloads that require high security and high performance. The Integrity family of operating systems is also compatible with other operating systems, including OpenVMS and NonStop operating systems.

![image](https://user-images.githubusercontent.com/73780930/230222355-0dfc37ec-dd22-49fc-990e-fa845b4d0012.png)
![image](https://user-images.githubusercontent.com/73780930/230222371-4dbdfdab-efc1-4858-9edf-2668c9544e39.png)

*HP-UX 11.11 Operation System*

It is a very well secured operating system. They are written to protect operating systems against unauthorized access. The Integrity operating system does not compromise on security-based applications in this regard.

# 2) GIS 
In Turkey, the GİS Operating System enables the indigenous development of important technologies used in the defense sector, such as UAVs, helicopters and aircrafts. Since the indigenous development of these technologies is ensured with national software, external intervention in the systems is also prevented. Officials stated that the GİS can be easily used in the integration of any project thanks to its scalable feature.

![image](https://user-images.githubusercontent.com/73780930/230222551-79aad076-8881-4e05-b90f-5b9b2458822c.png)

# 3) VXWorks
Wind River VXWorks, developed by Wind River Systems, is an operating system for real-time embedded systems. VXWorks is specifically designed for high-reliability, low latency, fast and deterministic embedded applications.

VXWorks is especially used in industries such as aerospace, defense, automotive, industrial automation, medical devices and telecommunications. Devices in these industries are often used in areas where factors such as reliability and speed are critical, and VXWorks is designed to meet these requirements.

VXWorks can run on different processor architectures and hardware platforms. It is also a suitable operating system for networked devices and has a TCP/IP protocol stack. VXWorks is also compatible with popular programming languages such as C/C++ and Ada, allowing developers to easily develop software.

VXWorks includes features critical for real-time applications. These features include event-driven scheduling, interrupt management, process prioritization, timing management and debugging tools. These features are a great help in the development of real-time applications, which are critical to the reliability and performance of devices.

# Real-Time Operating System Features:
The key factors in a real-time operating system are minimum interrupt latency and minimum thread switching latency; a real-time operating system is judged more on how quickly or how predictably it can react than on the amount of work it can perform in a given amount of time.

Task Priority: Identifying the most needed task or performing the control to achieve the target task state and obtain the resource.

Task Communication Mechanism: Synchronization mechanism for multiple tasks to communicate and ensure data integrity.

Multitasking: Allows multiple systemtasks to execute their tasks simultaneously. This topic is explained in the following code.

Deterministic behavior: Processes and interrupts are handled within a certain period of time. Interrupts are instantaneous changes in the flowchart that should occur in case of receiving data of situations that we may consider important.

Defined stack usage: A defined stack space/target task is allocated for each task

System management: Instead of resource management, application development is enabled.


# What is FreeRTOS?
It is the core of a real-time operating system for embedded devices ported to a microcontroller platform. Deployment takes place under this kernel. We will basically try to build on the microcontroller in the input area.

# Building a System Foundation with FreeRTOS CubeMX
FreeRTOS helps us in the case used to implement the operating system in embedded systems. This system is more of a generic system. It is not only for Stm32 based processors.  We will iplamente this system to the microcontroller. I proceeded from Cubemx as its applicability and Environment.

# Configuration
For time, here we are activating the Crystal state via RCC for the fast processing time of our processor.

I have also activated the user leds via GPIO Pins. The most critical configuration here will be to build the Timebase Source on any timer in the SYS area for the real simultaneous transmission system that we will install. This step will take place for the installed operating system.
The last step is to install the FreeRTOS files in this section with the FreeRTOS option via the Middleware tab with the convenience provided by Stm.
Here we can choose Interface I CMSIS_V1 or V2. If the interface here will use any system in the system, we will be able to run the commands by making adjustments here. 
After generating our code, after entering the cmsis_os header, we can see the libraries on rtos here. I copy the rtos-based libraries found here and add them to the user code section in our main code.
Let's eliminate the Tasks that will not be used here;
```C++
osThreadId defaultTaskHandle;
void StartDefaultTask(void const * argument);
```
deleting lines.

Also cmsis iplament lines;
```C++
  /* USER CODE BEGIN RTOS_MUTEX */
  /* add mutexes, ... */
  /* USER CODE END RTOS_MUTEX */

  /* USER CODE BEGIN RTOS_SEMAPHORES */
  /* add semaphores, ... */
  /* USER CODE END RTOS_SEMAPHORES */

  /* USER CODE BEGIN RTOS_TIMERS */
  /* start timers, add new ones, ... */
  /* USER CODE END RTOS_TIMERS */

  /* USER CODE BEGIN RTOS_QUEUES */
  /* add queues, ... */
  /* USER CODE END RTOS_QUEUES */

  /* Create the thread(s) */
  /* definition and creation of defaultTask */
  osThreadDef(defaultTask, StartDefaultTask, osPriorityNormal, 0, 128);
  defaultTaskHandle = osThreadCreate(osThread(defaultTask), NULL);

  /* USER CODE BEGIN RTOS_THREADS */
  /* add threads, ... */
  /* USER CODE END RTOS_THREADS */

  /* Start scheduler */
  osKernelStart();
  /* We should never get here as control is now taken by the scheduler */

```
and
```C++
/* USER CODE BEGIN Header_StartDefaultTask */
/**
  * @brief  Function implementing the defaultTask thread.
  * @param  argument: Not used
  * @retval None
  */
/* USER CODE END Header_StartDefaultTask */
void StartDefaultTask(void const * argument)
{
  /* USER CODE BEGIN 5 */
  /* Infinite loop */
  for(;;)
  {
    osDelay(1);
  }
  /* USER CODE END 5 */
}
```

As a result, I have prepared only the operating system iplamentation basic system codes in an active format. We will activate the task and peripherals we will use. Since this is an embedded software development, we need to use a pointer based parameter to run it.

I create a task to create our main loop.

```C++
void Task(void *pvParameters)
{
	while()
	{
	HAL_GPIO_TogglePin(GPIO8,GPIO_PIN_14);
	vTaskDelay(pdMS_TO_TICKS(500));
	}
}
```

In this draft, just before starting the system, we create the draft in the "begin" fields, that is, we activate it.

```C++
  /* USER CODE BEGIN 2 */
xTaskCreate(Task1,"task_start",128,NULL,0,NULL);
  /* USER CODE END 2 */
```
Another important point here is that when the threads are active in the system, the threads must be deleted, otherwise we will encounter an error situation. For this, we can mark thread I as pointer with the handler variable and delete the threads. Here we will select prioritized threads and prevent system confusion. Thread is the state of being able to do many processes together at the same time.

```C++
  /* USER CODE END 2 */
vTaskStartScheduler();
  /* Infinite loop */
```
This is how we will be able to start the system.

![image](https://user-images.githubusercontent.com/73780930/230230415-e18d73f7-ea31-47f6-8482-69a0b0beae0e.png)

Operating system parameter configuration settings section. Here let's change configSupport_STATIC_ALLOCATION from 1-> to 0.

Compilation Result:

![image](https://user-images.githubusercontent.com/73780930/230230488-d877115b-fcc6-4c97-a1fb-488a03dacd4e.png)


In the Two Task System, threads are separate tasks in the working principle software;

![image](https://user-images.githubusercontent.com/73780930/230230591-a1319aa2-ad03-4e82-82da-e64f1420870d.png)

```C++
/* Private user code ---------------------------------------------------------*/
/* USER CODE BEGIN 0 */
TaskHandle_t task1;
void Task1(void *pvParameters)
{
	while(1)
	{
	HAL_GPIO_TogglePin(GPIO_PIN_8,GPIO_PIN_14);
	vTaskDelay(pdMS_TO_TICKS(800));
	}
}

void Task2(void *pvParameters)
{
	while(1)
	{
	HAL_GPIO_TogglePin(GPIO_PIN_8,GPIO_PIN_7);
	vTaskDelay(pdMS_TO_TICKS(100));
	}
}
/* USER CODE END 0 */
```

The result of two task compilation;

![image](https://user-images.githubusercontent.com/73780930/230230666-9249387a-a090-4dba-a829-5f7eeda1207c.png)

# General Code View - FreeRTOS with 2 Task assignments:

```C++
/* USER CODE BEGIN Header */
/**
  ******************************************************************************
  * @file           : main.c
  * @brief          : Main program body
  ******************************************************************************
  * @attention
  *
  * Copyright (c) 2023 STMicroelectronics.
  * All rights reserved.
  *
  * This software is licensed under terms that can be found in the LICENSE file
  * in the root directory of this software component.
  * If no LICENSE file comes with this software, it is provided AS-IS.
  *
  ******************************************************************************
  */
/* USER CODE END Header */
/* Includes ------------------------------------------------------------------*/
#include "main.h"
//#include "cmsis_os.h"

/* Private includes ----------------------------------------------------------*/
/* USER CODE BEGIN Includes */
#include "FreeRTOS.h"
#include "task.h"
#include "timers.h"
#include "queue.h"
#include "semphr.h"
#include "event_groups.h"
/* USER CODE END Includes */

/* Private typedef -----------------------------------------------------------*/
/* USER CODE BEGIN PTD */

/* USER CODE END PTD */

/* Private define ------------------------------------------------------------*/
/* USER CODE BEGIN PD */

/* USER CODE END PD */

/* Private macro -------------------------------------------------------------*/
/* USER CODE BEGIN PM */

/* USER CODE END PM */

/* Private variables ---------------------------------------------------------*/


/* USER CODE BEGIN PV */

/* USER CODE END PV */

/* Private function prototypes -----------------------------------------------*/
void SystemClock_Config(void);
static void MPU_Config(void);
static void MX_GPIO_Init(void);


/* USER CODE BEGIN PFP */

/* USER CODE END PFP */

/* Private user code ---------------------------------------------------------*/
/* USER CODE BEGIN 0 */
TaskHandle_t task1;
void Task1(void *pvParameters)
{
	while(1)
	{
	HAL_GPIO_TogglePin(GPIO_PIN_8,GPIO_PIN_14);
	vTaskDelay(pdMS_TO_TICKS(800));
	}
}

void Task2(void *pvParameters)
{
	while(1)
	{
	HAL_GPIO_TogglePin(GPIO_PIN_8,GPIO_PIN_7);
	vTaskDelay(pdMS_TO_TICKS(100));
	}
}
/* USER CODE END 0 */

/**
  * @brief  The application entry point.
  * @retval int
  */
int main(void)
{
  /* USER CODE BEGIN 1 */

  /* USER CODE END 1 */

  /* MPU Configuration--------------------------------------------------------*/
  MPU_Config();

  /* MCU Configuration--------------------------------------------------------*/

  /* Reset of all peripherals, Initializes the Flash interface and the Systick. */
  HAL_Init();

  /* USER CODE BEGIN Init */

  /* USER CODE END Init */

  /* Configure the system clock */
  SystemClock_Config();

  /* USER CODE BEGIN SysInit */

  /* USER CODE END SysInit */

  /* Initialize all configured peripherals */
  MX_GPIO_Init();
  /* USER CODE BEGIN 2 */
xTaskCreate(Task1,"task_start",128,NULL,0,NULL);
xTaskCreate(Task2,"task_start2",128,NULL,0,NULL);

  /* USER CODE END 2 */
vTaskStartScheduler();
  /* Infinite loop */
  /* USER CODE BEGIN WHILE */
  while (1)
  {
    /* USER CODE END WHILE */

    /* USER CODE BEGIN 3 */
  }
  /* USER CODE END 3 */
}

/**
  * @brief System Clock Configurationb
  * @retval None
  */
void SystemClock_Config(void)
{
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};

  /** Configure the main internal regulator output voltage
  */
  __HAL_RCC_PWR_CLK_ENABLE();
  __HAL_PWR_VOLTAGESCALING_CONFIG(PWR_REGULATOR_VOLTAGE_SCALE3);

  /** Initializes the RCC Oscillators according to the specified parameters
  * in the RCC_OscInitTypeDef structure.
  */
  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_HSI;
  RCC_OscInitStruct.HSIState = RCC_HSI_ON;
  RCC_OscInitStruct.HSICalibrationValue = RCC_HSICALIBRATION_DEFAULT;
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_NONE;
  if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK)
  {
    Error_Handler();
  }

  /** Initializes the CPU, AHB and APB buses clocks
  */
  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK|RCC_CLOCKTYPE_SYSCLK
                              |RCC_CLOCKTYPE_PCLK1|RCC_CLOCKTYPE_PCLK2;
  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_HSI;
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV1;
  RCC_ClkInitStruct.APB2CLKDivider = RCC_HCLK_DIV1;

  if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_0) != HAL_OK)
  {
    Error_Handler();
  }
}

/**
  * @brief GPIO Initialization Function
  * @param None
  * @retval None
  */
static void MX_GPIO_Init(void)
{
  GPIO_InitTypeDef GPIO_InitStruct = {0};
/* USER CODE BEGIN MX_GPIO_Init_1 */
/* USER CODE END MX_GPIO_Init_1 */

  /* GPIO Ports Clock Enable */
  __HAL_RCC_GPIOH_CLK_ENABLE();
  __HAL_RCC_GPIOB_CLK_ENABLE();

  /*Configure GPIO pin Output Level */
  HAL_GPIO_WritePin(GPIOB, GPIO_PIN_14|GPIO_PIN_7, GPIO_PIN_RESET);

  /*Configure GPIO pins : PB14 PB7 */
  GPIO_InitStruct.Pin = GPIO_PIN_14|GPIO_PIN_7;
  GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
  GPIO_InitStruct.Pull = GPIO_NOPULL;
  GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
  HAL_GPIO_Init(GPIOB, &GPIO_InitStruct);

/* USER CODE BEGIN MX_GPIO_Init_2 */
/* USER CODE END MX_GPIO_Init_2 */
}

/* USER CODE BEGIN 4 */

/* USER CODE END 4 */


/* MPU Configuration */

void MPU_Config(void)
{
  MPU_Region_InitTypeDef MPU_InitStruct = {0};

  /* Disables the MPU */
  HAL_MPU_Disable();

  /** Initializes and configures the Region and the memory to be protected
  */
  MPU_InitStruct.Enable = MPU_REGION_ENABLE;
  MPU_InitStruct.Number = MPU_REGION_NUMBER0;
  MPU_InitStruct.BaseAddress = 0x0;
  MPU_InitStruct.Size = MPU_REGION_SIZE_4GB;
  MPU_InitStruct.SubRegionDisable = 0x87;
  MPU_InitStruct.TypeExtField = MPU_TEX_LEVEL0;
  MPU_InitStruct.AccessPermission = MPU_REGION_NO_ACCESS;
  MPU_InitStruct.DisableExec = MPU_INSTRUCTION_ACCESS_DISABLE;
  MPU_InitStruct.IsShareable = MPU_ACCESS_SHAREABLE;
  MPU_InitStruct.IsCacheable = MPU_ACCESS_NOT_CACHEABLE;
  MPU_InitStruct.IsBufferable = MPU_ACCESS_NOT_BUFFERABLE;

  HAL_MPU_ConfigRegion(&MPU_InitStruct);
  /* Enables the MPU */
  HAL_MPU_Enable(MPU_PRIVILEGED_DEFAULT);

}

/**
  * @brief  Period elapsed callback in non blocking mode
  * @note   This function is called  when TIM1 interrupt took place, inside
  * HAL_TIM_IRQHandler(). It makes a direct call to HAL_IncTick() to increment
  * a global variable "uwTick" used as application time base.
  * @param  htim : TIM handle
  * @retval None
  */
void HAL_TIM_PeriodElapsedCallback(TIM_HandleTypeDef *htim)
{
  /* USER CODE BEGIN Callback 0 */

  /* USER CODE END Callback 0 */
  if (htim->Instance == TIM1) {
    HAL_IncTick();
  }
  /* USER CODE BEGIN Callback 1 */

  /* USER CODE END Callback 1 */
}

/**
  * @brief  This function is executed in case of error occurrence.
  * @retval None
  */
void Error_Handler(void)
{
  /* USER CODE BEGIN Error_Handler_Debug */
  /* User can add his own implementation to report the HAL error return state */
  __disable_irq();
  while (1)
  {
  }
  /* USER CODE END Error_Handler_Debug */
}

#ifdef  USE_FULL_ASSERT
/**
  * @brief  Reports the name of the source file and the source line number
  *         where the assert_param error has occurred.
  * @param  file: pointer to the source file name
  * @param  line: assert_param error line source number
  * @retval None
  */
void assert_failed(uint8_t *file, uint32_t line)
{
  /* USER CODE BEGIN 6 */
  /* User can add his own implementation to report the file name and line number,
     ex: printf("Wrong parameters value: file %s on line %d\r\n", file, line) */
  /* USER CODE END 6 */
}
#endif /* USE_FULL_ASSERT */
```
