# Configuration

In order to use madonctl, you need to specify the instance name or URL, and
usually at least provide an account login/password (or a token).

These settings can be passed as command line arguments or environment variables,
but the easiest way is to use a configuration file.

Note that every variable from the configration file can also be set with an
environment variable (e.g. `export MADONCTL_INSTANCE='https://mamot.fr'`).

## Configuration file

The default configuration file is located at `$HOME/.config/madonctl/madonctl.yaml`.

We use [viper](http://spf13.com/project/viper), so you can use the format you
prefer between YAML, TOML or JSON.  The examples use the YAML format so the
configuration file will be named `madonctl.yaml`.

You can generate a sample configuration file for your settings with
``` sh
madonctl config dump -i mastodon.social -L username@domain -P password
```

The output of this command can be redirected to a file:
``` sh
madonctl config dump -i mstn.io -L email -P passw > madonctl.yaml
```

If you only provide the Mastodon instance, it will generate a configuration
file with an application ID/secret for this instance and you will have to add
the user credentials.

If you don't want to use the password or if you have enabled *Two-factor
authentication*, you can use **OAuth2** with the `oauth2` command, either
interactively or non-interactively:

`madonctl -i mastodon.social oauth2`

The output is similar to the previous `config dump` command, so you can create
your configuration file like this as well:

`madonctl -i mastodon.social oauth2 > madonctl.yaml`

Note: If don't want to use the tool interactively, check to `get-url` and `code`
subcommands:
``` sh
madonctl -i mastodon.social oauth2 get-url
# (Paste the link into your browser...)
madonctl -i mastodon.social code $CODE > config_file.yaml
```

Note that if you have set up madonctl to use a default theme, you will have
to force the output with `-o plain` to get the example configuration file.

## Settings

All the available settings should be displayed with *config dump* (assuming
the *safe_mode* variable is not set).

Option | Description
------ | -----------
`instance`  | Name of the Mastodon instance (e.g. 'mastodon.social')
`app_id`    | Application ID (generated by madonctl)
`app_secret`| Application secret (generated by madonctl)
`token`     | User Mastodon token (generated at login time)
`login`     | User login (email)
`password`  | User password
`safe_mode` | If set to *true*, the configuration cannot be dumped with *config dump*
`default_visibility` | Default toots visibillity (Mastodon's default is 'public')
`default_output`     | Default output format; one of plain, yaml, json or theme
`template_directory` | The local directory where templates and themes are installed
`default_theme`      | Default theme name (e.g. *ansi*)
`color`              | Default color setting (on, off, auto)
`verbose`            | Set to *true* for verbose mode

Note that if a token is set, the login and the password are not necessary.\
It is recommended to reuse the same token (and it will be faster).
