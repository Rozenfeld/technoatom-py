h1 Домашняя работа №2
========================
* Первый способ:
1. Введите требуемые значения url и port в файле [config.conf](./config.conf)
2. Запустите скрипт
```bash
python wsgi.py
```
3. Откройте браузер и введите в адресный строке localhost:port/ в соответствии с данными из [config.conf](./config.conf)
***
* Второй способ:
***
Потребуется сторонняя библиотека requests. Для ее установки воспользуйтесь менеджером пакета pip:
```bash
pip install requests
```
1. Введите требуемые значения url и port в файле [config.conf](./config.conf)
2. Запустите скрипт
```bash
python wsgi.py
```
3. Запустите скрипт
```bash
python test.py
```