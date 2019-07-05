# Themes

[[toc]]

## Overview

There are times when you'd like to customize the visual style of Nova to match your brand or colors. Nova provides a few ways to customize the look and feel of the admin panel.

Here's a video with a quick overview of how to change the main colors of the Nova admin: [Customizing Laravel Nova's CSS and Logo](https://www.youtube.com/watch?v=InK-mRH9z5M&t=85s)

## Generating a Custom Theme

Custom themes may be generated using the `nova:theme` Artisan command. By default, all custom themes will be placed in the `nova-components` directory of your application. When generating a theme using the `nova:theme` command, the theme name you pass to the command should follow the Composer `vendor/package` format. So, if we were building a theme called "Miami Ice", we might run the following command:

```bash
php artisan nova:theme example/miami-ice
```

This command will generate all of the boilerplate needed to generate your theme. In addition, a `ThemeServiceProvider` will be auto-registered with your application. This service provider registers your theme with Nova. You do not need to publish the theme CSS manually, as Nova handles this for you.

In the case that the theme service provider is not automatically registered, you can manually register it inside of `config/app.php` under the `providers` key:

```php
'providers' => [
    //...
    \Example\MiamiIce\ThemeServiceProvider::class,
    //...
],
```

### Assets

When Nova generates your theme, a `resources/css/theme.css` file is generated for you. This file contains your theme's styles. Inside you will find some example values already in place for you to edit:

```css
:root {
  --primary: rgb(254, 1, 129, 1);
  --primary-dark: rgb(209, 0, 105, 1);
  --primary-70: rgba(254, 1, 129, 0.7);
  --primary-50: rgba(254, 1, 129, 0.5);
  --primary-30: rgba(254, 1, 129, 0.3);
  --primary-10: rgba(254, 1, 129, 0.1);
  --logo: #430051;
  --sidebar-icon: #db34de;
}

.bg-grad-sidebar {
  background-image: -webkit-gradient(
    linear,
    left bottom,
    left top,
    from(rgb(254, 1, 129, 1)),
    to(#3c4655)
  );

  background-image: linear-gradient(
    0deg,
    rgb(254, 1, 129, 1),
    rgb(100, 5, 113)
  );
}
```

#### Compiling Assets

Your Nova theme contains a `webpack.mix.js` file, which is generated when Nova creates your theme. You may build your theme using the NPM `dev` and `prod` commands:

```bash
// Compile your assets for local development...
npm run dev

// Compile and minify your assets...
npm run prod
```

In addition, you may run the NPM `watch` command to auto-compile your assets when they are changed:

```bash
npm run watch
```