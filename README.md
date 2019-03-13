# PHP Validator ✔️

**php-validator** is a package to provide a validation  

[![Build Status](https://travis-ci.org/Aubind97/php-validator.png?branch=master)](https://travis-ci.org/Aubind97/php-validator)

# 📖 Documentation
## 💿 Installation
**php-validator** can be installed via `composer`, just execute the following command in your project root  
```sh
composer require aubind97/php-validator
```
Or you can add the following input in your `composer.json` file.  

```json
"require": {
  "aubind97/php-validator": "^1.0"
}
```
## 📚 Usage
> Make sure to use `composer` autoloading to load the package  
> Be sure to add the `use` statment or add the namespace before `Validator`

Using **php-validator** in your projet is super simple, here is an example
```php
$validator = (new Validator($_POST))
  ->email('email')
  ->length('firstname', 2, 100)
  ->length('lastname', 2, 100)
  ->length('nickname', 2, 100)
  ->required('email', 'firstname', 'lastname');
```
> here we validate `$_POST` but you can use any array

After the validation you can check if it's valid like this
```php
$validator->isValid();
```

If there are errors, you can get errors messages with
```php
$validator->getErrors();
```

### Advanced features
You can add a filter at the validator creation, to discard not needed agruments
```php
$validator = new Validator($_POST, ['firstname', 'lastname']);
```

You can also create validator with many rules, to validate all params of a model for instance, and apply rules only is the params is in the array params give at the construction
```php
$validator = new Validatro($_POST, ['firstname', 'lastname'], true);
```

## 📏 Available rules
Here is the list of all availables validation rules
### `required`
Check if the requested params are given
```php
$validator->required('key')
$validator->required('key1', 'key2')
```
### `dateTime`
Check if the requested param if a date that follow the specified format
```php
$validator->dateTime('key') // Default format 'Y-m-d H:i:s'
$validator->dateTime('key', 'Y-m-d')
```
### `email`
Check if the requested param is an email
```php
$validator->email('key')
```
### `exists`
Check if the requested param exists in the table (in a database)
```php
$validator->exists('key', 'column', 'table', $pdo) // $pdo is a \PDO connection
```
### `extension`
Check if the requested param is of the specified extensions
```php
$validator->extension('key', ['jpg', 'png']) // You can add the format you want
```
### `length`
Check if the requested param length
```php
$validator->length('key', 3) // more than 3 characters
$validator->length('key', null, 10) // less than 10 characters
$validator->length('key', 3, 10) // between 3 and 10 characters
```
### `money`
Check if the requested param correspond to a price value
```php
$validator->money('key')
```
### `notEmpty`
Check if the requested param is not empty
```php
$validator->notEmpty('key')
$validator->notEmpty('key1', 'key2')
```
### `numeric`
Check if the requested param is a numeric
```php
$validator->numeric('key')
```
### `slug`
Check if the requested param is a slug (word separated by '-')
```php
$validator->slug('key')
```
### `unique`
Check if the requested param is unique in a table (in a databse)
```php
$validator->unique('key', 'column', 'table', $pdo) // $pdo is a \PDO connection

// the value of 'key' is unique excluding the row with the id equal to 1
$validator->unique('key', 'column', 'table', $pdo, 1)
```
### `uploaded`
Check if the requested param is upload without errros
```php
$validator->('key')
```

## 🤝 Contributions
This repository is maintained by @aubind97  

> If you want to improve the system i'd love to merge your PR