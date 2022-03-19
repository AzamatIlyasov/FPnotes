# типы данных в erlang
их не много, всего 11 штук. Но можно сделать на базе этих.

- численные:
	- integer - выделяется столько, сколько нужно - default 1маш слово (4/8)
	- float - как у всех выполнен на базе IEEE754 ([IEEE 754 - Wikipedia](https://en.wikipedia.org/wiki/IEEE_754)) , соотвественно имеет проблемы с точностью в конце, и почему так, вот тут: [Что нужно знать про арифметику с плавающей запятой / Хабр (habr.com)](https://habr.com/ru/post/112953/)
- атомы - константные значения которое можно сравнивать. Применяется для "сопостоваления с образом" или pattern matching
	- [Сопоставление с образцом — Википедия (wikipedia.org)](https://ru.wikipedia.org/wiki/%D0%A1%D0%BE%D0%BF%D0%BE%D1%81%D1%82%D0%B0%D0%B2%D0%BB%D0%B5%D0%BD%D0%B8%D0%B5_%D1%81_%D0%BE%D0%B1%D1%80%D0%B0%D0%B7%D1%86%D0%BE%D0%BC)
	- [Pattern matching в C# 7 / Блог компании Microsoft / Хабр (habr.com)](https://habr.com/ru/company/microsoft/blog/423229/)
	- [Pattern matching. Теперь и в Python / Блог компании Яндекс.Практикум / Хабр (habr.com)](https://habr.com/ru/company/yandex_praktikum/blog/547902/)
	- 
- структуры: 
	- list
	- tuple
	- map
- идентификаторы
	- pid
	- port
	- reference
- функции
- binary
	
	
	