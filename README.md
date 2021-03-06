# WP Plugin Version Management
Simple WordPress Plugin Library To Handle Version Management To Provide Easy Upgrade Handling.

[![Latest Stable Version][latest-stable-version-img]][latest-stable-version-link]
[![Latest Unstable Version][latest-Unstable-version-img]][latest-Unstable-version-link]
[![Total Downloads][total-downloads-img]][total-downloads-link]
[![WP][wpcs-img]][wpcs-link]
[![License][license-img]][license-link]
[![composer.lock available][composerlock-img]][composerlock-link]

## Installation
The preferred way to install this extension is through [Composer][composer].

To install **WP Plugin Version Management library**, simply:

    $ composer require varunsridharan/wp-plugin-version-management

The previous command will only install the necessary files, if you prefer to **download the entire source code** you can use:

    $ composer require varunsridharan/wp-plugin-version-management --prefer-source

You can also **clone the complete repository** with Git:

    $ git clone https://github.com/varunsridharan/wp-plugin-version-management.git

Or **install it manually**:

[Download WP Plugin Version Management.zip][downloadzip]:

    $ wget https://github.com/varunsridharan/wp-plugin-version-management/archive/master.zip

## Arguments / Options
### `slug`
Unique Key for your plugin
### `version`
You Should Pass your plugins version.
### `logs`
If its set to true then it saves update / install logs in database
#### Example Log
```php
array(
	'1.0' => array(
		'user_id' => 1, // Stores Current User ID who install / upgrades the plugin
		'time'    => 2999391, // Stores Upgrade As Timestamp using `current_time('timestamp')`
		'from'    => false, // Which Version is upgraded from | false means its a fresh install
	),
	'1.1' => array(
		'user_id' => 1, // Stores Current User ID who install / upgrades the plugin
		'time'    => 3949391, // Stores Upgrade As Timestamp using `current_time('timestamp')`
		'from'    => '1.0', // Which Version is upgraded from | false means its a fresh install
	),
);
```

### `option_name`
Custom database key on where to save your plugins version and logs.
by default it stores all plugins version in database using 

#### Example of Common Storage
```php
array(
	'your-plugin-slug'    => array(
		'version' => '',
		'logs'    => '',
	),
	'another-plugin-slug' => array(
		'version' => '',
		'logs'    => array(),
	),
);
```

The above example are stored in `wp_options` table with a common database key `_vs_wp_plugin_upgrader`

## Activation Usage

```php
<?php

register_activation_hook( __FILE__, 'your_plugin_activation' );

if ( ! function_exists( 'your_plugin_install_v1' ) ) {
	function your_plugin_install_v1( $from_version = false, $to_version = false ) {
		// do your stuff.
		return true; // should return something | return true if update is sucess / return false
	}
}

if ( ! function_exists( 'your_plugin_install_v1_1' ) ) {
	function your_plugin_install_v1_1( $from_version = false, $to_version = false ) {
		// do your stuff.
		return true; // should return something | return true if update is sucess / return false
	}
}

if ( ! function_exists( 'your_plugin_activation' ) ) {
	function your_plugin_activation() {
		$upgrader = new Varunsridharan\WordPress\Plugin_Version_Management( array(
			'slug'    => 'your-plugin-slug', // Uniquq Slug For Your Plugin.
			'logs'    => true, // Set True to save upgrade logs.
			'version' => '1.2', // Your Plugins New Version
		), array(
			'1.0' => 'your_plugin_install_v1',
			'1.1' => 'your_plugin_install_v1_1',
		) );

		$upgrader->run(); // Run Function Should Be Called.
	}
}

```

## Methods
### `version()`
Return current plugins version stored in database

### `logs()`
Returns Current Plugins Logs

## Method Usage Example

```php
$upgrader = new Varunsridharan\WordPress\Plugin_Version_Management( array(
    'slug'    => 'your-plugin-slug', // Uniquq Slug For Your Plugin.
    'option_name'=> true,// use the same value which is used in register_plugin_activation if not set it to true
));


// Returns Current Version
$upgrader->version();

// Returns Logs
$upgrader->logs();
```

---

<!-- START common-footer.mustache  -->
## 📝 Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

