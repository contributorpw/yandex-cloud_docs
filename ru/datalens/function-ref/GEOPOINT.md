---
editable: false
---

# GEOPOINT

_Функции преобразования типов_

#### Синтаксис {#syntax}


```
GEOPOINT( value_1 [ , value_2 ] )
```

#### Описание {#description}
Формирует значение типа геоточка. Принимает на вход строку, либо значение типа "геоточка", либо координаты — широту `value_1` и долготу `value_2`. Если на вход подается одна строка, в ней должен содержаться список из двух чисел, координат (широты и долготы) в JSON-синтаксисе.

**Типы аргументов:**
- `value_1` — `Геоточка | Число | Строка`
- `value_2` — `Число | Строка`


**Возвращаемый тип**: `Геоточка`

#### Примеры {#examples}

```
GEOPOINT("[55.75222,37.61556]") = "[55.75222,37.61556]"
```

```
GEOPOINT(55.75222, 37.61556) = "[55.75222,37.61556]"
```


#### Поддержка источников данных {#data-source-support}

`Материализованный датасет`, `ClickHouse 1.1`, `Microsoft SQL Server 2017 (14.0)`, `MySQL 5.6`, `PostgreSQL 9.3`.