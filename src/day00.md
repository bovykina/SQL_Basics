# Задание 00 — Выборка людей по городу.
Вывести имена и возраст людей, проживающих в Казани.
```
SELECT
	NAME,
	AGE
FROM
	PERSON
WHERE
	ADDRESS = 'Kazan'
