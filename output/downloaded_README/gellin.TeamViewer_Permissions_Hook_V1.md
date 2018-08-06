# TeamViewer Permissions Hook V1
---
[![License](http://img.shields.io/badge/license-MIT-green.svg)](https://github.com/gellin/TeamViewer_Permissions_Hook_V1/blob/master/LICENSE)

**A proof of concept injectable C++ DLL, that uses naked inline hooking and direct memory modification to change TeamViewer permissions.**

## Features
* **As the Server** - Enables extra menu item options on the right side pop-up menu. Most useful so far to enable the "switch sides" feature which is normally only active after you have already authenticated control with the client, and initiated a change of control/sides.
* **As the Client** - Allows for control of mouse with disregard to servers current control settings and permissions.

## Demo

#### As the Server
![](server_switch_sides.gif?raw=true)

#### Client
![](client_takes_control.gif?raw=true)

## Rundown
* Utilizes signature/pattern scanning to dynamically locate key parts in the code at which the assembly registers hold pointers to interesting classes. Applies inline naked hooks a.k.a code caves, to hi-jack the pointers to use for modification via direct memory access to their reversed classes.
* Inject and follow the steps

## Requirements
* Your favorite Manual Mapper, PE Loader, DLL Injector, inject into - "TeamViewer.exe"
* This version was Built on Windows 10, for TeamViewer x86 Version 13.0.5058 - (Other versions of TeamViewer have not been tested but with more robust signatures it may work, linux not supported)

## Disclaimer
* Developed for educational purposes as a proof of concept for testing. I do not condone the or support the use of this software for unethical or illicit purposes. No responsibility is held or accepted for misuse.

## Credit
[@timse93](https://github.com/timse93) - Research and Testing