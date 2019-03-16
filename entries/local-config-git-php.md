# Local configuration with PHP and Git

You have your nice website source code, which is hosting in a Git repo. Your client asks for a few modifications, so you clone the repo on a dev server, and set it up to get running.

Now the source contains default settings, such as database connection credentials, API key for external services, etc. These settings need to be changed for the dev  site: different database, testing API key, verbose errors, etc.

So let's say you have all your default application settings in a file named `config.default.php`, which has been entered in the source repo.

Example `config.default.php`:

```
<?php

$config['Payment API key'] = "3f83h2870dc8117a8848h482657a87c8";
$config['Force SSL'] = true;
$config['Color theme'] = "blue";

// etc.

```

You would want your "local" configuration, which is specific to the dev server, to remain outside of your source repo.


Therefore, you create another file, `config.local.php` and tell Git to ignore it.

```bash
echo "config.local.php" >> .gitignore
```

Contents of `config.local.php`:

```php
<?php

// test API
$config['Payment API key'] = "187a0053f83f28737a8hcb8h102a0dd";
// dev server
$config['Force SSL'] = false;

```

Now these settings need to be loaded by your PHP app.

This local config file will not be committed into the repository, so there is no guarantee that it would exist. To avoid that your PHP app crashes when the file is not found, it has to be a conditional include.

So the code for including the local config is added to `config.default.php`. This is what it looks like, now:

```php
<?php

$config['Payment API key'] = "3f83h2870dc8117a8848h482657a87c8";
$config['Force SSL'] = true;
$config['Color theme'] = "blue";

// etc.

if(file_exists('config.local.php')) {
    include('config.local.php');
}

```

What this does is load default conf values into `$config`, then try to include `config.local.php` if it exists. The values defined in the local config will simple overwrite default values in `$config`.

Now you can adjust your local config to your liking, and work on your source.

After doing changes to the source code, you can just do the usual:
```
git add .
git commit -m "your commit message here"
git push
```

Git will ignore `config.local.php` and any changes made inside it.


You can adapt this method to other configuration patterns in PHP or even to a different platform.
