# Symfony Certification Study Notes
[Certification FAQ](https://certification.symfony.com/faq.html)

## [Technical Requirements](https://symfony.com/doc/5.0/setup.html#technical-requirements)
* PHP 7.2.5 or higher with extensions: Ctype, iconv, JSON, PCRE, Session, SimpleXML, and Tokenizer (which are installed by default)
* Composer

## [Installation](https://symfony.com/doc/5.0/setup.html)
There are two ways of installing Symfony:
* using the [Symfony CLI binary](https://github.com/symfony/cli) (which is not open source, it contains commands to manage Symfony Cloud projects)
* using the Composer `create project` command

### Using the Symfony CLI binary
```bash
$ symfony new my_project_name --version=5.0 --full
```

The above command is a wrapper around the composer create-project command.

The Symfony CLI binary can be used to:
* Create new Symfony applications
* Run a local web server with TLS support for development purposes
* Check for security vulnerabilities in a project
* Seamless integrate with platform.sh (Symfony Cloud, Symfony PaaS)

### Using composer create-project
```bash
$ composer create-project symfony/website-skeleton:"5.0.*" my_project_name
```

Either of the above methods of installation will result in a 5.0.x Symfony project being installed.

## PHP
### PHP API up to PHP 7.2 version
#### Arrays
```php
$numbers = array_merge([1, 2, 3], [4, 5, 6]);

var_dump($numbers);
array(6) {
  [0]=>
  int(1)
  [1]=>
  int(2)
  [2]=>
  int(3)
  [3]=>
  int(4)
  [4]=>
  int(5)
  [5]=>
  int(6)
}
```

```php
$a = [2, 3, 4];
$numbers = array_unshift($a, 1);

var_dump($numbers);
array(4) {
  [0]=>
  int(1)
  [1]=>
  int(2)
  [2]=>
  int(3)
  [3]=>
  int(4)
}
```
#### [References](https://www.php.net/manual/en/language.references.php)
> References in PHP are a means to access the same variable content by different names.
> References can be likened to hardlinking in the Unix filesystem.

Three usages:

* [assigning by reference](https://www.php.net/manual/en/language.references.whatdo.php#language.references.whatdo.assign)
* [passing by reference](https://www.php.net/manual/en/language.references.whatdo.php#language.references.whatdo.pass)
* [returning by reference](https://www.php.net/manual/en/language.references.return.php)

### [Object Oriented Programming](https://www.php.net/manual/en/language.oop5.php)
### Namespaces
* https://phptherightway.com/#namespaces
* https://www.php.net/language.namespaces
### [Interfaces](https://www.php.net/manual/en/language.oop5.interfaces.php)
### [Anonymous functions and closures](https://www.php.net/manual/en/functions.anonymous.php)
### [Abstract classes](https://www.php.net/manual/en/language.oop5.abstract.php)
### Exception and error handling
* [Exceptions](https://www.php.net/manual/en/language.exceptions.php)
* [Error handling](https://www.php.net/manual/en/language.errors.basics.php)
### [Traits](https://www.php.net/language.oop5.traits)
### [PHP extensions](https://www.php.net/manual/en/extensions.alphabetical.php)
### [SPL](https://www.php.net/manual/en/book.spl.php)

## HTTP
[Symfony and HTTP Fundamentals](https://symfony.com/doc/5.0/introduction/http_fundamentals.html)

**Other resources**
* [HTTP1.1 Specification](https://www.w3.org/Protocols/rfc2616/rfc2616.html)
* [IETF HTTP Working Group documents](https://datatracker.ietf.org/wg/httpbis/documents/)
* [XMLHttpRequest](https://en.wikipedia.org/wiki/XMLHttpRequest)
* [List of HTTP header fields](https://en.wikipedia.org/wiki/List_of_HTTP_header_fields)
* [Internet media types](https://www.iana.org/assignments/media-types/media-types.xhtml)

### Client / Server interaction
### [Status codes](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status)
### HTTP request
The [Accept](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept) request header is used to convey which content types, expressed as MIME types, the client is able to understand.
### HTTP response
The body of the response can be returned in different formats (HTML, JSON, XML) so the [Content-Type](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Content-Type) entity header (which can be used in both HTTP requests and HTTP responses) is used to convey which format ([Internet Media Type](https://developer.mozilla.org/en-US/docs/Glossary/MIME_type)) is being returned.
### [HTTP methods](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods)
There are nine HTTP methods defined by the HTTP specification:
* GET
* POST
* PUT
* PATCH
* DELETE
* HEAD
* CONNECT
* OPTIONS
* TRACE
### [Cookies](https://developer.mozilla.org/en-US/docs/Web/HTTP/Cookies)
### [Caching](https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#varying_responses)
> The HTTP [Vary](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Vary) response header determines how to match future request headers to decide whether a cached response can be used rather than requesting a fresh one from the origin server. It is used by the server to indicate which headers it used when selecting a representation of a resource in a content negotiation algorithm.

See https://developer.mozilla.org/en-US/docs/Web/HTTP/Caching#varying_responses
> When a cache receives a request that has a Vary header field, it must not use a cached response by default unless all header fields specified in the Vary header match in both the original (cached) request and the new request.

### [Content negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation)
> In HTTP, content negotiation is the mechanism that is used for serving different representations of a resource at the same URI, so that the user agent can specify which is best suited for the user (for example, which language of a document, which image format, or which content encoding).

The server should determine the best representation of the requested resource to return based on two mechanisms:

* Server-driven negotiation or proactive negotiation (HTTP Headers sent by the user-agent)
* Agent-driven negotiation or reactive negotiation ([300](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/300) (Multiple Choices) or [406](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/406) (Not Acceptable), [415](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/415) (Unsupported Media Type) HTTP response codes)

#### [Server-driven negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation#server-driven_content_negotiation)
In server-driven negotiation, the user-agent sends HTTP headers along with the request to convey the preferred choices of the user.

Headers:
* [Accept](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept)
* [Accept-Charset](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Charset)
* [Accept-Encoding](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Encoding)
* [Accept-Language](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language)

#### [Agent-driven negotiation](https://developer.mozilla.org/en-US/docs/Web/HTTP/Content_negotiation#agent-driven_negotiation)
In agent-driven negotiation, when a server receives an ambiguous request for a resources that has multiple representations, it sends a response (a page with a [300 Multiple Choices](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/300) HTTP status code) inviting the user (or user-agent) to select the preferred representation of the resource.

### [Language detection](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language)
The [Accept-Language](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Language) HTTP request header advertises which languages the client is able to understand, and which locale variant is preferred.

> If the server cannot serve any matching language, it can theoretically send back a [406](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status/406) (Not Acceptable) error code. But, for a better user experience, this is rarely done and more common way is to ignore the Accept-Language header in this case.
### [Symfony HttpClient component](https://symfony.com/doc/5.0/http_client.html)
See [The HttpClient Component](#the-httpclient-component)
## Symfony Architecture
### [Symfony Flex](https://symfony.com/doc/current/setup.html#installing-packages)

[Symfony Flex](https://github.com/symfony/flex) is a composer plugin that facilitates the installation of *recipes* using an alias.

So instead of listing out the vendor/name of the packages required:
```bash
$ composer require doctrine/orm doctrine/doctrine-bundle doctrine/doctrine-migrations-bundle
```

you can instead type:
```bash
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

```json
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

[An announcement made in September 2022](https://symfony.com/blog/symfony-flex-is-going-serverless) that https://flex.symfony.com will be going away and that the recipes will be generated by GitHub actions and served statically. In symfony/flex 1.16, a feature flag was introduced so that the new endpoint can be tested and in 1.17 it will be removed and replaced with a call to upgrade notification.

### [License](https://symfony.com/doc/5.0/contributing/code/license.html)
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

### [Components](https://symfony.com/doc/5.0/components/index.html)

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

```php
<?php

use Symfony\Component\BrowserKit\HttpBrowser;
use Symfony\Component\HttpClient\HttpClient;

require './vendor/autoload.php';

$browser = new HttpBrowser(HttpClient::create());
$crawler = $browser->request('GET', 'https://symfony.com');
```
#### [The Cache Component](https://symfony.com/doc/5.0/components/cache.html)
> The Cache component provides features covering simple to advanced caching needs. It natively implements [PSR-6](https://www.php-fig.org/psr/psr-6/) and the [Cache Contracts](https://github.com/symfony/contracts/blob/master/Cache/CacheInterface.php) for greatest interoperability. It is designed for performance and resiliency, ships with ready to use adapters for the most common caching backends. It enables tag-based invalidation and cache stampede protection via locking and early expiration.

> The component also contains adapters to convert between PSR-6, PSR-16 and Doctrine caches. See [Adapters For Interoperability between PSR-6 and PSR-16 Cache](https://symfony.com/doc/5.0/components/cache/psr6_psr16_adapters.html) and [Doctrine Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/doctrine_adapter.html).

The component includes two approaches to caching:
* [PSR-6 caching](https://symfony.com/doc/5.0/components/cache.html#cache-component-psr6-caching)
* [Cache contracts](https://symfony.com/doc/5.0/components/cache.html#cache-component-contracts) - this is the recommended approach

##### [Cache contracts](https://symfony.com/doc/5.0/components/cache.html#cache-contracts)

Classes extending vendor/symfony/cache-contracts/CacheInterface.php) have two methods:
* ```get()``` // Used to set (as well as get)
* ```delete()```

**The get() method arguments**
* first: string cache key. The cache key must be unique for each cache pool and should only contain the letters `(A-Z, a-z)`, numbers `(0-9)` and the `_` and `.` symbols.
* second: callable|CallbackInterface, the callable|CallbackInterface is executed on a cache miss and is responsible for generating and returning the value to cache
* third: float, the beta (the value used for probabilistic early expiration: defaults to 1.0, 0 disables early recompute, INF will force immediate recompute)
* fourth: array, metadata

Cache Contracts has built in Stampede prevention: it uses a combination of locking and probabilistic early expiration.

###### [Cache Adapters](https://symfony.com/doc/5.0/components/cache.html#available-cache-adapters)
* [APCu Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/apcu_adapter.html)
* [Array Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/array_cache_adapter.html)
* [Chain Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/chain_adapter.html)
* [Doctrine Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/doctrine_adapter.html)
* [Filesystem Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/filesystem_adapter.html)
* [Memcached Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/memcached_adapter.html)
* [PDO & Doctrine DBAL Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/pdo_doctrine_dbal_adapter.html)
* [PHP Array Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/php_array_cache_adapter.html)
* [PHP Files Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/php_files_adapter.html)
* [Proxy Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/proxy_adapter.html)
* [Redis Cache Adapter](https://symfony.com/doc/5.0/components/cache/adapters/redis_adapter.html)

##### [PSR-6 caching](https://symfony.com/doc/5.0/components/cache.html#basic-usage-psr-6)

Classes implementing the vendor/psr/cache/src/CacheItemPoolInterface.php interface have the following methods for interacting with the cache:
* getItem() // Takes a string cache key as its only argument and returns an instance of vendor/psr/cache/src/CacheItemInterface.php
* delete() // Remove an item from cache by its key

CacheItemInterface has the following methods:
* set() // Used to set the cache value
* isHit() // Used to determine whether an item was retrieved from the cache or not

[Cache Invalidation](https://symfony.com/doc/5.0/components/cache/cache_invalidation.html)

Two types of cache invalidation are available:
* [Tags-based invalidation](https://symfony.com/doc/5.0/components/cache/cache_invalidation.html#cache-component-tags)
* [Expiration based invalidation](https://symfony.com/doc/5.0/components/cache/cache_invalidation.html#cache-component-expiration)

###### Tags-based invalidation
**Symfony Cache Contracts Example**
```php
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\Cache\Adapter\FilesystemAdapter;
use Symfony\Contracts\Cache\ItemInterface;
use Symfony\Component\Cache\Adapter\TagAwareAdapter;

class DefaultController extends AbstractController
{
    public function index()
    {
        $cache = new TagAwareAdapter(new FilesystemAdapter());

        $time = $cache->get('app.time', function(ItemInterface $item) {
            $item->expiresAfter(10); // Cache the item for 10 seconds.
            $item->tag('tag_time');

            $now = new \DateTime('now', new \DateTimeZone('Europe/London'));

            return $now->format('H:i:s');
        });

        // Invalidate all cache items tagged with tag_time.
        $cache->invalidateTags(['tag_time']);

        return $this->render('default/index.html.twig', ['time' => $time]);
    }
}
```
**PSR-6 Cache Example**
```php
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\Cache\Adapter\FilesystemAdapter;
use Symfony\Contracts\Cache\ItemInterface;
use Symfony\Component\Cache\Adapter\TagAwareAdapter;

class DefaultController extends AbstractController
{
    public function index()
    {
        $cache = new TagAwareAdapter(new FilesystemAdapter());

        $timeCacheItem = $cache->getItem('app.time');
        $timeCacheItem->expiresAfter(10); // Cache the item for 10 seconds.
        $timeCacheItem->tag('tag_time');

        if (!$timeCacheItem->isHit()) {
            $now = new \DateTime('now', new \DateTimeZone('Europe/London'));
            $timeCacheItem->set($now->format('H:i:s'));
            $cache->save($timeCacheItem);
        }

        $time = $timeCacheItem->get();

        // Invalidate all cache items tagged with tag_time.
        $cache->invalidateTags(['tag_time']);

        return $this->render('default/index.html.twig', ['time' => $time]);
    }
}
```
###### Expiration based invalidation
**Symfony Cache Contracts Example**
```php
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\Cache\Adapter\FilesystemAdapter;
use Symfony\Contracts\Cache\ItemInterface;

class DefaultController extends AbstractController
{
    public function index()
    {
        $cache = new FilesystemAdapter();

        $time = $cache->get('app.time', function(ItemInterface $item) {
            $item->expiresAfter(10); // Cache the item for 10 seconds.
            $now = new \DateTime('now', new \DateTimeZone('Europe/London'));

            return $now->format('H:i:s');
        });

        return $this->render('default/index.html.twig', ['time' => $time]);
    }
}
```
**PSR-6 Cache Example**
```php
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Component\Cache\Adapter\FilesystemAdapter;
use Symfony\Contracts\Cache\ItemInterface;

class DefaultController extends AbstractController
{
    public function index()
    {
        $cache = new FilesystemAdapter();

        $timeCacheItem = $cache->getItem('app.time');
        $timeCacheItem->expiresAfter(10);

        if (!$timeCacheItem->isHit()) {
            $now = new \DateTime('now', new \DateTimeZone('Europe/London'));
            $timeCacheItem->set($now->format('H:i:s'));
            $cache->save($timeCacheItem);
        }

        $time = $timeCacheItem->get();

        return $this->render('default/index.html.twig', ['time' => $time]);
    }
}
```
#### [The Config Component](https://symfony.com/doc/5.0/components/config.html)
> The Config component provides several classes to help you find, load, combine, fill and validate configuration values of any kind, whatever their source may be (YAML, XML, INI files, or for instance a database).

##### [Defining and processing configuration values](https://symfony.com/doc/5.0/components/config/definition.html)
The definition part of the config component is responsible for ensuring that configuration values comply to structural hierarchy (that `connections` appears under `database`) and/or type (that `auto_connect` is a boolean) rules.

The config component also supports first-seen-wins/last-seen-wins strategies for configuration values (with `performNoDeepMerging()` and `cannotBeOverwritten()` methods) and also conditional validation of values: if key A is set, then key B must be set.

##### [Resources](https://symfony.com/doc/5.0/components/config/resources.html)
* [Locating resources](https://symfony.com/doc/5.0/components/config/resources.html#locating-resources)
* [Loading resources](https://symfony.com/doc/5.0/components/config/resources.html#resource-loaders)
* [Loader resolver](https://symfony.com/doc/5.0/components/config/resources.html#finding-the-right-loader)

This is all achieved with the [`Symfony\Component\Config\Definition\Builder\TreeBuilder`](https://symfony.com/doc/5.0/components/config/definition.html#defining-a-hierarchy-of-configuration-values-using-the-treebuilder) class.

[Node type](https://symfony.com/doc/5.0/components/config/definition.html#node-type)
* scalar (generic type that includes booleans, strings, integers, floats and null)
* boolean
* integer
* float
* enum (similar to scalar, but it only allows a finite set of values)
* array
* variable (no validation)

#### The Console Component
#### The Contracts Component
#### [The CssSelector Component](https://symfony.com/doc/5.0/components/css_selector.html)
> The CSS Selector component converts CSS selectors to XPath expressions using the `vendor/symfony/css-selector/CssSelectorConverter.php::toXPath()` method.
#### [The DependencyInjection Component](https://symfony.com/doc/5.0/components/dependency_injection.html)
#### [The DomCrawler Component](https://symfony.com/doc/5.0/components/dom_crawler.html)
> The DomCrawler component eases DOM navigation for HTML and XML documents.
#### The EventDispatcher Component
#### [The ExpressionLanguage Component](https://symfony.com/doc/5.0/components/expression_language.html)
> The ExpressionLanguage component provides an engine that can compile and evaluate expressions. An expression is a one-liner that returns a value (mostly, but not limited to, Booleans).

Expression language can be used for (and not limited to):
* configuration to facilitate more complex logic
* route annotations when more complex matching is required

[Expression syntax](https://symfony.com/doc/5.0/components/expression_language/syntax.html)

[Supported literals](https://symfony.com/doc/5.0/components/expression_language/syntax.html#supported-literals)
* strings
* numbers
* arrays
* hashes
* booleans
* null
* exponential

A backslash in a string must be escaped with four backslashes.
A backslash in a regular expression must be escaped with 8 backslashes.
Escape the \n control character with an extra backslash, \\n.

When working with objects, properties and methods can be addressed using a . operator... 'fruit.variety' and 'robot.say("Hello")'

Access to constant values is possible with the use of the constant() built in function, 'constant("PHP_VERSION")'... it's the only built in function but [custom functions can be registered and used](https://symfony.com/doc/5.0/components/expression_language/extending.html).

[Supported operators](https://symfony.com/doc/5.0/components/expression_language/syntax.html#supported-operators)
* Arithmetic operators:
    * ```+```
    * ```-```
    * ```*```
    * ```/```
    * ```%```
    * ```**```
* Bitwise operators:
    * ```&```
    * ```|```
    * ```^```
* Comparision operators:
    * ```==```
    * ```===```
    * ```!=```
    * ```!==```
    * ```<```
    * ```>```
    * ```<=```
    * ```>=```
    * ```matches```
* Logical operators:
    * ```not or !```
    * ```and or &&```
    * ```or or ||```
* String operators:
    * ```~```
* Array operators:
    * ```in```
    * ```not in```
* Numeric operators:
    * ```..```
* Ternary operators:
    * ```foo ? 'yes' : 'no'```
    * ```foo ?: 'no'```
    * ```for ? 'yes'```

[Caching Expressions Using Parser Caches](https://symfony.com/doc/5.0/components/expression_language/caching.html)
#### The Filesystem Component
#### [The Finder Component](https://symfony.com/doc/5.0/components/finder.html)
> The Finder component finds files and directories based on different criteria (name, file size, modification time, etc.) via an intuitive fluent interface.

Exclude directories from matching with the `exclude()` method.

#### The Form Component
#### [The HttpClient Component](https://symfony.com/doc/5.0/http_client.html)
> The HttpClient component is a low-level HTTP client with support for both PHP stream wrappers and [cURL](https://curl.se/). It provides utilities to consume APIs and supports synchronous and asynchronous operations.

HttpClient configuration can be set globally in `config/packages/framework.yaml`:

```yaml
# config/packages/framework.yaml
framework:
    http_client:
        default_options:
            ...
 ```

 or on a per request basis when you call the request method (HttpClientInterface::request): you can pass an array of options that will override (or add to) those set in configuration as the third argument).

 However, the [max_host_connections](https://symfony.com/doc/5.0/reference/configuration/framework.html#max-host-connections) option cannot be overridden per request.

See the [HttpClient configuration reference](https://symfony.com/doc/5.0/reference/configuration/framework.html#reference-http-client) for a complete list of HttpClient configuration options.

[Scoped client configuration](https://symfony.com/doc/5.0/http_client.html#scoping-client) uses the `Symfony\Component\HttpClient\ScopingHttpClient` class to enable the setting of default configuration *for specific requests*. To use it, add a `scoped_clients` key under the `http_client` key and specify the `scope` regular expression plus the configuration options that will be used when the `scope` regular expression matches the request URL.

Each scoped client configuration block automatically generates a corresponding [named autowiring alias](https://symfony.com/doc/5.0/service_container/autowiring.html#using-aliases-to-enable-autowiring).

**Injecting a named HttpClientInterface autowire alias**
```yaml
# config/packages/framework.yaml
framework:
    http_client:
        scoped_clients:
            symfony_client:
                base_uri: 'https://symfony.com'
 ```

 ```php
<?php

namespace App\Controller;

use Symfony\Bundle\FrameworkBundle\Controller\AbstractController;
use Symfony\Contracts\HttpClient\HttpClientInterface;

class DefaultController extends AbstractController
{
    /**
     * $symfonyClient will use passed a HttpClientInterface that is configured
     * with the symfony_client scoped_client configuration.
     */
    public function index(HttpClientInterface $symfonyClient)
    {
        $response = $symfonyClient->request('GET', '/what-is-symfony');
        ....
    }
}
 ```

 [Handling exceptions](https://symfony.com/doc/5.0/http_client.html#handling-exceptions)
 There are three types of exceptions:

* Exceptions implementing the `Symfony\Contracts\HttpClient\Exception\HttpExceptionInterface` are thrown when your code does not handle the status codes in the 300-599 range
* Exceptions implementing the `Symfony\Contracts\HttpClient\Exception\TransportExceptionInterface` are thrown when a lower level issue occurs
* Exceptions implementing the `Symfony\Contracts\HttpClient\Exception\DecodingExceptionInterface` are thrown when a content-type cannot be decoded to the expected representation

Exceptions can occur in calls to methods on the returned `Symfony\Contracts\HttpClient\ResponseInterface` so it's important to wrap not only the initial $client->request() method call but also calls to `ResponseInterface::getHeaders()` for example.

[Interoperability](https://symfony.com/doc/5.0/http_client.html#interoperability)
> The component is interoperable with four different abstractions for HTTP clients: [Symfony Contracts](https://github.com/symfony/contracts), [PSR-18](https://www.php-fig.org/psr/psr-18/), [HTTPlug v1/v2](https://github.com/php-http/httplug/#readme) and [native PHP streams](https://www.php.net/manual/en/book.stream.php). If your application uses libraries that need any of them, the component is compatible with all of them. They also benefit from autowiring aliases when the framework bundle is used.

#### The HttpFoundation Component
**[The HttpFoundation Request class](https://symfony.com/doc/5.0/introduction/http_fundamentals.html#symfony-request-object)**
>  The Symfony\Component\HttpFoundation\Request class is an object-oriented representation of the HTTP request message. With it, you have all the request information at your fingertips.

Incoming PHP variables are made available on the Request object as public properties:

```php
$request->request // Instance of Symfony\Component\HttpFoundation\ParameterBag, wraps $_GET
$request->query // Instance of Symfony\Component\HttpFoundation\ParameterBag, wraps $_POST
$request->cookies // Instance of Symfony\Component\HttpFoundation\ParameterBag, wraps $_COOKIE
$request->files // Instance of Symfony\Component\HttpFoundation\FileBag, FileBag extends ParameterBag, wraps $_FILES
$request->server // Instance of Symfony\Component\HttpFoundation\ServerBag, ServerBag extends ParameterBag, wraps $_SERVER
$request->headers // A class implementing the [IteratorAggregate](https://www.php.net/manual/en/class.iteratoraggregate.php) and [Countable](https://www.php.net/manual/en/class.countable.php) interfaces
```

You can reach inside each *bag* with the `get()` method.

```php
$request->query->get('name', 'a default value if name is not set');
```

**Request::isSecure()**
> As a bonus, the Request class does a lot of work in the background that you’ll never need to worry about. For example, the isSecure() method checks the three different values in PHP that can indicate whether or not the user is connecting via a secured connection (i.e. HTTPS).

Each of the following checks is made and in turn and the method returns early if any check returns true...

* inspects the [X-Forwarded-Proto](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/X-Forwarded-Proto) header (if the request is from a trusted proxy)
* inspects the value of `$_SERVER['HTTPS']`

TODO: Check the `Request::getTrustedValues()` method to see if that is checking for a secured connection.

**[The HttpFoundation Response class](https://symfony.com/doc/5.0/introduction/http_fundamentals.html#symfony-response-object)**
> Symfony also provides a Symfony\Component\HttpFoundation\Response class: a PHP representation of an HTTP response message. This allows your application to use an object-oriented interface to construct the response that needs to be returned to the client.

**Notable methods**
```php
$response->setContent() // Takes a string argument.
$response->setStatusCode() // Takes an integer as its first argument: the Response class has the HTTP methods as class constants (Response::HTTP_OK) and a string status message as its second argument.
```

Response headers can be set, `$response->headers` is a public class property which is an instance of `vendor/symfony/http-foundation/ResponseHeaderBag.php`:
```php
$response->headers->set('Content-Type', 'text/html');
```

**A little program**
```php
<?php

require './vendor/autoload.php';

use Symfony\Component\HttpFoundation\Response;

$response = new Response();

$response->setContent('Hello, world!');
$response->setStatusCode(Response::HTTP_OK, "Every little thing... is gonna be okay.");
$response->headers->set('Content-Type', 'text/html');

dd($response->__toString());

"""
HTTP/1.0 200 Every little thing... is gonna be okay.\r\n
Cache-Control: no-cache, private\r\n
Content-Type:  text/html\r\n
Date:          Wed, 31 Mar 2021 14:02:19 GMT\r\n
\r\n
Hello, world!
"""
```
There are some helper classes which extend Response and make it easy to return different types of responses:
* `vendor/symfony/http-foundation/BinaryFileResponse.php`
* `vendor/symfony/http-foundation/RedirectResponse.php`
* `vendor/symfony/http-foundation/StreamedResponse.php`
* `vendor/symfony/http-foundation/JsonResponse.php`

#### The HttpKernel Component
#### The Inflector Component
#### [The Intl Component](https://symfony.com/doc/5.0/components/intl.html)
> This component provides access to the localization data of the [ICU library](http://site.icu-project.org/). It also provides a PHP replacement layer for the C [intl extension](https://www.php.net/manual/en/book.intl.php).

[ICU library](http://site.icu-project.org/)
> ICU is a mature, widely used set of C/C++ and Java libraries providing Unicode and Globalization support for software applications. ICU is widely portable and gives applications the same results on all platforms and between C/C++ and Java software.

> The replacement layer is limited to the en locale. If you want to use other locales, you should [install the intl extension](https://www.php.net/manual/en/intl.setup.php). There is no conflict between the two because, even if you use the extension, this package can still be useful to access the ICU data.

TODO: https://symfony.com/doc/5.0/translation.html

#### The Ldap Component

#### [The Lock Component](https://symfony.com/doc/5.0/components/lock.html)
> The Lock Component creates and manages [locks](https://en.wikipedia.org/wiki/Lock_(computer_science)), a mechanism to provide exclusive access to a shared resource.

The Lock component isn't installed by default (when you've installed Symfony with `symfony new project-name --full`: it needs to be installed separately with `composer require symfony/lock` (or just `composer require lock` if you've got Symfony Flex installed).

I had to upgrade from PHP7.3 to PHP7.4 to satisfy a dependency on laminas/laminas-code.

**Notable classes**

* `Symfony\Component\Lock\LockFactory`
* `Symfony\Component\Lock\Store\SemaphoreStore`

These two classes are used together to create a lock factory as follows:

```php
use Symfony\Component\Lock\LockFactory;
use Symfony\Component\Lock\Store\SemaphoreStore;

$store = new SemaphoreStore();
$factory = new LockFactory($store);

/** @var \Symfony\Component\Lock\LockInterface $lock */
$lock = $factory->createLock('some-resource');

if ($lock->acquire()) {
    // Wrap job in try/catch/finally block as recommended.
    try {
        // Do processing...
    } finally {
        $lock->release();
    }
}
```

##### [Blocking locks](https://symfony.com/doc/5.0/components/lock.html#blocking-locks)
In some cases you may want to wait indefinitely to acquire a lock. This can be achieved by requesting _blocking lock_ as follows:

```php
// Create the lock as normal...
$lock->acquire(true);
// Code execution will continue here when the lock has been acquired.
```

##### [Expiring locks](https://symfony.com/doc/5.0/components/lock.html#expiring-locks)

By default, locks are released on instance destruction... however, a _persistant_ lock can be created with...

```php
// Create the lock, variables show arguments.
$ttl = 300.0;
$autoRelease = false;
$lock = $factory->createLock('some-process', $ttl, $autoRelease);
```

If the job involves unknown iterations, the lock can be _refreshed_ as follows:

```php
$lock = $factory->createLock('some-process', 5.0);
$lock->aquire();
try {
    foreach ($items as $item) {
        // Process $item.

        // Reset (refresh) the time-to-live to 5 seconds.
        $lock->refresh();

        // Alternatively, alter the time-to-live...
        $lock->refresh(10.0);
    }
} finally {
    $lock->release();
}
```

#### [The Mailer Component](https://symfony.com/doc/5.0/mailer.html)
> Symfony's Mailer & [Mime](https://symfony.com/doc/5.0/components/mime.html) components form a _powerful_ system for creating and sending emails - complete with support for multipart messages, Twig integration, CSS inlining, file attachments and a lot more.

Emails are _transported_, (there are various transport mechanisms), Symfony can use SMTP out-of-the-box with the configuration for the DSN (Delivery Status Notification) in the .env file as follows:

```
# .env
MAILER_DSN=smtp://user:pass@smtp.example.com:port
```

NOTE: [Swiftmailer](https://swiftmailer.symfony.com/docs/introduction.html) MAILER_DSN format is different.

```yaml
# Swiftmailer Configuration
swiftmailer:
    transport: "%mailer_transport%"
    host:      "%mailer_host%"
    username:  "%mailer_user%"
    password:  "%mailer_password%"
    spool:     { type: memory }

```

#### The Messenger Component
#### The Mime Component
#### The OptionsResolver Component
#### The PHPUnit Bridge
#### The Process Component
#### The PropertyAccess Component
#### The PropertyInfo Component
#### The PSR-7 Bridge
#### [The Security Component](https://symfony.com/doc/5.0/components/security.html)
Composed of four, smaller sub-components:

* symfony/security-core
* symfony/security-http
* symfony/security-csrf
* symfony/security-guard

UserCheckers implementing `Symfony\Component\Security\Core\Exception\AccountStatusException\UserCheckerInterface` need to implement the following methods:

* checkPreAuth()
* checkPostAuth()

[Security Configuration Reference (SecurityBundle)](https://symfony.com/doc/5.0/reference/configuration/security.html)

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
* For caching, using the Cache Contracts approach is recommended: it requires less code boilerplate and provides cache stampede protection by default.
* Use annotations for configuring routes
* Use Symfony CLI binary to create new projects
* Use the default Symfony directory structure
* Use Symfony Flex in projects
* Keep services private
* Do not inject the container because it hides the actual dependencies and gives too much access... doing so also requires that services be made public
* Put as little logic as possible in controllers (thin controllers)
* Use the same controller action to render and to process forms
* Redirect after a successful form submission to prevent the user from hitting the refresh button
* In Symfony versions prior to 4.0, it was recommended to organize your own application code using bundles. This is no longer recommended and bundles should only be used to share code and features between multiple applications.
* [Bundle naming conventions](https://symfony.com/doc/5.0/bundles/best_practices.html#bundle-name)

### [Release management](https://symfony.com/releases)
Symfony releases follow [semantic versioning](https://semver.org/) and the release schedule is:
* Symfony patch version every month - bug fixes, no breaking changes
* Symfony minor version every six months (May and November) - bug fixes and new features, no breaking changes
* Symfony major version every two years - may contain breaking changes

All major and minor releases are preceded by...
* four months of development (adding new features and enhancing existing ones)
* two months of stabilisation (bug fixing, release preparation, third-party libraries, bundles and projects to catch up)

Starting with Symfony 3.x, minor version releases are limited to five version per branch with the last minor version (3.4, 4.4, 5.4 etc) being considered the *LTS (long term support)* version. The other minor versions are considered *standard* versions. LTS versions of Symfony are released every two years.

Standard versions have bugs fixes for eight months and security issue fixes for eight months.

LTS versions have bug fixes for three years and security issue fixes for four years.

### [Backward compatibility promise](https://symfony.com/doc/5.0/contributing/code/bc.html)
The backward compatibility promise was introduced in Symfony 2.3 and ensures smooth minor release project upgrades with no backward compatibility breaks with the exception of:
* experimental features
* code marked with the `@internal` tag
* situations where a security fix necessitates a backward compatibility break

#### [Using Symfony code](https://symfony.com/doc/5.0/contributing/code/bc.html#using-symfony-code)
With the exception of code tagged with `@internal`, all...
* interfaces can be implemented
* classes can be extended but the adding of a new property or method is considered unsafe, in addition calling private methods or accessing private properties via reflection is considered unsafe
* traits can be used

#### [Contributing (working on Symfony code)](https://symfony.com/doc/5.0/contributing/code/bc.html#working-on-symfony-code)

### Deprecations best practices

**Symfony Standard Edition**
Symfony standard edition is no longer available since Symfony 4
A project using the Symfony standard edition will have symfony/symfony dependency in composer.json
Remove it with:
```bash
$ composer remove symfony/symfony
```

### Framework overloading
### [Release management and roadmap schedule](https://symfony.com/releases)
### Framework interoperability and PSRs
[Accepted](https://www.php-fig.org/psr/#accepted) as of April 2021
* PSR-1 Basic Coding Standard
* PSR-3 Logger Interface
* PSR-4 Autoloading Standard
* PSR-6 Caching Interface
* PSR-7 HTTP Message Interface
* PSR-11 Container Interface
* PSR-12 Extended Coding Style Guide
* PSR-13 Hypermedia Links
* PSR-14 Event Dispatcher
* PSR-15 HTTP Handlers
* PSR-16 Simple Cache
* PSR-17 HTTP Factories
* PSR-18 HTTP Client

[Abandoned](https://www.php-fig.org/psr/#abandoned)
* PSR-8 Huggable Interface
* PSR-9 Security Advisories
* PSR-10 Security Reporting Process

[Deprecated](https://www.php-fig.org/psr/#deprecated)
* PSR-0 Autoloading Standard
* PSR-2 Coding Style Guide
### Naming conventions
## [Controllers](https://symfony.com/doc/5.0/controller.html)
Every request passes through the `public/index.php` front controller.

### Naming conventions
### The base AbstractController class
**Provides access to parameters**
The AbstractController has a method called getParameter() which takes the string parameter name of the parameter to get.

```yaml
# config/services.yaml
parameters:
    app.greeting: 'Hello, world!'
```

```php
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
[Creating routes](https://symfony.com/doc/5.0/routing.html#creating-routes)
Routes can be configured in [YAML, XML, PHP](https://symfony.com/doc/5.0/routing.html#creating-routes-in-yaml-xml-or-php-files) or by using [annotations](https://symfony.com/doc/5.0/routing.html#creating-routes-as-annotations) (annotations is the Symfony recommendation).
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
[Twig Internals](https://twig.symfony.com/doc/3.x/internals.html)
**Steps performed to render a Twig template**
The template is loaded, if it's not compiled, the following three steps occur:
* the lexer tokenizes the template source code
* the parser converts the token stream into the abstract syntax tree
* the compiler converts the abstract syntax tree into PHP code
Finally, the `display()` method of the compiled template is called.

### Auto escaping
### Template inheritance
### Global variables
### Filters and functions
### Template includes
### Loops and conditions
### URLs generation
### Controller rendering
### Translations and pluralization
[How to Translate Validation Constraint Messages](https://symfony.com/doc/5.0/validation/translations.html)
> If you're using validation constraints with the Form component, you can translate the error messages by creating a translation resource for the *validators* domain.
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

```php
$this->createFormBuilder();
```
The `createFormBuilder()` method on the AbstractController class loads the `vendor/symfony/form/FormFactory.php` class and calls the `createBuilder()` method on it which returns an implementation of the FormBuilderInterface `vendor/symfony/form/FormBuilderInterface.php` which defaults to `vendor/symfony/form/FormBuilder.php`.

The `FormBuilderInterface` extends the `FormConfigBuilderInterface` (`vendor/symfony/form/FormConfigBuilderInterface.php`) which has the following notable methods:

```php
$formBuilder = $this->createFormBuilder();

...

$formBuilder->setMethod() // so that you can set your form action to POST or GET
$formBuilder->setAction() // so you can control where your form is submitted to
```

There are at least wo other ways of modifying the form:

**Passing options as the third argument to the $formFactory->create() method**

```php
$formFactory = $container->get('form.factory')->create(TaskForm::class, new Task(), ['method' => 'GET'] );
```

**In the template form function**

```twig
{{ form(form, {method: 'GET'}) }}
```

[HTTP method overrides](https://symfony.com/doc/5.0/reference/configuration/framework.html#configuration-framework-http-method-override)

If you set the action (method) of a form to be PUT, PATCH or DELETE, Symfony will include that in a hidden field (_method) on the form and the form will actually be POST'ed but Symfony alters the request method when it hits Symfony so in your controller where your form is submitted to, you could have something like:

```php
if ($request->getMethod() === Request::METHOD_DELETE) { // Do something... }
```

If you're using [Symfony's reverse proxy](https://symfony.com/doc/5.0/http_cache.html#symfony2-reverse-proxy), you need to add a line to public/index.php so:

```php
// public/index.php

$kernel = new Kernel($_SERVER['APP_ENV'], (bool) $_SERVER['APP_DEBUG']);
$request = Request::createFromGlobals();
```

becomes

```php
// public/index.php

$kernel = new Kernel($_SERVER['APP_ENV'], (bool) $_SERVER['APP_DEBUG']);
Request::enableHttpMethodParameterOverride();
$request = Request::createFromGlobals();
```

Create a named form with `$this->get('form.factory')->createNamed('somename', TaskForm::class, new Task());`

If you not extending `AbstractController` and you have autowiring enabled, you can type-hint constructor arguments to inject the form factory as follows:

```php
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
```php
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
### [Form events](https://symfony.com/doc/5.0/form/events.html)
>The Form component provides a structured process to let you customize your forms, by making use of the [EventDispatcher](https://symfony.com/doc/5.0/components/event_dispatcher.html) component. Using form events, you may modify information or fields at different steps of the workflow: from the population of the form to the submission of the data from the request.
### Form type extensions

## [Data Validation](https://symfony.com/doc/5.0/validation.html)
### PHP object validation
### Built-in validation constraints
### Validation scopes
### Validation groups
### Group sequence
### Custom callback validators
### Violations builder

## [Dependency Injection](https://symfony.com/doc/5.0/components/dependency_injection.html)

You can constructor-inject parameters as follows:
```yaml
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
```php
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
### [Service container](https://symfony.com/doc/5.0/service_container.html)
[How to Import Configuration Files/Resources](https://symfony.com/doc/5.0/service_container/import.html)
External service configuration can be imported in two different ways:

* imports
* services

TODO: Check imports and services is correct.

### Built-in services
### [Configuration parameters](https://symfony.com/doc/5.0/configuration.html#configuration-parameters)
`services._defaults.bind` can be used inject a parameter into any service or controller where the argument is named exactly the same.

```yaml
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

```php
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

### [Services registration](https://symfony.com/doc/5.0/service_container.html#creating-configuring-services-in-the-container)
### [Tags](https://symfony.com/doc/5.0/service_container/tags.html)
### Semantic configuration
### [Factories](https://symfony.com/doc/5.0/service_container/factories.html)
### [Compiler passes](https://symfony.com/doc/5.0/service_container/compiler_passes.html)
### [Services autowiring](https://symfony.com/doc/5.0/service_container/autowiring.html)
If you type-hint your controller constructor arguments, Symfony will pass in the services automagically: you don't even have to have your controller extend `AbstractController` if you don't want to.

For this to work, autowire must be true and classes in App\Controller must be tagged with `controller.service_arguments` which can be done like this:

```yaml
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

```php
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

```yaml
// config/services.yaml
services:
    App\Controller\DefaultController:
        tags: ['controller.service_arguments']
        bind:
            $formFactory: '@form.factory'
```

then in your controller:

```php
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

## [Security](https://symfony.com/doc/5.0/security.html)
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

```php
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

```bash
$ composer dump-env prod
```

dump-env is available in Symfony Flex 1.2 (or later)

dump-env parses all the .env files and dumps their final values in a file named .env.local.php

List environment variables with:

```bash
$ php bin/console debug:container --env-vars
$ php bin/console debug:container --env-vars app // TODO: Check why this didn't seem to work for me
$ php bin/console debug:container --env-var=APP_SECRET
```

TODO: https://symfony.com/doc/5.0/configuration/secrets.html

Requires libsodium (ships with >= PHP7.2)

Create an asymmetric cryptographic public (for encrypting/writing) and private (for decrypting/reading) keys.

dev keys can be safely committed to version control but the prod private key **MUST never be committed** (is .gitignored).

**Setting secrets**
```bash
# set your a default development value (can be overridden locally)
$ php bin/console secrets:set DATABASE_PASSWORD
```

```bash
# set your production value
$ php bin/console secrets:set DATABASE_PASSWORD --env=prod
```

**Accessing secrets**
```yaml
# config/packages/doctrine.yaml
doctrine:
    dbal:
        password: '%env(DATABASE_PASSWORD)%'
```

Environment variables override always take precedence over secrets if they have the same name.

Listing secrets**
```bash
$ php bin/console secrets:list --reveal
```

**Removing secrets**
```bash
$ php bin/console secrets:remove DATABASE_PASSWORD
```

If you don't deploy your `config/secrets/prod/prod.decrypt.private.php` file to your production target, you can base64 encode it and set the `SYMFONY_DECRYPTION_SECRET` environment variable.

```bash
$ php -r 'echo base64_encode(require "config/secrets/prod/prod.decrypt.private.php");'
```

To avoid PHP decrypting the secrets at runtime, you can run:

```bash
$ php bin/console secrets:decrypt-to-local --force --env=prod
```

which will decrypt all the secrets to the .env.prod.local file, after which the private key can be removed from the production server.

**Rotating keys**

```bash
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
### Filesystem and [Finder](https://symfony.com/doc/5.0/components/finder.html) components
The `Symfony\Component\Finder\Finder` class has a fluent interface and implements [IteratorAggregate](https://www.php.net/manual/en/class.iteratoraggregate.php) interface.

Each iteration of Finder will return an instance of `Symfony\Component\Finder\SplFileInfo` which extends [PHP's SplFileInfo class](https://www.php.net/manual/en/class.splfileinfo.php).

To read the contents of the file, call the `Symfony\Component\Finder\SplFileInfo::getContents()` method.

### Lock component
See notes for the [lock component](#the-lock-component) under the Components section.
### Web Profiler, Web Debug Toolbar and Data collectors
The Web Profiler configuration is located in `config/packages/dev/web_profiler.yaml`
### Internationalization and localization (and Intl component)

## Worth knowing about

### [Maker bundle](https://symfony.com/doc/current/bundles/SymfonyMakerBundle/index.html)

### [Webpack Encore](https://symfony.com/doc/5.0/frontend/encore/installation.html)
Install node.js and yarn package manager first.

If you're using Webpack Encore in a project that has Symfony Flex installed, then all you need to run is:

```bash
$ composer require symfony/webpack-encore-bundle
$ yarn install
```

Installing the symfony/webpack-encore-bundle will also create config/packages/assets.yaml and configure Symfony to use the JSON manifest versioning strategy by default.

### [Bundles](https://symfony.com/doc/5.0/bundles.html)
> A bundle is similar to a plugin in other software, but even better. The core features of Symfony framework are implemented with bundles (FrameworkBundle, SecurityBundle, DebugBundle, etc.) They are also used to add new features in your application via [third-party bundles](https://github.com/search?q=topic%3Asymfony-bundle&type=Repositories).

Bundle classes should extend the abstract class `Symfony\Component\HttpKernel\Bundle\Bundle`.

[Bundle naming conventions](https://symfony.com/doc/5.0/bundles/best_practices.html#bundle-name)

[Bundle directory structure](https://symfony.com/doc/5.0/bundles.html#bundle-directory-structure)

#### [Overriding bundles](https://symfony.com/doc/5.0/bundles/override.html)
Templates can be overridden by copying them to

### Logical paths
Logical paths are paths prefixed with @, for example @FooBundle/Resources/config/services.xml

The `vendor/symfony/http-kernel/Kernel.php::locateResource()` method is able to resolve a logical path to a physical path, constructor-inject Kernel by type-hinting `Symfony\Component\HttpKernel\KernelInterface` to make it available in controllers.

### [Performance](https://symfony.com/index.php/doc/5.0/performance.html)
It's recommended that the `realpath_cache_size` PHP setting in `php.ini` should be set to at least `4096K`.
