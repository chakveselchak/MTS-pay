<style>
  body {
    max-width: 60em;
  }
  h1, h2, h3, h4,h5, h6, p, i {
	  font-family: system-ui,-apple-system,"Segoe UI",Roboto,"Helvetica Neue","Noto Sans","Liberation Sans",Arial,sans-serif,"Apple Color Emoji","Segoe UI Emoji","Segoe UI Symbol","Noto Color Emoji";
  }
  h1,h2,h3,h4,h5mh6 {
    margin-top: 3em;
  }
  h5, h6 {
	font-style: normal;
  }
  p {
    font-size: 0.9em;
  }
  .indent {
    padding-left: 30px;
    border-left: 2px solid #f1f1f1;
  }
  p > code, h3 > code, h4 > code, h5 > code, h6 > code {
	color: #ae1212;
	background-color: rgb(188, 188,188, .15);
	padding: 4px;
	border-radius: 5px;
  }
  pre.sourceCode {
  border: 1px solid #e8e8e8;
  border-radius: 5px;
  background-color: #f6f6f6;
  padding: 5px 12px;
  }
  .param {
    background-color: #e8e8e8;
    padding: 3px 10px;
    color: #2d2626;
    border-radius: 4px;
    font-weight: bold;
    display: inline-block;
    margin-top: 0.9em;
    font-style: normal;
  }
  mark {
	background-color: transparent;
	font-family: SFMono-Regular,Menlo,Monaco,Consolas,"Liberation Mono","Courier New",monospace;
	font-size: 12px;
	margin-left: 12px;
	padding-left: 15px;
	border-left: 1px solid #c6c6c6;
	text-transform: lowercase;
  }
 mark::after {
    display: inline-block;
    top: -1px;
    position: relative;
    text-transform: lowercase;
 }
 mark.number::after {
    content: "number";
	color: #9b9b9b;
  }
 mark.object::after {
    content: "object";
	color: #9b9b9b;
  }
  mark.string::after {
    content: "string";
	color: #9b9b9b;
  }
  mark.array::after {
    content: "array";
	color: #9b9b9b;
  }
  mark.function::after {
    content: "funtion";
	color: #9b9b9b;
  }
  mark.required::after {
    content: "обязательное";
    color: #ef5353;
  }
  mark.optional::after {
    color: #9b9b9b;
    content: "необязательное";
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

MTS Pay асинхронно инициализируется, поэтому вся работа со модулем происходит в функции `window.mtsPayModule.OnReady((MtsPay) => {...})`

#### 3.1 Рендер кнопки
Для отрисовки кнопки требуется вызвать функцию `MtsPay.createButtonElement`

```js
<script>
	document.addEventListener('DOMContentLoaded', () => {
		window.mtsPayModule.onReady((MtsPay) => {
			const mtsPayButtonElement = MtsPay.createButtonElement();  
			document.querySelector('.mts-pay__container').append(mtsPayButtonElement);
		});
	});
</script>
```

<script src="https://web.rbsuat.com/mtsbank/modules/mts-pay/mts-pay.js"></script>
<div id ="example1"></div>
<script>
document.addEventListener('DOMContentLoaded', () => {
	window.mtsPayModule.onReady((MtsPay) => {
		const mtsPayButtonElement = MtsPay.createButtonElement();
		document.querySelector('#example1').append(mtsPayButtonElement);
	});
});
</script>

##### Параметры `MtsPay.createButtonElement`


<i class="param">theme</i> <mark class="optional"></mark>  <mark class="string"></mark>

Тема кнопки. Может принимать значения:

`red` - красный фон кнопки

`black` - черный фон кнопки

`white` - белый фон кнопки

<i class="param">phrase</i> <mark class="optional"></mark> <mark class="string"></mark>

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
	window.mtsPayModule.onReady((MtsPay) => {
		const mtsPayButtonElement = MtsPay.createButtonElement({ theme: 'black', phrase: 'Подписаться'});
		document.querySelector('#example2').append(mtsPayButtonElement);
	});
});
</script>
```

<div id ="example2"></div>
<script>
document.addEventListener('DOMContentLoaded', () => {
	window.mtsPayModule.onReady((MtsPay) => {
		const mtsPayButtonElement = MtsPay.createButtonElement({ theme: 'black', phrase: 'Подписаться'});
		document.querySelector('#example2').append(mtsPayButtonElement);
	});
});
</script>

#### 3.2 Передача параметров платежа
Для передачи параметров платежа, требуется создать экземпляр объекта `mtsModule`, который был передан в `onReady`, а затем его проинициализировать `init()`

```js
document.addEventListener('DOMContentLoaded', () => {
    window.mtsPayModule.onReady((MtsPay) => {
        const mtsPayButtonElement = MtsPay.createButtonElement({ phrase: 'Купить'});
        document.querySelector('#example3').append(mtsPayButtonElement);

        const mtsPaySession = new MtsPay({
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
    window.mtsPayModule.onReady((MtsPay) => {
        const mtsPayButtonElement = MtsPay.createButtonElement({ phrase: 'Купить'});
        document.querySelector('#example3').append(mtsPayButtonElement);

        const mtsPaySession = new MtsPay({
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

<i class="param">merchant</i> <mark class="required"></mark> <mark class="object"></mark>

Объект с информацией о продавце. Содержит в себе параметр `login`

<div class="indent">
<div><i class="param">login</i> <mark class="required"></mark> <mark class="string"></mark></div>
Логин продавца(мерчанта) в платежном шлюзе. Выдается мерчанту при регистрации в платежном шлюзе. Можно уточнить у поддержки.
</div>

<i class="param">order</i> <mark class="required"></mark> <mark class="object"></mark>

Объект с информацией о заказе. Содержит в себе следующие параметры:

<div class="indent">
<div><i class="param">amount</i> <mark class="required"></mark> <mark class="string"></mark></div>

Сумма заказа в <u>минорных единицах</u>. Например, для 5 рублей 30 копеек - 530.
 
<div><i class="param">currency</i> <mark class="required"></mark><mark class="string"></mark></div>
Валюта заказа. Циферный код валюты согласно [ISO 4217](https://www.iso.org/ru/iso-4217-currency-codes.html) <br>
Например, RUB - 643, USD - 840, EUR - 978 <br>
Значение по умолчанию: `643`

<i class="param">clientId</i> <mark class="optional"></mark> <mark class="string"></mark>

Идентификатор клиента. Требуется для функционала "Сохраненные карты"(связки), когда система узнает пользователя и предлагает к оплате карты, которые он сохранял ранее.

<i class="param">orderNumber</i> <mark class="optional"></mark> <mark class="string"></mark> 

Номер заказа в системе магазина. Можно не указывать, если в платежном шлюзе  выставлена настройка "Система генерирует номер заказа".
 
<i class="param">depositFlag</i> <mark class="optional"></mark> <mark class="string"></mark>

Флаг двухстадийной оплаты. Может принимать 2 значения:
`PRE_AUTH` - двустадийный платеж
`PURCHASE` - одностадийный платеж
Значение по умолчанию: `PURCHASE`;
 
<i class="param">sessionExpiredDate</i> <mark class="optional"></mark> <mark class="string"></mark>
 
<i class="param">description</i> <mark class="optional"></mark> <mark class="string"></mark>
 
<i class="param">orderParams</i> <mark class="optional"></mark> <mark class="object"></mark>
 
<i class="param">orderBundle</i> <mark class="optional"></mark> <mark class="object"></mark>

...

</div>
<i class="param">features</i> <mark class="optional"></mark> 
 
<i class="param">taxSystem</i> <mark class="optional"></mark> 
 
<i class="param">email</i> <mark class="optional"></mark> 
 
<i class="param">phone</i> <mark class="optional"></mark> 
 
<i class="param">postAddress</i> <mark class="optional"></mark> 
 
<i class="param">terminalId</i> <mark class="optional"></mark> 
 
<i class="param">additionalOfdParams</i> <mark class="optional"></mark> 
 
<i class="param">billingPayerData</i> <mark class="optional"></mark> 
...

###### <i class="param">successUrl</i> <mark class="optional"></mark>

###### <i class="param">failUrl</i> <mark class="optional"></mark>