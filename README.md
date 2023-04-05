# FreeRTOS
Real Time Operating System witch application from this Microcontroller

# What is RTOS?
Real-time operating systems provide support for resource management, communication, precise scheduling, synchronization and planning. RTOS has a deadline associated with the tasks and must complete the tasks before this deadline. RTOS should be deterministic, quality of service (QoS) and deadline driven.
For Example:

Deos (DDC-I),
embOS (SEGGER), 
FreeRTOS (Amazon),
Integrity (Green Hills Software), 
Keil RTX (ARM), LynxOS (Lynx Software Technologies), 
MQX (Philips NXP / Freescale), 
Nucleus (Mentor Graphics), 
Neutrino (BlackBerry), 
PikeOS (Sysgo), 
SafeRTOS (Wittenstein), 
ThreadX (Microsoft Express Logic), 
µC/OS (Micrium), VxWorks (Wind River), 
Zephyr (Linux Foundation) are popular real-time processing systems.

In addition to these;

I will explain the operating systems that I want to go into detail on my field and the operating systems I have researched and studied.

# Integrity
Integrity is an operating system product developed by Hewlett-Packard. It is designed for environments with high security requirements. Integrity is widely used in places with high security requirements, such as large enterprises, banks and government agencies.
In addition, it is also used as a reliable operating system, especially in air combat aircraft. 
For example, the operating system product that is part of this family, the Green Hills Software Integrity DO-178B real-time operating system (RTOS), also plays a role in the F35 fighter jet manufactured by Lockheed Martin. In Turkey, the Real-time National Operating System (RTOS), developed by TÜBİTAK and Havelsan, continues to be actively used.

The Integrity operating system is specifically optimized for applications that require high security and high performance. This operating system can run on multi-processor systems, allowing applications requiring high performance to be run in parallel.

The most widely used version of the Integrity operating system family is HP-UX. HP-UX is optimized for workloads that require high security and high performance. The Integrity family of operating systems is also compatible with other operating systems, including OpenVMS and NonStop operating systems.

![image](https://user-images.githubusercontent.com/73780930/230222355-0dfc37ec-dd22-49fc-990e-fa845b4d0012.png)
![image](https://user-images.githubusercontent.com/73780930/230222371-4dbdfdab-efc1-4858-9edf-2668c9544e39.png)

*HP-UX 11.11 İşletim Sistemi*

It is a very well secured operating system. They are written to protect operating systems against unauthorized access. The Integrity operating system does not compromise on security-based applications in this regard.

# GIS 
In Turkey, the GİS Operating System enables the indigenous development of important technologies used in the defense sector, such as UAVs, helicopters and aircrafts. Since the indigenous development of these technologies is ensured with national software, external intervention in the systems is also prevented. Officials stated that the GİS can be easily used in the integration of any project thanks to its scalable feature.

![image](https://user-images.githubusercontent.com/73780930/230222551-79aad076-8881-4e05-b90f-5b9b2458822c.png)

# VXWorks
Wind River VXWorks, developed by Wind River Systems, is an operating system for real-time embedded systems. VXWorks is specifically designed for high-reliability, low latency, fast and deterministic embedded applications.

VXWorks is especially used in industries such as aerospace, defense, automotive, industrial automation, medical devices and telecommunications. Devices in these industries are often used in areas where factors such as reliability and speed are critical, and VXWorks is designed to meet these requirements.

VXWorks can run on different processor architectures and hardware platforms. It is also a suitable operating system for networked devices and has a TCP/IP protocol stack. VXWorks is also compatible with popular programming languages such as C/C++ and Ada, allowing developers to easily develop software.

VXWorks includes features critical for real-time applications. These features include event-driven scheduling, interrupt management, process prioritization, timing management and debugging tools. These features are a great help in the development of real-time applications, which are critical to the reliability and performance of devices.

# What is FreeRTOS?

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


