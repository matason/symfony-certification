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

The process is quite involved and includes the following key activities:
* installing Symfony Flex
* removing the Symfony Standard Edition (if it has been used)
* adding back dependencies
* moving configuration files
* moving source code files
* moving source and public assets
* removing old directories
* rename SYMFONY_DEBUG and SYMFONY_ENV environment variables to APP_DEBUG and APP_ENV

To use Symfony Flex, which is a recommended best practice, the following directory structure (which is default for Symfony > 4) is recommended:

```
your-project/
+-- assets/
+-- bin/
|   +-- console
+-- config/
|   +-- bundles.php
|   +-- packages/
|   +-- routes.yaml
|   +-- services.yaml
+-- public/
|   +-- index.php
+-- src/
|   +-- ...
|   +-- Kernel.php
+-- templates/
+-- tests/
+-- translations/
+-- var/
+-- vendor/
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
Symfony source code is MIT license:

> A short and simple permissive license with conditions only requiring preservation of copyright and license notices. Licensed works, modifications, and larger works may be distributed under different terms and without source code.

Permitted:
* Commercial use
* Modification
* Distribution
* Private use

Limitations:
* Liability
* Warranty

### Components

If using Symfony components in non-Symfony projects: vendor/autoload.php must be included.

#### [Asset component](https://symfony.com/doc/5.0/components/asset.html)

> The Asset component manages URL generation and versioning of web assets such as CSS stylesheets, JavaScript files and image files.

Assets are managed through *packages*.

Packages implement the PackageInterface: `vendor/symfony/asset/PackageInterface.php`

A package facilitates versioning, allows a common base path to be set and enables a CDN to be configured (if desired).

**Versioning strategies**
There are three versioning strategies (custom versioning strategies can also be implemented):
* Empty version strategy: `vendor/symfony/asset/VersionStrategy/EmptyVersionStrategy.php`
* Static version strategy: `vendor/symfony/asset/VersionStrategy/StaticVersionStrategy.php`
* JSON manifest file strategy: `vendor/symfony/asset/VersionStrategy/JsonManifestVersionStrategy.php`

Custom versioning strategy classes must implement the VersionStrategyInterface - `vendor/symfony/asset/VersionStrategy/VersionStrategyInterface.php`

**Benefits of using the asset component**
* Keeps verbose includes out of templates
* Facilitates cache control of assets
* Facilitates an easy move of assets (should you wish to do so)
* Facilitates use of CDN's: without asset, it's hard to randomise the CDN targets

#### [BrowserKit component](https://symfony.com/doc/5.0/components/browser_kit.html)
> The BrowserKit component simulates the behavior of a web browser, allowing you to make requests, click on links and submit forms programmatically.

It's used in functional testing...

See it used in `vendor/symfony/framework-bundle/Test/WebTestCase.php::createClient()`

BrowserKit component can:

* simulate clicking on links
* reading cookies
* making requests passing in a cookie jar
* navigate backwards and forwards through the history

BrowserKit can also make HTTP request to external sites:

```
<?php

use Symfony\Component\BrowserKit\HttpBrowser;
use Symfony\Component\HttpClient\HttpClient;

require './vendor/autoload.php';

$browser = new HttpBrowser(HttpClient::create());
$crawler = $browser->request('GET', 'https://symfony.com');
```
#### The Cache Component
#### The Config Component
#### The Console Component
#### The Contracts Component
#### [The CssSelector Component](https://symfony.com/doc/5.0/components/css_selector.html)
> The CSS Selector component converts CSS selectors to XPath expressions using the `vendor/symfony/css-selector/CssSelectorConverter.php::toXPath()` method.
#### The DependencyInjection Component
#### [The DomCrawler Component](https://symfony.com/doc/5.0/components/dom_crawler.html)
> The DomCrawler component eases DOM navigation for HTML and XML documents.
#### The EventDispatcher Component
#### [The ExpressionLanguage Component](https://symfony.com/doc/5.0/components/expression_language.html)
> The ExpressionLanguage component provides an engine that can compile and evaluate expressions. An expression is a one-liner that returns a value (mostly, but not limited to, Booleans).
#### The Filesystem Component
#### The Finder Component
#### The Form Component
#### The HttpFoundation Component
#### The HttpKernel Component
#### The Inflector Component
#### The Intl Component
#### The Ldap Component
#### The Lock Component
#### The Mailer Component
#### The Messenger Component
#### The Mime Component
#### The OptionsResolver Component
#### The PHPUnit Bridge
#### The Process Component
#### The PropertyAccess Component
#### The PropertyInfo Component
#### The PSR-7 Bridge
#### The Security Component
#### The Serializer Component
#### The Stopwatch Component
#### The String Component
#### The Validator Component
#### The VarDumper Component
#### The VarExporter Component
#### The Workflow Component
#### The Yaml Component

### Bridges
### Code organization
### Request handling
### Exception handling
### Event dispatcher and kernel events
### [Official best practices](https://symfony.com/doc/5.0/best_practices.html)
Introduced by Fabien during his Symfony Live 2014 keynote in New York (whilst there were other Symfony Live conference talks online, I couldn't find any from New York).
* Use Symfony CLI binary to create new projects
* Use the default Symfony directory structure
* Use Symfony Flex in projects
* Keep services private
* Do not inject the container because it hides the actual dependencies and gives too much access... doing so also requires that services be made public
* Put as little logic as possible in controllers (thin controllers)
* Use the same controller action to render and to process forms
* Redirect after a successful form submission to prevent the user from hitting the refresh button

### Release management
### Backward compatibility promise
### Deprecations best practices

**Symfony Standard Edition**
Symfony standard edition is no longer available since Symfony 4
A project using the Symfony standard edition will have symfony/symfony dependency in composer.json
Remove it with:
```
$ composer remove symfony/symfony
```

### Framework overloading
### Release management and roadmap schedule
### Framework interoperability and PSRs
### Naming conventions

## Controllers
### Naming conventions
### The base AbstractController class
**Provides access to parameters**
The AbstractController has a method called getParameter() which takes the string parameter name of the parameter to get.

```
# config/services.yaml
parameters:
    app.greeting: 'Hello, world!'
