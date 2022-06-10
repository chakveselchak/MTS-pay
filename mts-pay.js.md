<style>
  body {
    max-width: 60em;
  }
  h1, h2, h3, h4,h5, h6, p, i, ul a, .toastify {
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
input[type="number"],input[type="text"] {
	padding: 4px 7px;
	margin: 0 3px;
}
.button {
  padding: 5px 7px;
  background-color: #fff;
  border: 1px solid #909090;
  border-radius: 5px;
  background: rgb(242,242,242);
  background: linear-gradient(1deg, rgba(242,242,242,1) 0%, rgb(239 239 239) 35%, rgba(255,255,255,1) 100%);
  cursor: pointer;
}
.button:hover {
    background: linear-gradient(1deg, rgb(244 244 244) 0%, rgb(255 255 255) 35%, rgba(255,255,255,1) 100%);
}
  .indent {
    padding-left: 15px;
    margin-left: 15px;
    border-left: 1px solid #f1f1f1;
  }
.indent i.param:before {
    content: '';
    display: table;
    width: 11px;
    position: absolute;
    color: #d7d7d7;
    left: -16px;
    top: 17px;
    border-bottom: 1px solid #e6e6e6;
}
  p > code, h3 > code, h4 > code, h5 > code, h6 > code {
	color: #ae1212;
	background-color: rgb(188, 188,188, .15);
	padding: 4px;
	border-radius: 5px;
  }
  div.sourceCode {
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
    position: relative;
  }
  blockquote {
  margin: 0;
  padding: 10px 20px;
  background-color: #e0f4ff;
  border: 1px solid #c3d8e6;
  border-radius: 5px;
  color: inherit;
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
  mark.boolean::after {
    content: "boolean";
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
.toastify {
	font-size: 12px;
}
#exampleStyleButton {
	width: 100%;
	height: 80px;
	border-radius: 12px;
	text-align: center;
	background-color: #ffffff;
	display: flex;
	align-content: center;
	flex-wrap: nowrap;
	align-items: center;
	justify-content: space-around;
}
hr {
	background-color: #ececec;
}
#exampleStyleButton.dark-background {
	background-color: #2c2c2c;
}
.container-center {
  margin: 0 auto;
  text-align: center;
}
select {
  padding: 5px 10px;
  border-radius: 5px;
  border: 1px solid #acacac;
  text-align: center;
}
</style>


## Оглавление

- [Шаг 1.  Укажите блок для размещения кнопки на странице](#шаг-1.-укажите-блок-для-размещения-кнопки-на-странице)
- [Шаг 2. Подключение mts-pay.js к странице](#шаг-2.-подключение-mts-pay.js-к-странице)
- [Шаг 3. Инициализация кнопки](#шаг-3.-инициализация-кнопки)
	- [3.1 Рендер кнопки](#рендер-кнопки)
		- [Параметры `MtsPay.createButtonElement`](#параметры-mtspay.createbuttonelement)
		- [Пример стилизованной кнопки](#пример-стилизованной-кнопки)
	- [3.2 Передача параметров платежа](#передача-параметров-платежа)
		- [Параметры `new MtsPay({})`](#параметры-new-mtspay)
		- [Пример MTS Pay c корзиной](#пример-mts-pay-c-корзиной)
- [События MTS Pay](#cобытия-mts-pay)
- [mtsPaySession.updateOrder() - Обновление информации в сессии](#mtspaysession.updateorder---обновление-информации-в-сессии)
- [mtsPaySession.destroy() - демонтаж кнопки](#mtspaysession.destroy---демонтаж-кнопки)
- [Определения статуса платежа](#определения-статуса-платежа)
- [Тестовые данные для проверки](#тестовые-данные-для-проверки)



## Пошаговое руководство по интеграции MTS-Pay.js
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

MTS Pay асинхронно инициализируется, поэтому вся работа со модулем происходит в функции <br> `window.mtsPayModule.OnReady((MtsPay) => {...})`

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
<div id="example2"></div>
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
<hr>

<div class="container container-center">
  <select id="btnColor">
    <option value="red">red</option>
    <option value="black">black</option>
    <option value="white">white</option>
  </select>
  <select id="btnText" value="subscribe">
    <option value=""></option>
    <option value="book">book</option>
    <option value="buy">buy</option>
    <option value="continue">continue</option>
    <option value="order">order</option>
    <option value="pay">pay</option>
    <option value="rent">rent</option>
    <option value="subscribe">subscribe</option>
    <option value="support">support</option>
  </select>
</div>
<div id="exampleStyleButton"></div>
<script>
var btnColor = document.getElementById('btnColor');
var btnText = document.getElementById('btnText');

btnColor.addEventListener('change', renderButton);
btnText.addEventListener('change', renderButton);

document.addEventListener('DOMContentLoaded', renderButton)

function renderButton() {
	document.querySelector('#exampleStyleButton').innerHTML = "";
	var color = btnColor.value;
	var text = btnText.value;
	if (color === 'white') {
		document.querySelector('#exampleStyleButton').classList.add('dark-background');
	} else {
		document.querySelector('#exampleStyleButton').classList.remove('dark-background');
	}
	
	window.mtsPayModule.onReady((MtsPay) => {
		const mtsPayButtonElement = MtsPay.createButtonElement({ theme: color, phrase: text });
		document.querySelector('#exampleStyleButton').append(mtsPayButtonElement);
	});
}

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
              login: 'mtsPayTestMerchant',
            },
            order: {
              description: 'Автомобиль DeLorean DMC-12',
              orderNumber: new Date().getTime().toString(),
              amount: 55000,
            }
        });
        mtsPaySession.init();
    });
});
```


При инициализации сессии, кнопка становится кликабельной.

<div id="example3"></div>

<script>
    window.mtsPayModule.onReady((MtsPay) => {
        const mtsPayButtonElement = MtsPay.createButtonElement({ phrase: 'Купить'});
        document.querySelector('#example3').append(mtsPayButtonElement);

        const mtsPaySession = new MtsPay({
            buttonElement: mtsPayButtonElement,
            merchant: {
              login: 'mtsPayTestMerchant',
            },
            order: {
              description: 'Автомобиль DeLorean DMC-12',
              orderNumber: new Date().getTime().toString(),
              amount: 55000,
            }
        });
        mtsPaySession.init();
    });
</script>

##### Параметры `new MtsPay({})`

<i class="param">merchant</i> <mark class="required"></mark> <mark class="object"></mark>

Объект с информацией о продавце. <br>
Содержит в себе параметр `login`

<div class="indent">
<div><i class="param">login</i> <mark class="required"></mark> <mark class="string"></mark></div>
Логин продавца(мерчанта) в платежном шлюзе. Выдается мерчанту при регистрации в платежном шлюзе. Можно уточнить у поддержки.
</div>

<i class="param">order</i> <mark class="required"></mark> <mark class="object"></mark>

Объект с информацией о заказе. <br>
Содержит в себе следующие параметры:

<div class="indent">
<div><i class="param">amount</i> <mark class="required"></mark> <mark class="number"></mark></div>

Сумма заказа в <u>минорных единицах</u>. Например, для 5 рублей 30 копеек - 530.
 
<div><i class="param">currency</i> <mark class="optional"></mark><mark class="string"></mark></div>
Валюта заказа. Циферный код валюты согласно [ISO 4217](https://www.iso.org/ru/iso-4217-currency-codes.html) <br>
Например, RUB - 643, USD - 840, EUR - 978 <br>
Значение по умолчанию: `643`

<i class="param">clientId</i> <mark class="optional"></mark> <mark class="string"></mark>

Идентификатор клиента. Требуется для функционала "Сохраненные карты"(связки), когда система узнает пользователя и предлагает к оплате карты, которые он сохранял ранее.

<i class="param">orderNumber</i> <mark class="optional"></mark> <mark class="string"></mark> 

Номер заказа в системе магазина. Можно не указывать, если в платежном шлюзе  выставлена настройка "Система генерирует номер заказа".
 
<i class="param">depositFlag</i> <mark class="optional"></mark> <mark class="string"></mark>

Флаг двухстадийной оплаты. Может принимать 2 значения:<br>
`PRE_AUTH` - двустадийный платеж<br>
`PURCHASE` - одностадийный платеж<br>
Значение по умолчанию: `PURCHASE`;
 
<i class="param">sessionExpiredDate</i> <mark class="optional"></mark> <mark class="string"></mark>

Дата истечения платежной сессии. Задается в формате `2022-04-22T09:09:00.443+00:00`
 
<i class="param">description</i> <mark class="optional"></mark> <mark class="string"></mark>

Описание заказа
 
<i class="param">orderParams</i> <mark class="optional"></mark> <mark class="object"></mark>

Дополнительные параметры заказа, которые можно передать в платежный шлюз. Можно передавать в формате ключ - значение.

```js
  "orderParams" :  {
     "customParamKey" : "customParamValue" 
  }
```
 
<i class="param">orderBundle</i> <mark class="optional"></mark> <mark class="object"></mark>

Корзина заказа

<div class="indent">
<i class="param">cartItems</i><mark class="optional"></mark> <mark class="array"></mark>

Массив  с объектами, описывающие товарные позиции. <br>
Пример:
```js
cartItems: [
	{
		positionId: 'i1',
		name: 'Кроссовки Bosco Sport 42',
		quantity: {
			measure: 'шт',
			value: '1',
		},
		itemAmount: 800000,
		itemCode: 'c1',
	},
	{
		positionId: 'i2',
		name: 'Злаковый батончик PumBar',
		quantity: {
		  measure: 'шт',
		  value: '2',
		},
		itemAmount: 10000,
		itemPrice: 5000,
		itemCode: 'c2',
	}
]
```

> **Важно!**
> Сумма товаров в корзине должна быть точно такой же как и `order.amount`

<div class="indent">
<i class="param">positionId</i><mark class="optional"></mark> <mark class="string"></mark>

Уникальный идентификатор товарной позиции внутри корзины заказа.

<i class="param">name</i><mark class="optional"></mark> <mark class="string"></mark>

Наименование или описание товарной позиции в свободной форме.

<i class="param">itemPrice</i><mark class="optional"></mark> <mark class="string"></mark>

Стоимость одной товарной позиции в минимальных единицах валюты.

<i class="param">itemAmount</i><mark class="optional"></mark> <mark class="string"></mark>

Сумма стоимости всех товарных позиций одного positionId в минимальных единицах валюты. <br>
`itemAmount` обязателен к передаче, только если не был передан параметр `itemPrice`. В противном случае передача `itemAmount` не требуется. <br>
Если же в запросе передаются оба параметра: `itemPrice` и `itemAmount`, то `itemAmount` должен равняться `itemPrice * quantity`, в противном случае запрос завершится с ошибкой.

<i class="param">itemCode</i><mark class="optional"></mark> <mark class="string"></mark>

Номер (идентификатор) товарной позиции в системе магазина.

<i class="param">quantity</i><mark class="optional"></mark> <mark class="object"></mark>

Общее количество товарных позиций одного `positionId` и их меру измерения.

<div class="indent">
<i class="param">measure</i><mark class="optional"></mark> <mark class="string"></mark>

Мера измерения количества товарной позиции.

<i class="param">value</i><mark class="optional"></mark> <mark class="string"></mark>

Количество товарных позиций данного `positionId`. 
Для указания дробных чисел используйте десятичную точку.

</div>
</div>
</div>
</div>
 
 
<i class="param">email</i> <mark class="optional"></mark> <mark class="string"></mark>

Электронная почта покупателя. На неё платежный шлюз отправит чек об операции.
 
<i class="param">phone</i> <mark class="optional"></mark> <mark class="string"></mark>

Телефон покупателя.  Если его указать, то он предзаполнится при вызове Mts Pay.  <br>
10 цифр. Указывается в формате `9000000000`
 
<i class="param">successUrl</i> <mark class="optional"></mark> <mark class="string"></mark>

Ссылка, на которую нужно перенаправить пользователя после успешной оплаты. <br>
Например: `https://example.com/success` <br>
По итогу к ссылке добавятся параметры `mdOrder` (идентификатор заказа в платежном шлюзе)

<i class="param">failUrl</i> <mark class="optional"></mark> <mark class="string"></mark>

Ссылка, на которую нужно перенаправить пользователя после неудачной оплаты. <br> 
Например: `https://example.com/fail` <br> 
По итогу к ссылке добавятся параметры `mdOrder` (идентификатор заказа в платежном шлюзе)

##### Пример MTS Pay c корзиной
```js
document.addEventListener('DOMContentLoaded', () => {
    window.mtsPayModule.onReady((MtsPay) => {
        // Создание кнопки MtsPay
        const mtsPayButtonElement = MtsPay.createButtonElement({ phrase: 'Купить'});
        document.querySelector('#example4').append(mtsPayButtonElement);

        // Описание платежной сессии заказа
        const mtsPaySession = new MtsPay({
            buttonElement: mtsPayButtonElement,
            merchant: {
                login: 'mtsPayTestMerchant',
            },
            order: {
                description: 'Спортивные товары в SportSensey',
                orderNumber: new Date().getTime().toString(),
                amount: 810000,
                phone: '9000000000',
                email: 'test@test.ru',
                successUrl: 'https://example.com/success',
                failUrl: 'https://example.com/fail',
                orderBundle: {
                    cartItems: [
                        {
                            positionId: 'i1',
                            name: 'Кроссовки Bosko Sport 42',
                            quantity: {
                                measure: 'шт',
                                value: '1',
                            },
                            itemAmount: 800000,
                            itemCode: 'c1',
                        },
                        {
                            positionId: 'i2',
                            name: 'Злаковый батончик PumBar',
                            quantity: {
                                measure: 'шт',
                                value: '2',
                            },
                            itemAmount: 10000,
                            itemPrice: 5000,
                            itemCode: 'c2',
                        }
                    ]
                }
            }
        });

        // Инициализация платежной сессии  
        mtsPaySession.init();
    });
});
```

<div id="example4"></div>

<script>
document.addEventListener('DOMContentLoaded', () => {
    window.mtsPayModule.onReady((MtsPay) => {
        // Создание кнопки MtsPay
        const mtsPayButtonElement = MtsPay.createButtonElement({ phrase: 'Купить'});
        document.querySelector('#example4').append(mtsPayButtonElement);

        // Описание платежной сессии заказа
        const mtsPaySession = new MtsPay({
            buttonElement: mtsPayButtonElement,
            merchant: {
                login: 'mtsPayTestMerchant',
            },
            order: {
                description: 'Спортивные товары в SportSensey',
                orderNumber: new Date().getTime().toString(),
                amount: 810000,
                phone: '9000000000',
                email: 'test@test.ru',
                successUrl: 'https://example.com/success',
                failUrl: 'https://example.com/fail',
                orderBundle: {
                    cartItems: [
                        {
                            positionId: 'i1',
                            name: 'Кроссовки Bosko Sport 42',
                            quantity: {
                                measure: 'шт',
                                value: '1',
                            },
                            itemAmount: 800000,
                            itemCode: 'c1',
                        },
                        {
                            positionId: 'i2',
                            name: 'Злаковый батончик PumBar',
                            quantity: {
                                measure: 'шт',
                                value: '2',
                            },
                            itemAmount: 10000,
                            itemPrice: 5000,
                            itemCode: 'c2',
                        }
                    ]
                }
            }
        });

        // Инициализация платежной сессии  
        mtsPaySession.init();
    });
});

</script>

## Cобытия MTS Pay
MTS Pay имеет внутренние события для более гибкой настройки платежа. События позволяют сайту магазина (который использует MTS Pay) гибко реагировать на поведение пользователя внутри MTS Pay. <br>
Событие нужно передавать как параметр в функцию `mtsPaySession.on()`


### MtsPay.Event.openDialog
Пользователь нажал кнопку оплаты MTS Pay. <br>
Пример:
```js
mtsPaySession.on(MtsPay.Event.openDialog, () => {
  // Ваш код, который выполнится после того как пользователь нажал кнопку оплаты MTS Pay
  console.info('Пользователь нажал кнопку оплаты');
});
```

### MtsPay.Event.CloseDialog
Пользователь закрыл окно оплаты.<br>
Пример:
```js
mtsPaySession.on(MtsPay.Event.CloseDialog, () => {
  // Ваш код, который выполнится после того как пользователь закрыл окно оплаты MTS Pay. 
  console.info('Пользователь закрыл окно оплаты');
});
```


### MtsPay.Event.UnfinishedOperation
Пользователь закрыл окно в момент опроса статуса оплаты. Т.е. оплата могла пройти успешно, однако пользователь недождался экрана с подтверждением этой информации.<br>
Пример:
```js
mtsPaySession.on(MtsPay.Event.UnfinishedOperation, () => {
  // Ваш код, который выполнится после того как пользователь закрыл окно оплаты MTS Pay в момент опроса статуса оплаты
  console.info('Пользователь закрыл окно в момент опроса статуса оплаты');
});

```


### MtsPay.Event.ChangePaymentStatus
Изменение статуса оплаты. Принимает параметры `status` и `orderId`
Для корректного определения статуса рекомендуется использовать метод `MtsPay.PendingStatuses.includes(status)` и `MtsPay.SuccessfulStatuses.includes(status)` <br>
`orderId` - id заказа внутри платежного шлюза МТС-Банка.<br>

Пример:
```js
mtsPaySession.on(MtsPay.Event.ChangePaymentStatus, ({ status, orderId }) => {

  if (MtsPay.PendingStatuses.includes(status)) {
    console.log('🕒️ Завершение операции.');
    
  } else if (MtsPay.SuccessfulStatuses.includes(status)) {
    console.log('✔️ Оплата выполнена УСПЕШНО.');
    
  } else {
    console.log('❌ Оплата выполнена НЕУСПЕШНО.');
  }
  
  console.log(`Статус заказа: ${status}. Номер заказа ${orderId}`);
});
```

### Пример
```js
const bgColors = [
  "linear-gradient(to right, #00b09b, #96c93d)",
  "linear-gradient(to right, #ff5f6d, #ffc371)",
  "linear-gradient(to right, #9a9a9a, #bdbdbd)",
];

function showToast(text, colorIndex) {
  Toastify({
    text: text,
    close: true,
    style: {
      background: bgColors[colorIndex],
    }
  }).showToast();
}

document.addEventListener('DOMContentLoaded', () => {
  window.mtsPayModule.onReady((MtsPay) => {
    // Создание кнопки MtsPay
    const mtsPayButtonElement = MtsPay.createButtonElement({ phrase: 'Купить'});
    document.querySelector('#example5').append(mtsPayButtonElement);

    // Описание платежной сессии заказа
    const mtsPaySession = new MtsPay({
        buttonElement: mtsPayButtonElement,
        merchant: {
            login: 'mtsPayTestMerchant',
        },
        order: {
            description: 'Герои Меча и Магии',
            orderNumber: new Date().getTime().toString(),
            amount: 101500,
            phone: '9000000000',
            email: 'test@test.ru'
        }
    });

    // Инициализация платежной сессии  
    mtsPaySession.init();

    // Слушаем события MTS Pay
    mtsPaySession.on(MtsPay.Event.ChangePaymentStatus, ({ status, orderId }) => {
      if (MtsPay.PendingStatuses.includes(status)) {
          showToast('🕒️ Завершение операции.', 2);
          
        } else if (MtsPay.SuccessfulStatuses.includes(status)) {
          showToast('✔️ Оплата выполнена УСПЕШНО', 0);
          
        } else {
          showToast('❌ Оплата выполнена НЕУСПЕШНО.', 1);
        }

        showToast(`Статус заказа: ${status}. Номер заказа ${orderId}`, 2);
      });

      mtsPaySession.on(MtsPay.Event.openDialog, () => {
        showToast('Пользователь нажал кнопку оплаты', 2);
      });

      mtsPaySession.on(MtsPay.Event.CloseDialog, () => {
        showToast('Пользователь закрыл окно оплаты', 2);
      });

      mtsPaySession.on(MtsPay.Event.UnfinishedOperation, () => {
        showToast('Пользователь закрыл окно в момент опроса статуса оплаты', 2);
      });

      mtsPaySession.on('*', (event, data) => {
        showToast(`${event}: ${JSON.stringify(data)}`, 2);
      });
  });
}); 

```

<link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/npm/toastify-js/src/toastify.min.css">
<script type="text/javascript" src="https://cdn.jsdelivr.net/npm/toastify-js"></script>

<div id="example5"></div>
<script>
const bgColors = [
  "linear-gradient(to right, #00b09b, #96c93d)",
  "linear-gradient(to right, #ff5f6d, #ffc371)",
  "linear-gradient(to right, #9a9a9a, #bdbdbd)",
];

function showToast(text, colorIndex) {
  Toastify({
    text: text,
    close: true,
    duration: -1,
    style: {
      background: bgColors[colorIndex],
    }
  }).showToast();
}

document.addEventListener('DOMContentLoaded', () => {
  window.mtsPayModule.onReady((MtsPay) => {
    // Создание кнопки MtsPay
    const mtsPayButtonElement = MtsPay.createButtonElement({ phrase: 'Купить'});
    document.querySelector('#example5').append(mtsPayButtonElement);

    // Описание платежной сессии заказа
    const mtsPaySession = new MtsPay({
        buttonElement: mtsPayButtonElement,
        merchant: {
            login: 'mtsPayTestMerchant',
        },
        order: {
            description: 'Герои Меча и Магии',
            orderNumber: new Date().getTime().toString(),
            amount: 101500,
            phone: '9000000000',
            email: 'test@test.ru'
        }
    });

    // Инициализация платежной сессии  
    mtsPaySession.init();

    // Слушаем события MTS Pay
    mtsPaySession.on(MtsPay.Event.ChangePaymentStatus, ({ status, orderId }) => {
      if (MtsPay.PendingStatuses.includes(status)) {
          showToast('🕒️ Завершение операции.', 2);
          
        } else if (MtsPay.SuccessfulStatuses.includes(status)) {
          showToast('✔️ Оплата выполнена УСПЕШНО', 0);
          
        } else {
          showToast('❌ Оплата выполнена НЕУСПЕШНО.', 1);
        }

        showToast(`Статус заказа: ${status}. Номер заказа ${orderId}`, 2);
      });

      mtsPaySession.on(MtsPay.Event.openDialog, () => {
        showToast('Пользователь нажал кнопку оплаты', 2);
      });

      mtsPaySession.on(MtsPay.Event.CloseDialog, () => {
        showToast('Пользователь закрыл окно оплаты', 2);
      });

      mtsPaySession.on(MtsPay.Event.UnfinishedOperation, () => {
        showToast('Пользователь закрыл окно в момент опроса статуса оплаты', 2);
      });

      mtsPaySession.on('*', (event, data) => {
	      debugger;
        showToast(`${event}: ${JSON.stringify(data)}`, 2);
      });
  });
}); 
</script>


## mtsPaySession.updateOrder() - обновление информации в сессии
Иногда требуется без перезагрузки страницы обновить информацию о цене, составе корзины, описания прямо в реальном времени. Для этого можно использовать метод `.updateOrder()`

Пример:
```html
<div id="controls" style="margin-bottom: 20px">

Сумма (в копейках): <input type="number" name="amount" value="9900" /><button type="button" id="apply">Изменить сумму</button>

</div>


<div id="example6"></div>


<script id="main-script">
document.addEventListener('DOMContentLoaded', () => {
  window.mtsPayModule.onReady((MtsPay) => {
    const mtsPayButtonElement = MtsPay.createButtonElement();
    document.querySelector('#example6').append(mtsPayButtonElement);

    const mtsPaySession = new MtsPay({
      buttonElement: mtsPayButtonElement,
      merchant: {
        login: 'mtsPayTestMerchant',
      },
      order: {
        description: 'Тестовый заказ',
        orderNumber: new Date().getTime().toString(),
        amount: Number(document.querySelector('[name="amount"]').value),
      },
    });

    mtsPaySession.init();

    document.querySelector('#apply').addEventListener('click', () => {
      mtsPaySession.updateOrder({
        ...mtsPaySession.options.order,
        amount: Number(document.querySelector('[name="amount"]').value),
      });
    });
  });
});
</script>
```

<div id="controls" style="margin-bottom: 20px">
Сумма (в копейках): <input type="number" name="amount" value="9900" /><button type="button" id="apply" class="button" >Изменить сумму</button>
</div>


<div id="example6"></div>

<script id="main-script">
document.addEventListener('DOMContentLoaded', () => {
  window.mtsPayModule.onReady((MtsPay) => {
    const mtsPayButtonElement = MtsPay.createButtonElement();
    document.querySelector('#example6').append(mtsPayButtonElement);

    const mtsPaySession = new MtsPay({
      buttonElement: mtsPayButtonElement,
      merchant: {
        login: 'mtsPayTestMerchant',
      },
      order: {
        description: 'Тестовый заказ',
        orderNumber: new Date().getTime().toString(),
        amount: Number(document.querySelector('[name="amount"]').value),
      },
    });

    mtsPaySession.init();

    document.querySelector('#apply').addEventListener('click', () => {
      mtsPaySession.updateOrder({
        ...mtsPaySession.options.order,
        amount: Number(document.querySelector('[name="amount"]').value),
      });
    });
  });
});

</script>

## mtsPaySession.destroy() - демонтаж кнопки
Метод `mtsPaySession.destroy()` используется для корректного удаления кнопки из DOM-дерева.

Пример:
```html
<div id="controls" style="margin-bottom: 20px">
  <button type="button" id="destroy">mtsPay.destroy()</button>
  <button type="button" id="destroyRemoveButton">mtsPay.destroy({removeButton: true})</button>
</div>

<div id="example7"></div>

<script>
  document.addEventListener('DOMContentLoaded', () => {
    window.mtsPayModule.onReady((MtsPay) => {
      const mtsPayButtonElement = MtsPay.createButtonElement();
      document.querySelector('#example7').append(mtsPayButtonElement);

      const mtsPaySession = new MtsPay({
        buttonElement: mtsPayButtonElement,
        merchant: {
          login: 'mtsPayTestMerchant',
        },
        order: {
          description: 'Тестовый заказ',
          orderNumber: '12345',
          amount: 5500,
        },
      });

      mtsPaySession.init();

      document.querySelector('#destroy').addEventListener('click', () => {
        mtsPaySession.destroy();
      });

      document.querySelector('#destroyRemoveButton').addEventListener('click', () => {
        mtsPaySession.destroy({ removeButton: true });
      });
    })
  });
</script>
```


<div id="controls" style="margin-bottom: 20px">
  <button type="button" class="button" id="destroy">mtsPay.destroy()</button>
  <button type="button" class="button"  id="destroyRemoveButton">mtsPay.destroy({removeButton: true})</button>
</div>

<div id="example7"></div>
<script>
  document.addEventListener('DOMContentLoaded', () => {
    window.mtsPayModule.onReady((MtsPay) => {
      const mtsPayButtonElement = MtsPay.createButtonElement();
      document.querySelector('#example7').append(mtsPayButtonElement);

      const mtsPaySession = new MtsPay({
        buttonElement: mtsPayButtonElement,
        merchant: {
          login: 'mtsPayTestMerchant',
        },
        order: {
          description: 'Тестовый заказ',
          orderNumber: '12345',
          amount: 5500,
        },
      });

      mtsPaySession.init();

      document.querySelector('#destroy').addEventListener('click', () => {
        mtsPaySession.destroy();
      });

      document.querySelector('#destroyRemoveButton').addEventListener('click', () => {
        mtsPaySession.destroy({ removeButton: true });
      });
    })
  });
</script>


## Определения статуса платежа
Для корректного и честного определения, что оплата по MTS Pay прошла рекомендуется делать реализацию через бек-офиc (backend).

### payment/status.do

Например, после того, как вы получили событие `MtsPay.Event.ChangePaymentStatus`, что оплата выполнена успешно,  <br>
магазин должен через backend сделать **POST** запрос с заголовком `Content-Type: application/json` и телом запроса `mdOrder: <orderId>`

где `<orderId>` - id заказа в платежном шлюзе. 
Его можно получить, либо через `MtsPay.Event.ChangePaymentStatus`,  <br>
либо взять из QUERY-параметра `orderId` для `successUrl` / `failUrl`.
Запрос делается на следующий адрес: <br>

**Для тестовой среды**
```
https://web.rbsuat.com/mtspay/payment/status.do
```

**Для продуктовой среды**
```
https://oplata.mtsbank.ru/mtspay/payment/status.do
```

### Поля ответа

<i class="param">success</i><mark class="boolean"></mark>

<i class="param">error</i><mark class="object"></mark>

<div class="indent">
<i class="param">code</i><mark class="string"></mark>

<i class="param">message</i><mark class="string"></mark>
</div>

<i class="param">data</i><mark class="object"></mark>

<div class="indent">
<i class="param">status</i><mark class="string"></mark>
</div>

## Тестовые данные для проверки
**Номер телефона** для проверки `9000000000` <br>
Будет некоторое время "грузить", затем перейдете ко второму шагу, выбору способа оплаты <br><br>

**Тестовая карта** <br>
card: `4111 1111 1111 1111` <br>
expiry: `12/24`    cvc: `123` <br><br>

**Код СМС, для подтверждения оплаты по карте** <br>
`12345678` <br>