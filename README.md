# Алгоритмы кодирования и сжатия

Здесь представлена реализация некоторых простых алгоритмов кодирования и сжатия в рамках 
курса Компьютерные сети (8 семестр).

### Алгоритмы
1. CRC (_Cyclic Redundancy Code_)
2. Код Хэмминга
3. Код Шеннона-Фано
4. Код Хаффмана 

### Задания

1-2. клиент/сервер, передача сообщения, рандомная ошибка и определение этой ошибки.
3-4. сжатие текста и оценка эффективности сжатия. Сравнить эффективность.


### 1. CRC

Клиент/сервер. Запуск сервера, потом - клиента. На клиенте производится ввод текстового сообщения.
После этого с вероятностью, близкой к 0.5, вносится случайная ошибка. Далее сообщение отправляется на сервер.

На сервере происходит получение сообщения от клиента, его раскодирование CRC. В случае ошибки, сервер запрашивает повторную 
отправку сообщения от клиента. Так происходит, пока сообщение не будет доставлено успешно

##### Пример: 

_client:_
```
Введите сообщение для отправки на сервер: >? Мама мыла раму
Сообщение в двоичном виде:
1101000010011100110100001011000011010000101111001101000010110000001000001101000010111100110100011000101111010000101110111101000010110000001000001101000110000000110100001011000011010000101111001101000110000011
Закодированное сообщение, готовое к отправке:
1101000010011100110100001011000011010000101111001101000010110000001000001101000010111100110100011000101111010000101110111101000010110000001000001101000110000000110100001011000011010000101111001101000110000011011
Внесена ошибка в 167 бите:
1101000010011100110100001011000011010000101111001101000010110000001000001101000010111100110100011000101111010000101110111101000010110000001000001101000110000000110100011011000011010000101111001101000110000011011
Ответ от сервера: Произошла ошибка при отправке!

Попытка повторной отправки...

Сообщение в двоичном виде:
1101000010011100110100001011000011010000101111001101000010110000001000001101000010111100110100011000101111010000101110111101000010110000001000001101000110000000110100001011000011010000101111001101000110000011
Закодированное сообщение, готовое к отправке:
1101000010011100110100001011000011010000101111001101000010110000001000001101000010111100110100011000101111010000101110111101000010110000001000001101000110000000110100001011000011010000101111001101000110000011011
Ответ от сервера: Сообщение успешно доставлено!

Введите сообщение для отправки на сервер: >?

...
```

_server:_
```
Подключено: ('127.0.0.1', 54138)
Полученные данные: 1101000010011100110100001011000011010000101111001101000010110000001000001101000010111100110100011000101111010000101110111101000010110000001000001101000110000000110100011011000011010000101111001101000110000011011
При отправке произошла ошибка. Отправляю запрос на переотправку...
Полученные данные: 1101000010011100110100001011000011010000101111001101000010110000001000001101000010111100110100011000101111010000101110111101000010110000001000001101000110000000110100001011000011010000101111001101000110000011011
Получено сообщение: Мама мыла раму

...
```
