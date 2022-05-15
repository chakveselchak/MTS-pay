<style>
  body {
    max-width: 60em;
  }
  h1, h2, h3, h4,h5, h6, p {
	  font-family: system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue","Noto Sans","Liberation Sans",Arial,sans-serif,"Apple Color Emoji","Segoe UI Emoji","Segoe UI Symbol","Noto Color Emoji";
  }
  h1,h2,h3,h4,h5mh6 {
    margin-top: 3em;
  }
  h5, h6 {
	font-style: normal;
  }
  p > code, h3 > code, h4 > code, h5 > code, h6 > code {
	color: #ae1212;
	background-color: rgb(188, 188,188, .24);
	padding: 4px;
	border-radius: 5px;
  }
  pre.sourceCode {
  border: 1px solid #e8e8e8;
  border-radius: 5px;
  background-color: #f6f6f6;
  padding: 5px 12px;
  }
  mark {
	background-color: transparent;
	font-family: SFMono-Regular,Menlo,Monaco,Consolas,"Liberation Mono","Courier New",monospace;
	font-size: 12px;
	margin-left: 15px;
	padding-left: 15px;
	border-left: 1px solid #c6c6c6;
  }
  mark.required {
	  color: #ef5353;
	  text-transform: lowercase;
  }
  mark.optional {
	  color: #9b9b9b;
	  text-transform: lowercase;
  }
</style>

Оглавление

