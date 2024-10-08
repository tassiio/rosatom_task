# **Тестовое задание на стажерскую позицию системного аналитика в Гринатом**

### Для информационной системы необходимо разработать форму ввода сведений о физическом лице. Интерфейс формы должен позволять вводить ФИО физического лица и его ИНН. Известно, что существует алгоритм проверки правильности ввода ИНН путём расчёта контрольной суммы.

Задание №1. _Необходимо описать таблицу хранения данных:_
   - _атрибутный состав;_
   - _тип атрибутов;_
        + _Какой тип данных для хранения ИНН и почему?_
        + _Можно ли использовать ИНН в качестве первичного ключа? Плюсы и минусы использования._
   - _описать первичный ключ таблицы, варианты типов данных для первичного ключа._

Решение задания №1.

#### Атрибутный состав:
   - id — первичный ключ; 
   - last_name — фамилия;
   - first_name — имя;
   - middle_name — отчество (может быть NULL, если у человека нет отчества);
   - inn — ИНН физического лица.

#### Типы атрибутов:

   - id — целочисленный тип (INTEGER или BIGINT);
   - last_name — строковый тип (VARCHAR(100));
   - first_name — строковый тип (VARCHAR(100));
   - middle_name — строковый тип (VARCHAR(100)), допускающий NULL;
   - inn — строковый тип (VARCHAR(12)).

Использование строкового типа данных для ИНН обусловлено следующими причинами:
- нули в начале: ИНН может начинаться с нуля. Если использовать числовой тип данных, ведущие нули будут автоматически отбрасываться (ИНН "0123456789" при хранении в числовом формате станет "123456789", что нарушит его корректность). Но нужно учитывать тот факт, что __двух нулей__ в начале ИНН быть не может;
- ИНН — это не число в математическом смысле: ИНН используется для идентификации пользователя, не участвует в арифметических операциях. Хранение его как строки позволяет избежать ошибок, связанных с его интерпретацией как числа;
- длина ИНН фиксирована: ИНН физического или самозанятого лица в России состоит из 12 цифр, а юридического — из 10 цифр. Хранение ИНН как строки с заданной длиной позволяет более точно контролировать ввод, проверяя, что пользователь ввёл необходимое количество символов.
Таким образом, использование строкового типа данных позволяет сохранить ИНН в точности таким, каким он был введён.

__Плюсы использования ИНН в качестве первичного ключа:__
+ ИНН уникален для каждого физического лица, что делает его подходящим кандидатом для уникальной идентификации.
  
__Минусы использования ИНН в качестве первичного ключа:__
+ ИНН может меняться, что недопустимо для первичного ключа, который должен быть стабильным;
+ хранение первичного ключа в виде длинного строкового значения может отрицательно сказаться на производительности базы данных.
  
_Заключение:_ лучше использовать отдельный целочисленный идентификатор (id) в качестве первичного ключа.

Первичный ключ — это __уникальный__ идентификатор записи в таблице базы данных. Поэтому он должен гарантировать, что каждая строка/запись в таблице может быть однозначно идентифицирована.

Наиболее часто встречаемые и используемые варианты PK:

### 1. Автоинкрементируемый числовой ключ (автоматически увеличивающийся числовой идентификатор, генерируемый при добавлении новой записи).

Тип данных такого ключа может быть INT (целочисленный тип данных, который подходит для таблиц с небольшим количеством записей) или BIGINT (расширенный целочисленный тип данных для таблиц с большим количеством записей).

Плюсы:
- такой ключ легок в создании и управлении;
- высокая производительность поиска.
- хорошо подходит для задач, в которых данные могут претерпевать изменения.

Однако есть существенные минусы:
- при удалении данных потребуется время на пересчёт и восстановление последовательности;
- отсутствие логической связи между ключом и сущностью.

Для создания такого типа ключа в SQL необходимо прописать команду:
```SQL
id INT AUTO_INCREMENT PRIMARY KEY
```
### 2. Уникальный идентификатор на основе UUID (специальный тип данных для хранения 128-битных значений).

В PostgreSQL существует встроенный тип данных для UUID, а в MySQL можно использовать строковый тип, который будет хранить UUID в текстовом формате.

Плюсы:
- гарантированная уникальность не только внутри одной таблицы, но и между разными системами;
- возможность генерации ключа на стороне клиента.

Минусы:
- замедленная производительность при поиске и индексировании по сравнению с числовыми ключами;
- большой размер ключа (16 байт против 8 байт у BIGINT).

```SQL
id UUID PRIMARY KEY
```
### 3. Составной (комбинированный) ключ

Составной ключ — это первичный ключ, который состоит из двух или более атрибутов. Значения атрибутов в комбинации должны быть уникальными для каждой записи.

Плюсы:
- поддерживает логическую связь между ключевыми атрибутами сущности;
- уникален.
 
