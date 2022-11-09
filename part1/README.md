## PART 1

В методе `_getInCondition` возвращается строка со значением 0, если массив данных пустой.
Но при этом проверки на значение нет при вызове метода `_loadObjectsByFilter`
Соответственно в SQL запрос у нас идёт примерно такой: 
```
SELECT * FROM $objectName WHERE 0
```

Предлагается изменить:
```
if (count($values) === 0) return '0'; 
```
на:
```
if (count($values) === 0) return false; 
```
также:
```
return $this->_loadObjectsByFilter('user', [$idsFilter]);
```
на:
```
if ($idsFilter) return $this->_loadObjectsByFilter('user', [$idsFilter]);
else return false;
```