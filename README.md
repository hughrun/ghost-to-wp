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
ghost-to-wp ghostexportfile.json
```

You should now have a new file called `WP_import.xml`. Import this file to your WordPress site using the WordPress site importer (`Tools - Import - WordPress`) - you will be able to map authors to existing users in Wordpress before the post and page import begins, as long as you have created user accounts for your authors ahead of importing.

## Caveats & Limitations

You will need to migrate images manually. Wordpress does not have an easy way to import images with a WXR file, and Ghost doesn't have an easy way to export them together with the JSON export.

Ghost doesn't have 'categories' so this only imports tags. You can use the WordPress [Categories to Tags Converter](https://wordpress.org/plugins/wpcat2tag-importer/) if you want to change some tags to categories once imported.

## License

GPL 3+