Минусы:
- усложняет структуру запросов и индексацию, а следовательно и замедляет производительность;
- затруднен процесс изменения атрибута, входящего в составной ключ.

На примере тех атрибутов, что были представлены в списке, составной ключ в SQL можно создать следующим образом:
```SQL
PRIMARY KEY (last_name, inn)
```

Задание №2. _Предложить варианты реализации проверки правильности ввода ИНН._
   - _на стороне frontend;_
   - _на стороне backend;_
   - _объяснить плюсы и минусы реализации проверки на стороне frontend и backend, описать взаимодействие frontend и backend._

Решение задания №2.

- Frontend ("клиентская" часть приложения, которая взаимодействует напрямую с пользователем):
   + проверка длины ИНН (10 или 12 символов) с помощью JavaScript;
   + ИНН должен состоять только из цифр. Можно проверить, что все символы являются числовыми;
   + ИНН включает контрольные цифры, которые вычисляются по специальному алгоритму. Реализовав алгоритм на JavaScript, можно проверять правильность контрольной суммы до отправки данных на сервер.
   + плюсы: быстрый отклик для пользователя, снижение нагрузки на сервер (если ошибки есть на клиентской стороне, сервер не перегружается ненужными запросами);
   + минусы: уязвимость к манипуляциям с JavaScript и возможность отключить его в браузере.
- Backend (серверная часть приложения, которая отвечает за обработку данных и взаимодействие с базой данных):
  + проверка длины ИНН (10 или 12 символов) и проверка контрольной суммы с помощью языков программирования backend;
  + ИНН должен состоять только из цифр. Можно проверить, что все символы являются числовыми, на сервере, а не на клиенте;
   + ИНН включает контрольные цифры, которые вычисляются по специальному алгоритму, который можно реализовать на языке программирования бэкенда;
   + плюсы: проверка выполняется на сервере, что делает её недоступной для манипуляций со стороны пользователя (это безопаснее), а также универсальность (проверка происходит на сервере, поэтому без разницы, какой браузер у пользователя).
   + минусы: нужно ждать ответа от сервера после отправки данных в течение какого-то промежутка времени, повышенная нагрузка на сервер.
     
__Промежуточный вывод__: лучше использовать комбинацию frontend и backend. При этом на стороне пользователя (фронт) будут выполняться базовые проверки на соответствие длины, формата ИНН, а также проверка контрольной суммы (и в случае ошибки данные не будут грузить сервер, время не будет потрачено), а на стороне сервера (бэк) — дополнительные проверки, которые предотвратят попытки злоумышленников, например, подделать ИНН или обойти алгоритмы фронтенда. 

Тогда можно описать взаимодействие фронта и бэка в виде последовательности действий:
1. Ввод ИНН на сайте.
2. На стороне frontend происходит базовая проверка, и в случае некорректных данных они не отправляются на сервер, а пользователь видит уведомление об ошибке сразу, без задержки по времени.
3. Если со стороны фронтенда все хорошо, то данные отправляются на сервер на бэк, где подвергаются дополнительным проверкам.
4. Результат проверки на бэке приходит на фронт, и пользователь видит итог ввода (наличие/отсутствие ошибок).

Задание №3. _Что такое функциональные и нефункциональные требования? Приведите пример в контексте текущей задачи. Проверка правильности ввода ИНН — это функциональное или нефункциональное требование?_

Решение задания №3.

__Функциональные требования__ — это требования к системе, программному обеспечению, вычислительному кластеру и т.д. (или к тому, кто их разрабатывает), которые содержат в себе описание поведения системы, выполняемых ею функций. Простыми словами, это список того, что система должна делать.

__Нефункциональные требования__, в свою очередь, описывают не действия, а способ осуществления этих действий. Опираясь на эти требования, можно провести оценку качества работы системы. 

То есть, если первые отвечали на вопрос "что система должна делать?", или "какие у системы функции?", то вторые отвечают на вопросы "как это должно быть сделано?" и "как это должно работать?".

Вообразим, что мы участвуем в разработке системы для проверки ИНН. Тогда список _функциональынх требований_ выглядел бы примерно так:
   
   система должна:
   - __предоставлять__ пользователю __возможность ввести__ свои данные;
   - __проверять__ корректность введеных данных (т.е. проверка ИНН — функциональное требование);
   - __хранить__ введенные данные при необходимости.
    
Это некоторые функции той системы, которую мы хотим разработать.

Теперь приведем список _нефункциональных требований_, или характеристик системы:
   - хорошая __производительность__;
   - __удобство использования__ и __понятный интерфейс__;
   - __безопасность__;
   - способность выдерживать большие нагрузки на сервер (__устойчивость__).

Это лишь некоторые из нефункциональных требований, которые можно предъявить к нашей системе. 