- [[#Шаг 1.  Укажите блок для размещения кнопки на странице|Шаг 1.  Укажите блок для размещения кнопки на странице]]
- [[#Шаг 2.  Подключение mts-pay.js к странице|Шаг 2.  Подключение mts-pay.js к странице]]
- [[#Шаг 3. Инициализация кнопки|Шаг 3. Инициализация кнопки]]
	- [3.1 Рендер кнопки](#рендер-кнопки)
	- [Параметры `mtsModule.createButtonElement`](Параметры `mtsModule.createButtonElement`)
	- [[#Шаг 3. Инициализация кнопки#Пример стилизованной кнопки|Пример стилизованной кнопки]]


# Пошаговое руководство по интеграции MTS-Pay.js
MTS Pay - собой способ оплаты на сайте в виде стилизованной кнопки "MTS Pay", при нажатии на которую открывается Popup-окно с выбором разных способов оплаты.
На текущий момент доступны следующие способы оплаты:
- оплата по банковской карте
- оплата с баланса телефона (только для клиентов МТС)


### Шаг 1.  Укажите блок для размещения кнопки на странице
В HTML-коде странице, где должна будет отображаться кнопка MTS Pay нужно указать блок, в который в итоге добавится кнопка. Блок должен размещаться строго внутри тега *\<body>*

> **Важно!**
> Класс элемента должен быть уникальным на странице, и не должен конфилктовать с другими элементами.

```html
<div class="mts-pay__container"></div>
```


### Шаг 2.  Подключение mts-pay.js к странице
В \<head> страницы нужно подключить скрипт mts-pay.js

Для **UAT** (Тестовый стенд) используется следующий код:
```html
<script src="https://web.rbsuat.com/mtsbank/modules/mts-pay/mts-pay.js"></script>
```

Для **PROD** (Продуктив) используется:
```html
<script src="https://oplata.mtsbank.ru/payment/modules/mts-pay/mts-pay.js"></script>
```


### Шаг 3. Инициализация кнопки
Подключение кнопки в странице должно происходить только после полной загрузки HTML-документа. 

```html
<script>
	document.addEventListener('DOMContentLoaded', function() {	
		// << Инициализация скрипта
	});
</script>
```

MTS Pay асинхронно инициализируется, поэтому вся работа со модулем происходит в функции `window.MtsPay.OnReady((mtsModule) => {...})`

#### 3.1 Рендер кнопки
Для отрисовки кнопки требуется вызвать функцию `mtsModule.createButtonElement`

```js
<script>
	document.addEventListener('DOMContentLoaded', () => {
		window.MtsPay.onReady((mtsModule) => {
			const mtsPayButtonElement = mtsModule.createButtonElement(); // 
			document.querySelector('.mts-pay__container').append(mtsPayButtonElement);
		});
	});
</script>
```

<script src="https://web.rbsuat.com/mtsbank/modules/mts-pay/mts-pay.js"></script>
<div id ="example1"></div>
<script>
document.addEventListener('DOMContentLoaded', () => {
	window.MtsPay.onReady((mtsModule) => {
		const mtsPayButtonElement = mtsModule.createButtonElement();
		document.querySelector('#example1').append(mtsPayButtonElement);
	});
});
</script>

##### Параметры `mtsModule.createButtonElement`

**theme** <mark class="optional">Необязательное</mark>

Тема кнопки. Может принимать значения:

`red` - красный фон кнопки

`black` - черный фон кнопки

`white` - белый фон кнопки

**phrase** <mark class="optional">Необязательное</mark>

Текст внутри кнопки. Может принимать значения:

`забронировать`
`купить`
`продолжить`
`заказать`
`оплатить`
`арендовать`
`подписаться`
`поддержать`
`поддержать`
`book`
`buy`
`continue`
`order`
`pay`
`rent`
`subscribe`
`support`

##### Пример стилизованной кнопки

```js
<div id ="example2"></div>
<script>
document.addEventListener('DOMContentLoaded', () => {
	window.MtsPay.onReady((mtsModule) => {
		const mtsPayButtonElement = mtsModule.createButtonElement({ theme: 'black', phrase: 'Подписаться'});
		document.querySelector('#example2').append(mtsPayButtonElement);
	});
});
</script>
```

<div id ="example2"></div>
<script>
document.addEventListener('DOMContentLoaded', () => {
	window.MtsPay.onReady((mtsModule) => {
		const mtsPayButtonElement = mtsModule.createButtonElement({ theme: 'black', phrase: 'Подписаться'});
		document.querySelector('#example2').append(mtsPayButtonElement);
	});
});
</script>

#### 3.2 Передача параметров платежа
Для передачи параметров платежа, требуется создать экземпляр объекта `mtsModule`, который был передан в `onReady`, а затем его проинициализировать (`init()`) 

```js
document.addEventListener('DOMContentLoaded', () => {
    window.MtsPay.onReady((mtsModule) => {
        const mtsPayButtonElement = mtsModule.createButtonElement({ phrase: 'Купить'});
        document.querySelector('#example3').append(mtsPayButtonElement);

        const mtsPaySession = new mtsModule({
            buttonElement: mtsPayButtonElement,
            merchant: {
              login: 'merchantLogin',
            },
            order: {
              description: 'Автомобиль DeLorean DMC-12',
              orderNumber: '1',
              amount: 55000,
            }
        });
        mtsPaySession.init();
    });
});
```

При инициализации сессии, кнопка становится кликабельной.
<div id ="example3"></div>

<script>
    window.MtsPay.onReady((mtsModule) => {
        const mtsPayButtonElement = mtsModule.createButtonElement({ phrase: 'Купить'});
        document.querySelector('#example3').append(mtsPayButtonElement);

        const mtsPaySession = new mtsModule({
            buttonElement: mtsPayButtonElement,
            merchant: {
              login: 'merchantLogin',
            },
            order: {
              description: 'Автомобиль DeLorean DMC-12',
              orderNumber: '1',
              amount: 55000,
            }
        });
        mtsPaySession.init();
    });
</script>

##### Параметры, которые может принимать `new mtsModule`

###### **merchant** <mark class="required">Обязательное</mark>

**login** <mark class="required">Обязательное</mark>

###### **order** <mark class="required">Обязательное</mark>

**amount** <mark class="required">Обязательное</mark>

**currency** <mark class="required">Обязательное</mark>

**returnUrl** <mark class="required">Обязательное</mark> ???? спросить антона

**clientId** <mark class="optional">Необязательное</mark> 

**orderNumber** <mark class="optional">Необязательное</mark> 

**depositFlag** <mark class="optional">Необязательное</mark> 

**sessionExpiredDate** <mark class="optional">Необязательное</mark> 

**description** <mark class="optional">Необязательное</mark> 

**orderParams** <mark class="optional">Необязательное</mark> 

**orderBundle** <mark class="optional">Необязательное</mark> 

...

**features** <mark class="optional">Необязательное</mark> 

**taxSystem** <mark class="optional">Необязательное</mark> 

**email** <mark class="optional">Необязательное</mark> 

**phone** <mark class="optional">Необязательное</mark> 

**postAddress** <mark class="optional">Необязательное</mark> 

**terminalId** <mark class="optional">Необязательное</mark> 

**additionalOfdParams** <mark class="optional">Необязательное</mark> 

**billingPayerData** <mark class="optional">Необязательное</mark> 
...

###### **successUrl** <mark class="optional">Необязательное</mark>

###### **failUrl** <mark class="optional">Необязательное</mark>