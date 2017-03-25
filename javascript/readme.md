# Навигация
* **[decodeExcelColPrefix](decodeExcelColPrefix)** - метод переводит буквенное название столбца Excel (A, B, C) в его соответствующий порядковый номер (0, 1, 2)

# Сниппеты
### decodeExcelColPrefix

```javascript
/**
  * Метод переводит буквенное название столбца Excel (A, B, C)
  * в его соответствующий порядковый номер (0, 1, 2)
  * @param prefix - буквенный код
  * @returns {number}
  */
 function decodeExcelColPrefix(prefix) {
 	//Через регулярное выражение определяем переданный буквенный код
 	let parsePrefix = prefix.match(/[a-zA-Z]+/)[0];
 	let pow = 1;
 	let res = 0;
 
 	//Обходим каждый полученный символ
 	for (let i = 0, len = parsePrefix.length; i < len; i++) {
 		//Переводим каждый символ в Юникод. Буквенные коды начинаются с 65 символа,
 		//поэтому вычитаем 64, таким образом получая нужно число.
 		//Множитель нужен в случае буквенных кодов второго и
 		//последующих порядков (e.g. AA, BX )
 		res += (parsePrefix[i].charCodeAt(0) - 64) * pow;
 		pow *= 25;
 	}
 	//Отнимаем единицу от результата, т.к. счет начинается с нуля
 	return (res > -1) ? res- 1 : false;
 }
 ```
 
 [Пример использования](https://codepen.io/GarikFF/pen/MpBwXx)
