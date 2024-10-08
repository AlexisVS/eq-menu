# eQual - Menu

Contributors: (this should be a list of wordpress.org userid's)

Tags: comments, spam

Requires at least: 4.5

Tested up to: 6.5

Requires PHP: 7.4.33

Stable tag: 0.1.3

License: GPLv2 or later

License URI: https://www.gnu.org/licenses/gpl-2.0.html

A plugin that adds a menu to the admin bar.

## Description

This plugin adds a menu to the admin bar.
Menus refer to eQual entities that are used.

## Features

- Add menus to the admin bar.
- Menus refer to eQual entities that are used.
- The plugin is compatible with the eQual framework.
- Submenu in WordPress: opening eQ contexts
- Ability to inject an App (double left menu)

### Usage

call the function `eq_add_menu` in your theme or plugin to add a menu to the admin bar.

```php
add_action( 'init', function () {
    if ( is_admin() ) {
        // Enqueue styles and scripts
        add_action( 'admin_enqueue_scripts', 'eq_menu_enqueue_styles_and_scripts' );

        // Add admin menu
        add_action( 'admin_menu', function () {
            eq_add_menu(
                [
                    [
                        "id"          => "settings.settings.settings_values",
                        "type"        => "entry",
                        "label"       => "Settings values",
                        "description" => "",
                        "context"     => [
                            "entity" => "core\setting\SettingValue",
                            "view"   => "list.default"
                        ]
                    ],
                    [
                        "id"          => "settings.settings.settings_choices",
                        "type"        => "entry",
                        "label"       => "Settings choices",
                        "description" => "",
                        "context"     => [
                            "entity" => "core\setting\SettingChoice",
                            "view"   => "list.default"
                        ]
                    ],
                    [
                        "id"          => "settings.settings.settings",
                        "type"        => "entry",
                        "label"       => "Available Settings",
                        "description" => "",
                        "context"     => [
                            "entity" => "core\setting\Setting",
                            "view"   => "list.default"
                        ]
                    ]
                ], 'eQual', 'Test', 'edit_posts', 'dashicons-menu' );
        } );
    }
} );
```

the menu is an array, and its item structure is as follows:

**JSON format:**

```json
{
    "menu": [
        {
            "id": "users",
            "type": "entry",
            "label": "Users",
            "icon": "person",
            "description": "",
            "context": {
                "entity": "core\\User",
                "view": "list.default"
            }
        },
        ...
    ]
}
```

**PHP format:**

```php
[
    [
        "id"          => "settings.settings.settings_values",
        "type"        => "entry",
        "label"       => "Settings values",
        "description" => "",
        "context"     => [
            "entity"  => "core\setting\SettingValue",
            "view"    => "list.default"
        ]
    ],
    ...
];
```

**eq_add_menu function signature:**

```php
/**
 * Add admin menu.
 *
 * @param string|array $menu_data it can be a path to a json file or an array containing the menu data.
 * An example : (string) $menu_data = plugin_dir(__FILE__). '/assets/menu.json' ;
 *
 * @return void
 */
function eq_add_menu(
    array | string  $menu_data,
    string          $page_title,
    string          $menu_title,
    string          $capability,
    string          $icon_url = ''
);
```

### Hooks and Filters used

- init
- admin_menu

## Installation

1. Upload `eq-menu.zip` to the `/public/wp-content/plugins/` directory or by WordPress plugin manager
2. Activate the plugin through the 'Plugins' menu in WordPress

## Frequently Asked Questions

## Screenshots

![](.\doc\images\poster.png)

## Developer notes

Take care of the following points when you want to use this plugin:

- ``/admin/assets/equal.bundle.js``: change the value of the ``backend_url`` and ``rest_api_url`` variables to the
  correct values.
    - The ``backend_url`` need to have the path to the ``equal.php`` file.
    - The ``rest_api_url`` need to have the path to the root of the eQual API + ``/``.

## Changelog

### 0.1.1

- Changed the value of the ``backend_url`` variable in the ``equal.bundle.js`` file.
- Added a Developer notes section to the README.md file.

### 0.1.2
- Updated the ``equal.bundle.js`` file.

### 0.1.3
- Added messages if a user is not logged in to eQual on the WordPress admin dashboard in the eQual menu sections.

### 0.1.4
- Removed Testing menus

## Upgrade Notice


