# Symfony Certification
[Certification FAQ](https://certification.symfony.com/faq.html)

## [Technical Requirements](https://symfony.com/doc/5.0/setup.html#technical-requirements)
* PHP 7.2.5 or higher with extensions: Ctype, iconv, JSON, PCRE, Session, SimpleXML, and Tokenizer (which are installed by default)
* Composer

## [Installation](https://symfony.com/doc/5.0/setup.html)
There are two ways of installing Symfony:
* using the [Symfony CLI binary](https://github.com/symfony/cli) (which is not open source, it contains commands to manage Symfony Cloud projects)
* using the Composer `create project` command

### Using the Symfony CLI binary
```
$ symfony new my_project_name --version=5.0 --full
```

The above command is a wrapper around the composer create-project command.

### Using composer create-project
```
$composer create-project symfony/website-skeleton:"5.0.*" my_project_name
```

Either of the above methods of installation will result in a 5.0.x Symfony project being installed.

## PHP
### PHP API up to PHP 7.2 version
### Object Oriented Programming
### Namespaces
### Interfaces
### Anonymous functions and closures
### Abstract classes
### Exception and error handling
### Traits
### PHP extensions
### SPL

## HTTP
### Client / Server interaction
### Status codes
### HTTP request
### HTTP response
### HTTP methods
### Cookies
### Caching
### Content negotiation
### Language detection
### Symfony HttpClient component

## Symfony Architecture
### [Symfony Flex](https://symfony.com/doc/current/setup.html#installing-packages)

[Symfony Flex](https://github.com/symfony/flex) is a composer plugin that facilitates the installation of *recipes* using an alias.

So instead of listing out the vendor/name of the packages required:
```
$ composer require doctrine/orm doctrine/doctrine-bundle doctrine/doctrine-migrations-bundle
```

you can instead type:
```
$ composer require doctrine
```

and Symfony Flex will resolve the alias (in this case, doctrine) to the corresponding [symfony/orm-pack Flex recipe](https://packagist.org/packages/symfony/orm-pack).

A Flex recipe consists of a composer.json file (of type *"symfony-pack"*) which defines the individual dependencies of the recipe itself. Flex will download those dependencies to the vendor directory and:

* will take care of adding any bundles included in the recipe to config/bundles.php
* will add any required entries to the .env file
* will copy any required baseline configuration files to either the config/packages directory or the config/routes directory

Symfony flex uses the following keys in the composer.json file:
* flex-require
* flex-require-dev

and a symfony.lock, which lives in the project root directory keeps track of the Symfony Flex recipes that have been installed.

Flex recipes can be inspected at https://flex.symfony.com/

[Upgrading existing project to use Symfony Flex](https://symfony.com/doc/5.0/setup/flex.html)

To use Symfony Flex, which is a recommended best practice, the following directory structure (which is default for Symfony > 4) must be used:

```
your-project/
+-- assets/
+-- **bin**/
|   +-- console
+-- **config**/
|   +-- bundles.php
|   +-- packages/
|   +-- routes.yaml
|   +-- services.yaml
+-- **public**/
|   +-- index.php
+-- **src**/
|   +-- ...
|   +-- Kernel.php
+-- templates/
+-- tests/
+-- translations/
+-- **var**/
+-- **vendor**/
```

NOTE: The location of five directories (bin, config, public, src, var and vendor) can be customised by specifying a key/value pair in the *extra* section of composer.json, for example:

```
{
    "extra": {
        "src-dir": "src/App"
    }
}
```

The five directories key values are:
* bin-dir
* config-dir
* var-dir
* public-dir
* src-dir

### License
### Components
### Bridges
### Code organization
### Request handling
### Exception handling
### Event dispatcher and kernel events
### Official best practices
### Release management
### Backward compatibility promise
### Deprecations best practices
### Framework overloading
### Release management and roadmap schedule
### Framework interoperability and PSRs
### Naming conventions

## Controllers
### Naming conventions
### The base AbstractController class
### The request
### The response
### The cookies
### The session
### The flash messages
### HTTP redirects
### Internal redirects
### Generate 404 pages
### File upload
### Built-in internal controllers

## Routing
### Configuration (YAML, XML, PHP & annotations)
### Restrict URL parameters
### Set default values to URL parameters
### Generate URL parameters
### Trigger redirects
### Special internal routing attributes
### Domain name matching
### Conditional request matching
### HTTP methods matching
### User's locale guessing
### Router debugging

## Templating with Twig
### Auto escaping
### Template inheritance
### Global variables
### Filters and functions
### Template includes
### Loops and conditions
### URLs generation
### Controller rendering
### Translations and pluralization
### String interpolation
### Assets management
### Debugging variables

## Forms
### Forms creation
### Forms handling
### Form types
### Forms rendering with Twig
### Forms theming
### CSRF protection
### Handling file upload
### Built-in form types
### Data transformers
### Form events
### Form type extensions

## Data Validation
### PHP object validation
### Built-in validation constraints
### Validation scopes
### Validation groups
### Group sequence
### Custom callback validators
### Violations builder

## Dependency Injection
### Service container
### Built-in services
### Configuration parameters
### Services registration
### Tags
### Semantic configuration
### Factories
### Compiler passes
### Services autowiring

## Security
### Authentication
### Authorization
### Configuration
### Providers
### Firewalls
### Users
### Passwords encoders
### Roles
### Access Control Rules
### Guard authenticators
### Voters and voting strategies

## HTTP Caching
### Cache types (browser, proxies and reverse-proxies)
### Expiration (Expires, Cache-Control)
### Validation (ETag, Last-Modified)
### Client side caching
### Server side caching
### Edge Side Includes

## Console
### Built-in commands
### Custom commands
### Configuration
### Options and arguments
### Input and Output objects
### Built-in helpers
### Console events
### Verbosity levels

## Automated Tests
### Unit tests with PHPUnit
### Functional tests with PHPUnit
### Client object
### Crawler object
### Profile object
### Framework objects access
### Client configuration
### Request and response objects introspection
### PHPUnit bridge
### Handling legacy deprecated code

## Miscellaneous
### Configuration (including DotEnv and ExpressionLanguage components)
### Error handling
### Code debugging
### Deployment best practices
### Process and Serializer components
### Messenger component
### Mime and Mailer components
### Filesystem and Finder components
### Lock component
### Web Profiler, Web Debug Toolbar and Data collectors
### Internationalization and localization (and Intl component)
