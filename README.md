# providerHrMessenger

PHP Фасад для API HrMessenger (www.hrmessenger.com)

---

> [!NOTE]
> ![IN PROGRESS](http://www.bc-energy.it/wp-content/uploads/2013/08/work-in-progress.png)

---

#### Реализация
Пакет реализует запросы к API HrMessenger через репозиторий [KnockKnock](https://github.com/andy87/KnockKnock)  
<p align="center"><a href="https://github.com/andy87/KnockKnock"><img src="https://github.com/andy87/KnockKnock/blob/master/assets/logo/KnockKnockLogo_256.png?raw=true" width=256></a></p>

 - API: реализация запросов к api сервису `HrMessenger`
 - Servcie: Фасад для класса API
   
### Использование Api
Методы Api возвращают массив с данными.
```php
use and_y87\provider_hr_messenger\ApiHrMessenger;
use and_y87\aprovider_hr_messenger\dto\HrMessengerApiRequisites;
use and_y87\provider_hr_messenger\cache\CacheProvider;

// Создание класса `RedisCacheProvider`
class RedisCacheProvider extends CacheProvider
{
    public function getValue( string $key ): string
    {
        return (string) Yii::$app->redis->get( $key );
    }

    public function setValue( string $key, mixed $value ): bool
    {
        return Yii::$app->redis->set( $key, $value );
    }
}

// Создание экземпляра класса `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Создание экземпляра класса `Requisites`
$hrMessengerApiRequisites = new HrMessengerApiRequisites( $client_id, $client_secret );

// Создание экземпляра класса `Api`
$apiHrMessenger = ApiHrMessenger( $hrMessengerApiRequisites, $redisCacheProvider );

// Использование `Api`
$me = $apiHrMessenger->me(); // return array

echo $me['name']; // получение значения массива по ключу (hardcode)
```

### Использование Service
Методы Service возвращают объекты(экзмпляры классов) содержащие актуальные для endpoint свойства, согласно документации сервиса.
```php
use and_y87\api_hr_messenger\service\HrMessengerService;

//Вводная часть при использовании сервиса аналогична Api

// Создание экземпляра класса `Service`
$hrMessengerService = new HrMessengerService($apiHrMessenger);

// Использование `Service`
$me = $hrMessengerService->myInfo(); // return and_y87\api_hr_messenger\response\Me();

echo $me->name; // Получение значение из объекта через обращение к свойству
```

#### Схема работы API
![Схема работы API](https://static.andy87.ru/github/api/apiLogivSchema.png?v=3)

### Исходная документация API `hrmessenger`: 
 - https://api.hrmessenger.com
