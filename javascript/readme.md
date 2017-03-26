# Навигация
* **[decodeExcelColPrefix](#decodeexcelcolprefix)** - функция переводит буквенное название столбца Excel (A, B, C) в его соответствующий порядковый номер (0, 1, 2)
* **[declensionOfNumber](#declensionofnumber)** - функция возвращает переданный текст, склоненный относительно числа
* **[divideNumberByPieces](#dividenumberbypieces)** - делит число разделителем на разряды

# Функции
### decodeExcelColPrefix

```javascript
/**
  * Функция переводит буквенное название столбца Excel (A, B, C)
  * в его соответствующий порядковый номер (0, 1, 2)
  * @param prefix - буквенный код
  * @returns {number|boolean}
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
 
 ### declensionOfNumber
 
 ```javascript
/**
  * Функция возвращает переданный текст, склоненный относительно числа
  * @param number - число, относительно которого нужно взять склонение
  * @param titles - массив вариантов склонения, например ['год', 'года', 'лет']
  * @returns {string} - строка из исходного числа и склоненного варианта, например - "5 лет"
  */
 function declensionOfNumber(number, titles) {
     cases = [2, 0, 1, 1, 1, 2];
     return [number, titles[ (number%100 > 4 && number%100 < 20) ? 2 : cases[(number%10 < 5) ? number%10 : 5] ]].join(' ');
 }
 ```
 [Пример использования](http://codepen.io/GarikFF/pen/LWBpVW)
 
### divideNumberByPieces
  
```javascript
/**
  * Делит число разделителем на разряды
  * http://stackoverflow.com/a/16637170
  * @param x - число
  * @param del - разделитель
  * @returns {string}
  */
function divideNumberByPieces(x, delimiter) {
  return x.toString().replace(/\B(?=(\d{3})+(?!\d))/g, delimiter || " ");
}
```
 [Пример использования](http://codepen.io/GarikFF/pen/QpBaBd)
 
