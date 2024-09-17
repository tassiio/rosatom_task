# **Тестовое задание на стажерскую позицию системного аналитика в Гринатом**


### Для информационной системы необходимо разработать форму ввода сведений о физическом лице. Интерфейс формы должен позволять вводить ФИО физического лица и его ИНН. Известно, что существует алгоритм проверки правильности ввода ИНН путём расчёта контрольной суммы.

### 1. _Необходимо описать таблицу хранения данных:_
1.1 _атрибутный состав_
#### 1.2 _тип атрибутов_
#### 1.2.1 _Какой тип данных для хранения ИНН и почему?_
#### 1.2.2 _Можно ли использовать ИНН в качестве первичного ключа? Плюсы и минусы использования._

Были даны некоторые рекомендации, позволяющие пользователю сделать первые шаги в освоении игры на гитаре.
Я решила оформить инструкцию как приложение к рекламному буклету некоторой условной музыкальной школы "TRIAD". 
Файл можно просмотреть по [ссылке](https://my.visme.co/view/mx8dk3zw-e0654p9dxz0y5np9).

### 2. _Можете дополнить первое задание схемой взаимодействия компонентов._
Для выполнения данного задания я изучила базовые понятия UML, с помощью которого решила создать простейшую схему взаимодействия (см. файл diagram.puml).

![Схема взаимодействия компонентов](https://github.com/tassiio/ozon_task/blob/main/pict/scheme.svg)

### 3. _Выберите любую статью из любого нашего документа и дайте ей обратную связь: вычитайте статью, укажите на слабые места, предложите исправления._

Выбранная статья: ["Мошенничество в интернете"](https://docs.ozon.ru/common/my-settings/bezopasnost/moshennichestvo-v-internete/?country=RU)

1. __"Обратите внимание, Ozon не рассылает сообщения на мессенджеры Viber или WhatsApp."__
    - В данном предложении необходимо либо двоеточие вместо запятой, либо "что" после запятой. 
    - На мой взгляд, уточнение о конкретных мессенджерах (Viber, WhatsApp) лишнее, так как мошенники могут использовать любую платформу (Telegram, VK и т.д.).
    - Не встречала форму "рассылать на мессенджеры", использовала бы вместо "на" предлог _"в"_. 

2. Рассмотрим подраздел __"Как распознать фишинг"__:
   - "в сообщении" я бы заменила на _"в тексте сообщения"_;
   - "Используют эмоции, например, пугают, что ваша учётная запись взломана или пароль украден, и сразу предлагают ссылку для его смены." Данное предложение я переписала бы следующим образом: _"Используют психологические приёмы, к примеру, пугают вас взломом учётной записи, кражей пароля или, наоборот, обещают крупную денежную сумму и другие призы за переход по ссылке или ввод персональных данных"_.
    - "Предлагают большие скидки при оплате не на официальном сайте." Замена конструкции "не на официальном сайте" на _"через неофициальный сайт"_ или _"на неоригинальном сайте"_.

Далее для удобства буду приводить только отредактированный вариант предложений и комментарии. Курсивом буду обозначать места, где были внесены изменения. 

3. Рассмотрим подраздел __"Схема мошенничества с помощью мобильного телефона"__:
    - "Вредоносное программное обеспечение (вирус) _может заразить_ мобильное устройство через _сайт-ловушку (фишинговый сайт)_. При попытке открыть с мобильного устройства _веб-страницу_ организации _или её подразделения_ вирус перенаправляет вас на специальный сайт-ловушку, имитирующий _оригинальный сайт любого из проектов Ozon_". (внесла исправления в связи с частым повторением слова "сайт")
    - "Для проверки _информации, предоставленной в письме,_ обратитесь в службу поддержки _(добавить электронный адрес поддержки)_, где подтвердят или опровергнут полученное вами сообщение."
  
4. Рассмотрим раздел __"Телефонное мошенничество"__:
    - "Например, это звонки ~~от~~ злоумышленников от имени банка с просьбой предоставить номер _и иные данные карты или счета_. "
    - _"Мошенники могут запугивать вас, сообщая о попытке кражи ваших денег со счета. Затем они могут предложить несколько вариантов для обеспечения защиты средств, например:..."_


### 4. Если вы хотели бы работать с документацией на английском языке, опишите, пожалуйста, любой экран мобильного приложения Ozon на английском языке.

Я выбрала раздел "Личный кабинет" для описания. Оригинальный скриншот находится в папке ./pics/screen.jpg. Полный текст можете проверить под изображением.

![Screen_and_text](https://github.com/tassiio/ozon_task/blob/main/pict/4.jpg)

### Text:

Let's take a look at the "My Account" tab in the Ozon mobile app.
At the top we see the search bar, which allows the user to search for the product of interest on the marketplace. In the upper right corner there is a chat symbol with the number of unread messages from stores and different Ozon services.
Next, there is a field containing the first name and the surname of the account owner. Clicking on this field will open a page containing the user's personal data.
Below are three equally sized fields. The first of them shows a heart. Here you can find the user's favorite products. The next field with the shopping cart is a list of all purchases made by the user. In the last section with the symbol "Б" you can find all products purchased by the user, for the evaluation of which you can get sellers' bonus points.
If you click on the box with the gift, you can find out about prize drawings held by Ozone.
Next, we see two fields that are the same width. The first one shows the number of bonus points received for purchases. The second field contains information about the installments that Ozon can offer to its customers.
The marketplace has its own Ozon Bank. Each user can get a virtual Ozon card and pay for purchases in the app and on the website with a certain discount. The card can be topped up through the SQP system. So, the next field displays the number of rubles on the Ozon card. The blue button is used to top up the card.
The last large section on this screen displays items that have been recently viewed by the user. By clicking on the hearts in the right corner of each product card you can add it to your favorites.
