# fp_api_erlang




Path = fp_db:to_path(FolderID),

fp:log(info,"DEBUG: timer test function for path ~p", [Path]),

fp_db:to_path({53, 1387}).

fp_db:to_path({53, 4843})

fp_db:to_path({302055498,1269}).



fp:to_json(Term) -> JSON
% Преобразует erlang term (список, map, числа) в json
% возвращает binary, которые является json

fp:from_json(JSON) -> Term
% Принимает на вход binary, который является JSON
% Возвращает erlang term

fp:open_tag(TagPath)  -> {ok, Object}
%% Работает только при включенном РАНТАЙМЕ
%% Принимает на вход путь к тегу, и возвращает объект
%% работает чуть бытрее чем fp_db:open(TagPath), так как кеширует данные

fp:get_value(Tag, Value) -> {ok, Value}
%% Работает только при включенном РАНТАЙМЕ
% Принимает путь к объекту и название поля%
% Возвращает значение поля, работает чуть быстрее чем fp_db:read_field(fp_db:open(tag), Value) так как кеширует данные


fp:get_value(Tag, Value, Default) -> {ok, Value}
% Работает также как и функция выше, но вернет Default, если значение поля не задано


fp:set_value(TagPath, Changes) -> ok
%% Работает только при включенном РАНТАЙМЕ
% Changes = [{Field1, Value1}, {Field2, Value2}, ...]
% Модифицирует поля заднные в Changes тега TagPath%
% Работает чуть быстрее чем fp_db:edit_object(fp_db:open(TagPath), #{Field1 => Value1, Field2 => Value2, ...}) так как кеширует данные


 fp:set_value(TagPath, Field, Value) -> ok
 %% Работает только при включенном РАНТАЙМЕ
 % Присвоит полю Field значение Value
 
 
 fp:archives_get(Points, Archives) -> [
 					[TS1, A1_value, A2_value, ...],
 					[TS1, A1_value, A2_value, ...],
 					...
 					]
 %Возвращает значения архивов в определенных моментах времени
 %  fp_archive:get(Points, Archives) работает аналогично

fp:archive_get_point(Archive, TS) -> {TS, Value}
% Возращает значение из архива в заданный момент времени
%  fp_archive:get_point( Archive, TS ) работает аналогично

fp:archives_get_periods(Params, Archives) -> [
 					[TS1, A1_value, A2_value, ...],
 					[TS1, A1_value, A2_value, ...],
 					...
 					]
% Возращает значение из архива в определенных моментах времени
% Моменты времени настраиваются через Params

fp:version() -> Version
%Вернет текущую версию 


fp_db:create_object(Params) -> Object
%Создаем обьект с заданными полями/параметрами%

fp_db:read_field(Object, Field) -> {ok, Value}
%Читаем значения из поля обьекта%


fp_db:read_field(Object, Field, Params) -> {ok, Value}
%Читаем значения из поля обьекта, но также можем указать доп параметры %
 
fp_db:read_fields(Object, Fields) -> #{Field1 => Value1, Field2 => Value2, ...}
%% Читаем сразу несколько полей из объекта

fp_db:edit_object(Object, #{Field => Value}) -> ok
% Задаем поле Field объекта значением Value

fp_db:query(Query) -> Result
%Запрос к базе данных(ecomet-у) 


 
 

