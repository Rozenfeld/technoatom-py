Репозиторий для домашних работ по факультативу "Программирование на Python"
=========================
Используемая версия Python: 3.5.2

Домашняя работа №1
---------------------------------
> Разработать класс Charge (денежная транзакция):
>
> - содержащий вычисляемый атрибут value - вещественное число, определяющее сумму денежной транзакции;
> - содержащий метод инициализации.
>
> После инициализации экземпляра класса, значение value изменять нельзя. Отрицательные значения соответствуют расходам, положительные - зачислениям на счет. Несмотря на реальные значения суммы транзакции, вычисляемые атрибут value не должен отдавать значения больше чем с двумя знаками после запятой. Используйте функцию round и либо декоратор, либо дескриптор на свое усмотрение.
>
> Разработать класс Account (банковский счет):
> - содержащий атрибут charges - список, определяющий последовательность денежных транзакций по счету;
> - содержащий атрибут total - вещественное число, определяющее текущее состояние счета;
> - содержащий метод инициализации;
> - содержащий методы добавления транзакций (приход и расход соответственно).
>
> Каждый элемент списка charges - экземпляр класса Charge. При инициализации экземпляра класса возможно задать начальное значение для состояния счета, по умолчанию - ноль. Атрибут total должен обновляться при вызове методов зачисления и списания, отрицательное значение атрибута невозможно.
>
> Дополнительно:
>
> Класс Account должен быть итерабелен (отдавать charges).

[Решение ДЗ №1](./hw_1/)

Домашняя работа №2
---------------------------------
> Определен следующий бесконечный генератор:
```python
from random import randint
from time import sleep
def events(max_delay, limit):
    while True:
        delay = randint(1, max_delay)
        if delay >= limit:
            sleep(limit)
            yield None
        else:
            sleep(delay)
            yield 'Event generated, awaiting %d s' % delay
```

>
>Генератор симулирует поступление событий в систему, на вход он получает максимальную задержку генерации max_delay для псевдослучайного времени ожидания и лимит времени ожидания. Если время ожидания превышает заданный лимит - генератор вернет значение None, что будет означать, что событий за интервал ожидания не произошло.
>
>Необходимо проинициализировать генератор (с произвольными параметрами) в глобальную переменную и определить класс WSGI-приложения, возвращающий события генератора. При этом в случае успеха (генератор вернул не None) приложение должно возвращать стутус 200 OK и строковое представление события, а в противном случае статус 204 No Content без тела сообщения.

[Решение ДЗ №2](./hw_2/)

Домашняя работа №3
---------------------------------
> Создать django-проект myfinance и django-приложение finance.
> Опеределить два маршрута:
> * Главная страница (корень r'^$')
> * Выписка по счету (например, r'^/charges/$')
>
> Главная страница должна содержать приветствие и ссылку на страницу выписки по счету.
> Страница выписки по счету должна содержать произвольную таблицу и ссылку на главную страницу.

[Решение ДЗ №3](./hw_3/)

Домашняя работа №4
---------------------------------
> Задана сущность Charge (денежная транзакция) содержащая поля: value - вещественное число (decimal.Decimal), сумма транзакции (может быть отрицательным или положительным); date - дата (datetime.date), день проведения транзакции. Необходимо разработать представление и форму для сущности Charge и реализовать необходимые проверки, при этом транзакции-списания (с отрицательным значением) не могут быть заведены на будущее (дата date в таких транзакциях должна быть меньше или равна сегодняшнему дню из date.today). В случае успеха или неудачи (определяемым по корректности заполнения формы) нужно выводить соответствующие сообщения.
>
> Задан генератор (источник данных), возвращающий случайное количество пар (date, value) для транзакций:
```python
from datetime import date
from decimal import Decimal
from random import randint
def random_transactions( ):
  today = date.today( )
  start_date = today.replace(month=1, day=1).toordinal()
  end_date = today.toordinal()
  while True:
    start_date = randint(start_date, end_date)
    random_date = date.fromordinal(start_date)
    if random_date >= today:
      break
    random_value = randint(-10000, 10000), randint(0, 99)
    random_value = Decimal('%d.%d' % random_value)
    yield random_date, random_value
```

> Необходимо разработать представление, которое будет получать от генератора список транзакций и выводить их на страницу (для этого следует использовать шаблоны). При этом транзакции-списания (с отрицательным занчением value) и транзакции-зачисления (с положительным значением value) должны выводиться в разные списки на странице (можно использовать для верстки html-списки или таблицы).

[Решение ДЗ №4 - продолжение ДЗ №3](./hw_3/)

Домашняя работа №5
---------------------------------
> Создать модели Account и Charge (аналогичные сущностям, используемым в предыдущих домашних заданиях), учесть что Account относится к Charge как один-ко-многим. Создать формы для этих моделей, используя Django Model Forms.
>
> Реализовать представления
> - Создание банковского счета
> - Просмотр банковского счета, содержащее:
> -- кнопку "Добавить приход/расход"
> -- списки транзакций по счету "Приход"/"Расход"
> - Создание транзакции с привязкой с счету (ссылок на счет не должно быть на форме)

[Решение ДЗ №5](./hw_5/)

Домашняя работа №6
---------------------------------
> Если это необходимо - использовать транзакции СУБД при изменении баланса счета и создании списания/зачисления на счет. Добавить в приложение представление статистики, где выводить изменения баланса в сумме по месяцам.

[Решение ДЗ №6 - продолжение дз №5](./hw_5/)