```

```
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;

class SomeController extends AbstractController
{
    public function index()
    {
        dd($this->getParameter('app.greeting'));
    }
}
```

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

* Build - in the controller or a dedicated form class
* Render - in a template
* Process - to validate submitted data and transform it into PHP data

### Forms creation

**The form builder class**
In a controller, if you're extending `vendor/symfony/framework-bundle/Controller/AbstractController.php`, you can call:

```
$this->createFormBuilder();
```
The `createFormBuilder()` method on the AbstractController class loads the `vendor/symfony/form/FormFactory.php` class and calls the `createBuilder()` method on it which returns an implementation of the FormBuilderInterface `vendor/symfony/form/FormBuilderInterface.php` which defaults to `vendor/symfony/form/FormBuilder.php`.

The `FormBuilderInterface` extends the `FormConfigBuilderInterface` (`vendor/symfony/form/FormConfigBuilderInterface.php`) which has the following notable methods:

```
$formBuilder = $this->createFormBuilder();

...

$formBuilder->setMethod() // so that you can set your form action to POST or GET
$formBuilder->setAction() // so you can control where your form is submitted to
```

There are at least wo other ways of modifying the form:

**Passing options as the third argument to the $formFactory->create() method**

```
$formFactory = $container->get('form.factory')->create(TaskForm::class, new Task(), ['method' => 'GET'] );
```

**In the template form function**

```
{{ form(form, {method: 'GET'}) }}
```

[HTTP method overrides](https://symfony.com/doc/5.0/reference/configuration/framework.html#configuration-framework-http-method-override)

If you set the action (method) of a form to be PUT, PATCH or DELETE, Symfony will include that in a hidden field (_method) on the form and the form will actually be POST'ed but Symfony alters the request method when it hits Symfony so in your controller where your form is submitted to, you could have something like:

```
if ($request->getMethod() === Request::METHOD_DELETE) { // Do something... }
```

If you're using [Symfony's reverse proxy](https://symfony.com/doc/5.0/http_cache.html#symfony2-reverse-proxy), you need to add a line to public/index.php so:

```
// public/index.php

$kernel = new Kernel($_SERVER['APP_ENV'], (bool) $_SERVER['APP_DEBUG']);
$request = Request::createFromGlobals();
```

becomes

```
// public/index.php

$kernel = new Kernel($_SERVER['APP_ENV'], (bool) $_SERVER['APP_DEBUG']);
Request::enableHttpMethodParameterOverride();
$request = Request::createFromGlobals();
```

Create a named form with `$this->get('form.factory')->createNamed('somename', TaskForm::class, new Task());`

If you not extending `AbstractController` and you have autowiring enabled, you can type-hint constructor arguments to inject the form factory as follows:

```
<?php

namespace App\Controller;

use Symfony\Component\Form\FormFactoryInterface;

class MyController
{
    protected $formFactory;

    public function __construct(FormFactoryInterface $formFactory)
    {

        $this->formFactory = $formFactory;
    }
}
```

### Forms handling
```
$form->isSubmitted() && $form->isValid()
```

The `$form->createView()` method `$form->handleRequest($request)`

TODO: https://symfony.com/doc/5.0/form/direct_submit.html

### Form types
It is best to extend `vendor/symfony/form/AbstractType.php`

A single input, a collection of inputs and an entire form are all *form types*.

There are a bunch of form types provided by Symfony and you can add your own.

TODO: Study up on built in form types - https://symfony.com/doc/5.0/reference/forms/types.html

### Forms rendering with Twig
### Forms theming
### CSRF protection
### [Handling file upload](https://symfony.com/doc/5.0/controller/upload_file.html)
### Built-in form types
### Data transformers
### Form events
### Form type extensions

## [Data Validation](https://symfony.com/doc/5.0/validation.html)
### PHP object validation
### Built-in validation constraints
### Validation scopes
### Validation groups
### Group sequence
### Custom callback validators
### Violations builder

## Dependency Injection

You can constructor-inject parameters as follows:
```
# config/services.yaml
parameters:
    app.greeting: 'Hello, world!'

services:
...
    App\Controller\:
        resource: '../src/Controller/'
        tags: ['controller.service_arguments']
...
    App\Controller\DefaultController:
        arguments:
            $greeting: '%app.greeting%'
```
and then:
```
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;

class DefaultController extends AbstractController
{
    protected $greeting;

    /**
     * DefaultController constructor.
     */
    public function __construct($greeting)
    {
        $this->greeting = $greeting;
    }
}
```
### Service container
### Built-in services
### [Configuration parameters](https://symfony.com/doc/5.0/configuration.html#configuration-parameters)
`services._defaults.bind` can be used inject a parameter into any service or controller where the argument is named exactly the same.

```
# config/services.yaml
services:
    _defaults:
        bind:
            # pass this value to any $projectDir argument for any service
            # that's created in this file (including controller arguments)
            $projectDir: '%kernel.project_dir%'
```

TODO: https://symfony.com/doc/5.0/service_container.html#services-binding

You can inject all parameters by type-hinting an argument with:

```
<?php

namespace App\Controller;

use Symfony\Component\DependencyInjection\ParameterBag\ContainerBagInterface;

class MyController
{
    protected $parameters;

    public function __construct(ContainerBagInterface $parameters)
    {
        $this->parameters = $parameters;
    }
}
```

### Services registration
### Tags
### Semantic configuration
### Factories
### Compiler passes
### [Services autowiring](https://symfony.com/doc/5.0/service_container/autowiring.html)
If you type-hint your controller constructor arguments, Symfony will pass in the services automagically: you don't even have to have your controller extend `AbstractController` if you don't want to.

For this to work, autowire must be true and classes in App\Controller must be tagged with `controller.service_arguments` which can be done like this:

```
// config/services.yaml
services:
	_defaults:
		autowire: true
...
    App\Controller\:
        resource: '../src/Controller/'
        tags: ['controller.service_arguments']
```

then your controller can be:

```
// src/Controller/DefaultController.php

<?php

namespace App\Controller;

use Symfony\Component\Form\FormFactoryInterface;

class MyController
{
    protected $formBuilder;

    public function __construct(FormFactoryInterface $formFactory)
    {
        $this->formBuilder = $formFactory->createBuilder();
    }
}
```

But if you choose not to extend `AbstractController` and don't have autowire enabled, you will need to define your controller as a service and use service binding as follows:

```
// config/services.yaml
services:
    App\Controller\DefaultController:
        tags: ['controller.service_arguments']
        bind:
            $formFactory: '@form.factory'
```

then in your controller:

```
// src/Controller/DefaultController.php

<?php

namespace App\Controller;

use Symfony\Component\Form\FormFactoryInterface;

class MyController
{
    protected $formBuilder;

    public function index(FormFactoryInterface $formFactory)
    {
        $formBuilder = $formFactory->createBuilder();
    }
}
```

## Security
Run php bin/console symfony check:security regularly.
### Authentication
### Authorization
### Configuration
* don't commit any local .env files to source control
* use secrets management system for sensitive environment variable values
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

## [Automated Tests](https://symfony.com/doc/5.0/testing.html)
Run ./bin/phpunit in the Symfony project root directory which will install PHPUnit on first run and then it will run your tests.

Tests should be in the tests directory... I created Functional/Controller/DefaultControllerTest.php inside the tests directory with the following code:

```
<?php

namespace App\Tests\Functional\Controller;

use Symfony\Bundle\FrameworkBundle\Test\WebTestCase;

class DefaultControllerTest extends WebTestCase
{
    public function test_index_page_displays_hello_world()
    {
        $client = static::createClient();
        $client->request('GET', '/');

        $this->assertSelectorTextSame('p', 'Hello, world!');
    }
}
```

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
dotenv is a Symfony component, it's available through Symfony flex with the alias dotenv

The .env file is read and parsed on every request, it should be committed to source control and should only contain default values that are good for a development environment.

The values are added to the `$_ENV` and `$_SERVER` PHP variables.

Values in `$_ENV` and `$_SERVER` are **NOT** overridden but values defined in .env files *overwrite* those found in earlier .env files.

The following is from a .env file after a fresh install:

```
# In all environments, the following files are loaded if they exist,
# the latter taking precedence over the former:
#
#  * .env                contains default values for the environment variables needed by the app
#  * .env.local          uncommitted file with local overrides
#  * .env.$APP_ENV       committed environment-specific defaults
#  * .env.$APP_ENV.local uncommitted environment-specific overrides
#
# Real environment variables win over .env files.
#
# DO NOT DEFINE PRODUCTION SECRETS IN THIS FILE NOR IN ANY OTHER COMMITTED FILES.
#
# Run "composer dump-env prod" to compile .env files for production use (requires symfony/flex >=1.2).
# https://symfony.com/doc/current/best_practices.html#use-environment-variables-for-infrastructure-configuration
```

You can use an env variable when setting another env var as follows:

```
SOME_THING=${SOME_OTHER_THING:-some-default-if-some-other-thing-is-not-set}
```

You can set env variables to the return value of expression (called embedding commands) using $(command-here):

```
DATE=$(date)
```

Symfony Flex can add third-party package variables to the .env file when they’re installed.

* .env - default variables suitable for development, committed to source control
* .env.local - overrides, not committed to source control, ignored when the environment is test
* .env.dev, .env.stage, .env.prod - overrides for a specific environment, committed to source control
* .env.dev.local, env.stage.local. env.prod.local - overrides for a specific environment, not committed to source control

Optimise the loading of environment variables by running:

```
$ composer dump-env prod
```

dump-env is available in Symfony Flex 1.2 (or later)

dump-env parses all the .env files and dumps their final values in a file named .env.local.php

List environment variables with:

```
$ php bin/console debug:container --env-vars
$ php bin/console debug:container --env-vars app // TODO: Check why this didn't seem to work for me
$ php bin/console debug:container --env-var=APP_SECRET
```

TODO: https://symfony.com/doc/5.0/configuration/secrets.html

Requires libsodium (ships with >= PHP7.2)

Create an asymmetric cryptographic public (for encrypting/writing) and private (for decrypting/reading) keys.

dev keys can be safely committed to version control but the prod private key **MUST never be committed** (is .gitignored).

**Setting secrets**
```
# set your a default development value (can be overridden locally)
$ php bin/console secrets:set DATABASE_PASSWORD
```

```
# set your production value
$ php bin/console secrets:set DATABASE_PASSWORD --env=prod
```

**Accessing secrets**
```
# config/packages/doctrine.yaml
doctrine:
    dbal:
        password: '%env(DATABASE_PASSWORD)%'
```

Environment variables override always take precedence over secrets if they have the same name.

Listing secrets**
```
$ php bin/console secrets:list --reveal
```

**Removing secrets**
```
$ php bin/console secrets:remove DATABASE_PASSWORD
```

If you don't deploy your `config/secrets/prod/prod.decrypt.private.php` file to your production target, you can base64 encode it and set the `SYMFONY_DECRYPTION_SECRET` environment variable.

```
$ php -r 'echo base64_encode(require "config/secrets/prod/prod.decrypt.private.php");'
```

To avoid PHP decrypting the secrets at runtime, you can run:

```
$ php bin/console secrets:decrypt-to-local --force --env=prod
```

which will decrypt all the secrets to the .env.prod.local file, after which the private key can be removed from the production server.

**Rotating keys**

```
$ php bin/console secrets:generate-keys --rotate
```

will regenerate the asymmetric cryptographic keys, decrypt all the secrets with the old key and re-encrypt all the secrets with the new key.

### Error handling
### Code debugging
### Deployment best practices
* have the deployment run composer dump-env to dump out variable final values to .env.local.php
* have the deployment process copy your config/secrets/prod/prod.decrypt.private.php to your deployment target

### Process and Serializer components
### Messenger component
### Mime and Mailer components
### Filesystem and Finder components
### Lock component
### Web Profiler, Web Debug Toolbar and Data collectors
### Internationalization and localization (and Intl component)

## Worth knowing about

### [Maker bundle](https://symfony.com/doc/current/bundles/SymfonyMakerBundle/index.html)

### [Webpack Encore](https://symfony.com/doc/5.0/frontend/encore/installation.html)
Install node.js and yarn package manager first.

If you're using Webpack Encore in a project that has Symfony Flex installed, then all you need to run is:

```
$ composer require symfony/webpack-encore-bundle
$ yarn install
```

Installing the symfony/webpack-encore-bundle will also create config/packages/assets.yaml and configure Symfony to use the JSON manifest versioning strategy by default.
