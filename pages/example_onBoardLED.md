# Blikání LED na desce KETCube

Kód interaguje s KETCube terminálem - po startu vypíše na terminál "My First LED blink Example!" a nastaví obé LED na desce KETCube do režimu trvalého blikání.


```c
void setup() {
  // Zobrazí zprávu v terminálu během inicializace
  KETCube.Terminal.print("My First LED blink Example!");

  // Nastaví PINy LED1 a LED2 jako budiče LED
  KETCube.LED.init(LED1, LOW);
  KETCube.LED.init(LED2, LOW);

  // Nastaví LED na trvalé blikání
  KETCube.LED.set(LED1, LED_BLINK_CONT);
  KETCube.LED.set(LED2, LED_BLINK_CONT);
}

void loop() {
  // žádný periodický kód

}
```

Proveďte tyto příkazy v terminálu:

```
>>
>> enable Arduino 2
Executing command: enable
Command execution OK
>> set core severity 2
Executing command: severity
Command execution OK
severity returned: 2
>>
>> reload

```

Poté sledujte terminálový výstup KETCube:

```
Executing command: reload

Performing system reset and reloading KETCube configuration ...

Welcome to KETCube Command-line Interface
-----------------------------------------
Version: 0.2-dev (build: e0f8b59)

Use [TAB] key to show build-in help for current command
Use [ENTER] key to execute current command
Use [+]/[-] keys to browse command history

List of commands:
        about   Print ABOUT information: Copyright, License, ...
        help    Print HELP
        disable Disable KETCube module
        enable  Enable KETCube module
        list    List available KETCube modules
        reload  Reload KETCube
        show    Show LoRa, SigFox ... parameters
        showr   Show LoRa, SigFox ... RUNNING parameters
        set     Set LoRa, SigFox ... parameters
        setr    Set LoRa, SigFox ... RUNNING parameters

--- "core" Init() START ---
KETCube core base period set to: 500 ms
KETCube start delay set to: 25000 ms
KETCube core severity level: INFO
KETCube driver severity level: NONE
--- "core" Init() END ---

--- "Arduino" Init() START ---
Module severity level: ERROR
Arduino :: My First LED blink Example!
--- "Arduino" Init() END ---

>>
>>

```

Nyní vidíte synchronní blikání obou LED.
