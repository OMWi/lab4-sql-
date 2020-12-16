# Проделанная работа
1.Восстановлена БД AdventureWorks2019  
2.Выбраны 5 таблиц:Person.Person, Person.EmailAddress, Person.Address, Person.Password, Person.Phone. Person.Address связана AddressID, остальные - BusinessID  
3.Написано 5 хранимых процедур. Пример одной из них:  
```
USE [AdventureWorks2019]   
GO   
SET ANSI_NULLS ON   
GO   
SET QUOTED_IDENTIFIER ON  
GO  
ALTER PROCEDURE [dbo].[GetEmailByBuid]   
	@bid int  
AS  
BEGIN  
	SET NOCOUNT ON;  
	SELECT EmailAddress, BusinessEntityID  
	FROM AdventureWorks2019.Person.EmailAddress  
	WHERE BusinessEntityID = @bid  
END  
```
4.Разработан слой DataAccessLayer, в котором есть 5 интерфейсов, которые реализованы в моделях  
5.Разработан слой ServiceLayer(ServiceModel) содержащий строку подключения к БД, которая берется из ServiceConfig.json с помощью ConfigProvider из 3 лабы  
6.Все разнесено в разные проекты  
7.Для каждой модели создан отдельный проект  
8.Разработан XmlCreator, который создает XML документ и XSD схему модели ServiceModel  
9.В XmlCreator передается путь по которому надо отправить XML и XSD  
10.Конфигурацию читаем из ServiceConfig.json   
11.Конфигурацию читаем из ServiceConfig.json   
12.В решении есть 6 проектов  
13.Создана отдельная база для логирования. Она содержит таблицу Errors с полями для записи ошибок и хранимую процедуру:  
```
USE [ErrorLogging]  
GO  
SET ANSI_NULLS ON  
GO  
SET QUOTED_IDENTIFIER ON  
GO  
ALTER PROCEDURE [dbo].[AddError]  
	@errorMess nvarchar(MAX),  
	@time datetime  
AS  
BEGIN  
	SET NOCOUNT ON;  
	INSERT INTO Errors(ErrorMessage, DateTime)  
	VALUES (@errorMess, @time)  
END  
```

14.Создан слой LoggerLayer, который содержит функцию для добавления ошибок в таблицу БД  
15.Везде используются хранимые процедуры, но не в TransactionScope  
16.Все разбито на разные проекты с разными пространствами  
17.Статику нигде не используется. Также ORM-библиотеки, автомапперы и другие запретные вещи не были употреблены.  
