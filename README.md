Горчаков Роман Владимирович. Вариант 4
# Лабораторная работа 2.21. Взаимодействие с базами данных SQLite3 с помощью языка программирования Python.

Сами по себе СУБД редко используются для работы с базами данных. В том смысле, что в реальных проектах связки БД + СУБД бывает недостаточно. Обычно с СУБД работают через какой-либо язык программирования. Это позволяет более гибко принимать запросы, обрабатывать ответы перед передачей их куда-либо далее. Ведь у императивного, а не декларативного как SQL, языка программирования средств для работы с данными больше, да и логика богаче.
 
Чтобы использовать SQLite3 в Python, прежде всего, вам нужно будет импортировать модуль sqlite3, а затем создать объект соединения, который соединит нас с базой данных и позволит нам выполнять операторы SQL. Объект соединения создается с помощью функции connect(). Будет создан новый файл под названием "mydatabase.db", в котором будет храниться наша база.
данных.

Для взаимодействия с базой данных SQLite3 в Python необходимо создать объект cursor. Вы можете создать его с помощью метода cursor(). Курсор SQLite3 – это метод объекта соединения. Для выполнения инструкций SQLite3 сначала устанавливается соединение, а затем создается объект курсора с использованием объекта соединения следующим образом. При создании соединения с SQLite3 автоматически создается файл базы данных, если он еще не существует. Этот файл базы данных создается на диске, мы также можем создать базу данных в оперативной памяти с помощью функции :memory: with the connect. Такая база данных называется базой данных в памяти.

Сначала импортируется модуль sqlite3, а затем определяется функция с именем sql_connection. Внутри функции у нас есть блок try, где функция connect() возвращает объект соединения после установления соединения. В случае возникновения ошибок при установке соединения с базой данных выполняются операторы блока except , в котором в данном случае просто печатается содержимое объекта ошибки.

Для создания таблицы в SQLite3 можно использовать запрос CREATE TABLE в методе execute(). Таким образом для создания таблицы в базе данных SQLit3 необходимо выполнить следующую последовательность шагов:
1. Создать объект соединения.
2. Создать объект курсора с помощью объекта соединения.
3. Используя метод execute объекта cursor выполнить запрос CREATE TABLE.

Чтобы проверить, создана ли наша таблица, вы можете использовать браузер DB для sqlite; для просмотра вашей таблицы. Откройте файл mydatabase.db с помощью программы, и вы увидите свою таблицу. SQL-команды выполняются с помощью метода execute() и некоторых других. Если запрос длинный, и его удобно разбить на несколько строк, используют тройные кавычки.

Обратим внимание, что в конце SQL-запросов здесь точка с запитой не ставятся. Также метод возвращает сам объект. Заполнять таблицы можно тоже с помощью execute(). Однако, если требуется вставить несколько записей, лучше воспользоваться методом executemany(). Мы создаем список из кортежей. Каждый кортеж – это отдельная запись таблицы. Метод executemany() выполняет SQL-команду по отношению к каждому элементу списка. При этом данные из кортежа подставляются вместо знаков вопроса. Такая подстановка работает и через execute().

Есть еще метод executescript(). В качестве аргумента передается скрипт на языке SQL, который может включать несколько запросов, каждый из которых заканчивается точкой с запятой. У объекта-курсора есть методы fetchone(), fetchmany() и fetchall(), которые позволяют извлекать из него данные, если sql-запрос предполагал их передачу. По сути, они наделяют курсор свойствами объекта-итератора (такой имеет метод next()).

Чтобы вставить данные в таблицу, используется оператор INSERT INTO. Мы также можем передавать значения/аргументы оператору INSERT в методе execute (). Вы можете использовать знак вопроса (?) в качестве заполнителя для каждого значения.

Чтобы обновить данные в таблице, просто создайте соединение, затем создайте объект курсора с помощью соединения и, наконец, используйте оператор UPDATE в методе execute (). Оператор SELECT используется для выбора данных из определенной таблицы. Если вы хотите выбрать все столбцы данных из таблицы, вы можете использовать звездочку (*).

В SQLite3 оператор SELECT выполняется в методе execute объекта cursor. Чтобы извлечь данные из базы данных, мы выполним оператор SELECT, а затем используем метод fetchall() объекта cursor для хранения значений в переменной. После этого мы пройдем по циклу через переменную и выведем все значения. Если вы хотите получить определенные данные из базы данных, вы можете использовать предложение WHERE.

SQLite3 rowcount используется для возврата количества строк, которые были затронуты или выбраны последним выполненным SQL-запросом. Когда мы используем rowcount с оператором SELECT, будет возвращено значение -1, поскольку количество выбранных строк неизвестно до тех пор, пока все они не будут извлечены. Когда оператор DELETE используется без какого-либо условия (предложение WHERE), все строки в таблице будут удалены, а общее количество удаленных строк будет возвращено с помощью rowcount.

Чтобы перечислить все таблицы в базе данных SQLite3, вы должны запросить данные из таблицы sqlite_master, а затем использовать fetchall() для получения результатов из инструкции SELECT. sqlite_master – это главная таблица в SQLite3, которая хранит все таблицы. При создании таблицы мы должны убедиться, что она еще не существует. Аналогично, при
удалении/удалении таблицы она должна существовать.

Метод executemany можно использовать для вставки нескольких строк одновременно. В базе данных Python SQLite3 мы можем легко хранить дату или время, импортируя модуль datetime.
