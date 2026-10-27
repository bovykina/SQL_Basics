## Задание 00 — Выборка людей по городу.
Вывести имена и возраст людей, проживающих в Казани.
```
SELECT
	NAME,
	AGE
FROM
	PERSON
WHERE
	ADDRESS = 'Kazan'
```

## Задание 01 — Фильтрация по полу и городу.
Вывести имена и возраст женщин из Казани, отсортировав результат по имени.
```
SELECT
	NAME,
	AGE
FROM
	PERSON
WHERE
	ADDRESS = 'Kazan'
	AND GENDER = 'female'
ORDER BY
	NAME
```

## Задание 02 — Фильтрация по рейтингу.
Двумя способами выбрать пиццерии с рейтингом от 3,5 до 5 и отсортировать их по рейтингу.
```
SELECT
	NAME,
	RATING
FROM
	PIZZERIA
WHERE
	RATING <= 5
	AND RATING >= 3.5
ORDER BY
	RATING
```
```	
SELECT
	NAME,
	RATING
FROM
	PIZZERIA
WHERE
	RATING BETWEEN 3.5 AND 5
ORDER BY
	RATING
```

## Задание 03 — Уникальные посетители.
Найти идентификаторы людей, посещавших пиццерии в заданный период или пиццерию с указанным идентификатором.
```
SELECT DISTINCT
	PERSON_ID
FROM
	PERSON_VISITS
WHERE
	(VISIT_DATE BETWEEN '2022-01-06' AND '2022-01-09')
	OR (PIZZERIA_ID = '2')
ORDER BY
	PERSON_ID DESC
```

## Задание 04 — Формирование строки.
Объединить имя, возраст, пол и адрес человека в одно вычисляемое поле и отсортировать результат.
```
SELECT
	CONCAT(
		NAME,
		' (age:',
		AGE,
		',gender: ',
		'''',
		GENDER,
		'''',
		' ,address: ',
		'''',
		ADDRESS,
		'''',
		')'
	) PERSON_INFORMATION
FROM
	PERSON
ORDER BY
	PERSON_INFORMATION
```

## Задание 05 — Подзапрос в SELECT.
Получить имена людей, заказавших пиццы с указанными идентификаторами меню 7 января 2022 года, без `JOIN` и `IN`.
```
SELECT 
	(
		SELECT
			NAME
		FROM
			PERSON
		WHERE
			PERSON.ID = PERSON_ORDER.PERSON_ID
	)
FROM
	PERSON_ORDER
WHERE
	(
		MENU_ID = 13
		OR MENU_ID = 14
		OR MENU_ID = 18
	)
	AND (ORDER_DATE = '2022-01-07')
```

## Задание 06 — Проверка имени.
Дополнить запрос из задания 05 вычисляемым полем, которое проверяет, зовут ли человека Denis.
```
SELECT
	(
		SELECT
			NAME
		FROM
			PERSON
		WHERE
			PERSON.ID = PERSON_ORDER.PERSON_ID
	),
	(
		SELECT
			NAME
		FROM
			PERSON
		WHERE
			PERSON.ID = PERSON_ORDER.PERSON_ID
	) = 'Denis' CHECK_NAME
FROM
	PERSON_ORDER
WHERE
	(
		MENU_ID = 13
		OR MENU_ID = 14
		OR MENU_ID = 18
	)
	AND (ORDER_DATE = '2022-01-07')
```

## Задание 07 — Возрастные интервалы.
Распределить людей по заданным возрастным группам с помощью условной логики и отсортировать результат.
```
SELECT
	ID,
	NAME,
	CASE
		WHEN (
			AGE >= 10
			AND AGE <= 20
		) THEN 'interval #1'
		WHEN (
			AGE > 20
			AND AGE < 24
		) THEN 'interval #2'
		ELSE 'interval #3'
	END AS INTERVAL_INFO
FROM
	PERSON
ORDER BY
	INTERVAL_INFO
```

## Задание 08 — Чётные идентификаторы.
Вывести все записи заказов, у которых идентификатор является чётным числом.
```
SELECT
	*
FROM
	PERSON_ORDER
WHERE
	ID % 2 = 0
ORDER BY
	ID
```

## Задание 09 — Подзапрос в FROM.
Получить имена людей и названия посещённых ими пиццерий за заданный период, используя вложенный запрос и сортировку по двум полям.
```
SELECT
	(
		SELECT
			NAME
		FROM
			PERSON
		WHERE
			PERSON.ID = PV.PERSON_ID
	) PERSON_NAME,
	(
		SELECT
			NAME
		FROM
			PIZZERIA
		WHERE
			PIZZERIA.ID = PV.PIZZERIA_ID
	) PIZZERIA_NAME
FROM
	(
		SELECT
			PERSON_ID,
			PIZZERIA_ID
		FROM
			PERSON_VISITS
		WHERE
			VISIT_DATE BETWEEN '2022-01-07' AND '2022-01-09'
	) AS PV
ORDER BY
	PERSON_NAME,
	PIZZERIA_NAME DESC
```

