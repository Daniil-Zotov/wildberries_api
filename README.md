#### 25.05.2022

Wildberries API 1.0.2 OAS3  
https://suppliers-api.wildberries.ru/swagger/index.html  
Официальная документация (swagger)

Реализация методов API Wildberries в сервисе Postman
https://www.postman.com/bblkovo/workspace/wildberies/api/e04926ff-d77a-4bd5-95d0-d0f94d124ee6

# Описание работы API Wildberries

1. [Вступление](#intro)  
2. [Особенности работы системы:](#special)  
3. [Аутентификация с помощью токена](#auth)  
4. Работа с ценами  
    + [Загрузка цен. За раз можно загрузить не более 1000 номенклатур. (POST​/public​/api​/v1​/prices)](#POST​-public​-api​-v1​-prices)  
    + [Получение информации по номенклатурам, их ценам, скидкам и промокодам. Если не указывать фильтры, вернётся весь товар. (GET​/public​/api​/v1​/info)](#GET​-public​-api​-v1​-info)  
5. Промокоды и скидки  
    + [Установка скидок для номенклатур. Максимальное количество номенклатур на запрос - 1000 (POST​/public​/api​/v1​/updateDiscounts)](#POST​-public​-api​-v1​-updateDiscounts)  
    + [Сброс скидок для номенклатур (POST​/public​/api​/v1​/revokeDiscounts)](#POST​-public​-api​-v1​-revokeDiscounts)  
    + [Установка промокодов для номенклатур. Максимальное количество номенклатур на запрос - 1000 (POST​/public​/api​/v1​/updatePromocodes)](#POST​-public​-api​-v1​-updatePromocodes)  
    + [Сброс промокодов для номенклатур (POST​/public​/api​/v1​/revokePromocodes)](#POST​-public​-api​-v1​-revokePromocodes)  
6. Marketplace  
    + [Возвращает список поставок (GET​/api​/v2​/supplies)](#GET​-api​-v2​-supplies)  
    + [Создаёт новую поставку (POST​/api​/v2​/supplies)](#POST​-api​-v2​-supplies)  
    + [Добавляет к поставке заказы (PUT​/api​/v2​/supplies​/{id})](#PUT​-api​-v2​-supplies-id)  
    + [Закрывает поставку (POST​/api​/v2​/supplies​/{id}​/close)](#POST​-api​-v2​-supplies-id-close)  
    + [Возвращает штрихкод поставки в заданном формате (GET​/api​/v2​/supplies​/{id}​/barcode)](#GET​-api​-v2​-supplies-id-barcode)  
    + [Возвращает список заказов, закреплённых за поставкой (GET​/api​/v2​/supplies​/{id}​/orders)](#GET​-api​-v2​-supplies-id-orders)  
    + [Возвращает список товаров поставщика с их остатками (GET​/api​/v2​/stocks)](#GET​-api​-v2​-stocks)  
    + [Обновляет остатки товаров (POST​/api​/v2​/stocks)](#POST​-api​-v2​-stocks)  
    + [Удаляет остатки товаров (DELETE​/api​/v2​/stocks)](#DELETE​-api​-v2​-stocks)  
    + [Возвращает список складов поставщика (GET​/api​/v2​/warehouses)](#GET​-api​-v2​-warehouses)  
    + [Возвращает список сборочных заданий поставщика. (GET​/api​/v2​/orders)](#GET​-api​-v2​-orders)  
    + [Обновляет статус переданных сборочных заданий. (PUT​/api​/v2​/orders)](#PUT​-api​-v2​-orders)  
    + [Возвращает список стикеров по переданному массиву сборочных заданий. (POST​/api​/v2​/orders​/stickers)](#POST​-api​-v2​-orders​-stickers)  
    + [Возвращает список стикеров в формате pdf по переданному массиву сборочных заданий. (POST​/api​/v2​/orders​/stickers​/pdf)](#POST​-api​-v2​-orders​-stickers​-pdf)  
7. [Работа с карточками товара](#products-card)
     + [Создание одной карточки (POST​/card​/create)](#POST​-card​-create)  
     + [Создание группы карточек (POST​/card​/batchCreate)](#POST​-card​-batchCreate)  
     + [Получить список карточек поставщика с фильтром и сортировкой (POST​/card​/list)](#POST​-card​-list)  
     + [Получение карточки поставщика по imt id (POST​/card​/cardByImtID)](#POST​-card​-cardByImtID)  
     + [Обновить карточку (POST​/card​/update)](#POST​-card​-update)  
     + [Удалить номенклатуру из карточки (POST​/card​/deleteNomenclature)](#POST​-card​-deleteNomenclature)  
     + [Сгенерировать шк (POST​/card​/getBarcodes)](#POST​-card​-getBarcodes)  
     + [Загрузить файл в хранилище (POST​/card​/upload​/file​/multipart)](#POST​-card​-upload​-file​-multipart)  
     + [Выгрузить файл из хранилища (GET​/card​/file​/{supplierID}​/{fileID})](#GET​-card​-file​-supplierID-fileID)  
8. Конфигуратор полей карточки  
    + [Получение конфигурации предмета (GET​/api​/v1​/config​/get​/object​/translated)](#GET​-api​-v1​-config​-get​-object​-translated)  
    + [Поиск предмета по паттерну (GET​/api​/v1​/config​/get​/object​/list)](#GET​-api​-v1​-config​-get​-object​-list)  
    + [Справочник основных и дополнительных цветов (GET​/api​/v1​/directory​/colors)](#GET​-api​-v1​-directory​-colors)  
    + [Справочник пол (GET​/api​/v1​/directory​/kinds)](#GET​-api​-v1​-directory​-kinds)  
    + [Справочник стран (GET​/api​/v1​/directory​/countries)](#GET​-api​-v1​-directory​-countries)  
    + [Справочник коллекций (GET​/api​/v1​/directory​/collections)](#GET​-api​-v1​-directory​-collections)  
    + [Справочник сезонов (GET​/api​/v1​/directory​/seasons)](#GET​-api​-v1​-directory​-seasons)  
    + [Справочник комплектации (GET​/api​/v1​/directory​/contents)](#GET​-api​-v1​-directory​-contents)  
    + [Справочник составов (GET​/api​/v1​/directory​/consists)](#GET​-api​-v1​-directory​-consists)  
    + [Справочник тнвэд (GET​/api​/v1​/directory​/tnved)](#GET​-api​-v1​-directory​-tnved)  
    + [Справочник дополнительных свойств (GET​/api​/v1​/directory​/options)](#GET​-api​-v1​-directory​-options)  
    + [Справочник брендов (GET​/api​/v1​/directory​/brands)](#GET​-api​-v1​-directory​-brands)  
    + [Справочник систем измерений (GET​/api​/v1​/directory​/si)](#GET​-api​-v1​-directory​-si)  
    + [Справочник значений для дополнительных свойств (GET​/api​/v1​/directory​/ext)](#GET​-api​-v1​-directory​-ext)  
    + [Справочник российских размеров (GET​/api​/v1​/directory​/wbsizes)](#GET​-api​-v1​-directory​-wbsizes)  
    + [Все доступные справочники (GET​/api​/v1​/directory​/get​/list)](#GET​-api​-v1​-directory​-get​-list)  
    + [Все доступные предметы (GET​/api​/v1​/config​/get​/object​/all)](#GET​-api​-v1​-config​-get​-object​-all)  
    + [Все паренты (GET​/api​/v1​/config​/get​/object​/parent​/list)](#GET​-api​-v1​-config​-get​-object​-parent​-list)  
    + [Получение списка объектов по паренту (GET​/api​/v1​/config​/object​/byparent)](#GET​-api​-v1​-config​-object​-byparent)  


<a name="POST​-public​-api​-v1​-prices"></a>
<a name="GET​-public​-api​-v1​-info"></a>
<a name="POST​-public​-api​-v1​-updateDiscounts"></a>
<a name="POST​-public​-api​-v1​-revokeDiscounts"></a>
<a name="POST​-public​-api​-v1​-updatePromocodes"></a>
<a name="POST​-public​-api​-v1​-revokePromocodes"></a>
<a name="GET​-api​-v2​-supplies"></a>
<a name="POST​-api​-v2​-supplies"></a>
<a name="PUT​-api​-v2​-supplies-id"></a>
<a name="POST​-api​-v2​-supplies-id-close"></a>
<a name="GET​-api​-v2​-supplies-id-barcode"></a>
<a name="GET​-api​-v2​-supplies-id-orders"></a>
<a name="GET​-api​-v2​-stocks"></a>
<a name="POST​-api​-v2​-stocks"></a>
<a name="DELETE​-api​-v2​-stocks"></a>
<a name="GET​-api​-v2​-warehouses"></a>
<a name="GET​-api​-v2​-orders"></a>
<a name="PUT​-api​-v2​-orders"></a>
<a name="POST​-api​-v2​-orders​-stickers"></a>
<a name="POST​-api​-v2​-orders​-stickers​-pdf"></a>
<a name="GET​-api​-v1​-config​-get​-object​-translated"></a>
<a name="GET​-api​-v1​-config​-get​-object​-list"></a>
<a name="GET​-api​-v1​-directory​-colors"></a>
<a name="GET​-api​-v1​-directory​-kinds"></a>
<a name="GET​-api​-v1​-directory​-countries"></a>
<a name="GET​-api​-v1​-directory​-collections"></a>
<a name="GET​-api​-v1​-directory​-seasons"></a>
<a name="GET​-api​-v1​-directory​-contents"></a>
<a name="GET​-api​-v1​-directory​-consists"></a>
<a name="GET​-api​-v1​-directory​-tnved"></a>
<a name="GET​-api​-v1​-directory​-options"></a>
<a name="GET​-api​-v1​-directory​-brands"></a>
<a name="GET​-api​-v1​-directory​-si"></a>
<a name="GET​-api​-v1​-directory​-ext"></a>
<a name="GET​-api​-v1​-directory​-wbsizes"></a>
<a name="GET​-api​-v1​-directory​-get​-list"></a>
<a name="GET​-api​-v1​-config​-get​-object​-all"></a>
<a name="GET​-api​-v1​-config​-get​-object​-parent​-list"></a>
<a name="GET​-api​-v1​-config​-object​-byparent"></a>


<details><summary>Старое меню</summary>

###  Создание карточки/карточек товаров.
[ Create. `https://suppliers-api.wildberries.ru/card/create`](#create-card)  
[ BatchCreate](#batch-create)  
[ Получение карточки/карточек.](#CardByImtID)  
### **CardByImtID**. `https://suppliers-api.wildberries.ru/card/cardByImtID` 
[ Обновление карточки.](#update-card)  
#### Create. `https://suppliers-api.wildberries.ru/card/update`
[ Удаление номенклатуры](#delete-nomenclature)  
[ List. `https://suppliers-api.wildberries.ru/card/list`](#list-card)  
[ Генерация ШК для карточки.](#get-barcode)  
#### GetBarcodes. `https://suppliers-api.wildberries.ru/card/getBarcodes`   
[ Описание процесса загрузки файлов](#upload)  
[ Files. https://suppliers-api.wildberries.ru/card/upload/file/multipart](#multipart)  
[ Добавление файла в карточку товара](#card-create)  
[ Добавление файла со стороннего ресурса в карточку товара](#foregin-files)  
[ Сервис конфигурации предметов и характеристик объекта.](#config-items)  
[ Поиск ключа объекта](#find-key-obj)  
[ Получение списка доступных справочников](#get-dir-list)  
[ Получение ТНВЭД](#get-tnved)  
[ Получение данных справочника](#get-dir-data)  
[ Получение всех данных справочника](#get-dir-all-data)  

</details>




#  <a name="intro"></a> Вступление:

Документ описывает основные методы необходимые для работы с API Wildberries

Официальная документация в swagger [https://suppliers-api.wildberries.ru/swagger/index.html](https://suppliers-api.wildberries.ru/swagger/index.html)

Для начала работ **обязательно** необходимо убедится, что Вы **входили** на [https://suppliers-portal.wildberries.ru/](https://suppliers-portal.wildberries.ru/) в качестве поставщика со своим номером телефона. [В личном кабинете поставщика](https://suppliers-portal.wildberries.ru/ui-user-profile) номер телефона должен быть связан с поставщиком иначе доступа для работы с карточками товара не будет.

Всё взаимодействие ведётся в рамках протокола [json-rpc](https://www.jsonrpc.org/)

Номер телефона должен быть связан также с учётной записью на сайте [https://www.wildberries.ru/](https://www.wildberries.ru/)


https://t.me/wildberriesApiForDev  
⚠️ Не официальная группа по обсуждению API Wildberries

https://t.me/wbofficialchat  
🔗 Чат по общим вопросам.  


#  <a name="special"></a> Особенности работы системы:

1. Тестового окружения для поставщиков не предусмотрено. Все карточки сразу создаются в продуктовой среде. В случае ошибок, для исправления которых нет методов в API можно обращаться в службу поддержки с темой **Заявка на API Content**
2. Цены для карточек указываются на момент создания - это требование системы. Изменение цен происходит в разделе ["Цены и скидки"](https://suppliers-portal.wildberries.ru/discount/setDiscounts). Также можно воспользоваться [API](https://suppliers-api.wildberries.ru/swagger/index.html) 

# <a name="auth"></a> Аутентификация с помощью токена

При каждом запросе на сервер API в заголовке запроса в поле `Authorization` необходимо указывать токен доступа.  
Для того чтобы получить `токен` требуется перейти в раздел [Доступ к новому API](https://suppliers-portal.wildberries.ru/supplier-settings/access-to-new-api).

*Раздел и генерация токена доступна только владельцу аккаунта!*

Указать имя токена и нажать кнопку ` Сгенерировать токен`
Вам будет предоставлен токен доступа для работы с API - его сразу необходимо скопировать.  
При повторном заходе на страницу получения токена скопировать уже выпущенные токены не удастся.  
Время жизни токена не ограничено, но его можно отозвать (удалить).  
На странице будет доступна информация о дате создания и дате последнего использования токена.  
Токен доступа представляет собой jwt-токен, состоящий из 3 частей: тип и алгоритм шифрования, "accessID" пользователя, подпись токена - для проверки его целостности.  
Проверить на валидность токен можно на https://jwt.io/ 

<details><summary>Пример запроса:</summary>  
    
```json
POST https://suppliers-api.wildberries.ru/card/cardByImtID
Content-Type: application/json
Authorization: eyJhbGciOiJIUznR5cCI6IkpXVCJ9.eyJhY2Nlc3NJRCI6IjNlOTA1ZmEyLWNFjMy1iZWZjLTM3YmMwMTNlZTNjNSJ9.MGymMDsOb8o7

{
    "id": "4cdf17da-5e7b-4c56-9531-7437d44a13fb",
    "jsonrpc": "2.0",
    "params": {
        // Идентификатор карточки. Можно получить методом "List", который рассмотрен ниже.
        "imtID": 0
    }
}
```
</details>

#  <a name="products-card"></a> Работа с карточками товара



<a name=POST​-card​-batchCreate></a>
<a name=POST​-card​-list></a>
<a name=POST​-card​-cardByImtID></a>
<a name=POST​-card​-update></a>
<a name=POST​-card​-deleteNomenclature></a>
<a name=POST​-card​-getBarcodes></a>
<a name=POST​-card​-upload​-file​-multipart></a>
<a name=GET​-card​-file​-supplierID-fileID></a>



Перед началом работы, если есть необходимость в изучении API на примере — можно посмотреть принцип работы [https://suppliers-portal.wildberries.ru/goods/products-card/](https://suppliers-portal.wildberries.ru/goods/products-card/)  
Через инструмент разработчика - сеть.  
Все запросы идентичны и отличаются лишь заголовками и URL

###  <a name="POST​-card​-create"></a> Создание одной карточки (POST /card/create)

**Описание**: метод позволяет создать одну новую карточку товара.

<details><summary>Заголовок запроса:</summary>  
    
```  
POST https://suppliers-api.wildberries.ru/card/create
Content-Type: application/json
Authorization: {{token}}
```
</details>

Параметры запроса- отсутствуют  

<details><summary>Тело запроса выглядит следующим образом:</summary>  
    
```json
   {
        // Идентификатор отправляемого запроса. Служит для сопоставления ответа отправленному запросу. Необходимо генерировать уникальные идентификаторы для каждого запроса. Во избежание пересечений с другими поставщиками, рекомендуется избегать простых идентификаторов, таких как 1, 2, 3 и т.д.
        "id": "8a41f7a8-6ed1-4910-bbd3-ac83e214ec81",                                                    
        // Версия протокола. Всегда должна быть "2.0".
        "jsonrpc": "2.0",                                           
        // Параметры.
        "params": {                                                 
            "card": {                                             
                    // Страна проиводитель. 
                    "countryProduction": "string",                      
                    // Категория товара (Джинсы, Книги и другие).
                    "object": "string",            
                    // Артикул поставщика.
                    "supplierVendorCode": "string",
                    // Структура, содержащая характеристики карточки, общие для всех номенклатур и размеров.
                    "addin": [                                          
                        {
                            // Название характеристики. Пример: "Бренд"
                            "type": "string",                           
                            // Массив значений характеристики. У характеристик, содержащих одно значение, массив будет содержать только 1 элемент. Пример: "{"type": "Бренд", "params": [{"value": "Имя_бренда"}]}".
                            "params": [                                 
                                {
                                    // Численное значение характеристики.
                                    "count": 0,                         
                                    // Единицы измерения характеристики ("см", "%" и другие).
                                    "units": "string",                  
                                    // Текстовое значение характеристики ("Имя_бренда").
                                    "value": "string"                   
                                }
                            ]
                        }
                    ],
                    // Массив номенклатур товара. 
                    "nomenclatures": [                                  
                        {
                            // Артикул товара.
                            "vendorCode": "string",                     
                            // Массив вариаций товара. Одна цена - один размер - одна вариация.
                            "variations": [                             
                                {
                                    // Штрихкод товара.
                                    "barcode": "string",                
                                    // Структура, содержащая характеристики конкретной вариации товара.
                                    "addin": [                               
                                        {
                                            // Название характеристики.
                                            "type": "string",           
                                            // Массив значений характеристики. У характеристик, содержащих одно значение, массив будет содержать только 1 элемент. Пример: "{"type": "Размер", "params": [{"value": "S"}]}".
                                            "params": [                  
                                                {
                                                    // Численное значение характеристики.
                                                    "count": 0,      
                                                    // Единицы измерения характеристики.
                                                    "units": "string",  
                                                    // Текстовое значение характеристики.
                                                    "value": "string"   
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ],
                            // Структура, содержащая характеристики конкретной номенклатуры.
                            "addin": [                                  
                                {
                                    // Название характеристики
                                    "type": "string",                   
                                    // Массив значений характеристики. У характеристик, содержащих одно значение, массив будет содержать только 1 элемент. Пример: "{"type": "Основной цвет", "params": [{"value": "Красный"}]}".
                                    "params": [                          
                                        {
                                            // Численное значение характеристики.
                                            "count": 0,                 
                                            // Единицы измерения характеристики.
                                            "units": "string",          
                                            // Текстовое значение характеристики.
                                            "value": "string"           
                                        }
                                    ]
                                }
                            ]
                        }
                    ]
                } 
        }
    }
```
    
</details>
<details><summary>Пример запроса:</summary>

```json
POST https://suppliers-api.wildberries.ru/card/create
Content-Type: application/json
Authorization: {{token}}

{
  "params": {
    "card": {
      "countryProduction": "Россия",
      "object": "Джинсы",
      "addin": [
        {
          "type": "Состав",
          "params": [
            {
              "value": "хлопок",
              "count": 100
            }
          ]
        },
        {
          "type": "Бренд",
          "params": [
            {
              "value": "ЛОГОС"
            }
          ]
        },
        {
          "type": "Комплектация",
          "params": [
            {
              "value": "Джинсы - 1 шт"
            }
          ]
        },
        {
          "type": "Тнвэд",
          "params": [
            {
              "value": "6203411000"
            }
          ]
        },
        {
          "type": "Пол",
          "params": [
            {
              "value": "Мужской"
            }
          ]
        }
      ],
      "nomenclatures": [
        {
          "vendorCode": "bluee-123",
          "variations": [
            {
              "barcode": "2001925979004",
              "addin": [
                {
                  "type": "Розничная цена",
                  "params": [
                    {
                      "count": 2222
                    }
                  ]
                },
                {
                  "type": "Размер",
                  "params": [
                    {
                      "value": "56"
                    }
                  ]
                },
                {
                  "type": "Рос. размер",
                  "params": [
                    {
                      "value": "42"
                    }
                  ]
                }
              ]
            }
          ],
          "addin": [
            {
              "type": "Фото",
              "params": []
            },
            {
              "type": "Фото360",
              "params": []
            },
            {
              "type": "Видео",
              "params": []
            }
          ]
        }
      ]
    }
  },
  "jsonrpc": "2.0",
  "id": "json-rpc_8"
}
```

</details>
    
    
Ответ:

```json
{"id":"8a41f7a8-6ed1-4910-bbd3-ac83e214ec81","jsonrpc":"2.0","result":{}}
```

###  <a name="batch-create"></a> BatchCreate

`https://suppliers-api.wildberries.ru/card/batchCreate` **Описание**: метод позволяет создавать сразу много карточек.



<details><summary>Тело запроса выглядит следующим образом:</summary>

```json
POST https://suppliers-api.wildberries.ru/card/batchCreate
Content-Type: application/json
Authorization: {{token}}

{
  "id": "30d03c9e-809b-5c5d-84d3-f9a43c79f5d9",
  "jsonrpc": "2.0",
  "params": {
    "card": [
      {
        "countryProduction": "Россия",
        "object": "Джинсы",
        "addin": [
          {
            "type": "Состав",
            "params": [
              {
                "value": "хлопок",
                "count": 100
              }
            ]
          },
          {
            "type": "Бренд",
            "params": [
              {
                "value": "ЛОГОС"
              }
            ]
          },
          {
            "type": "Комплектация",
            "params": [
              {
                "value": "Джинсы - 1 шт"
              }
            ]
          },
          {
            "type": "Тнвэд",
            "params": [
              {
                "value": "6203411000"
              }
            ]
          },
          {
            "type": "Пол",
            "params": [
              {
                "value": "Мужской"
              }
            ]
          }
        ],
        "nomenclatures": [
          {
            "vendorCode": "bluee-123",
            "variations": [
              {
                "barcode": "2001925979004",
                "addin": [
                  {
                    "type": "Розничная цена",
                    "params": [
                      {
                        "count": 2222
                      }
                    ]
                  },
                  {
                    "type": "Размер",
                    "params": [
                      {
                        "value": "56"
                      }
                    ]
                  },
                  {
                    "type": "Рос. размер",
                    "params": [
                      {
                        "value": "42"
                      }
                    ]
                  }
                ]
              }
            ],
            "addin": [
              {
                "type": "Фото",
                "params": []
              },
              {
                "type": "Фото360",
                "params": []
              },
              {
                "type": "Видео",
                "params": []
              }
            ]
          }
        ]
      }
    ]
  }
}
```

</details>
Ответ:

```json
{"id":"30d03c9e-809b-5c5d-84d3-f9a43c79f5d9","jsonrpc":"2.0","result":{}}
```

**ADDIN** `Addin` - структура, хранящая в себе характеристики товаров, которые могут различаться у разных категорий товаров. Она состоит из следующих полей:

```
"type" - название характеристики товара
"params" - массив значений характеристики
```

`params`, в свою очередь, содержит следующие поля для более удобного хранения характеристик:

```
"value" - текстовое значение характеристики
"count" - числовое значение характеристики
"units" - единицы измерения характеристики
```

Все характеристики для определённой категории товаров можно получить, совершив следующий запрос:

```
GET https://suppliers-api.wildberries.ru/api/v1/config/get/object/translated?name=Кроссовки
Authorization: {{token}}
```

В результате в формате `json` вернётся список характеристик данной категории товаров (в примере используется категория `Кроссовки`) и требования к ним. Получение списка возможных категорий товаров будет описано ниже в пункте “Поиск ключа объекта”. Некоторые характеристики требуется заполнять из словарных значений. Для получения списка возможных значений характеристик используется следующий запрос:

```
GET https://suppliers-api.wildberries.ru/api/v1/directory/brands?pattern=nike&top=50
Authorization: {{token}}
```

В данном запросе имеется 3 параметра: `pattern` позволяет указать шаблон для поиска значения характеристики; `lang` - обязательный параметр, на данный момент используется только `ru`; `top` - ограничение по количеству объектов, если не указано - 10 шт.

Список всех доступных категорий можно получить запросом

```
GET https://suppliers-api.wildberries.ru/api/v1/config/get/object/all?top=10000
Authorization: {{token}}
```

###  <a name="CardByImtID"></a> Получение карточки/карточек.

Для получения карточек существует метод:

### **CardByImtID**. `https://suppliers-api.wildberries.ru/card/cardByImtID`

**Описание**: метод позволяет получить карточку поставщика с указанным ID. Тело запроса выглядит следующим образом:

```json
{
        "id": "4cdf17da-5e7b-4c56-9531-7437d44a13fb",
        "jsonrpc": "2.0", 
        "params": {
            // Идентификатор карточки. Можно получить методом "List", который рассмотрен ниже.
            "imtID": 0    
        }
}
```

<details><summary>Ответ:</summary>

```json
{
  "id": "4cdf17da-5e7b-4c56-9531-7437d44a13fb",
  "jsonrpc": "2.0",
  "result": {
    "card": {
      "id": "2d1e2646-ba13-52cd-8bec-3210b8302b7f",
      "imtId": 18907504,
      "userId": 0,
      "imtSupplierId": 0,
      "object": "Джинсы",
      "parent": "Одежда",
      "countryProduction": "Россия",
      "supplierVendorCode": "",
      "addin": [
        {
          "type": "Бренд",
          "params": [
            {
              "value": "ЛОГОС"
            }
          ]
        },
        {
          "type": "Пол",
          "params": [
            {
              "value": "Мужской"
            }
          ]
        },
        {
          "type": "Описание",
          "params": [
            {
              "value": ""
            }
          ]
        },
        {
          "type": "Тнвэд",
          "params": [
            {
              "value": "6203411000"
            }
          ]
        },
        {
          "type": "Состав",
          "params": [
            {
              "value": "хлопок",
              "count": 100,
              "units": "%"
            }
          ]
        },
        {
          "type": "Комплектация",
          "params": [
            {
              "value": "Джинсы - 1 шт"
            }
          ]
        }
      ],
      "nomenclatures": [
        {
          "id": "07a1f28a-a8f7-4501-94ea-ef2bf65eae01",
          "nmId": 25626080,
          "vendorCode": "bluee-123",
          "variations": [
            {
              "id": "8d140bf8-d9ca-4864-857c-01167920b267",
              "chrtId": 59602201,
              "barcode": "2001925979004",
              "addin": [
                {
                  "type": "Размер",
                  "params": [
                    {
                      "value": "56"
                    }
                  ]
                },
                {
                  "type": "Рос. размер",
                  "params": [
                    {
                      "value": "42"
                    }
                  ]
                }
              ],
              "errors": null
            }
          ],
          "addin": [
            {
              "type": "Коллекция",
              "params": [
                {
                  "value": "Базовая коллекция"
                }
              ]
            }
          ]
        }
      ],
      "createdAt": "2021-03-30T15:32:45.39408587Z",
      "updatedAt": "2021-03-30T15:32:45.39408587Z",
      "uploadID": "00000000-0000-0000-0000-000000000000"
    }
  }
}
```

</details>

### <a name="update-card"></a> Обновление карточки.

#### Create. `https://suppliers-api.wildberries.ru/card/update`

**Описание**: метод позволяет обновить одну карточку товара.

Для того чтобы обновить карточку предпочтительнее, запросить её из сервиса методом  `/card/cardByImtID` и в уже полученной структуре менять поля.


<details><summary>Пример тела для обновление карточки:</summary>

```json
{
  "params": {
    "card": {
      "id": "2d1e2646-ba13-52cd-8bec-3210b8302b7f",
      "imtId": 18907504,
      "countryProduction": "Россия",
      "object": "Джинсы",
      "addin": [
        {
          "type": "Бренд",
          "params": [
            {
              "value": "ЛОГОС"
            }
          ]
        },
        {
          "type": "Комплектация",
          "params": [
            {
              "value": "Джинсы - 1 шт"
            }
          ]
        },
        {
          "type": "Тнвэд",
          "params": [
            {
              "value": "6203411000"
            }
          ]
        },
        {
          "type": "Состав",
          "params": [
            {
              "value": "хлопок перкаль",
              "count": 100
            }
          ]
        },
        {
          "type": "Пол",
          "params": [
            {
              "value": "Мужской"
            }
          ]
        },
        {
          "type": "Ключевые слова",
          "params": [
            {
              "value": "Слово1"
            },
            {
              "value": "слово2"
            }
          ]
        }
      ],
      "nomenclatures": [
        {
          "nmId": 25626080,
          "vendorCode": "bluee-123",
          "variations": [
            {
              "barcode": "2001925979004",
              "chrtId": 59602201,
              "addin": [
                {
                  "type": "Розничная цена",
                  "params": [
                    {
                      "count": 0
                    }
                  ]
                },
                {
                  "type": "Размер",
                  "params": [
                    {
                      "value": "56"
                    }
                  ]
                },
                {
                  "type": "Рос. размер",
                  "params": [
                    {
                      "value": "42"
                    }
                  ]
                }
              ]
            }
          ],
          "addin": [
            {
              "type": "Коллекция",
              "params": [
                {
                  "value": "Базовая коллекция"
                }
              ]
            },
            {
              "type": "Фото",
              "params": []
            },
            {
              "type": "Фото360",
              "params": []
            },
            {
              "type": "Видео",
              "params": []
            }
          ]
        }
      ]
    }
  },
  "jsonrpc": "2.0",
  "id": "e7ba66f5-bdde-48b5-9e14-ea6a285bf57"
}
```
    
</details>

Ответ:

```json
{"id":"e7ba66f5-bdde-48b5-9e14-ea6a285bf57","jsonrpc":"2.0","result":{}}
```


### <a name="delete-nomenclature"></a> Удаление номенклатуры

Метод POST `https://suppliers-api.wildberries.ru/card/deleteNomenclature`

**Описание**: метод позволяет удалить номенклатуру из карточки поставщика с указанным ID. Тело запроса выглядит следующим образом:

```json
{
        "id": "1",
        "jsonrpc": "2.0", 
        "params": {
            // Идентификатор номенклатуры. 
            "nomenclatureID": 0  
        }
}
```

Пример запроса:
```json
POST https://suppliers-api.wildberries.ru/card/deleteNomenclature
Content-Type: application/json
Authorization: {{token}}

{
    "id": "1",
    "jsonrpc": "2.0",
    "params": {
    "nomenclatureID": 12862200
    }
}
```
Ответ
```json
{
  "id": "1",
  "jsonrpc": "2.0",
  "result": {}
}
```

### <a name="list-card"></a> List. `https://suppliers-api.wildberries.ru/card/list`

**Описание**: метод позволяет получить список карточек по указанным параметрам. Фильтрация позволяет исключить из итогового списка карточек те, в которых указанное поле `column` содержит значение `excludedValues`. Поиск позволяет оставить в итоговом списке карточек только те, у которых поле `column` имеет значение `search`, если это число, если это строка, то значение поля начинается с `search`. Сортировка позволяет отсортировать список по полю `column` в порядке `order`. `query` содержит значения `limit` и `offset` который указывают соответственно на максимальное количество карточек, которые надо вывести и на количество карточек, которые с самого начала списка нужно пропустить. Наименования полей соответствуют пути до этого поля через точку. Так, например, чтобы добраться до поля `barcode`, понадобится путь `nomenclatures.variations.barcode`. Исключения - параметры, лежащие внутри структуры `addin`. Чтобы добраться до них, требуется в пути после `addin` через точку указать `type` этого параметра. Например, чтобы получить `бренд`, потребуется путь `addin.Бренд`. `Бренд` написан с большой буквы, так как `type` был написан тоже с большой. Тело запроса выглядит следующим образом:

```json
    {
        "id": "1",
        "jsonrpc": "2.0",
        "params": {
            "filter": {
                // Поиск в соответсвии с условиями запроса
                "find": [
                  {
                    "column": "imtId", // поиск по ИМТ id (Доступные поля для поискаописаны ниже )
                    "search": 19247 // значение типа int
                  }
                ],
                // Сортировка по указанному полю в указанном порядке.
                "order": {                                                      
                    "column": "createdAt",
                    "order": "asc"
                }
            },
            // Пагинация. Вывести максимум 10 карточек после пропуска 20. Выведутся карточки с 20 по 30 из тех, которые соотетствуют фильтру.
            "query": {                                                          
                "limit": 10,
                "offset": 20
            },
            "withError": true // параметр указывающий, что вернуться только карточки в которых есть ошибки, которые не удалось создать. Параметр не обязательный, если его не указывать вернуться только созадныне карточки.
        }
    }
```

В результате вышеприведённого запроса нам вернутся все карточки поставщика `00000000-0000-0000-0000-000000000000`, среди которых не будет карточек с красными цветами и джинс, у всех карточек будут товары с размером “M”. И все эти карточки будут отсортированы по дате создания в порядке возрастания (сначала старые).


<details><summary>Поля доступные поля для использования в "find":</summary>

```json
{
    "column": "imtId", // поиск по ИМТ id 
    "search": 19247 // значение типа int или массив значений [123,54656,4323]
}
```

```json
{
    "column": "nomenclatures.nmId", // поиск по NM id
    "search": 19247 // значение типа int или массив значений [123,54656,4323]
}
```

```json
{
    "column": "nomenclatures.variations.chrtId", // поиск по chrtId
    "search": 60570035 // значение типа int или массив значений [123,54656,4323]
}
```

```json
{
    "column": "nomenclatures.variations.barcode", // поиск по баркоду
    "search": "2002126418002" // значение типа string или массив значений ["2002126418002","2002126418003"]
}
```

```json
{
    "column": "nomenclatures.vendorCode", // поиск по артикулу
    "search": "11" // значение типа string или массив значений ["11","12"]
}
```

```json
{
    "column": "object", // поиск по предмету
    "search": "Кофе молотый" // значение типа string или массив значений ["Кофе молотый","Носки"]
}
```
</details>


<details><summary>Пример запроса:</summary>

```json
POST https://suppliers-api.wildberries.ru/card/list
Content-Type: application/json
Authorization: {{token}}

{
  "id": "11",
  "jsonrpc": "2.0",
  "params": {
    "filter": {
      "order": {
        "column": "updatedAt",
        "order": "desc"
      }
    },
    "query": {
      "limit": 1,
      "offset": 0
    }
  }
}
```
    
</details>

<details><summary>Ответ</summary>

```json
{
  "id": "11",
  "jsonrpc": "2.0",
  "result": {
    "cards": [
      {
        "id": "e7ba66f5-bdde-48b5-9e14-ea6a285bf57",
        "imtId": 1403347,
        "userId": 1,
        "imtSupplierId": 8759,
        "object": "Свитшоты",
        "countryProduction": "Китай",
        "supplierVendorCode": "артикулдлясвитшотов",
        "addin": [
          {
            "type": "Состав",
            "params": [
              {
                "value": "хлопок"
              }
            ]
          },
          {
            "type": "Тнвэд",
            "params": [
              {
                "value": "610590900"
              }
            ]
          },
          {
            "type": "Бренд",
            "params": [
              {
                "value": "WB"
              }
            ]
          },
          {
            "type": "Комплектация",
            "params": [
              {
                "value": "Свитшот базовый"
              }
            ]
          },
          {
            "type": "Пол",
            "params": [
              {
                "value": "Женский"
              }
            ]
          },
          {
            "type": "Ключевые слова",
            "params": [
              {
                "value": "Слово1"
              },
              {
                "value": "слово2"
              }
            ]
          }
        ],
        "nomenclatures": [
          {
            "id": "b06b93a5-083a-4d74-80f9-83e140be2f",
            "nmId": 1889397,
            "photos": [],
            "vendorCode": "синий",
            "variations": [
              {
                "id": "f572767f-1fd3-4409-99df-a314fda22b",
                "chrtId": 5082952,
                "barcode": "2001114123800",
                "addin": [
                  {
                    "type": "Розничная цена",
                    "params": [
                      {
                        "count": 50000
                      }
                    ]
                  },
                  {
                    "type": "Размер",
                    "params": [
                      {
                        "value": "44"
                      }
                    ]
                  },
                  {
                    "type": "Рос. размер",
                    "params": [
                      {
                        "value": "32"
                      }
                    ]
                  }
                ],
                "errors": []
              }
            ],
            "photoStatus": "",
            "status": "",
            "addin": [
              {
                "type": "Фото",
                "params": [
                  {
                    "value": "https://img1.wildberries.ru/big/new/18890000/18890000-1.jpg"
                  }
                ]
              },
              {
                "type": "Фото360",
                "params": []
              },
              {
                "type": "Видео",
                "params": []
              }
            ]
          }
        ],
        "createdAt": "2021-01-27T11:44:11.322Z",
        "updatedAt": "2021-01-27T11:44:11.322Z"
      }
    ],
    "cursor": {
      "total": 1000,
      "limit": 1,
      "offset": 0
    }
  }
}
```
</details>

### <a name="get-barcode"></a> Генерация ШК для карточки.

Для того чтобы сгенерировать шк для размера требуется вызвать метод: 
#### GetBarcodes. `https://suppliers-api.wildberries.ru/card/getBarcodes` 
**Описание**: генерации ШК для размера Тело запроса выглядит следующим образом:

```json
   {
        "id": "{{uuid}}", // uuid запроса
        "jsonrpc": "2.0", 
        "params": {
            // Количество ШК которые необходимо сгенерировать
            "quantity": 1
        }
    }
```

Пример ответа:

```json
{
  "id": "deb3a313-c168-4e2a-bb9f-b126e185c3bb",
  "jsonrpc": "2.0",
  "result": {
    "barcodes": [
      "2000429418026"
    ]
  }
}
```

#  <a name="upload"></a> Описание процесса загрузки файлов

Для работы с запросами требуется пройти аутентификацию пользователя.

### <a name="multipart"></a> Files. https://suppliers-api.wildberries.ru/card/upload/file/multipart

Заголовок должен содержать следующее поля:

- X-File-ID – сгенерированный идентификатор файла в формате uuid v4, его в дальнейшем и надо передавать в карточку товара. Идентификатор поставщик генерирует своими силами.
- Authorization – токен полученный в личном кабинете (пример WBToken=AvvYxgfMn7P0C8zCuPQLQhkkkt-C…)
- 
Время жизни файла во временном хранилище не более 2 суток, после этого он автоматически удалится

В тело запроса передаётся файл. Пример запроса:

```json
POST https://suppliers-api.wildberries.ru/card/upload/file/multipart
Authorization: {{token}}
Content-Type: multipart/form-data; boundary=boundaryImage
X-File-Id: 00000000-0000-0000-0000-000000000001

--boundaryImage
Content-Disposition: form-data; name="uploadfile"; filename="photo.jpg"

bytes photo.jpg
--boundaryImage--
```

Пример CURL запроса который можно использовать для загрузки файла:

```
$ curl -X POST --location "https://suppliers-api.wildberries.ru/upload/file/multipart" \
    -H "Authorization: {{token}}" \
    -H "X-File-id: 00000000-0000-0000-0000-000000000001" \
    -H "Content-Type: multipart/form-data; boundary=img" \
    -F "uploadfile=@Downloads/photo.jpg;filename=photo.jpg;type=*/*"
```


### <a name="card-create"></a> Добавление файла в карточку товара

Для добавления файла надо создать или обновить карточку товара

Create. https://suppliers-api.wildberries.ru/card/create

<details><summary>Запрос</summary>

```json
{
  "id": "8a41f7a8-6ed1-4910-bbd3-ac83e214ec8e",
  "jsonrpc": "2.0",
  "params": {
    "card": {
      "object": "Мячики",
      "countryProduction": "Россия",
      "supplierVendorCode": "svc-100",
      "nomenclatures": [
        {
          "vendorCode": "test-with-photo",
          "variations": [
            {
              "barcode": "4603374564721",
              "addin": [
                {
                  "type": "Размер",
                  "params": [
                    {
                      "value": "4"
                    }
                  ]
                },
                {
                  "type": "Розничная цена",
                  "params": [
                    {
                      "count": 70000,
                      "units": "рублей"
                    }
                  ]
                }
              ]
            }
          ],
          "addin": [
           {
            "type": "Фото",
            "params": [
             {
              "value": "e3ee6410-a09b-4dfe-a84b-ce8946abc521",
              "units": "images/jpeg"
             }
            ]
           },
            {
              "type": "Основной цвет",
              "params": [
                {
                  "value": "Синий"
                }
              ]
            }
          ]
        }
      ],
      "addin": [
        {
          "type": "Бренд",
          "params": [
            {
              "value": "adidas"
            }
          ]
        },
        {
          "type": "Описание",
          "params": [
            {
              "value": "Описание"
            }
          ]
        },
        {
          "type": "Пол",
          "params": [
            {
              "value": "Мужской"
            }
          ]
        },
        {
          "type": "Ключевые слова",
          "params": [
            {
              "value": "Слово1"
            },
            {
              "value": "слово2"
            }
          ]
        },
        {
          "type": "Материал изделия",
          "params": [
            {
              "value": "Полиуретан"
            }
          ]
        }
      ]
    }
  }
}
```

</details>

После синхронизаций с системами фото удаляется из хранилища и перемещается на CDN в связи с этим меняется секция:

```json

           {
            "type": "Фото",
            "params": [
             {
              "value": "e3ee6410-a09b-4dfe-a84b-ce8946abc521",
              "units": "images/jpeg"
             }
            ]
           },
```

На подобную:

```json

{
              "type": "Фото",
              "params": [
                {
                  "value": "https://img1.wildberries.ru/big/new/17640000/17620024-1.jpg"
                }
              **]
}
```

### <a name="foregin-files"></a> Добавление файла со стороннего ресурса в карточку товара

Для добавления файла надо создать или обновить карточку товара

Create. https://suppliers-api.wildberries.ru/card/create



Для добавления медиафайла со стороннего ресурса необходимо добавить в номенклатуру

<details><summary>Пример</summary>
    
```bigquery
"addin": [
    {
        "type": "Фото",
        "params": [
         {
          "value": "http://images.wbstatic.net/c516x688/new/13190000/13194759-1.jpg",
         }
        ]
    },
    {
        "type": "Фото360",
        "params": [
         {
          "value": "http://images.wbstatic.net/c516x688/new/13190000/13194759-1.jpg",
         }
        ]
    },
    {
        "type": "Видео",
        "params": [
         {
          "value": "http://images.wbstatic.net/c516x688/new/13190000/13194759-1.mp4",
         }
        ]
    }
]
```

```json
{
  "id": "8a41f7a8-6ed1-4910-bbd3-ac83e214ec8e",
  "jsonrpc": "2.0",
  "params": {
    "card": {
      "object": "Мячики",
      "countryProduction": "Россия",
      "supplierVendorCode": "svc-100",
      "nomenclatures": [
        {
          "vendorCode": "test-with-photo",
          "variations": [
            {
              "barcode": "4603374564721",
              "addin": [
                {
                  "type": "Размер",
                  "params": [
                    {
                      "value": "4"
                    }
                  ]
                },
                {
                  "type": "Розничная цена",
                  "params": [
                    {
                      "count": 70000,
                      "units": "рублей"
                    }
                  ]
                }
              ]
            }
          ],
          "addin": [
           {
            "type": "Фото",
            "params": [
             {
              "value": "http://images.wbstatic.net/c516x688/new/13190000/13194759-1.jpg",
             }
            ]
           },
            {
              "type": "Основной цвет",
              "params": [
                {
                  "value": "Синий"
                }
              ]
            }
          ]
        }
      ],
      "addin": [
        {
          "type": "Бренд",
          "params": [
            {
              "value": "adidas"
            }
          ]
        },
        {
          "type": "Описание",
          "params": [
            {
              "value": "Описание"
            }
          ]
        },
        {
          "type": "Пол",
          "params": [
            {
              "value": "Мужской"
            }
          ]
        },
        {
          "type": "Ключевые слова",
          "params": [
            {
              "value": "Слово1"
            },
            {
              "value": "слово2"
            }
          ]
        },
        {
          "type": "Материал изделия",
          "params": [
            {
              "value": "Полиуретан"
            }
          ]
        }
      ]
    }
  }
}
```

    
</details>
#  <a name="config-items"></a> Сервис конфигурации предметов и характеристик объекта.

Требуется для того чтобы сконфигурировать карточку товара

Список всех методов доступен по адресу [https://suppliers-api.wildberries.ru/swagger/index.html](https://suppliers-api.wildberries.ru/swagger/index.html#/%D0%9A%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%82%D0%BE%D1%80%20%D0%BF%D0%BE%D0%BB%D0%B5%D0%B9%20%D0%BA%D0%B0%D1%80%D1%82%D0%BE%D1%87%D0%BA%D0%B8)

###  <a name="find-key-obj"></a> Поиск ключа объекта

Для осуществления поиска ключа следует выполнить GET запрос например: `https://suppliers-api.wildberries.ru/api/v1/config/get/object/list?pattern=игр` В полученном ответе требуется обратить внимание на столбик с названиями на русском языке. Именно они являются названиями категорий товаров и должны использоваться при создании карточек в поле `object`.

```json
{
  "additionalErrors": null,
  "data": {
    "Toy phones": "Игровые телефоны",
    "Pet toys": "Игрушки для животных",
    "Bathroom toys": "Игрушки для ванной",
    "Play mats": "Игровые коврики",
    "Toy food": "Игрушечные продукты",
    "Play sets": "Игровые наборы",
    "Toys for adults": "Игрушки для взрослых",
    "Toy kitchenware": "Игрушечная посуда",
    "Game tents": "Игровые палатки",
    "Baby crib mobiles": "Игрушки-подвески",
    "Toy parking": "Игрушечные парковки",
    "Toy garages": "Игрушечные гаражи",
    "Games (digital content)": "Игры (цифровой контент)",
    "Antistress toys": "Игрушки антистресс",
    "Toy arms": "Игрушечное оружие",
    "Toy musical instruments": "Игрушечные музыкальные инструменты",
    "Game consoles": "Игровые консоли",
    "Toy vehicles": "Игровая техника",
    "Toys": "Игрушки-дергунчики",
    "Toy instruments": "Игрушечные инструменты",
    "Cat game furniture": "Игровые комплексы для кошек",
    "Baby game centers": "Игровые центры для малышей"
  },
  "error": false,
  "errorText": ""
}
```

###  <a name="get-dir-list"></a> Получение списка доступных справочников

Метод GET `https://suppliers-api.wildberries.ru/api/v1/directory/get/list`

```json
{
  "additionalErrors": null,
  "data": {
    "/options": 5599,
    "/wbsizes": 70758,
    "/si": 123,
    "/countries": 254,
    "/seasons": 33,
    "/consists": 11280,
    "/brands": 102895,
    "/factories": 142690,
    "/ext": 313208,
    "/colors": 372,
    "/kinds": 7,
    "/collections": 69,
    "/contents": 10009,
    "/tech-sizes": 124391
  },
  "error": false,
  "errorText": ""
}
```

###  <a name="get-tnved"></a> Получение ТНВЭД

```json
GET https://suppliers-api.wildberries.ru/api/v1/directory/tnved?subject=%D0%9C%D0%B0%D1%81%D0%BB%D0%B0
Authorization: {{token}}
```

###  <a name="get-dir-data"></a> Получение данных справочника

Пример получения значения из справочника `"/options"`, для получения данных следует выполнить GET запрос: `https://suppliers-api.wildberries.ru/api/v1/directory/options?pattern=Ширина&top=10` Как и в случае с категориями товаров, из ответа данного запроса требуется извлечь поля `translate` и использовать для создания карточки.

<details><summary>Полный пример создания карточки с учётом всех справочников:</summary>

```json
{
  "additionalErrors": null,
  "data": [
    {
      "key": "Processing width",
      "translate": "Ширина обработки"
    },
    {
      "key": "Strap width",
      "translate": "Ширина ремешка"
    },
    {
      "key": "Curtain width",
      "translate": "Ширина штор"
    },
    {
      "key": "Working area width",
      "translate": "Ширина рабочей площади"
    },
    {
      "key": "Finished model width",
      "translate": "Ширина готовой модели"
    },
    {
      "key": "Work surface width",
      "translate": "Ширина рабочей поверхности"
    },
    {
      "key": "Neck Width",
      "translate": "Ширина грифа"
    },
    {
      "key": "Installed Tent Width",
      "translate": "Ширина установленной палатки"
    },
    {
      "key": "Kerf width",
      "translate": "Ширина пропила"
    },
    {
      "key": "Frame width",
      "translate": "Ширина оправы"
    }
  ],
  "error": false,
  "errorText": ""
}
```
    
</details>

###  <a name="get-dir-all-data"></a> Получение всех данных справочника

Пример получения значения из справочника `"/options"`, для получения данных следует выполнить GET запрос: `https://suppliers-api.wildberries.ru/api/v1/directory/options?lang=ru&top=10`

<details><summary>Полный пример создания карточки с учётом всех справочников:</summary>

```json
{
  "additionalErrors": null,
  "data": [
    {
      "key": "Picture painting",
      "translate": "Рисунок картины"
    },
    {
      "key": "Filter view",
      "translate": "Вид фильтра"
    },
    {
      "key": "Number of rolls",
      "translate": "Количество рулонов"
    },
    {
      "key": "Installation furnaces",
      "translate": "Печи по установке"
    },
    {
      "key": "Minimum staple size",
      "translate": "Минимальный размер скоб"
    },
    {
      "key": "Type of constructor",
      "translate": "Тип конструктора"
    },
    {
      "key": "MKL diameter",
      "translate": "Диаметр МКЛ"
    },
    {
      "key": "Number of stations",
      "translate": "Количество станций"
    },
    {
      "key": "Print Resolution (Color)",
      "translate": "Разрешение печати (цветная)"
    }
  ],
  "error": false,
  "errorText": ""
}
```
    
</details>

<details><summary>Полный пример создания карточки с учётом всех справочников:</summary>
```json
{
 "params": {
  "card": [
   {
    "countryProduction": "Россия",
    "supplierVendorCode": "qwe-112",
    "object": "Куртки",
    "addin": [
     {
      "type": "Состав",
      "params": [
       {
        "value": "Кожа и текстиль",
        "count": 100
       }
      ]
     },
     {
      "type": "Тнвэд",
      "params": [
       {
        "value": "6101209000"
       }
      ]
     },
     {
      "type": "Бренд",
      "params": [
       {
        "value": "SNOB ARMY"
       }
      ]
     },
     {
      "type": "Комплектация",
      "params": [
       {
        "value": "куртка"
       }
      ]
     },
     {
      "type": "Пол",
      "params": [
       {
        "value": "Мужской"
       }
      ]
     },
     {
      "type": "Описание",
      "params": [
       {
        "value": "Описание"
       }
      ]
     },
      {
        "type": "Ключевые слова",
        "params": [
          {
            "value": "Слово1"
          },
          {
            "value": "слово2"
          }
        ]
      }
    ],
    "nomenclatures": [
     {
      "vendorCode": "black-123",
      "variations": [
       {
        "barcode": "2001092382003",
        "addin": [
         {
          "type": "Розничная цена",
          "params": [
           {
            "count": 17000
           }
          ]
         },
         {
          "type": "Размер",
          "params": [
           {
            "value": "56"
           }
          ]
         },
         {
          "type": "Рос. размер",
          "params": [
           {
            "value": "56"
           }
          ]
         }
        ]
       }
      ],
      "addin": [
       {
        "type": "Основной цвет",
        "params": [
         {
          "value": "черный"
         }
        ]
       },
       {
        "type": "Коллекция",
        "params": [
         {
          "value": "Осень-Зима 2021-2022"
         }
        ]
       },
       {
        "type": "Фото",
        "params": []
       },
       {
        "type": "Фото360",
        "params": []
       },
       {
        "type": "Видео",
        "params": []
       }
      ]
     }
    ]
   }
  ]
 },
 "jsonrpc": "2.0",
 "id": "8a41f7a8-6ed1-4910-bbd3-ac83e214ec81"
}
```

</details>
