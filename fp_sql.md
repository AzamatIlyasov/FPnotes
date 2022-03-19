# fp_sql

Erlang может подключится к Postgre через модуль odbc
С этим модулем мы можем работать через user скрипты или консоль  
1) odbc:start(). Запускаем модуль odbc 
2) {ok, Ref} = odbc:connect("Driver={/usr/lib/x86_64-linux-gnu/odbc/psqlodbca.so};Server=192.168.2.158;Port=5432;Database=BZ2;Uid=postgres;Pwd=2312;",[]). Устанавливаем соединение с базой данных
3) odbc:sql_query(Ref, "SELECT * FROM table"). Теперь можем обращаться к таблицам в базе данных посредством SQL запросов
4) odbc:disconnect(Ref) После работы с базой данных мы разрываем с ней соединение
5) odbc:stop() Завершаем работу odbc модуля

Создаете к примеру user script, внутри него через odbc соединяетесь с ms-sql 2000

odbc строка будет иметь следубщий вид "Driver=/usr/lib/x86_64-linux-gnu/odbc/libtdsodbc.so;Server=192.168.210.172,1433;Database=remont;Uid=wacs;Pwd=wacs"

https://www.connectionstrings.com/microsoft-sql-server-odbc-driver/

Разумеется вам предварительно нужно установить необходимый драйвер

Для этого на ОС Ubuntu достаточно будет выполнить следующие команды
1) sudo apt-get update
2) sudo apt-get install unixodbc
3) sudo apt-get install tdsodbc




[Подключение из Linux или macOS - ODBC Driver for SQL Server | Microsoft Docs](https://docs.microsoft.com/ru-ru/sql/connect/odbc/linux-mac/connection-string-keywords-and-data-source-names-dsns?view=sql-server-ver15)

[Установка Microsoft ODBC Driver for SQL Server (Linux) - ODBC Driver for SQL Server | Microsoft Docs](https://docs.microsoft.com/ru-ru/sql/connect/odbc/linux-mac/installing-the-microsoft-odbc-driver-for-sql-server?view=sql-server-ver15#driver-files)


libmsodbcsql-17.X.so.X.X или libmsodbcsql-13.X.so.X.X

Общий объект (`so`) файла динамической библиотеки, содержащий все функциональные возможности драйвера. Этот файл устанавливается в папке `/opt/microsoft/msodbcsql17/lib64/` для версии 17 драйвера и в папке `/opt/microsoft/msodbcsql/lib64/` для версии 13.



{ok,Ref1} = odbc:connect("Driver=/usr/lib/x86_64-linux-gnu/odbc/libtdsodbc.so;Server=192.168.210.172,1433;Database=remont;Uid=wacs;Pwd=wacs;use_unicode=true",[]).

AzaTest1=odbc:sql_query(Ref1,"SELECT [god] ,[nn] ,[shifrIMJ] ,[data_post] ,[nom_RDC] ,[oboryd] ,[data_p_N] ,[data_p_K],[vidrem] ,[osn_rab] ,[sost] ,[data_r_N] ,[data_r_K] ,[data_f_N] ,[data_f_K] FROM [remont].[utpo].[r_ORZ] where sost in (SELECT NAM FROM [remont].[utpo].[i_sostRZ] WHERE COD IN ('03','04','08' ,'01','02','05','13')) AND GOD >= '2021' AND [shifrIMJ] Like '__00______'").



[ODBC + MSSQL: проблема с кодировкой. (google.com)](https://groups.google.com/g/erlang-russian/c/CD8gktiBGeU?pli=1)


