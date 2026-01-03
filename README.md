🚗 Android Automotive – Car Property & VHAL Integration Demo
📌 Overview

This project is an Android Automotive OS demo application that showcases how to interact with Vehicle HAL (VHAL) using the Car API and CarPropertyManager.

The application runs as a background service, starts automatically after system boot, and listens to vehicle property changes in real time. It also demonstrates how to send commands from the application back to the vehicle using VHAL properties.

The architecture is modular, scalable, and production-oriented, making it suitable for OEM-level Android Automotive development.

✨ Key Features

✅ Automatic startup after vehicle boot

✅ Background service for continuous vehicle signal monitoring

✅ Connection to Android Automotive Car API

✅ Read & write VHAL properties using CarPropertyManager

✅ Real-time property change callbacks

✅ Handler-based architecture for scalability

✅ Support for both Vehicle → App and App → Vehicle communication

✅ Clean separation of concerns

🏗️ Architecture Overview
+-------------------+
| Vehicle (VHAL)    |
+---------+---------+
          |
          v
+-------------------+
| CarPropertyManager|
+---------+---------+
          |
          v
+-------------------+
| Property Handlers |
| (Base + Concrete) |
+---------+---------+
          |
          v
+-------------------+
| Repository Layer  |
+-------------------+
          |
          v
+-------------------+
| UI / Business     |
| Logic             |
+-------------------+

📂 Project Structure
com.io.utkarsh.vhal_demo_app
│
├── core
│   └── CarPropertyManager.java
│
├── handler
│   ├── BasePropertyHandler.java
│   └── CarPropertyHandler.java
│
├── receiver
│   └── BootCompleteReceiver.java
│
├── service
│   └── CarPropertyServiceManager.java
│
├── repository
│   └── CarPropertyCallbackRepository.java
│
└── interfaces
    └── IBasePropertyHandler.java

🧠 Core Components Explanation
🔹 CarPropertyManager (Core Layer)

Connects to the Android Automotive Car API

Retrieves CarPropertyManager

Initializes property handlers

Registers and unregisters vehicle properties

Fetches default values from VHAL

🔹 BasePropertyHandler (Abstract Layer)

Acts as a reusable base class for all vehicle property handlers

Handles:

Property registration

Callback management

Common get/set utility methods

Ensures consistency and scalability

🔹 CarPropertyHandler (Business Logic Layer)

Implements actual vehicle signal logic

Handles:

Exterior work light status

Gear selection (example extension)

Processes property change events

Sends updates to repository layer

🔹 CarPropertyServiceManager (Background Service)

Keeps the app running in the background

Initializes CarPropertyManager

Uses START_STICKY to ensure reliability

Cleans up property callbacks on destroy

🔹 BootCompleteReceiver

Starts the service automatically after system boot

Ensures continuous vehicle signal monitoring

🔄 Data Flow
Vehicle → App

VHAL updates a property

onChangeEvent() is triggered

Property handler reads value

Data is forwarded to repository

UI or business logic consumes the data

App → Vehicle

App sets a command value

CarPropertyManager.setIntProperty() is called

VHAL receives the command

Vehicle state is updated

🚦 Supported Vehicle Properties (Example)
Property	Direction	Description
Exterior Work Light Status	Vehicle → App	Reads current light status
Exterior Work Light Command	App → Vehicle	Sends command to vehicle
Gear Selection	Vehicle → App	Reads current gear position
🔧 How to Add a New Vehicle Property

Add property ID in generatePropertyList()

Handle property in onChangeEvent()

Read value using helper methods

Forward data to repository

(Optional) Add setter method for commands

Thanks to the handler-based architecture, no changes are required in the core manager or service.

▶️ Getting Started
Prerequisites

Android Automotive OS

System-level app permissions

Access to VHAL properties

Android Studio

Build & Run

Clone the repository

Import into Android Studio

Build as a system app

Deploy to Automotive emulator or target hardware

Reboot system to trigger boot receiver

🧪 Logging & Debugging

All major lifecycle events and property updates are logged using Logcat:

CarPropertyManager
BasePropertyHandler
CarPropertyHandler
CarPropertyServiceManager

🚀 Future Enhancements

Add more vehicle signals (speed, indicators, doors, HVAC)

UI integration using LiveData / Flow

Error handling and reconnection logic

Unit testing for property handlers

Multi-area property support

📌 Use Cases

Android Automotive OEM apps

Vehicle signal monitoring

Infotainment integrations

Automotive middleware prototyping

Interview & learning reference project

📝 License

This project is intended for educational and demonstration purposes.
Adapt and extend according to OEM or project requirements.

💬 Final Note

This project demonstrates real-world Android Automotive development patterns using clean architecture, background services, and VHAL integration.

⭐ If you find this useful, consider starring the repository!
