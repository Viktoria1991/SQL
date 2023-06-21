Выведите поля member_id, member_name и status из таблицы FamilyMembers.
SELECT member_id, member_name, status FROM FamilyMembers 

Выведите поле name из таблицы Passenger. При выводе данного поля используйте псевдоним "passengerName"
SELECT name AS  "passengerName" FROM Passenger

Выведите все столбцы из таблицы Payments.
SELECT * FROM Payments

Выведите только уникальные имена first_name студентов из таблицы Student.
SELECT DISTINCT first_name FROM Student

Выведите только уникальные пары значений идентификатор учителя teacher и идентификатор предмета subject из таблицы Schedule.
SELECT DISTINCT teacher, subject FROM Schedule

Выведите только уникальные имена first_name студентов из таблицы Student.
SELECT DISTINCT first_name FROM Student

Выведите идентификаторы товаров (поле good) из таблицы Payments, стоимость которых больше 2000 единиц. Стоимость товара хранится в поле unit_price.
SELECT good FROM Payments
WHERE unit_price >2000

Выведите имена (поле member_name) членов семьи из таблицы FamilyMembers, чей статус (поле status) равен "father".
SELECT member_name FROM FamilyMembers
WHERE status = 'father'

Выведите имя (поле member_name) и дату рождения (поле birthday) членов семьи из таблицы FamilyMembers, чей статус (поле status) равен "father" или "mother".
SELECT member_name , birthday FROM FamilyMembers
WHERE status = 'father' OR status = 'mother'

Необходимо получить все комнаты, в которых есть как кухня (поле has_kitchen), так и интернет (поле has_internet). Напишите запрос, удовлетворяющий вышеописанному условию, который выводит все поля из таблицы Rooms.
Наличие обозначается 1 или true, а отсутствие 0 или false.
SELECT* FROM Rooms
WHERE has_kitchen = 1 AND has_internet = 1

Выведите имена first_name и фамилии last_name студентов из таблицы Student, у кого отсутствует отчество middle_name
SELECT first_name , last_name  FROM Student
WHERE middle_name IS NULL

Выведите резервации комнат (поля room_id, start_date, end_date) из таблицы Reservations, у которых итоговая стоимость аренды (поле total) находится в промежутке от 500 до 1200 включительно.
SELECT room_id, start_date, end_date FROM Reservations
WHERE total BETWEEN 500 AND 1200

Выведите всех членов семьи с фамилией "Quincey".
SELECT member_name 
FROM FamilyMembers
WHERE member_name LIKE '%Quincey'

Для каждого отдельного платежа выведите идентификатор товара и сумму, потраченную на него, в отсортированном по убыванию этой суммы виде. Список платежей находится в таблице Payments.
Для вывода суммы используйте псевдоним sum.
select good, amount * unit_price as sum from payments 
order by sum desc

Выведите список членов семьи с фамилией Quincey, в отсортированном по возрастанию столбцам status и member_name виде.
SELECT * FROM FamilyMembers
WHERE member_name LIKE '%Quincey'
ORDER BY status , member_name ASC

Подсчитайте количество учеников в каждом классе, а также отсортируйте их по убыванию количества учеников. Принадлежность ученика к конкретному классу вы можете получить из таблицы Student_in_class. В качестве результата необходимо вывести идентификатор класса (поле class) и количество учеников в этом классе.
Для вывода количества учеников используйте псевдоним count.
SELECT class, COUNT (student)  AS count FROM Student_in_class GROUP BY class  ORDER BY count DESC

Для каждого из существующих статусов (поле status) найдите самого старого человека (используйте поле birthday). Выведите статус и дату рождения.
Для вывода даты рождения используйте псевдоним birthday.
SELECT status, MIN (birthday) AS Birthday FROM FamilyMembers
GROUP BY status 

Объедините таблицы Class и Student_in_class с помощью внутреннего соединения по полям Class.id и Student_in_class.class. Выведите название класса (поле Class.name) и идентификатор ученика (поле Student_in_class.student).
SELECT name, student FROM Student_in_class
JOIN Class ON Student_in_class.class=Class.id

Дополните запрос из предыдущего задания, добавив ещё одно внутреннее соединение с таблицей Student. Объедините по полям Student_in_class.student и Student.id и вместо идентификатора ученика выведите его имя (поле first_name).
SELECT name, first_name FROM  Class
JOIN Student_in_class ON Class.id = Student_in_class.class
JOIN Student ON Student_in_class.student  = Student.id

Выведите названия продуктов, которые покупал член семьи со статусом "son". Для получения выборки вам нужно объединить таблицу Payments с таблицей FamilyMembers по полям family_member и member_id, а также с таблицей Goods по полям good и good_id.
SELECT good_name FROM Goods
JOIN Payments ON Goods.good_id = Payments.good
JOIN FamilyMembers ON Payments.family_member = FamilyMembers.member_id WHERE status = 'son' 

Выведите идентификатор (поле room_id) и среднюю оценку комнаты (поле rating, для вывода используйте псевдоним avg_score), составленную на основании отзывов из таблицы Reviews.
Данная таблица связана с Reservations (таблица, где вы можете взять идентификатор комнаты) по полям reservation_id и Reservations.id.
SELECT room_id, AVG(rating) AS avg_score FROM Reservations
JOIN Reviews ON Reservations.id = Reviews.reservation_id 
GROUP BY room_id 

Отсортируйте список компаний (таблица Company) по их названию в алфавитном порядке и выведите первые две записи.
SELECT * FROM Company 
ORDER BY name
LIMIT 2

