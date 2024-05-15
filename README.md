# api hrm messenger

## IN PROGRESS

PHP Фасад для API HrMessenger (hrmessenger.com)

#### Реализация
 - API: реализация запросов к api сервису `HrMessenger`
 - Servcie: Фасад для класса API
   
### Использование Api
Методы Api возвращают массив с данными.
```php
use and_y87\api_hr_messenger\ApiHrMessenger;
use and_y87\api_hr_messenger\dto\HrMessengerApiRequisites;
use and_y87\api_hr_messenger\cache\CacheProvider;

// Add `CacheProvider`
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

// Create object `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Create object `Requisites`
$hrMessengerApiRequisites = new HrMessengerApiRequisites( $client_id, $client_secret );

// Create object `Api`
$apiHrMessenger = ApiHrMessenger( $hrMessengerApiRequisites, $redisCacheProvider );

// Use `Api`
$data = $apiHrMessenger->me(); // return array
```
### Использование Service
Методы Service возвращают Объекты с данными.
```php
use and_y87\api_hr_messenger\service\HrMessengerService;

//Вводная часть при использовании сервиса аналогична Api

// Create object `Service`
$hrMessengerService = new HrMessengerService($apiHrMessenger);

// Use `Service`
$me = $hrMessengerService->me(); // return and_y87\api_hr_messenger\response\Me();
```

#### Схема работы API
![Схема работы API](https://static.andy87.ru/github/api/apiLogivSchema.png)

### Исходная документация API `hrmessenger`: 
 - https://api.hrmessenger.com
