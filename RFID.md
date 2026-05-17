```
#include <SPI.h>
#include <MFRC522.h>

#define SS_PIN 10
#define RST_PIN 9

MFRC522 rfid(SS_PIN, RST_PIN);

// UID autorizado
byte authorizedUID[4] = {0xBD, 0x31, 0x15, 0x2B};

void setup() {
  Serial.begin(9600);
  SPI.begin();

  rfid.PCD_Init();

  Serial.println("Aproxime a tag RFID...");
}

void loop() {

  // Verifica se existe cartão
  if (!rfid.PICC_IsNewCardPresent()) {
    return;
  }

  // Lê cartão
  if (!rfid.PICC_ReadCardSerial()) {
    return;
  }

  Serial.print("UID: ");

  bool autorizado = true;

  // Mostra UID
  for (byte i = 0; i < rfid.uid.size; i++) {

    Serial.print(rfid.uid.uidByte[i], HEX);
    Serial.print(" ");

    // Verifica UID
    if (rfid.uid.uidByte[i] != authorizedUID[i]) {
      autorizado = false;
    }
  }

  Serial.println();

  // Resultado
  if (autorizado) {
    Serial.println(">>> ACESSO LIBERADO <<<");
  } else {
    Serial.println(">>> ACESSO NEGADO <<<");
  }

  Serial.println();
```
  rfid.PICC_HaltA();
}
`` 
