# Blikání LED na desce KETCube

V tomto příkladu si osvojíte základní práci s KETCube a rozblikáte LED diody na desce.

## Zapojení

K tomuto příkladu není potřeba ke KETCube připojovat žádné periferie. KETCube pouze připojte k PC: zapojte Micro USB kabel do desky KETCube UART.

## Programování a spuštění

Nahrajte následující kód do KETCube.

```c
void setup() {
  // Zobrazení zprávy v terminálu na začátku inicializace
  KETCube.Terminal.print("Blikajici LED @ KETCube");

  // Nastavení PINů LED1 a LED2 - budiče LED
  KETCube.LED.init(LED1, HIGH);
  KETCube.LED.init(LED2, HIGH);

  // Nastavení LED na trvalé blikání
  KETCube.LED.set(LED1, LED_BLINK_CONT);
  KETCube.LED.set(LED2, LED_BLINK_CONT);
}

void loop() {
  // V každé periodě: vypsání textu
  KETCube.Terminal.print("basePeriod @ KETCube");
}
```

Vy výpisu kódu vidíte dvě funkce: *setup()* a *loop()*. zatímco funkce *setup()* se vykoná pouze jednou - a to ihned po startu KETCube, funkce *loop()* se vykonává opakovaně a periodu jejího opakování lze změnit pomocí terminálového příkazu *set core basePeriod*.

Funkce dostupné na KETCube jsou ćlenény do několika kategorií a volány pomocí tečkové notace.

Uvnitř funkce *setup()* vidíte volání funkce *print()* z kategorie *Terminál*, která je volána pomocí tečkové notace takto: *KETCube.Terminal.print()*. Tato funkce vypíše během fáze inicializace na Terminál text "Blikajici LED @ KETCube".

Pomocí kategorie LED můžeme rovnou nastavit vybrané PINy jako řadiče LED diod a přiřadit jim určité chování: funkce *KETCube.LED.init()* nastaví PINy jako řadiče LED a funkce *KETCube.LED.set()* nastaví obě LED do režimu trvalého blikání.

## Nastavení KETCube

Nejprve si přečtěte sekci [nastavení KETCube](settings.md).

Aby KETCube spustil Váš kód, musíte v Terminálu nejprve povolit modul *Arduino*.

Proveďte v terminálu tyto příkazy:

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

Nyní je modul *Arduino* povolen.

Máte-li povolen modul *Arduino* a úspěšně jste nahráli kód tohoto příkladu do KETCube, vidíte synchronní blikání obou LED diod - zároveň pozorujte terminálový výstup KETCube:

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
