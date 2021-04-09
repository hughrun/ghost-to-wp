# Ghost to Wordpress Blog Migration Tool

Use `ghost-to-wp` to migrate a Ghost blog to Wordpress.

You will get the full HTML content, author, and tags for all posts and pages, including whether it's a page or a post, published or draft, and featured/sticky or not.

## Usage

[Export your Ghost site data](https://ghost.org/faq/the-importer) as a JSON file.

Make sure you have [nodejs](https://nodejs.org/en/) installed on your machine (if you've been using Ghost, you probably already have it, at least on your server)

Install:

```
npm i -g ghost-to-wp
```

Convert your Ghost export file:

```
ghost-to-wp ghostexportfile.json [https://blog.example.com]
```

The first argument should be your ghost export file, and the optional second argument is the base URL of your blog without a trailing slash.

The optional URL argument does two things:

1. replaces any references to `__GHOST_URL__` with your actual URL
2. fixes any doubled-up URLs (e.g. `https://blog.example.comhttps://blog.example.com`)

Note that due to (2) you need to use the current/old URL if you are changing your URL as well as your blog software. If you are changing the URL, run the script with the old URL first, then do a find and replace on the XML import file that is created before importing it.

You should now have a new file called `WP_import.xml`. Import this file to your WordPress site using the WordPress site importer (`Tools - Import - WordPress`) - you will be able to map authors to existing users in Wordpress before the post and page import begins, as long as you have created user accounts for your authors ahead of importing.

## Images

Migrating images requires an extra step. If you have a lot of images to migrate it is recommended that you include the optional URL argument.

The script will automatically update your image directory references from `/content/images` to `/wp-content/uploads/`. You should therefore be able to upload (using FTP, rsync or something else) everything in your Ghost server's `/content/images` directory to your WordPress server's `wp-content/uploads/` directory and your images will display. Note however that this has not been tested much (at all) so may not work. Ghost doesn't provide a browser-based image export function and WordPress doesn't provide an inbuilt browser-based image import funtion so you will need to do this manually.

## Caveats & Limitations

Ghost doesn't have 'categories' so this only imports tags. You can use the WordPress [Categories to Tags Converter](https://wordpress.org/plugins/wpcat2tag-importer/) if you want to change some tags to categories once imported.

## License

GPL 3+