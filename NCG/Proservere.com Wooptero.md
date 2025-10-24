# Developer environment
[VVV Dashboard](http://vvv.test/)
[proservere.test/wp-admin](http://proservere.test/wp-admin/)
Sjekk ut Yaak [Open Source, Path Params, and Query Import](https://yaak.app/blog/2024.9.0)
## Terminaltilgang
```
cd ~/vvv-local
vagrant up
```
admin/pass satt i config.yml
# Prosessdiagram
Se [[Proservere.com Wooptero Prosessdiagram]]
## Kjøp av abonnement
1. Kunde kjøper produkt og fyller ut (i checkout eller etter checkout?):
	1. brukernavn og passord (dele brukernavn passord med panelet?)
	2. navn på server - sjekke om man må oppgi det i `/create server`
	3. annet?
	4. [# additional-checkout-fields.md](https://github.com/woocommerce/woocommerce/blob/trunk/docs/cart-and-checkout-blocks/additional-checkout-fields.md)
2. Hooke inn i [`checkout_after_processing_with_success`](https://github.com/woocommerce/woocommerce/blob/trunk/docs/cart-and-checkout-blocks/how-checkout-processes-an-order.md#11-emit-the-checkout_after_processing_with_success-event-file)
## Lage server
1. Liste Noder - finne ut av Node ID
2. Liste Allocations - finne hva som er brukbart
3. Create allocation
4. Liste Allocations - finne den nye som ble opprettet
5. Create server
## Avslutning av abonnement
1. Betaling ikke gjennomført
2. Betalingsperiode utløpt
3. Abonnement utløpt/avsluttet/ikke trukket


# Elementer
## Adminpanel
1. Pterodactyl Admin API-key
	1. [woocommerce/docs/extension-development/implementing-settings.md at trunk · woocommerce/woocommerce · GitHub](https://github.com/woocommerce/woocommerce/blob/trunk/docs/extension-development/implementing-settings.md)
2. Pterodactyl Panel-URL
3. Diverse innstillinger?
## Produktoppsett
1. Nest ID (dropdown)
2. Egg ID (dropdown)
3. Port Array
	- Mange spill trenger flere porter. Blesta mangler det
	- Antall porter
	- Port-range som er lovlig
	- Type porter
4. Location
5. Node



# Ressurser
## WordPress
- [Plugin Handbook | Developer.WordPress.org](https://developer.wordpress.org/plugins/)
- HTTP-requests
	- [Making HTTP requests – Common APIs Handbook | Developer.WordPress.org](https://developer.wordpress.org/apis/making-http-requests/)

## WooCommerce
- [woocommerce/docs/getting-started/developer-tools.md at trunk · woocommerce/woocommerce · GitHub](https://github.com/woocommerce/woocommerce/blob/trunk/docs/getting-started/developer-tools.md)
- [How to build your first extension - Woo Developer Docs](https://developer.woocommerce.com/docs/how-to-build-your-first-extension/)
	- [woocommerce/docs/building-a-woo-store/adding-a-custom-field-to-variable-products.md at trunk · woocommerce/woocommerce · GitHub](https://github.com/woocommerce/woocommerce/blob/trunk/docs/building-a-woo-store/adding-a-custom-field-to-variable-products.md)
- [Cart and Checkout - Checkout flow and events - Woo Developer Docs](https://developer.woocommerce.com/docs/cart-and-checkout-checkout-flow-and-events/)
- [Customizing checkout fields using actions and filters - Woo Developer Docs](https://developer.woocommerce.com/docs/customizing-checkout-fields-using-actions-and-filters/)
	- [Checkout Field Editor - WooCommerce Marketplace](https://woocommerce.com/products/woocommerce-checkout-field-editor/)
- Bygge en mellommann som spørr Woocommerce om ordrestatus gjennom REST API og så overfører informasjon til Pterodactyl?
- [woocommerce/docs/extension-development/how-to-design-a-simple-extension.md at trunk · woocommerce/woocommerce · GitHub](https://github.com/woocommerce/woocommerce/blob/trunk/docs/extension-development/how-to-design-a-simple-extension.md)
## Vipps
- Vipps har en plugin for Woocommerce-abonnement, men den krever Woocommerce Subscriptions
	- [Vipps/MobilePay recurring payments | Vipps MobilePay Technical Documentation](https://developer.vippsmobilepay.com/docs/plugins-ext/recurring-woocommerce/)
	- [WooCommerce Subscriptions - WooCommerce](https://woocommerce.com/products/woocommerce-subscriptions/)

## Pterodactyl
- [https://dashflo.net/docs/api/pterodactyl/v1/](https://dashflo.net/docs/api/pterodactyl/v1/)
- Pterodactyl støtter ikke OIDP/OAuth/liknende løsninger [Authentication using http header · Issue #4026 · pterodactyl/panel · GitHub](https://github.com/pterodactyl/panel/issues/4026)

## Inspirasjon
- Vipps-kode
	- [vipps-woocommerce/VippsApi.class.php at master · vippsas/vipps-woocommerce · GitHub](https://github.com/vippsas/vipps-woocommerce/blob/master/VippsApi.class.php)
	- [vipps-woocommerce/WC\_Gateway\_Vipps.class.php at master · vippsas/vipps-woocommerce · GitHub](https://github.com/vippsas/vipps-woocommerce/blob/master/WC_Gateway_Vipps.class.php)
### Eksisterende løsninger
- [GitHub - Flappeh/pterodactyl\_woocommerce: my take on connecting woocommerce and pterodactyl panel using webhook and api](https://github.com/Flappeh/pterodactyl_woocommerce)
- Blesta-pterodactyl [Pterodactyl - User Manual - Confluence](https://docs.blesta.com/display/user/Pterodactyl)
	- Blesta Produkt-panel bilde [[Proservere.com Wooptero-20240827201014612.jpg]]
- Paymenter-pterodactyl [Paymenter | Paymenter Docs](https://paymenter.org/features/pterodactyl/)
	- [kode @ GitHub](https://github.com/Paymenter/Paymenter/blob/master/app/Extensions/Servers/Pterodactyl/Pterodactyl.php)


## Dev-environment
- [Installation | VVV](https://varyingvagrantvagrants.org/docs/en-US/installation/)
	- [GitHub - Varying-Vagrant-Vagrants/custom-site-template: A site provisioner for VVV](https://github.com/Varying-Vagrant-Vagrants/custom-site-template)
- https://developer.wordpress.org/block-editor/reference-guides/packages/packages-env/
- [Setting up your development environment - Woo Developer Docs](https://developer.woocommerce.com/docs/setting-up-your-development-environment/)
	- [Installation | pnpm](https://pnpm.io/installation)
	- [Composer](https://getcomposer.org/download/)
	- [How to set up WooCommerce development environment · woocommerce/woocommerce Wiki · GitHub](https://github.com/woocommerce/woocommerce/wiki/How-to-set-up-WooCommerce-development-environment/9f2a66e277f2a6d08b9656397b0a826ef203a839#clone-woocommerce-repository)
- [PHP Playground](https://php-play.dev/?c=DwfgDgFmBQAkCuAnANgAgLyoOQQC67AGcAuAelMIBMBDAJgGZaBGR4APgDoQQBjAewC2WANzQAlgDNUACgljkuAKaIA%2BgDdqiaQhQAaVADEAkgBkAKgFEASioBqAQRNGAIvcsqAqlZMBKDOkwDRwBlCz8Ab2hUaNRKMUVpLAA5PlxUalQNZDFKVC8TLB9RAF8gA&v=8.3&f=html)
vvv-config
```
sites:

  # latest version of WordPress, can be used for client work and testing
  # Check the readme at https://github.com/Varying-Vagrant-Vagrants/custom-site-template
  proservere-plugin-ptero-woo:
    skip_provisioning: false
    description: "A standard WP install, useful for building plugins, testing things, etc"
    repo: https://github.com/Varying-Vagrant-Vagrants/custom-site-template.git
    hosts:
      - proservere.test
    custom:
      delete_default_plugins: true
      wpconfig_constants:
        WP_DEBUG: true
        WP_DEBUG_LOG: true
        WP_DISABLE_FATAL_ERROR_HANDLER: true # To disable in WP 5.2 the FER mode
      install_plugins:
        - query-monitor
      admin_user: admin # Only on install of WordPress
      admin_password: pass  # Only on install of WordPress
      admin_email: admin@local.test # Only on install of WordPress

```


# [Best Practices](https://developer.woocommerce.com/docs/woocommerce-extension-development-best-practices/#0-best-practices)
1. [x] **Check if WooCommerce is active**. Most WooCommerce plugins do not need to run unless WooCommerce is already active. [Learn how to check if WooCommerce is active](https://developer.woocommerce.com/docs/how-to-check-if-woocommerce-is-active/).
2. [x] **The main plugin file should adopt the name of the plugin**. For example: A plugin with the directory name `plugin-name` would have its main file named `plugin-name.php`.
3. [ ] **The text domain should match your plugin directory name**. For example: A plugin with a directory name of `plugin-name` would have the text domain `plugin-name`. Do not use underscores.
4. [ ] **Internationalization**: Follow guidelines for [Internationalization for WordPress Developers](https://codex.wordpress.org/I18n_for_WordPress_Developers)
5. [ ] **Localization**: All text strings within the plugin code should be in English. This is the WordPress default locale, and English should always be the first language. If your plugin is intended for a specific market (e.g., Spain or Italy), include appropriate translation files for those languages within your plugin package. Learn more at [Using Makepot to translate your plugin](https://codex.wordpress.org/I18n_for_WordPress_Developers#Translating_Plugins_and_Themes).
6. [ ] **Follow WordPress PHP Guidelines**. WordPress has a [set of guidelines](http://make.wordpress.org/core/handbook/coding-standards/php/) to keep all WordPress code consistent and easy to read. This includes quotes, indentation, brace style, shorthand php tags, yoda conditions, naming conventions, and more. Please review the guidelines.
7. [ ] **Avoid creating custom database tables**. Whenever possible, use WordPress [post types](http://codex.wordpress.org/Post_Types#Custom_Post_Types), [taxonomies](http://codex.wordpress.org/Taxonomies), and [options](http://codex.wordpress.org/Creating_Options_Pages). For more, check out our [primer on data storage](https://developer.woocommerce.com/docs/data-storage-primer/).
8. [ ] **Prevent Data Leaks** by ensuring you aren’t providing direct access to PHP files. [Find out how](https://developer.woocommerce.com/docs/how-to-prevent-data-leaks-in-woocommerce/).
9. [ ] **All plugins need a [standard WordPress README](http://wordpress.org/plugins/about/readme.txt)**. See an example in the [WordPress plugin README file standard](https://wordpress.org/plugins/readme.txt).
10. [ ] **Follow our conventions for your Plugin header comment**. View our [example WordPress plugin header comment](https://developer.woocommerce.com/docs/example-wordpress-plugin-header-comment-for-woocommerce-extensions/) and follow the conventions listed, including: `Author:`, `Author URI:` , `Developer:`, `Developer URI`, `WC requires at least:`and `WC tested up to:`, and `Plugin URI:`.
11. [ ] **Make it extensible**: use WordPress actions and filters to allow for modification/customization, and if your plugin creates a front-end output, we recommend having a templating engine in place so users can create custom template files in their theme’s WooCommerce folder to overwrite the plugin’s template files.For more information, check out Pippin’s post on [Writing Extensible Plugins with Actions and Filters](http://code.tutsplus.com/tutorials/writing-extensible-plugins-with-actions-and-filters--wp-26759).
12. [ ] **Avoid external libraries**. The use of entire external libraries is typically not suggested as this can open up the product to security vulnerabilities. If an external library is absolutely necessary, developers should be thoughtful about the code used and assume ownership as well as of responsibility for it. Try to only include the strictly necessary part of the library, or use a WordPress-friendly version or opt to build your own version. For example, if needing to use a text editor such as TinyMCE, we recommend using the WordPress-friendly version, TinyMCE Advanced.
13. [ ] **Remove unused code**. With version control, there’s no reason to leave commented-out code; it’s annoying to scroll through and read. Remove it and add it back later if needed.
14. [ ] **Use Comments** to describe the functions of your code. If you have a function, what does the function do? There should be comments for most if not all functions in your code. Someone/You may want to modify the plugin, and comments are helpful for that. We recommend using [PHP Doc Blocks](http://en.wikipedia.org/wiki/PHPDoc) similar to [WooCommerce](https://github.com/woocommerce/woocommerce/).
15. [ ] **Avoid God Objects**. [God Objects](http://en.wikipedia.org/wiki/God_object) are objects that know or do too much. The point of object-oriented programming is to take a large problem and break it into smaller parts. When functions do too much, it’s hard to follow their logic, making bugs harder to fix. Instead of having massive functions, break them down into smaller pieces.
16. [ ] **Test Your Code with [WP_DEBUG](http://codex.wordpress.org/Debugging_in_WordPress)** mode on, so you can see all PHP warnings sent to the screen. This will flag things like making sure a variable is set before checking the value.
17. [ ] **Separate Business Logic & Presentation Logic.** It’s a good practice to separate business logic (i.e., how the plugin works) from [presentation logic](http://en.wikipedia.org/wiki/Presentation_logic) (i.e., how it looks). Two separate pieces of logic are more easily maintained and swapped if necessary. An example is to have two different classes – one for displaying the end results, and one for the admin settings page.
18. [ ] **Use Transients to Store Offsite Information**. If you provide a service via an API, it’s best to store that information so future queries can be done faster and the load on your service is lessened. [WordPress transients](http://codex.wordpress.org/Transients_API) can be used to store data for a certain amount of time.
19. [ ] **Log data that can be useful for debugging purposes**, with two conditions: Allow any logging as an ‘opt in’, and Use the [WC_Logger](https://woocommerce.com/wc-apidocs/class-WC_Logger.html) class. A user can then view logs on their system status page. Learn [how to add a link to logged data](https://developer.woocommerce.com/docs/add-link-to-logged-data/) in your extension.


# Adminpanel

|             |               |                    |                                                                                                           |
| ----------- | ------------- | ------------------ | --------------------------------------------------------------------------------------------------------- |
| location_id | integer >= 0  | Dropdown           | Sets the location where the server will be deployed.                                                      |
| egg_id      | integer >= 0  | Dropdown           | Sets the ID of the egg the server will use.                                                               |
| memory      | integer >= 1  | Quantity, Dropdown | Sets the amount of memory to be assigned to the server in MB.                                             |
| cpu         | integer >= 1  | Quantity, Dropdown | Sets the amount of CPU to be assigned to the server in %. 100% is equivalent to one core.                 |
| disk        | integer >= 1  | Quantity, Dropdown | Sets the amount of disk space to be assigned to the server in MB.                                         |
| io          | integer >= 10 | Quantity, Dropdown | Sets the IO weight of the server. Within a range from 10 to 1000.                                         |
| startup     | string        | Text               | Sets the custom startup command to assign to the server.                                                  |
| image       | string        | Text, Dropdown     | Sets the Docker image to be deployed to the server.                                                       |
| databases   | integer >= 1  | Quantity, Dropdown | Sets the total amount of databases the user can create for the server.                                    |
| allocations | integer >= 1  | Quantity, Dropdown | Sets the total amount of allocations the user can create for the server                                   |
| backups     | integer >= 1  | Quantity, Dropdown | Sets the total amount of backups the user is allowed to create for the server.                            |
| nest_id     | integer >= 0  | Dropdown           | Sets the ID of the nest the server will use.                                                              |
| port_range  | string        | Text               | Sets the port range that will be allocated to the server separated by comma. e.g. 25565-25570,25580-25590 |
| pack_id     | integer >= 0  | Dropdown           | Sets the ID of the pack that will be installed in the server.                                             |
| swap        | integer >= 0  | Quantity, Dropdown | Sets the amount of SWAP memory to be assigned to the server in MB.                                        |
# API-endepunkter
