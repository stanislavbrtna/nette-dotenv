
# nette-dotenv-array

This little extension helps you to work with environment variables in config.neon. This is a fork of original netted-dotenv that allows passing csv formatted arrays from environment variables (or .env file) to your app.
To make it even more convenient, this extension also variables from `.env` file - a feature well known to Laravel users.

## Install

Via Composer

```bash
$ composer require wodcz/nette-dotenv
```

Then register extension in your `config.neon`
```neon
extensions:
	env: wodCZ\NetteDotenv\DotEnvExtension
```
In your composer.json add nette-dotenv array
```
"repositories": [
        {
            "type": "vcs",
            "url": "https://github.com/stanislavbrtna/nette-dotenv"
        }
    ],
```

And change the nette-dotenv line to:
```
"wodCZ/nette-dotenv": "dev-array"
```
## Usage
#### Get

You can access any environment variable using `@env.get('key', 'default')` syntax:

```neon
services:
    - App/MyConnection(@env::get('DB_HOST', '127.0.0.1'))
```
#### GetArray
In addition to *get*, you can use *getArray* `@env.getArray('key', 'default')` syntax:

```neon
parameters:
    EmailWarningsTo: @env::getArray('WARN_EMAILS', 'admin@example.net')
```

Environment variables are often set by a `docker`, `docker-compose`, or your CI server.
To make working with environment variables even easier, you can specify them in `.env` file
in root directory of your application.

This file should be hidden from VCS using `.gitignore` or so,
because each developer/server could require different environment configuration.
Furthermore, having `.env` file with credentials in repository would be a security risk.

This is an example on how your `.env` file might look like:

```
DB_HOST=192.168.0.10
DB_USER=myprojuser
DB_NAME=myproj
GOOGLE_API_KEY=my_own_key_used_for_development
WARN_EMAILS=tom@example.com,jerry@example.com
```
If you want to have spaces in your CSV formated environmental variable, use following format:
```
NAMES="'John Doe','Jane Doe'"
```

Have a look at [vlucas/phpdotenv documentation](https://github.com/vlucas/phpdotenv) for more comprehensive examples.

## Configuration

You can change behavior of this extension using `neon` configuration. Here is a list of available options with their
default values.
```neon
env:
	directory: "%appDir%/../"
	fileName: ".env"
	overload: false
	localOnly: false
	prefix: false
	csvDelimiter: ","
	csvEnclosure: "\'"
	class: \wodCZ\NetteDotenv\EnvAccessor
```

| Option | Description |
|--------|-------------|
| `directory` | Where your `.env` file is located |
| `fileName` | Name of your `.env` file |
| `overload` | Whether options in the `.env` file should override existing environment variables |
| `localOnly` | [Set to true to only return local environment variables (set by the operating system or putenv).](http://php.net/getenv#refsect1-function.getenv-parameters) |
| `prefix` | Whether to prefix the service name with the extension name |
|`csvDelimiter`|String used as csv delimiter for *getArray*.|
|`csvEnclosure`|String used as csv enclosure for *getArray*.|
| `class` | Class used to access environment variables |

## Change log

Please see [CHANGELOG](CHANGELOG.md) for more information on what has changed recently.

## Testing

``` bash
$ composer test
```

## Contributing

Please see [CONTRIBUTING](CONTRIBUTING.md) and [CONDUCT](CONDUCT.md) for details. Please consider contributing to the original https://github.com/wodCZ/nette-dotenv instead of this fork.

## Credits

- [Martin Janeček][link-author]
- [Vašek Henzl](https://github.com/vhenzl)
- Stanislav Brtna
- [All Contributors][link-contributors]


## License

The MIT License (MIT). Please see [License File](LICENSE.md) for more information.

[link-author]: https://github.com/wodCZ
[link-contributors]: ../../contributors