[Checkout CHANGELOG.md](https://github.com/varunsridharan/wp-plugin-version-management/blob/main/CHANGELOG.md)


## 🤝 Contributing
If you would like to help, please take a look at the list of [issues](https://github.com/varunsridharan/wp-plugin-version-management/issues/).


## 📜  License & Conduct
- [**GNU General Public License v3.0**](https://github.com/varunsridharan/wp-plugin-version-management/blob/main/LICENSE) © [Varun Sridharan](website)
- [Code of Conduct](https://github.com/varunsridharan/wp-plugin-version-management/blob/main/.github/CODE_OF_CONDUCT.md)


## 📣 Feedback
- ⭐ This repository if this project helped you! :wink:
- Create An [🔧 Issue](https://github.com/varunsridharan/wp-plugin-version-management/issues/) if you need help / found a bug


## 💰 Sponsor
[I][twitter] fell in love with open-source in 2013 and there has been no looking back since! You can read more about me [here][website].
If you, or your company, use any of my projects or like what I’m doing, kindly consider backing me. I'm in this for the long run.

- ☕ How about we get to know each other over coffee? Buy me a cup for just [**$9.99**][buymeacoffee]
- ☕️☕️ How about buying me just 2 cups of coffee each month? You can do that for as little as [**$9.99**][buymeacoffee]
- 🔰         We love bettering open-source projects. Support 1-hour of open-source maintenance for [**$24.99 one-time?**][paypal]
- 🚀         Love open-source tools? Me too! How about supporting one hour of open-source development for just [**$49.99 one-time ?**][paypal]

<!-- Personl Links -->
[paypal]: https://sva.onl/paypal
[buymeacoffee]: https://sva.onl/buymeacoffee
[twitter]: https://sva.onl/twitter/
[website]: https://sva.onl/website/


## Connect & Say 👋
- **Follow** me on [👨‍💻 Github][github] and stay updated on free and open-source software
- **Follow** me on [🐦 Twitter][twitter] to get updates on my latest open source projects
- **Message** me on [📠 Telegram][telegram]
- **Follow** my pet on [Instagram][sofythelabrador] for some _dog-tastic_ updates!

<!-- Personl Links -->
[sofythelabrador]: https://www.instagram.com/sofythelabrador/
[github]: https://sva.onl/github/
[twitter]: https://sva.onl/twitter/
[telegram]: https://sva.onl/telegram/


---

<p align="center">
<i>Built With ♥ By <a href="https://sva.onl/twitter"  target="_blank" rel="noopener noreferrer">Varun Sridharan</a> <a href="https://en.wikipedia.org/wiki/India">
   <img src="https://cdn.svarun.dev/flag-india.jpg" width="20px"/></a> </i> <br/><br/>
   <img src="https://cdn.svarun.dev/codeispoetry.png"/>
</p>

---


<!-- END common-footer.mustache  -->


[composer]: http://getcomposer.org/download/
[downloadzip]:https://github.com/varunsridharan/wp-plugin-version-management/archive/master.zip



[latest-stable-version-img]: https://poser.pugx.org/varunsridharan/wp-plugin-version-management/version
[latest-Unstable-version-img]: https://poser.pugx.org/varunsridharan/wp-plugin-version-management/v/unstable
[total-downloads-img]: https://poser.pugx.org/varunsridharan/wp-plugin-version-management/downloads
[Latest-Unstable-version-img]: https://poser.pugx.org/varunsridharan/wp-plugin-version-management/v/unstable
[wpcs-img]: https://img.shields.io/badge/WordPress-Standar-1abc9c.svg
[license-img]: https://poser.pugx.org/varunsridharan/wp-plugin-version-management/license
[composerlock-img]: https://poser.pugx.org/varunsridharan/wp-plugin-version-management/composerlock

[latest-stable-version-link]: https://packagist.org/packages/varunsridharan/wp-plugin-version-management
[latest-Unstable-version-link]: https://packagist.org/packages/varunsridharan/wp-plugin-version-management
[total-downloads-link]: https://packagist.org/packages/varunsridharan/wp-plugin-version-management
[Latest-Unstable-Version-link]: https://packagist.org/packages/varunsridharan/wp-plugin-version-management
[wpcs-link]: https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards/
[license-link]: https://packagist.org/packages/varunsridharan/wp-plugin-version-management
[composerlock-link]: https://packagist.org/packages/varunsridharan/wp-plugin-version-management
