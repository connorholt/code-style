@todo Идет процесс разработки собственного код стайла, для своих проектов
Добавление к psr2

- БД
- Код. классы
- Код. функции
- Код. переменные
- Код. комментарии

## 1. Работа с БД

<a name="tables-name"></a><a name="1.1"></a>
- [1.1](#tables-name) Имена таблиц во множественном числе, но все модели, контроллеры, называются в единственном. 
    > Зачем? Все логично, если брать пример, в базе хранятся все пользователи, но используя модель или контроллер мы работаем с определенным пользователем, если это конечно не вывод списка. @todo обоснование

    ```php
    // неправильно
    class Users extends Model {
        protected $tableName = 'user';
    }
    // неправильно
    class Users extends Model {
        protected $tableName = 'users';
    }

    // правильно
    class User extends Model {
        protected $tableName = 'users';
    }
    ```
   
   
   <a name="tables-columns-name"></a><a name="1.1"></a>
- [1.2](#tables-columns-name) Названия полей в базе через подчеркивание. Все имена должны быть осмыслены. Нельзя называть поля одинаковыми имена с разными цифрами в окончании abc2 abc3 и т.д.

    ```sql
    # неправильно
    CREATE TABLE users (
        id BIGSERIAL,
        isActive INT(2),
        EmailConfirmed STRING,
        json JSONB
    );

    # правильно
    CREATE TABLE abc (
        id BIGSERIAL,
        is_active INT(2),
        email_confirmed STRING,
        additional_information JSONB
    );
    ```
- Во всех таблицах должно быть поле id. Тип даннных для ID bigserial, serial


- Если сложно образовать название таблицы во множественном числе
- Поля содержащие id на другие таблицы должны именоваться как название сущности в ед числе с окончанием id. Например user_id, category_id
- Поля содержащие даты должны называться с окончанием date, time. Например checkin_date, но если поля относятся не сущности а к физическому состоянию то должны именоваться без указания типа, created_at, created типичные поля должны быть названы одинаково во все таблицах
- Все поля содержащие буленов тип должны научиться с is или has, is_admin, is_deleted
- В названиях не допустимы слова не связанные с сущностью, например ids_array
- Все функции возвращающие булка тип должны быть названы начиная с is или has, запрещается использовать названия в стиле check
- В названии не должно фигурировать имя сущности используемое в имени класса , например правильно: WhiteIpList::has(), не правильно WhiteIpList::hasIp()
- Все функции возвращающие булев тип должны читаться сначала как true, не правильно user::isNotAdmin(), правильно ! User::isAdmin
- Количество if в функции не должно быть больше 3
- Вложенности if не должно быть больше двух
- Кол-во условных функция и циклов должно быть не больше 3, максимум 6, считается по кол-во  открытых фигурных скобок
- Аргументов в функции должно быть строго меньше шести
- Недопустимо использовать else, если есть возможность продолжить код без вложенности
- Исправление одной строки не должно приводить к исправлению других строк
- Все релэйшионы должны называться во множественном числе если связь многие компании многим или один конец многим, иначе в единственном
- Все переменные должны быть и находится рядом с тем местом в котором используются. Не правильно:                              defaultName = 'igor'                                                  // сторонний код
- Использовать скобки для определения приоритетности в выражениях (7 + 8) * 2
- False true всегда писать после =
- При переносе чего либо, незавершенного выражения должна быть очевидна!
- При переносе строк в вызове метода использовать отступ стандартного размера
- Больше 4 параметров в методе должны начинаться каждый с новой строки
- Не выравнивать правы части выражений присваиваивания, если не ассоциативный массив
- Размещение одного оператора на строке
- Стр 743
- Код должен быть узнаваем и читаем в одинаковом смысле стр 763в читалки
- Объявлять переменные рядом с местом их первого использования
- Упорядочить объявления по алфавиту или по длине
- Отделять каждый комментарий хотя бы одной строкой
- Нельзя присваивать в условных операторах
- Порядок методов в классе, данные класса, открытые методы, защищенные методы, закрытые методы
- Стр 782 в читалкн
- Глупые комментарии стр 769
- Не использовать в комментариях *** !!!! Только @todo
- Комментарии в конце строк стр 795 в читалке
- В комментариях должна быть цель
- Описывать хитрости в комментариях используя слово @hack и описание в чем смысл
- Для дат использовать объект datiletime или carbon, если это ларавел
- Не использовать сокращения сущностей, если это не общепринятое сокращение по всей системе в комментариях,  и а названиях функций и переменных. Не правильно bk = {} , если везде мсполуется booking
- Комментировать решения если это обход ошибок языка или фреймворка, обосновывать в комментариях любое отступление от код стайла, используя сначала фразу @todo
- Недлкументировать плохой код переписать его
- Каждый метод должен содержать phpdoc в котором должно быть короткое описание, отвечающая на вопрос какая цель? Должны быть описаны все параметры, и возвращает значение, также дата и автор
- В комментариях должны быть указаны исключегия
- ретурн обязательно что-то возвращает не делать просто return;



---------------


1. внутри if только функциии или две строчки
2. параметров в функции 0-2, не больше
3. нельзя передавать boolean параметры в функцию, это говорит о нарушении солид
4. комментарии загрязняют код, если нужно оставить комментарий, значит названия не передают смысл
5. не нужно в названия использовать data, info и прочее абстрактные слова, когда нет разницы customerData или customerInfo
6. не нужно смешивать в одной функции разные уровни абстракции
7. не нужно в именах использовать отсыл к типу перменной, называть array, object, str, int, bool
8. switch использовать только для полиморфизма и возвращения разныъ объектов
9. четкое соответствие солид принципу
10. порядок атрибутов и констант. сначала const, public, protected, private. функции распологаются так же, под функции по порядку использования в функции
11.всегда должен бвть порядок, если склеивается html, то первым должен находиться заголовок, последник футер и такая логика везде. дана начала всегде раньше даты окончания, и в параметрах функции и в использовании
12.если нужно более трех аргументов, возможно есть смысл передать объект и внести в атрибуты
13. классы называются существительным, функции содержат глагол
14. функция делает только одно действие и имеет только одну причину для изменения
15. единообрезное именование действий, если используется для добавления везде функция append, не надо называть функцию add
16. побочные действия функций, когда они выполняют больше одного действия, но при этом этого нет в именовании
17. изолировать ветвления ошибок с помощью try catch, не делать сравнение с ошибками стр 72
18. Функции должны выполнять одну операцию. Обработка ошибок — это одна
операция. Значит, функция, обрабатывающая ошибки, ничего другого делать не
должна. Отсюда следует, что если в функции присутствует ключевое слово try,
то оно должно быть первым словом в функции, а после блоков catch
ничего другого быть не должно (как в предыдущем примере).
19. DRY не повторяйтесь
20. сначала написать логику, потом ее рефакторить по принципам
21. писать комментарии в phpdoc и только в редких случаях (описать в каких(предупреждение о последствиях)). не писать очевидные комментарии
22. не писать комментарии, там где можно использовать переменную или функцию
23. Форматирование везде одинаковое как в psr
24. Переменные объявлять как можно ближе к месту использования (внутри функции)
25. Переменные класс только в начале класса
26. Если одна функция вызывает другую, то эти функции
должны располагаться вблизи друг от друга по вертикали, а вызывающая 
функция должна находиться над вызываемой (если это возможно). Тем самым 
формируется естественная структура программного кода.
27. кол-во символов в строке 80
28. Исключения вместо кодов с ошибками
29. Возвращать null не правильно, использовать null объект
30. Не передавать null в параметрах функции
31. Классы должны быть компактными, важно не кол-во функций а кол-во ответственности класса.
32. Имя класса должно описывать его ответственности.
33. В частности, присутствие в именах классов слов-
проныр «Processor», «Manager» и «Super» часто свидетельствует о нежелательном
объединении ответственностей.
34. Краткое описание класса должно укладываться примерно в 25 слов, без 
выражений «если», «и», «или» и «но».
35. Принцип единой ответственности (SRP1) утверждает, что класс или модуль
должен иметь одну — и только одну — причину для изменения.
36. Каждый метод класса должен оперировать с одной или несколькими из этих переменных.
37. Классы должны быть открыты для расширений, но закрыты для модификации.
38. Код следует размещать там, где читатель ожидает его увидеть. Константа PI должна находиться там, где 
объявляются тригонометрические функции. Константа OVERTIMERATE объявляется
в классе HourlyPayCalculator.
39. В общем случае отдавайте предпочтение нестатическим методам перед 
статическими. Если сомневаетесь, сделайте функцию нестатической. Если вы твердо 
уверены, что функция должна быть статической, удостоверьтесь в том, что от нее не
потребуется полиморфное поведение.
40. Избегайте отрицательных условий
Отрицательные условия немного сложнее для понимания, чем положительные.
Таким образом, по возможности старайтесь формулировать положительные
условия.
41. Функции должны выполнять одну операцию
42. Выбирайте имена
на подходящем уровне абстракции
