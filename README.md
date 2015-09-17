# Style guide reference repo

Будем собирать здесь наше видение верстки на примере сайта про фототуры.

Итак, поехали.

## 1 Верстка "классами" 
 
Идея заключается в том, что для разметки мы используем только классы. ID нужны только для программирования.
Никаких ID и тегов. Пример.

```css
/* Хорошо */
.content-article { /* ... */ }

/* Плохо */
p {...}
#content {...}
```

## 2 Компонентный подход

Посыл: **Количество зависимостей между отдельными модулями страницы стремится к 0.**

При таком подходе блоки можно менять местами, не боясь что верстка "поедет", 
блоки можно использовать повторно и в других проектах.

### 2.1 Каждый блок в своем CSS-файле

Для формы заказа звонка - свой файл, для футера - свой, для блока со ссылкой на фототур - свой.

Чем меньше отдельные блоки - тем, в общем случае, лучше.

Ну и, как обычно, наш девиз - **без фанатизма** :-)

В итоге, файл с версткой, подключаемый на страницу выглядит вот так:

```css

@import header.css;
@import footer.css;
@import tour.css;
@import feedback.css;
/* ...еще 100500 импортов... */
```

Перед загрузкой на **production** при сборке проекта все такие импорты собираются в один файл, который как единое целое и будет встроен в HTML-страницу.

Следствия из п2.1 - в п2.2, 2.3

### 2.2 Верстка без reset.css

Ибо reset.css как устанавливает правила для всего - даже для тех блоков и модулей, где он не нужен.
Если нужно установить свои стили - делаем это внутри css-файла блока.

### 2.3 Верстка без вложенных селекторов

Ну, почти без вложенных. Наш девиз - **без фанатизма** - еще никто не отменял.

```css

/* Хорошо */
.header {...}
.header__title {...}
.header__title__slogan {...}

/* Плохо */
.header .title .slogan{...}
```

"Why?" - спросите Вы. 

1. Да потому, что **title** может быть где-то еще в 150 местах на сайте.  
  И не факт что внутри Header он будет один.  
  Придется переопределять правила... Потом искать где и что поломалось... Нафиг оно нам? 

2. Потому, что если мы поменяем верстку (добавим какие-нибудь обертки или вынесем .slogan из .title), в первом случае
не поломается *ничего*, а во втором - что-нибудь по-любому нужно будет править.


### 3 Пиксели и другие единицы измерения

1. Шрифты лучше делать в **em** или **rem**.
2. Отступы между блоками в px - это нормально.  
   Отступы в тексте лучше делать через **em** или **rem**
