# Библиотека Pic для PHP v0.2&beta;
Маленькая библиотека для работы с изображениями средствами PHP
>Обратите внимание, поддерживаются только версии PHP7.1 и старше
# Функции
## Создание класса и загрузка изображения
Напомню, библиотека предназначена для работы с уже готовыми изображениями, так что создание *холстов* не предусмотрено. Загружаемое изображение указывается при вызове класса. Если изображение небыло загружено, то функция `$im->getErr()` вернет строку, иначе - `false`.
```php
<?php
  var $im = Pic('myImg.jpg');
?>
```
Всё, с изображением теперь можно работать.
## Изменене размера
Казалось бы, что в этой функции может быть сложного? Однако, данная библиотека создана именно для неё.

>Обратите внимание, что данная функция не возвращает измененную копию изображение, а изменяет свою.
```php
$im->resize(новая_ширина, новая_высота[, тип_изменения, фоновый_цвет])
```
Если отношение сторон изначального и конечного изображения совпадают, то проблем нет. Но что если нет? Тогда есть три варианта.

### Первый - растянуть/сжать (stretch)
Изображение растягивается или сжимается по обеим осям до нужного соотношения сторон. Самоя простая и редкоиспользуемая функция. Она, ввиду её простоты и логичности, используется по умолчанию.
```php
$im->resize(100, 100);//Указывать тип или фоновый цвет не имеет смысла
```
### Второй - приблизить (approx)
Изображение изменяет соотношение сторон так, что одна часть изображения вылезает, у другая располагается по всей ширине/высоте. Для такого изменения понадобится указать тип, но нет смысла изменять фоновый цвет. Фона просто нет.
```php
$im->resize(100, 100, 'approx');//Указывать фоновый цвет не имеет смысла
```
### Третий - наращивание (upbuild)
Изображению "наращивается" недостающее соотношение сторон. Здесь уже имеет смысл указать наращиваемый цвет. По умолчанию - белый.
```php
$im->resize(100, 100, 'upbuild', [0, 0, 0]);
```
>Обратите внимание, что цвет задается массивом `[$r, $g, $b]`, каждое значение в диапазоне от **0** до  **255**.

# Полезные советы
>Если надо работать подряд с несколькими изображениями, то можно использовать одну копию класса, а при переходе к новому изображению, загрузить его через функцию `$im->load('new.jpg')`. Старое автоматически сотрется из памяти.

***
# Особенности версии
* Изображения надо указывать относитьльно выполняемого файла, указание ссылки приведет к ошибке определение MIME-типа.
