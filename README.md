# chat-app
Laravel + Echo

<p align="center"><img height="700" src="https://raw.githubusercontent.com/alikamal1/chat-app/master/screenshot.PNG"></p>

## Project setup
```
composer require laravel/ui
php artisan ui vue --auth
npm install && npm run dev
php artisan migrate
php artisan db:seed
npm install --save pusher-js laravel-echo
composer require pusher/pusher-php-server
php artisan make:event NewMessage
```
