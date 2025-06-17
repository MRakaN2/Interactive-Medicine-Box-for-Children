#include <Wire.h>
#include <RTClib.h>
#include <SoftwareSerial.h>
#include <DFRobotDFPlayerMini.h>
#include <Servo.h>
#include <LowPower.h>

Servo myServo;  // Membuat objek servo

// RTC
RTC_DS3231 rtc;

// DFPlayer via SoftwareSerial
SoftwareSerial dfSerial(10, 11); // RX = 10, TX = 11
DFRobotDFPlayerMini pemutarAudio;

// Pin
#define PIN_LED 2
#define PIN_BUZZER 3
#define PIN_TOMBOL 7

// Status logika
bool sudahDinyalakan = false;
bool sudahDirespon = false;
bool sudahPeringatanLambat = false;

// Variabel tombol (tanpa debounce)
bool lastStateTombol = HIGH;

// Untuk tampilan waktu
unsigned long waktuTerakhirCetak = 0;

void setup() {
  Serial.begin(9600);
  Wire.begin();

  myServo.attach(9); // Menghubungkan servo ke pin digital 9

  pinMode(PIN_LED, OUTPUT);
  pinMode(PIN_BUZZER, OUTPUT);
  pinMode(PIN_TOMBOL, INPUT_PULLUP);

  digitalWrite(PIN_LED, HIGH);
  noTone(PIN_BUZZER);

  if (!rtc.begin()) {
    Serial.println("RTC tidak terdeteksi!");
    while (1);
  }
  Serial.println("RTC terdeteksi!");
  rtc.adjust(DateTime(F(_DATE), F(TIME_)));

  dfSerial.begin(9600);
  if (!pemutarAudio.begin(dfSerial)) {
    Serial.println("Gagal memulai DFPlayer Mini.");
    while (1);
  }
  // myServo.write(0);
  delay(1000);
  pemutarAudio.volume(30); // 0–30
  // pemutarAudio.play(5);    // Putar 005.mp3 saat start
}

bool tombolDitekan() {
  bool currentState = digitalRead(PIN_TOMBOL);
  if (lastStateTombol == HIGH && currentState == LOW) {
    lastStateTombol = currentState;
    return true;
  }
  lastStateTombol = currentState;
  return false;
}

void loop() {
  myServo.write(90);
  DateTime sekarang = rtc.now();

  if (millis() - waktuTerakhirCetak >= 1000) {
    waktuTerakhirCetak = millis();
    Serial.print("Waktu: ");
    Serial.print(sekarang.hour());
    Serial.print(":");
    if (sekarang.minute() < 10) Serial.print("0");
    Serial.print(sekarang.minute());
    Serial.print(":");
    if (sekarang.second() < 10) Serial.print("0");
    Serial.println(sekarang.second());
  }

  bool tombol = tombolDitekan();
  int jam = sekarang.hour();
  int menit = sekarang.minute();
  int detik = sekarang.second();

  // Reset status setelah lewat batas telat
  if ((jam < 20 || (jam > 21)) && (sudahDinyalakan || sudahDirespon || sudahPeringatanLambat)) {
    sudahDinyalakan = false;
    sudahDirespon = false;
    sudahPeringatanLambat = false;
    digitalWrite(PIN_LED, HIGH);
    noTone(PIN_BUZZER);
  }

  // Alarm aktif
  if (jam == 20 && menit == 0 && !sudahDinyalakan) {
    playMelody2();
    sudahDinyalakan = true;
    pemutarAudio.play(5);
    delay(5000);
    tone(PIN_BUZZER, 300); 
  }

  if (sudahDinyalakan && !sudahDirespon) {
    if (millis() % 1000 < 500) {
      digitalWrite(PIN_LED, HIGH);
    } else {
      digitalWrite(PIN_LED, LOW);
    }

    // Tombol ditekan sesuai jadwal
    if (tombol) {
      playMelody2();
      sudahDirespon = true;
      myServo.write(0);
      delay(1000);
      digitalWrite(PIN_LED, HIGH);
      noTone(PIN_BUZZER);
      pemutarAudio.play(3);
      delay(10000);
      playMelody2();
    }

    // Peringatan telat
    if (!sudahPeringatanLambat && (jam == 21 && menit == 0)) {
      sudahPeringatanLambat = true;
      noTone(PIN_BUZZER);
      pemutarAudio.play(2);
      delay(5000);
      tone(PIN_BUZZER, 300);
    }

    // Dinyatakan telat dan tidak boleh minum lagi
    if (sudahPeringatanLambat && !sudahDirespon && (jam == 22 && menit == 0)) {
      digitalWrite(PIN_LED, HIGH);
      noTone(PIN_BUZZER);
      sudahDirespon = true;
      pemutarAudio.play(4); 
      delay(5000);
    }
  } else {
    digitalWrite(PIN_LED, HIGH);
    noTone(PIN_BUZZER);
  }

  // Tombol ditekan di luar jadwal = salah waktu
  if ((jam < 20 && jam > 21) || sudahDirespon) && digitalRead(PIN_TOMBOL) == LOW) {
    playMelody();
    pemutarAudio.play(1); 
    delay(6000);
    playMelody();
  }

  LowPower.idle(SLEEP_15MS, ADC_OFF, TIMER2_ON, TIMER1_ON, TIMER0_ON, 
                SPI_OFF, USART0_ON, TWI_ON);
}

void playTone(int freq, int dur) {
  tone(PIN_BUZZER, freq, dur);
  delay(dur * 1.2); // jeda antar nada
}

void playMelody() {
  playTone(659, 150); // E5
  playTone(784, 150); // G5
  playTone(880, 150); // A5
  playTone(988, 150); // B5
  playTone(1046, 250); // C6
  playTone(880, 150);  // A5
  playTone(784, 150);  // G5
  playTone(659, 300);  // E5
  noTone(PIN_BUZZER);  // Matikan suara
}

void playMelody2() {
  playTone(523, 120);  // C5
  playTone(659, 120);  // E5
  playTone(784, 120);  // G5
  playTone(988, 180);  // B5
  playTone(784, 100);  // G5
  playTone(1046, 250); // C6
  playTone(784, 100);  // G5
  playTone(880, 300);  // A5
  noTone(PIN_BUZZER);
}
