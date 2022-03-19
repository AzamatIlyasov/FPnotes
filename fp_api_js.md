# fp_api_js

/// *****************************************      DISCLAIMER    **********************************************
/// Для всех API-шных функций использовать приставку await если нужно получить возвращаемое значение из них ***
/// ***********************************************************************************************************	


//Вернет значение поля value из тега /root/PROJECT/TAGS/AI
let value = await fp.api.get_value('/root/PROJECT/TAGS/AI', 'value');

// Так мы запишем в соответствующие поля тега /root/PROJECT/TAGS/AI значения 5, 10.5 
fp.api.set_value('/root/PROJECT/TAGS/AI', 'value', 10.5);
fp.api.set_value('/root/PROJECT/TAGS/AI', 'valueH', 5);

//Печатаем сообщения в консоль с заданным уровнем
// Всего 4 уровня  debug | info | warning | error
fp.api.log("debug", "debug message");
fp.api.log("info", "info message");
fp.api.log("warning", "warning message");
fp.api.log("error", "error message");


//Создаем тег типа AI, в папке /root/PROJECT/TAGS/folder с именем mytag, также дополнительно говорим что поле value будет равно 1
//Возвращает строку, которая является неким идентификатором обьекта, этот идентификатор можно использовать в функциях вместо пути
// ниже будут примеры таких функций 
let obj = await fp.db.create_object({".name": "mytag", ".folder" : "/root/PROJECT/TAGS/folder", ".pattern" : "/root/.patterns/AI", value : 1.0});
//если идентификатор не нужен можно просто вызвать функцию
fp.db.create_object({".name": "mytag", ".folder" : "/root/PROJECT/TAGS/folder", ".pattern" : "/root/.patterns/AI", value : 1.0});


//Модифицирует обьект или созадст его, если такого нет 
let obj = await fp.db.edit_or_create({".name": "mytag", ".folder" : "/root/PROJECT/TAGS/folder", ".pattern" : "/root/.patterns/AI", value : 10.0, valueH : 100});

//Читаем значение из поля тега, можно вместо пути к тегу можно использовать идентификатор
let value = await fp.db.read_field('/root/PROJECT/TAGS/AI', 'value');
// или пример с использованием идентификатора
let obj = await fp.db.create_object({".name": "mytag", ".folder" : "/root/PROJECT/TAGS/folder", ".pattern" : "/root/.patterns/AI", value : 1.0});
let value = await fp.db.read_field(obj, 'value');


//Также вместо пути к тегу можно использовать идентификатор обьекта
let fields = await fp.db.read_fields('/root/PROJECT/TAGS/AI', ['value', 'valueH']);


//Редактирвание полей обьекта, можно использовать идентификатор вместо пути
fp.db.edit_object('/root/PROJECT/TAGS/AI', {value : 1.0, valueH :10, title : "qwe"});
//пример с идентификатором
let obj = await fp.db.create_object({".name": "mytag", ".folder" : "/root/PROJECT/TAGS/folder", ".pattern" : "/root/.patterns/AI", value : 1.0});
fp.db.edit_object(obj, {value : 1.0, valueH :10, title : "qwe"});


//Редактирвание полей обьекта, можно использовать идентификатор вместо пути, 'грязный' вариант
//Он работает быстрее, в остальном все аналогично
fp.db.dirty_edit_object('/root/PROJECT/TAGS/AI', {value : 1.0, valueH :10, title : "qwe"});
//пример с идентификатором
let obj = await fp.db.create_object({".name": "mytag", ".folder" : "/root/PROJECT/TAGS/folder", ".pattern" : "/root/.patterns/AI", value : 1.0});
fp.db.dirty_edit_object(obj, {value : 1.0, valueH :10, title : "qwe"});


//Удаляем обьект, в качестве параметра можно передать путь или идентификатор
//
// create new object
let obj = await fp.db.create_object({".name": "mytag", ".folder" : "/root/PROJECT/TAGS/folder", ".pattern" : "/root/.patterns/AI", value : 1.0});
// delete created object [what arguments are required?]
fp.db.delete_object(obj);

//Пример запроса, который выводит все имена и папки всех тегов типа AI 
let result = await fp.db.query("get .name, .folder from root where .pattern=$oid('/root/.patterns/AI')");


//Вернет oid объекта, вернее сказать трансформированный oid в виде строки
let oid = await fp.db.to_oid("/root/PROJECT/TAGS/AI");

//Можно получить путь к объекту через его идентификатор
let obj = await fp.db.create_object({".name":"Issa", ".folder":"/root/PROJECT/TAGS", ".pattern":"/root/.patterns/AI"});
let path = await fp.db.to_path(obj); /*   /root/PROJECT/TAGS/Issa    */



//Также есть возможность создать новый обьект, взяв некоторые поля из cтарого
//Только надо помнить, что надо изменить хотя бы одно из трех полей (.name, .folder, .pattern) иначе операция выдаст ошибку
let obj = await fp.db.create_object({".name":"Issa", ".folder":"/root/PROJECT/TAGS", ".pattern":"/root/.patterns/AI", value:1.0});
let new_object = await fp.db.copy_object(obj, {".name":"Kostya"}); //В той же папке создали тег AI, но с другим именем


// Получить значение из архива за определенные промежутки времени
// Можно указать сразу несколько архивов и для каждого архива свою агрегирующую функцию, ниже приведены примеры вызова
// Список агрегирующих функций {min, max, sum, avg, steps, categories}
let data = await fp.api.archives_get([TS1, TS2, TS3], [["/root/PROJECT/TAGS/archive_1", 'avg']]);
let data = await fp.api.archives_get([TS1, TS2, TS3, TS4], [["/root/PROJECT/TAGS/archive_1", 'avg'], ["/root/PROJECT/TAGS/archive_2", 'min'], ["/root/PROJECT/TAGS/archive_2", 'sum']]);


// Данные из архива можно получить и по другому, step_unit и step_size указывают шаг, step_count количество данных
// start говорит что нужно получить step_count данных начиная со start с шагом step_unit * step_count 
// end говорит что нужно получить step_count данных заканчивая со end с шагом step_unit * step_count 
// Виды step_unit {year, month, week, day, hour, minute, second, millisecond}
let data = await fp.api.archives_get_periods({step_unit: "second", step_size: 1, step_count: 10, start:TS }, [["/root/PROJECT/TAGS/archive_1", "avg"]]);
let data = await fp.api.archives_get_periods({step_unit: "second", step_size: 1, step_count: 10, end:TS }, [["/root/PROJECT/TAGS/archive_1", "avg"]]);

//Получить путь к каталогу с шаблоном my_catalog и id 1
let node = await fp.api.catalog_find_node('my_catalog', 1);


// Начало транзакции
fp.db.start_transaction();

//Коммит транзакции
fp.db.commit_transaction();

//Конец транзакции
fp.db.rollback_transcation();