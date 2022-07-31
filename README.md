# E-commerce Website
Websites built on the Magento platform are search engine friendly. And a search friendly website helps customers find our site with less pain. Magento also provides the search engine friendly tools structure like sitemap, URL writer etc, that help your site become more visible to the search engines.

A set of Magento rules for [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) tool.

## Installation within a Magento 2 site

To use within your Magento 2 project you can use:

```bash
composer require --dev magento/magento-coding-standard
```

Due to security, when installed this way the Magento standard for phpcs cannot be added automatically.
You can achieve this by adding the following to your project's `composer.json`:

```json
"scripts": {
    "post-install-cmd": [
      "([ $COMPOSER_DEV_MODE -eq 0 ] || vendor/bin/phpcs --config-set installed_paths ../../magento/magento-coding-standard/)"
    ],
    "post-update-cmd": [
      "([ $COMPOSER_DEV_MODE -eq 0 ] || vendor/bin/phpcs --config-set installed_paths ../../magento/magento-coding-standard/)"
    ]
}
```
# Technical Architecture:
<img src="https://github.com/Sourav19990711/E-commerce-Website/blob/main/archi_diagram_desired-state.png" width= "400"/>

### Installation for development

You can install Magento Coding Standard by cloning this GitHub repo:

```bash
git clone git@github.com:magento/magento-coding-standard.git
cd magento-coding-standard
composer install
```

It is possible also to install a standalone application via [Composer](https://getcomposer.org)

```bash
composer create-project magento/magento-coding-standard --stability=dev magento-coding-standard
```

### Verify installation

Command should return the list of installed coding standards including Magento2.

```bash
vendor/bin/phpcs -i
```

## Usage

Once installed, you can run `phpcs` from the command-line to analyze your code `MyAwesomeExtension`

```bash
vendor/bin/phpcs --standard=Magento2 app/code/MyAwesomeExtension
```

### Fixing issues automatically

Also, you can run `phpcbf` from the command-line to fix your code `MyAwesomeExtension` for warnings like "PHPCBF CAN FIX THE [0-9]+ MARKED SNIFF VIOLATIONS AUTOMATICALLY"

```bash
vendor/bin/phpcbf --standard=Magento2 app/code/MyAwesomeExtension
```





## Testing

All rules should be covered by unit tests. Each `Test.php` class should be accompanied by a `Test.inc` file to allow for unit testing based upon the PHP_CodeSniffer parent class `AbstractSniffUnitTest`.
You can verify your code by running

```bash
vendor/bin/phpunit
```

Also, verify that the sniffer code itself is written according to the Magento Coding Standard:

```bash
vendor/bin/phpcs --standard=Magento2 Magento2/ --extensions=php
```

### ESLint
Prerequisites: [Node.js](https://nodejs.org/) (`^12.22.0`, `^14.17.0`, or `>=16.0.0`).

You need to run the following command to install all the necessary packages described in the `package.json` file:
```bash
npm install
```

You can execute ESLint as follows:
```bash
npm run eslint -- path/to/analyze
```

### RECTOR PHP
From `magento-condign-standard` project, you can execute rector php as follows:
```bash
vendor/bin/rector process Magento2 Magento2Framework PHP_CodeSniffer --dry-run --autoload-file vendor/squizlabs/php_codesniffer/autoload.php
```
The rules from rector that are applied are set inside the config file: `rector.php`

The option `--dry-run` displays errors found, but code is not automatically fixed.

To run rector for `magento` projects you need to:
- Specify the magento path and the autoload file for the magento project: 
```bash
vendor/bin/rector process MAGENTO_PATH --dry-run --autoload-file MAGENTO_AUTOLOAD_FILE
```
Example:
```bash
vendor/bin/rector process magento2ce/app/code/Magento/Cms/Model --dry-run --autoload-file magento2ce/vendor/autoload.php
```

