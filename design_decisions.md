# Deisgn Decisions

This document covers the various design decisions for the projects. Broken down by category.

## System Architecture

The top-level system architecture is a star pattern of a central hub, and client nodes. Clients generate and receive events. The hub simply provides a mechanism for clients to communicate with each other. 

We could have used a mesh architecture to acheive the same outcome, but at the start there were few mature mesh frameworks available and easy to use. Instead, the hub has an MQTT server, and clients communicate to it using that protocol. Clients subscribe to topics and publish to topics to communicate with each other.

The hub can serve as an access point well as an MQTT server, or can be a wifi client with only the MQTT server. For those crafty enough, the hub is not required at all -- all clients can be on a wifi network and the MQTT server could be on a RPI or computer or VM. For simplicity for the causal user, the hub is provided without any peripherals or frills.

## Hardware Platform

First and foremost, the platform is based on the ESP32. Simply put, the Espressif platform checks all the boxes for the project. It is low cost, well supported, supports all the wireless technologies required, and readily available. 

Other platforms considered include:
* Raspberry Pi - meets most requirements but too expensive
* RP2040 - not available when the project was started; not well supported; a little expensive
* Arduino - generally does not support wifi or bluetooth without extra HW
* STM32 - no native networking

## Hardware Design

We decided early on a custom PCB would be required. None of the availabnle ESP32 modules broke out all the IO pins, and nearly all had odd hardware configurations or were intended for battery operation. We simply don't need all the extra circuitry and added cost.

The system is based on a single highly configurable core mother board. The core can be configured as a client or a hub, and can support a wide-range of peripherals. The user can selectively enable or disable peripherals on demand and the hardware will reconfigure itself.

All peripherals are external from the main mother board and connect via cables and high density connectors (e.g., typically JST SH 3 or 4 pin connectors). 

The motherboard can be powered via an external power module that converts 120 or 240 to 5V, or via a 5V power supply.

## Software Architecture

Given the selection of the ESP32, we could fully exploit the real time operating system (RTOS) capabilities of FreeRTOS. As such, the application is fully multi-threaded. We try to keep the number of threads to a minimum, but because of the multi-threaded nature of the application, we use events to propagate actions throughout the application. This does complicate understanding exactly how things "happen" at times, but provides a lot of flexibility.

We try to localize responses to events to specific "managers" to simplify understandabiliy. Example, listening for and reacting to events to change the indicators is handled exclusively within the IndicatorManager. Even if many things needs to happen based on a single event, a specific manager will focus on just one of them. Multiple managers will listen for the event and respond accordingly.

## Saving Information

Any information that needs to be persisted across power cycles is stored in Flash, specifically ESP32 "Preferences".

Individual preferences are stored key/value. Anything more complicated is stored as a JSON string. That lets us easily send and receive changes easily.

Routines are stored individually so we don't have to save the entire file each time a single routine is modified.
