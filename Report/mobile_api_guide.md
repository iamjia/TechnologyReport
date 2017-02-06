# API guide for mobile APP


## Architechure

* `RESTful API`:
	* [PayPal REST API guide](https://github.com/paypal/api-standards/blob/master/api-style-guide.md)
	* [Microsoft REST API guide](https://github.com/Microsoft/api-guidelines/blob/master/Guidelines.md)

* `Response for APP`: responses return **HTTP code 200 always**, with business code in response body.

* `Response JSON only`: JSON property name must be JSON style (linux style), **never camelCased**

* `Different environment`: environment for develop, production (maybe preview release)

* `Business code`: confirm to HTTP standard code, except some specialized situations with custom code for specific errors.


## Security

* HTTPS only: confirm **TLS1.2** at least

	You can validate SSL in [qcloud](https://www.qcloud.com/product/ssl).

* Optional access token: to validate user identity, JWT is suggested.


## Request by APP

Common data like APP info, device info, token should fill in **request head**.


### Token in HTTP HEAD

Token will be passed with `Authorization` field in **HTTP HEAD**

``` javascript
{
    "Accept-Language": "en;q=1",
    "Authorization": "eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9eyJvcGVyYXRvcl9pZCI6MiwiaWF0IjoxNDg2MTg2NDMwLCJpc3MiOiJndWd1YmFuZyJ9.5-cwqbZN4CknOD8jZcO_2MQdK4pjCk4PJE7PfVstwpw",
}
```


### APP info, device info in HTTP HEAD

APP info and device info passed as `User-Agent` field in **HTTP HEAD**

*for iOS:*

``` javascript
{
    "Accept-Language": "en;q=1",
    "User-Agent": "SDYClient/2.1.0 (iPhone; iOS 10.2; Scale/2.00)",
}
```

**User-Agent** format: 
`$[BundleName]/$[AppVersion] ($[Device]; $[OS] $[OSVersion]; Scale/$[Resolution])`

| Field | Description |
|:-------------|:-------------|
| $[BundleName] | iOS app bundle name, eg: SDYClient | 
| $[AppVersion] | app version, eg: 2.1.0 | 
| $[Device] | device hardware, eg: iPhone, iPad | 
| $[OS] | operating system, eg: iOS, watchOS, Mac OS X | 
| $[OSVersion] | operating system version, eg: 9.1, 10.1.2 | 
| $[Resolution] | iOS screen resolution, eg: 1.0, 2.0, 3.0, 2.75 | 


*for Android:*

``` javascript
{
    "Accept-Language": "en;q=1",
    "User-Agent": "cn.sudiyi.app.courier/2.1.0 (Motorola XT1085; Android 5.1; Scale/2.00)"
}
```

**User-Agent** format: 
`$[PackageName]/$[AppVersion] ($[Device]; $[OS] $[OSVersion]; Scale/$[Density])`

| Field | Description |
|:-------------|:-------------|
| $[PackageName] | Android app PackageName, eg: cn.sudiyi.app.courier | 
| $[AppVersion] | app version, eg: 2.1.0 | 
| $[Device] | device hardware, eg: Motorola XT1085 | 
| $[OS] | operating system, eg: Android | 
| $[OSVersion] | operating system version, eg: 5.1 | 
| $[Density] | Android screen density, eg: 1.0, 1.5, 2.0,3.0 | 


### Paging

Pages of results should be referred to consistently by the query parameters `page` and `page_size`.

* `page`: refers to the requested page, always begin with 0

* `page_size`: refers to the amount of results per request

* `total_items`: refers to response items total count, stay in response root

* `total_pages`: refers to response items total pages count, stay in response root


## Response to APP

``` javascript
{
   "data": {}, // or [ ] or others
   "total_items": 48, // optional
   "total_pages": 2, // optional
   "err": "description for develper", // debug message for developer
   "code": 200, // 200 is ok
   "text": "prompt to user", // prompt to user
   "alert": 0, 
}
```

`total`

| alert | Description |
|:-------------|:-------------|
| 0 | determine by client | 
| 1 | Toast/HUD success | 
| 2 | Toast/HUD failed | 
| 3 | Toast/HUD info | 
| 4 | dialog | 

