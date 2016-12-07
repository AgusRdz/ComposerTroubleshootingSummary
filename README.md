##Composer. Troubleshooting Summary

###Common issues

1. **Check the system configuration.**
 `composer diagnose`

2. **Update your version of Composer.**
 `composer self-update`
 
3. **Increases the level of detail of messages.** 
 `-vvv`

4. **Delete the `vendor` folder and the` composer.lock` file and run `composer install`.** 
 
5. **Empty the internal cache.**

 `composer clear-cache`
 `composer install` o `composer update`

###Specific issues.

- **Composer is very slow when updating / installing packages.**
 **Disable xDebug ** in your `php.ini` file while using Composer commenting on matching lines. 

 > With xDebug enabled, the Composer installation and update process can take up to 20 times more!
 
 > **Note**: Check if you have xDebug enabled. (`Xdebug` will appear)
 > Windows: `php -m | findstr xdebug`.
 > Unix: `php -m | grep xdebug`.
 
 You can use `--prefer-dist` to download the packages in .zip format.
 
- **Timeout Error.**

 `composer config --global process-timeout 1500` 

 > You can also set the Timeout with the `COMPOSER_PROCESS_TIMEOUT` environment variable.

- **Warning: Outdated lock file.**

 ```
 Warning: The lock file is not up to date with the latest changes in composer.json, you may be getting outdated dependencies, 
 run update to update them.
```
 `composer update --lock`.

- **Warning: extensión openssl.**

 `openssl extension is missing` o `must enable the openssl extension`
 Enable the `php_openssl.dll` extension in your` php.ini` file.
 
- **'Your requirements could not be resolved to an installable set of packages'.**

 > **Note:** Check first that package names are spelled correctly.

 1. Delete `"prefer-stable": true` from your `composer.json` file.
 2. Add `"minimum-stability": "dev"`
 3. Stability and testing.
 4. Add `"prefer-stable": true`.

 Defines an [Alias] (Solve-conflicts-of-versions-and-requirements-in-Composer-(Aliases).

- **Error 503 when downloading the .zip files from GitHub.**

  `composer install --prefer-source` or `composer update --prefer-source`.
 
###Important

- Add the `composer.json` and` composer.lock` files to your Git repository.
- Use `composer install` instead of` composer update`.
- In production, use `--no-dev` unless you need to install the development libraries.
- In production, use `--optimize-autoloader`.
- Combine `"minimum-stability": "dev"` with `"prefer-stable": true`.
- Remember to use the `--dev` parameter of the `composer require` command.
- Before a `push`, run `composer validate` to validate your `composer.json` file.
- Always add the `vendor` folder to your` .gitignore` file.

###Sources:

[Composer: Solving problems (spanish)](https://styde.net/composer-resolviendo-problemas/)

[Download Composer](https://getcomposer.org)   

[Interactive Summary Sheet of Composer - By JoliCode](http://composer.json.jolicode.com/)
