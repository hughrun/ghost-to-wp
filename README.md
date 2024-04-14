# NOTE THIS PROJECT HAS BEEN ARCHIVED

There will be no further maintenance or development.

## Ghost to Wordpress Blog Migration Tool

Use `ghost-to-wp` to migrate a Ghost blog to Wordpress.

You will get the full HTML content, author, and tags for all posts and pages, including whether it's a page or a post, published or draft, and featured/sticky or not.

If you use the optional second argument, all image filepaths will also be updated for easy image migration.

## Usage

1. [Export your Ghost site data](https://ghost.org/faq/the-importer) as a JSON file.
2. Make a copy of your site images stored at the `/content/images/` directory, or if hosted by `ghost.org`, ask for your image archive.
3. Make sure you have [nodejs](https://nodejs.org/en/) and [npm](https://www.npmjs.com/) installed on your machine.
4. Install:

```
npm i -g ghost-to-wp
```

5. Convert your Ghost export file:

```
ghost-to-wp EXPORT_FILE [DOMAIN_NAME]
```

For example:

```
ghost-to-wp /Users/hugh/backups/example.ghost.2021-04-17-11-17-45.json https://blog.example.com
```

You should now have a new file called `WP_import.xml`. Import this file to your WordPress site using the WordPress site importer (`Tools - Import - WordPress`) - you will be able to map authors to existing users in Wordpress before the post and page import begins, as long as you have created user accounts for your authors ahead of importing.

### Arguments

The first argument should be the filepath to your ghost export file, and the optional second argument is the base domain of your blog including the protocol (http/s) but *not* including a trailing slash. If you are changing your domain this argument should be the _new_ domain.

## Images

Migrating images requires the second argument.

WordPress expects image URLs to be absolute, not [relative](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2), but Ghost doesn't really mind either way. If you provide the second (domain name) argument this will:

1. replace any relative image links you may have with absolute URLs
2. replace any references to `__GHOST_URL__` in your image links
3. update your image directory references from `/content/images/` to `/wp-content/uploads/`.

You can then copy (using FTP, rsync or something else) everything from your Ghost `/content/images/` directory to your WordPress `/wp-content/uploads/` directory and your images should display.

Ghost doesn't provide a browser-based image export function and WordPress doesn't provide an inbuilt browser-based image import function so you will need to do this manually as per the above.

## Caveats & Limitations

1. Ghost doesn't have 'categories' so this only imports tags. You can use the WordPress [Categories to Tags Converter](https://wordpress.org/plugins/wpcat2tag-importer/) if you want to change some tags to categories once imported.

2. The image migration tool using the second argument is a simple regex find-and-replace. If you have a lot of posts where you write about `/content/images/` filepaths or use that string in a code example, `ghost-to-wp` will replace that text as well.

## License

GPL 3+
