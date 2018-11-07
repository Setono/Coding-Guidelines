# Setono Coding Guidelines
This is a list of coding guidelines for Setono employees and partners and they are targeted **Sylius development**. If you find an error or outdated information, please create a PR and fix it :)

## 1. Use Easy Coding Standard
Always use Easy Coding Standard to style your code the Sylius way.

Follow the installation instructions [here](https://github.com/Symplify/EasyCodingStandard).

After that put a `easy-coding-standard.yml` file in the root of your project with the following contents:

```yaml
imports:
    - { resource: 'vendor/sylius-labs/coding-standard/easy-coding-standard.yml' }
```

Now you can run a code style check with this command:

```bash
$ vendor/bin/ecs check src
```

and fix errors using this command:

```bash
$ vendor/bin/ecs check src --fix
```

## 2. Use PHPStan
Any plugin must have 0 PHPStan errors. If you add an error to the ignore list you must have a very good reason.

## 3. Setup Travis
First of all use the default .travis.yml file bundled with Sylius plugin skeleton.

After that you need to add the plugin to travis-ci.org/com (depending on the public setting of the repository).

Remember to add a cron job that will test the plugin weekly.

Add a badge to the README.md file.

## 4. Setup Scrutinizer
Add the `.scrutinizer.yml` file to your project. Here is an example:

```yaml
build:
    environment:
        variables:
            COMPOSER_MEMORY_LIMIT: -1

filter:
    excluded_paths: [tests/*, spec/*]
```

Add the plugin to [scrutinizer-ci.com](https://scrutinizer-ci.com). 

Finally add the code quality badge.

We aim for 10 in code quality!

## 5. Resources
When adding resources to your plugin use the [Sylius\Bundle\ResourceBundle\AbstractResourceBundle](https://github.com/Sylius/Sylius/blob/master/src/Sylius/Bundle/ResourceBundle/AbstractResourceBundle.php) as a base for your plugin to add resource configs in code instead of yaml/xml.

Also put entities in a `Model` directory instead of a `Entity` directory.

See an example of the above [here](https://github.com/Setono/SyliusRedirectPlugin/blob/master/src/SetonoSyliusRedirectPlugin.php) and [here](https://github.com/Setono/SyliusRedirectPlugin/blob/master/src/DependencyInjection/Configuration.php).

When adding database mapping files we use underscore in column names. Here is an example of how to do that: `<field name="apiKey" column="api_key" />`

## 6. Install Php Inspections (EA Extended)
Install the [PHP Inspections plugin](https://github.com/kalessil/phpinspectionsea/blob/master/docs/getting-started.md) in your PhpStorm and inspect your code before pushing. You do this by clickig `Code > Inspect Code`.

