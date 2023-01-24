# Домашнее задание к занятию "`Базы данных`" - `Никулин Михаил Сергеевич`



---

### Задание 1

`Базу данных можно разбить на 8 таблиц:`

1. employee
2. employee_position
3. division_type
4. division
5. division_address
6. region
7. city
8. project

---

`Состав и типы данных в этих таблицах следующие:`

employee (

employee_id, первичный ключ, serial,

name, varchar(50),

salary, money,

position_id, внешний ключ, integer,

division_type_id, внешний ключ, integer,

division_id, внешний ключ, integer,

hire_date, datetime,

division_address_id, внешний ключ, integer,

project_id, внешний ключ, integer

)

---

employee_position (

position_id, первичный ключ, serial,

position, varchar(50)

)

---

division_type (

division_type_id, первичный ключ, serial,

name, varchar(50)

)

---

division (

division_id, первичный ключ, serial,

name, varchar(50),

division_type_id, внешний ключ, integer,

division_address_id, внешний ключ, integer,

)

---

division_address (

division_address_id, первичный ключ, serial,

region_id, внешний ключ, integer,

city_id, внешний ключ, integer,

address, varchar(50)

)

---

region (

region_id, первичный ключ, serial,

name, varchar(50)

)

---

city (

city_id, первичный ключ, serial,

name, varchar(50)

)

---

project (

project_id, первичный ключ, serial,

name, varchar(50)

)

---


## Дополнительные задания (со звездочкой*)


### Задание 2*

`Столбцы таблицы имеют следующие функциональные зависимости:`

* `ФИО сотрудника в данной таблице не повторяется и напрашивается вывод, что данный столбец является основным, от которого
следует начинать нормализацию. К нему слудует привязать новый столбец employee_id, который будет уникальным ключем для связи с другими таблицами.
Связь у нового столбца будет один-к-одному для столбцов ФИО, Оклад, Дата найма (Оклад и Дата найма оставляем без выделения в отдельную таблицу, 
т.к. в них нет повторений, таким образом одному значению столбца employee_id соответствует одно значение столбцов Оклад и Дата найма). Дальнейшее 
увеличение штата сотрудников маловероятно приведет к появлению повторений в данных столбцах, т.к.согласно таблице Оклад сотрудника жестко не 
привязан к другим данным и варьируется в определенном пределе. Так же Дата найма имеет свойство всегда увеличиваться и создавать для нее 
отдельную таблицу с первичным ключем неуелесообразно из-за большого кол-ва неповторяющихся данных`
* `Связи со столбцами Должность, Тип подразделения, Структурное подразделение, Адрес филиала - один-ко-многим, т.к. 
множество сотрудников может занимать только одну должность, работать в одном отделе и по одному адресу. Таким образом для 
нормализации принято решение выделить данные столбцы в отдельные таблицы: employee_position, division, division_type, division_address`
* `Связь со столбцом Проект в текущей таблице - один-ко-многим. В ней каждый сотрудник занят только над одним проектом, но над 
одним проектом работает несколько сотрудников, поэтому таннный столбец выделен в отдельную таблицу project. В дальнейшем скорее 
всего имеет смысл связать данные таблицы по схеме многие-ко-многим и построить связь через дополнительную таблицу, на текущем этапе это излишне`
* `Если присмотреться к столбцу Адрес филиала, то можно обратить внимание на повторяющиеся наименования Регионов, Городов и Адресов. 
Здесь также присутствует связь один-ко-многим. Для органицации связи и избавления от повторений столбец адрес вынесен в отдельную 
таблицу division_address и разбит на 2 дополнительные таблицы region и  city`


