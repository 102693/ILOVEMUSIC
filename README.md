# ILOVEMUSIC

Что нужно
Arduino Nano
Micro SD Card Module (SPI)
microSD карта в FAT32
датчик DS18B20
резистор 4.7 кОм
кнопка
усилитель TPA3118
динамик



9. Краткая распиновка
D2 → кнопка
D4 → DS18B20 DATA
D9 → звук на усилитель
D10 → SD CS
D11 → SD MOSI
D12 → SD MISO
D13 → SD SCK



2. Что должно лежать на SD карте

Формат карты: FAT32

Файл музыки:

sound.wav

Файл с логом температуры:

temp.csv

temp.csv может создаться сам после запуска.

3. Подключение к Arduino Nano
3.1. SD модуль

Подключение по SPI:

VCC → 5V Arduino
GND → GND Arduino
CS → D10 Arduino
MOSI → D11 Arduino
MISO → D12 Arduino
SCK → D13 Arduino

Вставь microSD карту в модуль.

3.2. Датчик температуры DS18B20
VCC → 5V Arduino
GND → GND Arduino
DATA → D4 Arduino

Резистор 4.7 кОм поставить между DATA и 5V.

3.3. Кнопка
один контакт → D2 Arduino
второй контакт → GND Arduino

В коде используется INPUT_PULLUP, поэтому отдельный резистор не нужен.

3.4. Выход звука на усилитель TPA3118
D9 Arduino → AUDIO IN усилителя
GND Arduino → GND усилителя

Питание усилителя:

VIN+ → плюс питания
VIN− → минус питания
3.5. Динамик
выход усилителя OUT+ → динамик
выход усилителя OUT− → динамик
4. Питание

Если используешь DC-DC:

вход DC-DC → аккумулятор
выход DC-DC → 5V для Arduino и SD модуля

Усилитель TPA3118 можно питать отдельно, если ему нужно другое напряжение.

5. Как это работает
Нажимаешь кнопку
Arduino запускает sound.wav
Каждые 10 секунд Arduino:
читает температуру с DS18B20
дописывает строку в temp.csv
В конце получаешь файл для графика
6. Структура файла лога

Пример temp.csv:

time_s,temp_c
0,23.50
10,23.62
20,23.71
30,23.80

7. Библиотеки

В Arduino IDE нужно установить:

TMRpcm
OneWire
DallasTemperature
SD
SPI


8. Важные замечания
sound.wav должен быть WAV PCM, лучше моно
карта должна быть FAT32
если звук не стартует, проверь:
имя файла
формат WAV
питание SD модуля
общий GND у всех модулей
