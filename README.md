<H1><strong>Gas Sensor Alarm – ESP32</strong></H1>
Tento projekt využívá ESP32 a plynový senzor (např. MQ-2 / MQ-135) k detekci nebezpečné koncentrace plynů.
Jakmile naměřená hodnota překročí nastavený limit, systém automaticky spustí akustický alarm pomocí bzučáku.
<H2><strong>Funkce</strong></H2>
<P>
  ·  Měření koncentrace plynu v reálném čase 

  ·  Nastavitelná mezní hodnota

  ·  Automatická aktivace bzučáku při překročení limitu

  ·  Vhodné pro domácí detekci úniku plynu nebo jako školní projekt
</P>

<H2> <strong> Použité komponenty</strong></H2>
<P>
  · ESP32 C3 mini

  · Plynový senzor MQ

  · Bzučák
</P>

<h2>Zapojení hardwaru</h2>
<p>
  <strong>Zapojení plynového senzoru (MQ-2):</strong>

  · VCC → 5V (VIN) na ESP32

  · GND → GND

  · AO (Analog Output) → GPIO 0 (analogový vstup)

  
  <strong>Zapojení bzučáku:</strong>

   (SIGNAL) → GPIO 4

   (GND) → GND

  Schéma zapojení podobného alarmu je popsáno v návodech [3] [5].
</p>
<br> <img src="Assets/%5B1%5DFoto-Dokumentace.png" alt="vizualizovat" width="400"> </br>

<h2>Příprava vývojového prostředí</h2>
<p>
  Nainstaluj Arduino IDE

  Přidej podporu pro ESP32 (Board Manager) [1]

  Vyber správnou desku (např. ESP32C3 Dev Module)

  Nastav správný COM port

  Podrobný postup instalace ESP32 do Arduino IDE je popsán ve zdroji [1].
</p>

<h2>Programování ESP32</h2>
<p>
  Program funguje na principu:

  načtení analogové hodnoty ze senzoru

    void loop() {
      int hodnota = analogRead(GAS_SENSOR_PIN);
      Serial.println(hodnota);

  porovnání s mezní hodnotou --> zapnutí bzučáku při překročení limitu

    if (hodnota < 500) {
      digitalWrite(8, LOW);   // ticho  
    } else {
       digitalWrite(8, HIGH);  // alarm

  Zjednodušený princip:

  Pokud je hodnota nižší než limit → alarm vypnut

  Pokud je hodnota vyšší než limit → alarm zapnut

  Podobná logika je použita v projektech detekce plynu [2] [3].
</p>
<h2>Nastavení mezní hodnoty</h2>
<p>
  Mezní hodnota (threshold) se nastavuje přímo v kódu.
  Doporučuje se:

  sledovat hodnoty senzoru v Serial Monitoru

  určit běžnou hodnotu bez plynu

  nastavit limit o něco výš

  Kalibrace senzoru MQ je popsána v externích návodech [4].
</p>

<h2>Testování zařízení</h2>
<p>
  Připoj ESP32 k napájení

  Otevři Serial Monitor

  Nech senzor zahřát (cca 20–30 s)

  Přibliž k senzoru zdroj plynu (např. zapalovač bez zapálení)

  Ověř, že se při překročení limitu aktivuje bzučák
</p>
<h2>Problémy a jejich řešení</h2>
<p>
  Během realizace projektu se vyskytlo několik problémů, které bylo nutné vyřešit.

  Prvním problémem bylo zprovoznění bzučáku (pípáku). Při programování se bzučák po aktivaci nevypínal a nereagoval správně na změnu hodnot ze senzoru plynu. Tento problém se podařilo vyřešit úpravou programu a logiky řízení výstupu, se kterou mi pomohl Jakub Daško.

  Dalším problémem byla hardwarová závada, konkrétně prasklý propojovací vodič, kvůli kterému zařízení nefungovalo spolehlivě. Po kontrole zapojení byl vodič vyměněn, čímž se problém odstranil.

  Pak ještě , že GPIO 8 nebyl vhodný pro řízení bzučáku u ESP32-C3 mini kvůli možným problémům při bootování. Proto byl v projektu použit GPIO 4, který je stabilní digitální výstup.

  Podobné problémy jsou zmiňovány i v komunitních návodech [2] [5].

  Tyto komplikace přispěly k lepšímu pochopení jak programové, tak hardwarové části projektu.
</p>

<h2>Zdroje</h2>
<P>
  [1] ESP32IO. ESP32 – Gas Sensor [online]. Dostupné z:
  https://esp32io.com/tutorials/esp32-gas-sensor
  [cit. 2026-01-11].<br>

  [2] ESP32IO. ESP32 – Gas Sensor with Relay [online]. Dostupné z:
  https://esp32io.com/tutorials/esp32-gas-sensor-relay
  [cit. 2026-01-11].<br>

  [3] CYTRON TECHNOLOGIES. ESP32 Smoke Detection Alarm [online]. Dostupné z:
  https://my.cytron.io/tutorial/esp32-smoke-detection-alarm
  [cit. 2026-01-11].<br>

  [4] OPENELAB. Smart Gas Detector with ESP32 and MQ-2 Sensor [online]. Dostupné z:
  https://openelab.io/cs/blogs/learn/smart-gas-detector-with-esp32-and-mq-2-sensor
  [cit. 2026-01-11].<br>

  [5] SUNFOUNDER. ESP32 Gas Leak Alarm [online]. Dostupné z:
  https://docs.sunfounder.com/projects/umsk/en/latest/03_esp32/esp32_lesson36_gas_leak_alarm.html
  [cit. 2026-01-11].<br>

  [6]OPENELAB. Smart Gas Detector with ESP32 and MQ-2 Sensor. openelab.io [online]. Dostupné z:
  https://openelab.io/cs/blogs/learn/smart-gas-detector-with-esp32-and-mq-2-sensor [cit. 2026-01-11]. <br>

  [7]YouTube. MQ-2 Gas Sensor Tutorial for Arduino / ESP32 [video]. Dostupné z:
  https://www.youtube.com/watch?v=AnLn72h3HlM [cit. 2026-01-11].<br>
</P>


