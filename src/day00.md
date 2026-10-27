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
