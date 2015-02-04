#Translation for Laravel 4

##Installation

Require translation in your composer.json file

    "stevebauman/translation": "1.0.*"
    
Then run the composer update command on your project source

    composer update
    
Add the service provider to your `app.php` config file

    'Stevebauman\Translation\TranslationServiceProvider',
    
Add the facade to your aliases in your `app.php` config file

    'Translation' => 'Stevebauman\Translation\Facades\Translation',
    
Run the migrations

    php artisan migrate --package="stevebauman/translation"
    
Your good to go!
    
##Usage

Anywhere in your application, either use the the shorthand function (can be disabled in config file)

    _t('Translate me!')
    
Or

    Translation::translate('Translate me!')
    
This is typically most useful in blade views:

    {{ _t('Translate me!') }}
    
And you can even translate models easy by just plugging in your content:

    {{ _t($post->title) }}
    
In your `locales` database table you'll have:

    | id | code | name | lang_code |
       1    en    NULL      NULL

In your 'translations' database table you'll have:

    | id | locale_id | translation_id | translation |
      1        NULL         NULL        'Translate me!'
      
To switch languages for the users session, all you need to call is:

    Translation::setLocale('fr') // Setting to French locale
    
Now, once you visit the page you'll have this in your `locales` table:

    | id | code | name | lang_code |
       1    en    NULL      NULL
       2    fr    NULL      NULL

And this in your `translations` table:

    | id | locale_id | translation_id | translation |
       1        NULL         NULL        'Translate me!'
       2        NULL          1          'Translate me!'
       
You provide you're own way of updating translations (controllers/views etc).