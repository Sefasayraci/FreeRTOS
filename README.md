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
