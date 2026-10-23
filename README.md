# Laravel Places Scout

![Laravel Places Scout package banner](art/banner.png)

A Laravel client for Google Places Text Search and Place Details. Responses are
returned as typed data objects.

[![Tests](https://github.com/eloquage/laravel-places-scout/actions/workflows/run-tests.yml/badge.svg)](https://github.com/eloquage/laravel-places-scout/actions/workflows/run-tests.yml)
[![Latest Version](https://img.shields.io/packagist/v/illuma-law/laravel-places-scout)](https://packagist.org/packages/illuma-law/laravel-places-scout)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE.md)

Requires PHP 8.3+ and Laravel 11, 12, or 13.

## Install

```bash
composer require illuma-law/laravel-places-scout
php artisan vendor:publish --tag=places-scout-config
```

Set your Google Places API key in `.env`:

```dotenv
GOOGLE_PLACES_API_KEY=your-api-key
```

## Search for places

```php
use IllumaLaw\PlacesScout\Facades\PlacesScout;

$response = PlacesScout::textSearch('coffee shops in Lisbon');

foreach ($response?->results ?? [] as $place) {
    echo $place->name;
    echo $place->formattedAddress;
}
```

## Get place details

```php
$place = PlacesScout::getPlaceDetails('ChIJ...');

if ($place !== null) {
    echo $place->name;
    echo $place->website;
}
```

Both methods return `null` when the Google API request fails. You can pass
`withApiKey($key)` before either method to use a per-request key.

## Tests

```bash
composer test
composer analyse
composer format -- --test
```

## License

MIT. See [LICENSE.md](LICENSE.md).
