# api hrm messenger

PHP Фасад для API HrMessenger (hrmessenger.com)

#### Схема работы API
https://miro.com/app/board/uXjVKHFfUB0=/

#### Реализация
 - API: реализация запросов к api сервису `Head Hunter`
 - Servcie: Фасад для класса API
   
### Использование Api
```php
use and_y87/api_hr_messenger/ApiHrMessenger;
use and_y87/api_hr_messenger/dto/HrMessengerApiRequisites;
use and_y87/api_hr_messenger/tools/CacheProvider;

// Add `CacheProvider`
class RedisCacheProvider extends CacheProvider
{
    public function getValue(string $key )
    {
        Yii::$app->redis->get( $key );
    }

    public function setValue( string $key, string $value )
    {
        Yii::$app->redis->set( $key, value );
    }
}

// Create object `CacheProvider`
$redisCacheProvider = new RedisCacheProvider();

// Create object `Requisites`
$hrMessengerApiRequisites = new HrMessengerApiRequisites( $client_id, $client_secret );

// Create object `Api`
$apiHrMessenger = ApiHrMessenger( $hrMessengerApiRequisites, $redisCacheProvider );

// Use `Api`
```

### Исходная документация API `hrmessenger`: 
 - https://api.hrmessenger.com
