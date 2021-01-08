# Nastavení LoRaWAN v KETCube

Pro úspěšné připojení do sítě LoRaWAN musíte nakonfigurovat KETCube a zároveň provést příslušná nastavení sítě tak, aby se KETCube mohl do sítě připojit. Tento text pokrývá pouze nastavení zařízení KETCube, proces nastavení zařízení v síti se může lišit dle provozovatele sítě. Většina poskytovatelů však poskytuje podrobnou dokumentaci, podle které byste měli při nastavení zařízení v síti postupovat. Použitá terminologie vychází ze standardu LoRaWAN, můžete tedy postupovat dle tohoto návodu a termíny použít jako odkazy do uživatelské dokumentace vašeho poskytovatele sítě LoRaWAN. 

---
**Poznámka**

Využíváte-li síť [města Plzně](https://lora.plzen.eu/) nebo síť společnosti [LORATECH](https://app.loratech.cz), nastavte údaje na serveru podle [manuálu](https://app.loratech.cz/manual.pdf) (cs).

Využíváte-li síť [The Things Network](https://www.thethingsnetwork.org/), postupujte podle návodu [na webu TTN](https://www.thethingsnetwork.org/docs/devices) (en).

---

KETCube EDU je kompatibilní s protokolem LoRaWAN verze 1.0.3, i když specifické verze KETCube podporují LoRaWAN protokol verze 1.1.0, tento manuál se vztahuje ke KETCube EDU, a tedy k verzi 1.0.3.

## Základní pojmy

### ABP (Activation-By-Personalization)
Nejjednodušší metoda připojení k síti LoRaWAN. Zařízení se připojí do sítě na základě statické adresy (*devAddr*) a klíčů sezení - *appSKey* a *nwkSKey* - jež jsou trvale uloženy v zařízení.

### AES (Advanced-Encryption-Standard)
Standardizovaný šifrovací algoritmus. V síti LoRa se pracuje se 128-bitovými AES klíči.

### OTAA (Over-The-Air Activation)
Preferované metoda připojení k síti LoRaWAN. Zařízení se připojí do sítě na základě identifikátorů *appEUI*, *devEUI* a *appKey* a je mu dynamicky přiřazena síťová adresa *nwkAddr* a jsou vygenerovány šifrovací klíče pro samotné zabezpečení komunikace (*appSKey* a *nwkSKey*).

### appEUI
Identifikátor aplikace o délce 64 bitů.

### appKey
Aplikační klíč o délce 128 bitů. V případě použití metody *OTAA* slouží k autentizaci zařízení v síti a odvození relačních klíčů.

### appSKey
Aplikační klíč relace o délce 128 bitů. Používá se pro šifrování přenášených aplikačních dat. V případě *OTAA* je odvozen od *appKey*, v případě *ABP* je jeho hodnota pro dané zařízení konstantní.

### devAddr
Adresa zařízení v síti LoRaWAN o délce 32 bitů; prefix adresy zařízení je tvořen adresou sítě.

### devClass
Třída zařízení: A, B nebo C. Třída zařízení definuje chování zařízení v síti: zařízení třídy A periodicky odesílá zprávy do sítě LoRaWAN a je připraveno přijímat zprávy ze sítě jen v definovaný okamžik - v tzv. okně (RX window). Zařízení třídy C je schopno pŕijímat zprávy ze sítě v kterýkoli okamžik, avšak za cenu vyšší spotřeby. Třída B definuje zařízení pracující synchronně a umožňuje zařízení přijímat zprávy v definované okamžiky - třída B je v KETCube EDU podporována pouze experimentálně.

### devEUI
Jednoznačný identifikátor zařízení o délce 64 bitů, který je přiřazen výrobcem zařízení.

### nwkSKey
Síťový klíč relace o délce 128 bitů. Používá se pro ověření integrity přenášených dat. V případě *OTAA* je odvozen od *appKey*, v případě *ABP* je jeho hodnota pro dané zařízení konstantní.

## Kontrola aktuálního nastavení
Aktuální nastavení modulu LoRa v KETCube zjistíte pomocí [terminálu](settings.md): je-li modul **LoRa** povolen s nastavenou závažností (severity) na úrovni INFO, je po resetu KETCube vypsáno aktuální nastavení modulu - včetně všech důležitých parametrů:

```
Module severity level: INFO
LoRa :: LoRaWAN SPEC version: 1.0.3
LoRa :: Device class A
LoRa :: OTAA Mode enabled
LoRa :: devEUI=37-30-36-30-7B-39-84-06
LoRa :: appEUI=00-00-00-00-00-00-00-00
LoRa :: appKey=00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00
>>
```

Většinu z těchto parametrů lze změnit pomocí příkazu **set** a individuálně vypsat pomocí příkazu **show**, např.:

```
>> set LoRa appEUI 0011223344556677
...
>> show LoRa appEUI
...
```

Všimněte si, že dlouhá čísla - jako klíče a identifikátory se zadávají v hexadecimálním formátu. 

LoRaWAN parametry musíte nastavit shodně na aplikačním serveru vaší LoRaWAN sítě a v zařízení KETCube. KETCube umožňuje modifikovat parametr *devEUI*, ale tento postup není doporučen pro běžné užití.

Pro většinu případů doporučujeme definovat zařízení jako zařízení třídy A (výchozí hodnota) a k síti se doporučujeme připojovat metodou *OTAA* (výchozí hodnota).

Použijete-li metodu *OTAA*, stačí na serveru nastavit *devEUI* vašeho zařízení a nastavit shodně parametry *appEUI* a *appKey*.

Poté, co provedete nastavení všech parametrů modulu LoRa a provedete nastavení na straně síťového aplikačního serveru můžete KETCube restartovat příkazem **reload** a vyčkat na připojení. Za předpokladu, že jste v dosahu vaší sítě a modul **LoRa** povolen s nastavenou závažností (severity) na úrovni INFO, uvidíte na terminálu KETCube - po úspěšném připojení k síti - obdobný výpis:

```
>>
LoRa :: Not joined
LoRa :: NetID: 0x916019
LoRa :: DevAddr: 0x3314FC05
LoRa :: Datarate: DR_0
LoRa :: CFList :: New Freq: 867100000 Hz
LoRa :: CFList :: New Freq: 867300000 Hz
LoRa :: CFList :: New Freq: 867500000 Hz
LoRa :: CFList :: New Freq: 867700000 Hz
LoRa :: CFList :: New Freq: 867900000 Hz
LoRa :: Joined
>>

...

LoRa :: Transmitting sensor data: SUCCESS
>>
```

## Nejčastější problémy

### Jednou za čas se nepodaří zprávu odeslat: na terminálu vidím chybové hlášení modulu LoRa.

Vidíte-li v KETCube terminálu podobný výpis:

```
LoRa :: Transmitting sensor data: ERROR
```
pak máte s velkou pravděpodobností špatně nastaven poměr mezi periodou měření - parametr *core basePeriod* -  a tzv. *data-rate* - parametr *LoRa txDatarate*.

V síti LoRaWAN může zařízení vysílat na daném kanále maximálně 1% času. Modulace LoRa, která je v síti LoRaWAN použita umožňuje velmi spolehlivý přenos dat za cenu délky vysílání. To však znamená, že trvá-li vysílání např. 1 sekundu, na témže kanále může KETCube vysílat až za 99 sekund. 

LoRaWAN však umožňuje nastavení parametrů vysílání a modulace tak, že se doba vysílání zkrátí - za cenu snížení spolehlivosti přenosu a tedy i dosahu. Obecně lze říci, že máte-li dobré pokrytí sítě LoRaWAN, můžete snížit dobu vysílání a vysílat častěji. Jste-li však velmi vzdáleni od nejbližšího vysílače (*gateway*), nebo je vaše zařízení umístěno v místech s nižší penetrací signálu (železobetonové budovy, sklepy, apod.), měli byste zvýšit periodu vysílání a použít spolehlivější přenos.

V případě dobrého pokrytí nastavte parametr *txDatarate* až na hodnotu 5, v případě velmi špatného pokrytí na hodnotu 0 (výchozí hodnota - nejspolehlivější přenos). Podle parametru *txDatarate* pak nastavte parametr *basePeriod* tak, abyste eliminovali neúspěšné pokusy o vysílání.

Příklad nastavení při nízké *txDatarate*:

```
>> set LoRa txDatarate 0
>> set core basePeriod 120000
```

Příklad nastavení při vysoké *txDatarate*:

```
>> set LoRa txDatarate 4
>> set core basePeriod 10000
```
