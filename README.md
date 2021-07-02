<h1 align="center"> Weather </h1>

<p align="center">基于高德开放平台的PHP天气信息查询组件。</p>


## 安装

```shell
$ composer require imingxin/weather -vvv
```

## 配置
使用本扩展之前，你需要去 [高德开放平台](https://lbs.amap.com/dev/id/newuser) 注册账号，然后创建应用，获取应用的 API key。

## 使用

```php
use Imingxin\Weather\Weather;

$key = 'xxxxxxxxxxxxxxxxxxxxx';
$weather = new Weater($key);
```

## 获取实时天气

```php
$response = $weather->getWeather('深圳');
```

## 示例

```json
{
    "status": "1",
    "count": "1",
    "info": "OK",
    "infocode": "10000",
    "lives": [
        {
            "province": "广东",
            "city": "深圳市",
            "adcode": "440300",
            "weather": "多云",
            "temperature": "30",
            "winddirection": "西南",
            "windpower": "5",
            "humidity": "79",
            "reporttime": "2021-07-02 10:30:09"
        }
    ]
}
```

## 获取近期天气预报

```php
$response = $weather->getWeather('深圳', 'all');
```

## 示例

```json
{
	"status": "1",
	"count": "1",
	"info": "OK",
	"infocode": "10000",
	"forecasts": [{
		"city": "深圳市",
		"adcode": "440300",
		"province": "广东",
		"reporttime": "2021-07-02 10:30:09",
		"casts": [{
				"date": "2021-07-01",
				"week": "4",
				"dayweather": "多云",
				"nightweather": "多云",
				"daytemp": "33",
				"nighttemp": "27",
				"daywind": "南",
				"nightwind": "南",
				"daypower": "≤3",
				"nightpower": "≤3"
			},
			{
				"date": "2021-07-02",
				"week": "5",
				"dayweather": "多云",
				"nightweather": "多云",
				"daytemp": "32",
				"nighttemp": "27",
				"daywind": "西南",
				"nightwind": "西南",
				"daypower": "≤3",
				"nightpower": "≤3"
			},
			{
				"date": "2021-07-03",
				"week": "6",
				"dayweather": "多云",
				"nightweather": "多云",
				"daytemp": "33",
				"nighttemp": "27",
				"daywind": "北",
				"nightwind": "北",
				"daypower": "≤3",
				"nightpower": "≤3"
			},
			{
				"date": "2021-07-04",
				"week": "7",
				"dayweather": "晴",
				"nightweather": "多云",
				"daytemp": "33",
				"nighttemp": "28",
				"daywind": "北",
				"nightwind": "北",
				"daypower": "≤3",
				"nightpower": "≤3"
			}
		]
	}]
}
```

## 获取 XML 格式返回值

第三个参数为返回值类型，可选 json 与 xml，默认为 json：

```php
$response = $weather->getWeather('深圳', 'base', 'xml');
```

## 示例

```xml
<?xml version="1.0" encoding="UTF-8"?>
<response>
    <status>1</status>
    <count>1</count>
    <info>OK</info>
    <infocode>10000</infocode>
    <lives type="list">
        <live>
            <province>广东</province>
            <city>深圳市</city>
            <adcode>440300</adcode>
            <weather>多云</weather>
            <temperature>30</temperature>
            <winddirection>西南</winddirection>
            <windpower>5</windpower>
            <humidity>77</humidity>
            <reporttime>2021-07-02 11:00:12</reporttime>
        </live>
    </lives>
</response>
```

## 参数说明

```php
array|string getWeather(string $city, string $type = 'base', string $format = 'json')
```

* $city - 城市名，比如：深圳；
* $type - 返回内容类型：base 返回实时天气，all 返回预报天气；
* $format - 输出数据格式，默认为 json 格式，当 output 设置为 xml 时，输出的为 XML 格式的数据。

## 在 Laravel 中使用

在 laravel 中使用也是同样的安装方式，配置写在 `config/services.php` 中：

```php
.
.
.
'weather' => [
    'key' => env('WEATHER_API_KEY'),
]
```

然后在 .env 中配置 WEATHER_API_KEY：

```text
WEATHER_API_KEY=xxxxxxxxxxxxxxxxxxxx
```

可以使用两种方式来获取 Imingxin\Weather\Weather 实例：

## 方法参数注入

```php
.
.
.
public function show(Weather $weather)
{
    $response = $weather->getWeather('深圳');
}
```

## 服务名访问

```php
.
.
.
public function show()
{
    $response = app('weather')->getWeather('深圳');
}
```

## 参考

* [高德开放平台天气接口](https://lbs.amap.com/api/webservice/guide/api/weatherinfo/)

## License

MIT