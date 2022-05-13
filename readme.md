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
	window.MtsPay.onReady((paymentModule) => {
		const mtsPayButtonElement = paymentModule.createButtonElement();
		document.querySelector('#example1').append(mtsPayButtonElement);
	});
});
</script>
