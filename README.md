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

### 2.1 Use PHPStan strict rules
```bash
composer require --dev phpstan/phpstan-strict-rules
```

```neon
includes:
    - vendor/phpstan/phpstan-strict-rules/rules.neon
```

### 2.2 Use PHPStan safe rule
```bash
composer require --dev thecodingmachine/phpstan-safe-rule
```

```neon
includes:
    - vendor/thecodingmachine/phpstan-safe-rule/phpstan-safe-rule.neon
```

### 2.3 Use PHPStan generic rules
```bash
composer require --dev korbeil/phpstan-generic-rules
```

```neon
includes:
    - vendor/korbeil/phpstan-generic-rules/extension.neon
```

## 3. Setup Travis
First of all use the default .travis.yml file bundled with Sylius plugin skeleton.

After that you need to add the plugin to travis-ci.org/com (depending on the public setting of the repository).

Remember to add a cron job that will test the plugin weekly.

Add a badge to the README.md file.

## 4. Setup Scrutinizer
Add the `.scrutinizer.yml` file to your project. Here is an example:

```yaml
build:
    nodes:
        analysis:
            tests:
                override:
                    - php-scrutinizer-run
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

## 7. Add `.gitattributes` file
Add a `.gitattributes` file to minimize the payload when installing packages. An example could be:

```text
/etc                        export-ignore
/features                   export-ignore
/spec                       export-ignore
/tests                      export-ignore
/.gitattributes             export-ignore
/.gitignore                 export-ignore
/.scrutinizer.yml           export-ignore
/.travis.yml                export-ignore
/behat.yml.dist             export-ignore
/easy-coding-standard.yml   export-ignore
/phpspec.yml.dist           export-ignore
/phpstan.neon               export-ignore
/README.md                  export-ignore
```

## 8. Use EditorConfig plugin and file
Download and install the [EditorConfig plugin](https://plugins.jetbrains.com/plugin/7294-editorconfig) and include a `.editorconfig` file in the root of the plugin. An example could be (taken from [Sylius](https://raw.githubusercontent.com/Sylius/Sylius-Standard/master/.editorconfig)):

## 9. Use subscribers instead of listeners
When you define event listeners/subscribers, use subscribers. See [tomasvotruba.cz/blog/2019/05/16/don-t-ever-use-listeners/](https://www.tomasvotruba.cz/blog/2019/05/16/don-t-ever-use-listeners/)

## 10. Normalize composer.json
Install:

```bash
composer require --dev localheinz/composer-normalize
```

Run:
```bash
composer normalize
```

For CI tools (like Travis):
```bash
composer normalize --dry-run
```

## 11. Guard against development packages in production
Read more here: [kalessil/production-dependencies-guard](https://github.com/kalessil/production-dependencies-guard)

Just run this and it will work:

```bash
composer require --dev kalessil/production-dependencies-guard:dev-master
```

## 12. Add github actions

See a good example of the workflow file here: [github.com/Setono/SyliusRedirectPlugin/blob/master/.github/workflows/build.yaml](https://github.com/Setono/SyliusRedirectPlugin/blob/master/.github/workflows/build.yaml)