# Čtení analogové hodnoty

V tomto příkladu se naučíte číst analogové hodnoty. 

Pokud jste ještě nepracovali s Terminálem a LED diodami, podívejte se nejprve na příklad [Blikání LED na desce KETCube](example_onBoardLED.md)

Nastavení KETCube je totožné jako v příkladu [Blikání LED na desce KETCube](example_onBoardLED.md)

## Zapojení desky

TODO: PIN AN připojte přes potenciometr k zemi a přes pull-up k napájení.

Poté KETCube připojte k PC: zapojte Micro USB kabel do desky KETCube UART.

---
**TODO**

schéma

---

## Programování a spuštění

Nahrajte následující kód do KETCube.

```c
void setup() {
  // Zobrazí zprávu v terminálu na začátku inicializace
  KETCube.Terminal.print("ADC @ KETCube");

  // Nastaví PIN AN jako analogový vstup
  KETCube.IO.pinMode(AN, ANALOG);

  // Inicializuje ADC
  KETCube.Analog.init();
}

void loop() {
  // V každé periodě změří napětí na potenciometru
  // a hodnotu napětí vypíše na Terminál
  KETCube.Terminal.print("U = %d mV", KETCube.Analog.read(AN));
}
```

Ve funkci *setup()* nastavujeme PIN AN jako analogový vstup, ale navíc musíme také nastavit převodník analogové hodnoty - ADC (Analog to Digital Converter) - to uděláme pomocí funkce *KETCube.Analog.init()*.

Voláním funkce *KETCube.Analog.read()* v každé periodě (ve funkci *loop()*) získáme okamžitou hodnotu napětí na PINu AN v milivoltech.

Po úspěšném překladu a nahrání kódu do KETCube otáčejte potenciometrem a sledujte hodnotu naměřeného napětí v Terminálu.
