# Huawei Push Kit PHP

> [!IMPORTANT]
> This is a replacement for a `afiqiqmal/huawei-push` package that is currently not being updated.

### Installation

```sh
composer require avto-dev/huawei-push-kit
```

### Usage

#### Get Access Token

References : [Huawei OAuth](https://developer.huawei.com/consumer/en/doc/development/HMSCore-Guides-V5/open-platform-oauth-0000001053629189-V5#EN-US_TOPIC_0000001053629189__section12493191334711)
```php
$access = HuaweiPushKit::make([
    'app_id' => 'YOUR APP ID',
    'client_secret' => 'YOUR CLIENT SECRET'
])
    ->getAccessToken();


//Laravel
$access = HuaweiPushKit::make(config('huawei'))->getAccessToken();
$access = app(HuaweiPushKit::class)->getAccessToken();
```

Response

```json
{
    "access_token": "ACCESS TOKEN",
    "expires_in": 3600,
    "token_type": "Bearer"
}
```

#### Push Message

References : [Huawei Push Kit](https://developer.huawei.com/consumer/en/doc/development/HMSCore-References-V5/https-send-api-0000001050986197-V5#EN-US_TOPIC_0000001050986197__p2559323141314)
```php
$response = HuaweiPushKit::make([])
    ->withAccessToken('ACCESS TOKEN')
    ->push(
        NotificationPayload::make()
            ->setValidateOnly(false)
            ->setMessage(
                Message::make()
                    ->setNotification(
                        Notification::make()
                            ->setTitle("Testing Title")
                            ->setBody("Body")
                            ->setImage("https://seeklogo.com/images/L/laravel-logo-41EC1D4C3F-seeklogo.com.png")
                    )
                    ->setAndroid(
                        Config::make() // AndroidConfig
                            ->setUrgency(2)
                            ->setCategory(1)
                            ->setTimeToLive(3360)
                            ->setTags('TrumpIsDown')
                            ->isStaging(true)
                            ->setNotification(
                                AndroidNotification::make() // Notification
                                    ->setClickAction(
                                        ClickAction::make()
                                        ->setType(1)
                                        ->setIntent("pushscheme://com.huawei.hms.hmsdemo/deeplink?#Intent;i.isFeed=1;S.feedDocId=0LauP4X6;end")
                                        ->setUrl('https://www.google.com')
                                    )
                                    ->setImage('https://seeklogo.com/images/L/laravel-logo-41EC1D4C3F-seeklogo.com.png')
                                    ->setIcon('/raw/ic_launcher2')
                                    ->setColor('#FFFFFF')
                                    ->setSound('/raw/shake')
                                    ->setDefaultSound(false)
                                    ->setPriority(3)
                                    ->setChannelId("HMSTestDemo")
                                    ->setAutoClear(100000) // ms
                                    ->setSummary("Summary")
                                    ->setStyle(0)
                                    ->setNotifyId(123456)

                                    ->setButtons([
                                        Button::make()->setName("Home")->setActionType(0)
                                    ])
                            )
                    )
                    ->setTopic("Topic")
            )
    );
```

Response

```json
{
    "code": "80000000",
    "msg": "Success",
    "requestId": "160502268063038626000406"
}
```



### TODO

- WebPUSH
- APNS


## License
Licensed under the [MIT license](http://opensource.org/licenses/MIT)


<a href="https://www.paypal.com/paypalme/mhi9388?locale.x=en_US"><img src="https://i.imgur.com/Y2gqr2j.png" height="40"></a>
