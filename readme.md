## WordPress CSV Importer

Import posts from CSV files into WordPress.


## Description

This plugin imports posts from CSV (Comma Separated Value) files into your
WordPress blog. It can prove extremely useful when you want to import a bunch
of posts from an Excel document or the like - simply export your document into
a CSV file and the plugin will take care of the rest.

### Features

*   Imports post title, body, excerpt, tags, date, categories etc.
*   Supports custom fields, custom taxonomies and comments
*   Deals with Word-style quotes and other non-standard characters using
    WordPress' built-in mechanism (same one that normalizes your input when you
    write your posts)
*   Columns in the CSV file can be in any order, provided that they have correct
    headings
*   Multilanguage support


## Screenshots

1.  Plugin's interface


## Installation

Installing the plugin:

1.  Unzip the plugin's directory into `wp-content/plugins`.
1.  Activate the plugin through the 'Plugins' menu in WordPress.
1.  The plugin will be available under Tools -> CSV Importer on
    WordPress administration page.


## Usage

Click on the CSV Importer link on your WordPress admin page, choose the
file you would like to import and click Import. The `examples` directory
inside the plugin's directory contains several files that demonstrate
how to use the plugin. The best way to get started is to import one of
these files and look at the results.

CSV is a tabular format that consists of rows and columns. Each row in
a CSV file represents a post; each column identifies a piece of information
that comprises a post.

### Basic post information

*   `csv_post_title` - title of the post
*   `csv_post_post` - body of the post
*   `csv_post_type` - `post`, `page` or a custom post type.
*   `csv_post_excerpt` - post excerpt
*   `csv_post_categories` - a comma separated list of category names or ids. It's also possible to assign posts to non-existing subcategories, using &gt; to denote category relationships, e.g. `Animalia > Chordata > Mammalia`. It's also possible to specify the parent category using an id, as in `42 > Primates > Callitrichidae`, where `42` is an existing category id.
*   `csv_post_tags` - a comma separated list of tags.
*   `csv_post_date` - about any English textual description of a date and time.

[custom_post_types]: http://codex.wordpress.org/Custom_Post_Types
[strtotime]: http://php.net/manual/en/function.strtotime.php

###  General remarks

*   WordPress pages [don't have categories or tags][pages].
*   Most columns are optional. Either `csv_post_title`, `csv_post_post` or
    `csv_post_excerpt` are sufficient to create a post. If all of these
    columns are empty in a row, the plugin will skip that row.
*   The plugin will attempt to reuse existing categories or tags; if an
    existing category or tag cannot be found, the plugin will create it.
*   To specify a category that has a greater than sign (>) in the name, use
    the HTML entity `&gt;`

[pages]: http://codex.wordpress.org/Pages

## Advanced Usage

*   `csv_post_author` - numeric user id or login name. If not specified or
    user does not exist, the plugin will assign the posts to the user
    performing the import.
*   `csv_post_slug` - post slug used in permalinks.
*   `csv_post_parent` - post parent id.
*   `csv_ctax_{taxonomy_name}` - for a custom taxonomy.
*   `csv_attachment_{attachment_name}` - to import an attachment.
*   `csv_attachment_thumbnail` - to import an attachment as a featured image

### Custom taxonomies

Once custom taxonomies are set up in your theme's functions.php file or by using 
a 3rd party plugin, `csv_ctax_{taxonomy_name}` columns can be used to assign 
imported data to the taxonomies.

The syntax for non-hierarchical taxonomies is straightforward and is essentially
the same as the `csv_post_tags` syntax.

The syntax for hierarchical taxonomies is more complicated. Each hierarchical
taxonomy field is a tiny two-column CSV file, where _the order of columns
matters_. The first column contains the name of the parent term and the second
column contains the name of the child term. Top level terms have to be preceded
either by an empty string or a 0 (zero).

Sample `examples/custom-taxonomies.csv` file included with the plugin
illustrates custom taxonomy support. To see how it works, make sure to set up
custom taxonomies from `functions.inc.php`.

Make sure that the quotation marks used as text delimiters in `csv_ctax_`
columns are regular ASCII double quotes, not typographical quotes like “
(U+201C) and ” (U+201D).

### Comments

An example file with comments is included in the `examples` directory.
In short, comments can be imported along with posts by specifying columns
such as `csv_comment_*_author`, `csv_comment_*_content` etc, where * is
a comment ID number. This ID doesn't go into WordPress. It is only there
to have the connection information in the CSV file.

### Attachments

To import an attachment, upload the files via ftp and then including 
the full URL to the attachment file including images, documents or any 
other file type that WordPress supports

### Custom fields

Any column that doesn't start with `csv_` is considered to be a custom field
name. The data in that column will be imported as the custom fields value.

## Credits

This plugin uses [php-csv-parser](http://code.google.com/p/php-csv-parser/) by Kazuyoshi Tlacaelel.
It was inspired by JayBlogger's [CSV Import](http://www.jayblogger.com/the-birth-of-my-first-plugin-import-csv/) plugin.

Contributors:

*   [Bryan Headrick](https://github.com/BHEADRICK/) (custom taxonomy & attachment support)
*   Kevin Hagerty (post_author support)
*   Edir Pedro (root category option and tableless HTML markup)
*   Frank Loeffler (comments support)
*   Micah Gates (subcategory syntax)
*   David Hollander (deprecation warnings, linebreak handling)
