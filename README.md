# LSDMS

### Technology Stacks

Lets find out our technology stacks here:

* [Laravel 8]
* [Bootstrap 5]
* [jQuery]
* [AJAX]


### Things I have done

From a suitable directory, I have run the following commands in CLI:


composer create-project laravel/laravel LSDMS "8.*"

cd LSDMS/

npm install

npm install --save bootstrap@next

npm install --save @popperjs/core

npm install --save jquery

npm install @fortawesome/fontawesome-free --save-dev

Now, all these packages need to be wraped with laravel mix, right? 

So, I have done some necessary code changes as follows:

- `resources/js/bootstrap.js` : added the following code under *axios*

```
window.$ = window.jQuery = require("jquery");

```

- `resources/js/app.js` : added the following code under *require('./bootstrap')*

```
$(function(){
    console.log('it is working');
});
```

- Renamed `resources/css` to `resources/sass`
- Renamed `resources/sass/app.css` to `resources/sass/app.scss`
- `resources/sass/app.scss` : added the following code:

```
@import '~bootstrap/scss/bootstrap';
@import "~@fortawesome/fontawesome-free/scss/fontawesome";
@import "~@fortawesome/fontawesome-free/scss/regular";
@import "~@fortawesome/fontawesome-free/scss/solid";
@import "~@fortawesome/fontawesome-free/scss/brands";

body,
html {
    height: 100%;
    overflow-y: auto;
}
```

- `webpack.mix.js` : replaced with the following code:

```
const mix = require('laravel-mix');

mix
    .js('resources/js/app.js', 'public/assets/js').minify('public/assets/js/app.js')
    .sass('resources/sass/app.scss', 'public/assets/css').minify('public/assets/css/app.css')
    .copy(
        'resources/images',
        'public/assets/images'
    )
    .copy(
        'node_modules/@fortawesome/fontawesome-free/webfonts',
        'public/assets/webfonts'
    );

mix.browserSync("localhost:10008");
```

Now, why did I change the mix configuration like above? Well:

- To group all the resource script files
- To copy all required assets file images
- To copy all required assets file fonts
- To move all required asset files  under a specific public directory, to organize them in a better way
- And, used [BrowserSync](https://laravel-mix.com/docs/5.0/browsersync)

After all above, I have run the following commands in CLI (twice):

```
npm run dev
```

Why twice? Sometimes laravel mix fails to generate all the resource assets properly. So doing double time puts extra assurity. 


#### Structuring Backend


composer require laravel/fortify

php artisan vendor:publish --provider="Laravel\Fortify\FortifyServiceProvider"



You should ensure `Laravel\Fortify\FortifyServiceProvider` class is registered within the providers array of your application's config/app.php configuration file.

In this project, we will only use the `Login` process part of Fortify. So, lets be sure the `app/Providers/FortifyServiceProvider.php` has the following code under `boot()` function:

```
RateLimiter::for('login', function (Request $request) {
    return Limit::perMinute(5)->by($request->email . $request->ip());
});

Fortify::loginView(function () {
    return view('home');
});
``` 

php artisan storage:link
php artisan key:generate

php artisan make:model Student --migration
php artisan make:model Result --migration

php artisan make:seeder UserSeeder


php artisan migrate:fresh --seed

php artisan serve --port 10008

login : admin@gmail.com
password : admin1123
