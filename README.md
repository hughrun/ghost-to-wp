# Ghost to Wordpress Blog Migration Tool

Version 1.1.0

This script can be used to migrate a Ghost blog to Wordpress.

You will get the full HTML and tags for all posts and pages, including whether it's a page or a post, published or draft, and featured/sticky or not.

## Usage

* [Export your Ghost site data](https://help.ghost.org/hc/en-us/articles/224112927-Import-Export-Data).
* make sure you have [node](https://nodejs.org/en/) installed on your machine (if you've been using Ghost, you probably already have it, at least on your server)
* Download ghost-to-wordpress, then run these two commands:

`npm install`

`npm start path/to/your/exportfile.json`

* Import the new `WP_import.xml` file to your WordPress site using the _Wordpress Importer_ plugin.

## Caveats & Limitations

This _should_ migrate users, but it doesn't - I'll look into this when I have time to work out why.

You will need to migrate images manually. Wordpress does not have an easy way to import images with a WXR file, and Ghost doesn't have an easy way to export them with the rest of the posts info. If it's any consolation, I feel your pain.

Ghost doesn't have categories so this only imports tags. You can use the WordPress _categories to tags converter importer_ if you want to change some tags to categories once imported.

## TODOs

* fix author migration
* publish npm package maybe

## License

GPL 3+