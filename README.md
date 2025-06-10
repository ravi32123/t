<p align="center"><a href="https://www.uvdesk.com/en/" target="_blank">
    <img src="https://s3-ap-southeast-1.amazonaws.com/cdn.uvdesk.com/uvdesk/bundles/webkuldefault/images/uvdesk-wide.svg">
</a></p>

UVDesk Community Telegram Package
----------------------------------

The Telegram package adds support for the Telegram platform to your community helpdesk system.

This package works with the [uvdesk/ecommerce][1] package to easily integrate any number of Telegram stores with your community helpdesk system enabling support agents to seamlessly fetch order details and integrate it with tickets to provide quality support without having to leave the helpdesk system.

Installation
--------------

>**Please Note:**
> 
>This package is dependent on the free **uvdesk/ecommerce** package so ensure you've installed that package before proceeding with installation.
>
>[Learn more about the uvdesk community eCommerce package][1].

To add this package to your helpdesk system, simply download this package within the **apps/uvdesk** directory such that the final path of your package will be **apps/uvdesk/telegram** relative to your project's root.

Once you've copied the package to the specified directory, run the following command from your project's root:

```bash
$ php bin/console uvdesk_extensions:configure-extensions
$ php bin/console assets:install
$ php bin/console doctrine:migrations:diff
$ php bin/console doctrine:migrations:migrate
```

These commands will automatically search and configure any available packages found within the apps directory. Once your packages have been configured successfully, they are ready for use.

Use **@BotFather** on Telegram:

* Follow the prompts to **name your bot** and get a **bot token**.

* Now add **bot token**, into Telegram app Configuration into your Helpdesk under App section.

* Set webhook URL to receive webhooks from telegram by running below curl request.

```bash
curl -X POST "https://api.telegram.org/bot<your_bot_token>/setWebhook" \
  -d "url=https://helpdesk.example.com/telegram/bot"
```

* Now add below URL in **security.yaml** file under **config/packages** folder and add URL under **access_control** section.

```bash
- { path: /%uvdesk_site_path.member_prefix%/telegram/bot, roles: [IS_AUTHENTICATED_ANONYMOUSLY] }
```

* **Note**: Add above URL before this: { path: /%uvdesk_site_path.member_prefix%/, roles: ROLE_AGENT }

* Finally Clear project cache by below command:

```bash
php bin/console c:c --env prod
```

> That's it, You can send telegram message to telegram user Id for which you have created bot token and accordingly ticket will be process and create.

[1]: https://github.com/uvdesk/ecommerce
