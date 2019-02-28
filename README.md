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
Download and install the [EditorConfig plugin](https://plugins.jetbrains.com/plugin/7294-editorconfig) and include a `.editorconfig` file in the root of the plugin. An example could be (taken from [Sylius](https://github.com/Sylius/Sylius-Standard/blob/master/.editorconfig)):
```text
# EditorConfig helps developers define and maintain consistent
# coding styles between different editors and IDEs
# editorconfig.org

root = true

[*]
# Change these settings to your own preference
indent_style = space
indent_size = 4

# We recommend you to keep these unchanged
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true

[*.feature]
indent_style = space
indent_size = 2

[*.js]
indent_style = space
indent_size = 2

[*.json]
indent_style = space
indent_size = 2

[*.md]
indent_style = space
indent_size = 4
trim_trailing_whitespace = false

[*.neon]
indent_style = tab
indent_size = 4

[*.php]
indent_style = space
indent_size = 4

[*.sh]
indent_style = tab
indent_size = 4

[*.{yaml,yml}]
indent_style = space
indent_size = 4
trim_trailing_whitespace = false

[.babelrc]
indent_style = space
indent_size = 2

[.gitmodules]
indent_style = tab
indent_size = 4

[.php_cs{,.dist}]
indent_style = space
indent_size = 4

[composer.json]
indent_style = space
indent_size = 4

[docker-compose{,.override}.{yaml,yml}]
indent_style = space
indent_size = 2

[Dockerfile]
indent_style = tab
indent_size = 4

[package.json]
indent_style = space
indent_size = 2

[phpspec.yml{,.dist}]
indent_style = space
indent_size = 4

[phpstan.neon]
indent_style = tab
indent_size = 4

[phpunit.xml{,.dist}]
indent_style = space
indent_size = 4
```

## 9. Use subscribers instead of listeners
When you define event listeners/subscribers, use subscribers. 