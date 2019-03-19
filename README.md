# Bright Components - Model Lite
### Eloquent-esque base class for custom models in your php application. (Fork of jenssegers/model).

[![Latest Version on Packagist](https://img.shields.io/packagist/v/bright-components/model-lite.svg)](https://packagist.org/packages/bright-components/model-lite)
[![Build Status](https://img.shields.io/travis/bright-components/model-lite/master.svg)](https://travis-ci.org/bright-components/model-lite)
[![Quality Score](https://img.shields.io/scrutinizer/g/bright-components/model-lite.svg)](https://scrutinizer-ci.com/g/bright-components/model-lite)
[![Total Downloads](https://img.shields.io/packagist/dt/bright-components/model-lite.svg)](https://packagist.org/packages/bright-components/model-lite)

![Bright Components](https://s3.us-east-2.amazonaws.com/bright-components/bc_large.png "Bright Components")


Features
--------

 - Accessors and mutators
 - Model to Array and JSON conversion
 - Hidden attributes in Array/JSON conversion
 - Guarded and fillable attributes
 - Appending accessors and mutators to Array/JSON conversion
 - Attribute casting

You can read more about these features and the original Eloquent model on http://laravel.com/docs/eloquent

Installation
------------

Install using composer:

```
composer require bright-components/model-lite
```

Example
-------

```php
class User extends Model {

    protected $hidden = ['password'];

    protected $guarded = ['password'];

    protected $casts = ['age' => 'integer'];

    public function save()
    {
        return API::post('/items', $this->attributes);
    }

    public function setBirthdayAttribute($value)
    {
        $this->attributes['birthday'] = strtotime($value);
    }

    public function getBirthdayAttribute($value)
    {
        return new DateTime("@$value");
    }

    public function getAgeAttribute($value)
    {
        return $this->birthday->diff(new DateTime('now'))->y;
    }
}

$item = new User(array('name' => 'john'));
$item->password = 'bar';

echo $item; // {"name":"john"}
```
