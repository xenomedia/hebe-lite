# Hebe Lite

This repository is a fork of [example-drops-8-composer](https://github.com/pantheon-systems/example-drops-8-composer).

This repository is a start state for a Composer-based Drupal workflow with Pantheon at Xenod Media.

## Installation

Start off by creating a new Drupal 8 site; then, before installing Drupal, set your site to git mode and do the following from your local machine:
```
$ composer create-project xenomedia/hebe-lite my-site
$ cd my-site
$ composer prepare-for-pantheon
$ git init
$ git add -A .
$ git commit -m "web and vendor directory from composer install"
$ git remote add origin ssh://ID@ID.drush.in:2222/~/repository.git
$ git push --force origin master
```
* The `--team` flag is optional and refers to a Pantheon organization. Pantheon organizations are often web development agencies or Universities. Setting this parameter causes the newly created site to go within the given organization. Run the Terminus command `terminus org:list` to see the organizations you are a member of. There might not be any.

## Important files and directories

### `/web`

Pantheon will serve the site from the `/web` subdirectory due to the configuration in `pantheon.yml`, facilitating a Composer based workflow. Having your website in this subdirectory also allows for tests, scripts, and other files related to your project to be stored in your repo without polluting your web document root.

#### `/config`

One of the directories moved to the git root is `/config`. This directory holds Drupal's `.yml` configuration files. In more traditional repo structure these files would live at `/sites/default/config/`. Thanks to [this line in `settings.php`](https://github.com/pantheon-systems/example-drops-8-composer/blob/54c84275cafa66c86992e5232b5e1019954e98f3/web/sites/default/settings.php#L19), the config is moved entirely outside of the web root.

### `composer.json`

If you are just browsing this repository on GitHub, you may notice that the files of Drupal core itself are not included in this repo.  That is because Drupal core and contrib modules are installed via Composer and ignored in the `.gitignore` file. Specific contrib modules are added to the project via `composer.json` and `composer.lock` keeps track of the exact version of each modules (or other dependency). Modules, and themes are placed in the correct directories thanks to the `"installer-paths"` section of `composer.json`. `composer.json` also includes instructions for `drupal-scaffold` which takes care of placing some individual files in the correct places like `settings.pantheon.php`.

## Behat tests

So that CircleCI will have some test to run, this repository includes a configuration of Behat tests. You can add your own `.feature` files within `/tests/features/`.

## Updating your site



