# Kompilace a nahrání kódu do KETCube

Po editaci textu kódu provedete kompilaci (ověření) stiskem tlačítka se symbolem “háčku” -  první tlačítko v horní liště pod menu nabídkou.

---
**Poznámka**

Dokumentaci API KETCube EDU naleznete na webu: [https://edu.ketcube.cz/files/apidoc/](https://edu.ketcube.cz/files/apidoc/) 

---

V nabídce  Nástroje / Upload Method zvolte položku **STM32Flash (serial bootloader)**. 

Nahrátí kódu provedete stiskem tlačítka se symbolem “šipky vpravo” - druhé v horní liště pod menu nabídkou. 

Po prvním nahrání kódu pokračujte [nastavením KETCube](settings.md).

---
**Poznámka**
KETCube EDU se dodává v konfiguraci pro automatické nahrání aplikačního kódu - s deskou KETCube UART a KETCube mainBoard propojenou přídavnými “jehlovými konektory”. Pokud Vaše konfigurace není vybavena “jehlovými konektory”, je potřeba před stiskem tlačítka pro nahrání kódu inicializovat Bootloader. Bootloader inicializujete stiskem a podržením levého tlačítka **BOOT** na desce KETCube, krátkým stiskem pravého tlačítka **RST** a puštěním tlačítka **BOOT**.

Bootloader je malý program, který se stará o aktualizaci aplikačního kódu v KETCube.

---

