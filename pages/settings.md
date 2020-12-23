# Nastavení KETCube
KETCube je vyvinut pro aplikace s nízkou spotřebou. Proto běh programu tomu také odpovídá. Po spuštění proběhne nastavení modulů a poté následuje běh smyčky následujícím způsobem: provádění činností všech zapnutých modulů - činnost terminálu - uspání se. Další činnost započne až po uplynutí základní periody (basePeriod - kterou lze pomocí terminálu nastavit).

Po nahrátí kódu nakonfigurujte KETCube v programu Putty. Ten lze po zvolení tohoto programu v menu **Nástroje / Upload Method** spustit z prostředí Arduino IDE stiskem tlačítka se symbolem “šipky”. V tomto terminálu lze sledovat běh kódu nebo provádět nastavení KETCube.

## Práce v terminálu (program Putty)

Pro konfiguraci a zobrazení informací lze použít tyto příkazy (terminál je case sensitive a je třeba tedy dodržovat malá a velká písmena):

  * about   - Výpis informací o KETCube
  * help    - Zobrazení nápovědy
  * disable - Zakázání modulu
  * enable  - Povolení modulu
  * list    - Zobrazení seznamu modulů
  * reload  - Restart KETCube a reset nastavení
  * show    - Zobrazení parametrů (výchozí hodnoty - po resetu)
  * showr   - Zobrazení parametrů (aktuální hodnoty)
  * set     - Nastavení parametrů (výchozí hodnoty - po resetu)
  * setr    - Nastavení parametrů (aktuální hodnoty)
  
Seznam modulů zobrazíte příkazem list.

```
>> list
Executing command: list

Available modules:
  N     D       LoRa    LoRaWAN module
  N     D       HDCX080 On-board RHT sensor - TI HDCX080
  N     D       batMeas On-chip battery voltage measurement
  N     D       ADC     Measure mVolts on PA4
  I     E       Arduino KETCube Arduino Support

Module State: E == Module Enabled; D == Module Disabled
Module severity: N = NONE, R = ERROR; I = INFO; D = DEBUG
Command execution OK
>>
```

V prvním sloupci je uvedena závažnost (severity) výpisů. Závažnost **None** nevypisuje žádné informace, závažnost **Error** pouze chybová hlášení, závažnost **Info** informace o běhu modulu a závažnost **Debug** ladící hlášení.

V druhém sloupci je uvedena informace o tom, zda je modul zapnutí či nikoliv. Písmeno **E** značí enable, tedy zapnutý modul, písmeno **D** pak disable, tedy vypnutý modul.

Ve třetím sloupci jsou uvedeny názvy modulů a ve čtvrtém stručné anotace.

Modul zapneme příkazem **enable {jméno modulu} {číslo severity}**. Např. pro spuštění modulu Arduino se závažností info: enable Arduino 2 a kód v KETCube znovu zavedeme příkazem **reload**.

Pro nastavení parametrů použijte příkaz **set**, pokud nastavujete globální parametry uložené v paměti EEPROM (zůstávají i po restartu) nebo příkaz **setr** pro nastavení přechodných parametrů (platí pouze do restartu).
Zobrazení globálních parametrů provedete příkazem **show**, přechodných parametrů pak příkazem **showr**.

## Základní moduly KETCube

### LoRa
KETCube je vyvinut pro aplikace ve světě tzv. Internetu věcí (IoT). Tento modul řídí komunikaci pomocí protokolu LoRaWAN.

### HDCX080
KETCube má na desce implementován senzor relativní vlhkosti a teploty. Tento modul řídí měření těchto fyzikálních parametrů prostředí a komunikaci se senzorem.

### batMeas 
Tento modul provádí měření napětí napájecí baterie. Protože při práci s KETCube EDU je zařízení napájené prostřednictvím USB kabelu, nebudete tento modul patrně používat.

### ADC
Tento modul provádí měření napětí v mV na pinu AN.

### Arduino
Modul, jehož funkci můžete programovat v prostředí Arduino IDE. **Pracujete-li s KETCube EDU, programujete funkci právě tohoto modulu.**

## Hlavní parametry KETCube
Hlavní parametry, nebo také parametry jádra KETCube, definují základní chování KETCube. Nastavení se provádí příkazem ve formátu **set core {CMD}**.

Hlavní parametry jádra KETCube jsou:

### basePeriod
Základní perioda, po které se KETCube probudí a provede periodické akce definované v povolených modulech.

### startDelay
Doba po startu, po kterou KETCube čeká před provedením první periodické akce. Tato doba je ve výchozím nastavení náhodné číslo od 1 do 60s.

### severity
Informuje o úrovni s jakou se vypisují informace jádra. To ovlivňuje zejména množství informací vypsaných na terminál při inicializaci KETCube.

## Nastavení modulu Arduino

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
