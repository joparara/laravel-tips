# laravel-tips
notes on probably useful laravel snippets

### Session driver mismatch issue

There is a known issue with laravel when you use the database driver for sessions, but the ID isn't using an integer. (ie sometimes people like to use uuid string or roll their own.) 

The workaround is proposed by the proposed merge by lesichkovm: https://github.com/laravel/laravel/pull/6494#issue-2666083027

```
Schema::table('sessions', function (Blueprint $table) {
    $table->dropIndex('sessions_user_id_index');
});
Schema::table('sessions', function (Blueprint $table) {
    $table->string(column: 'user_id', length: 40)->nullable()->index()->nullable()->change();
});
```


### Fresh laravel 11 filament requirements could not be resolved

https://stackoverflow.com/questions/78195658/fresh-laravel-11-filament-install-requirements-could-not-be-resolved-to-an-insta

### Can not install because of platform requirements

"Yes, you can use --ignore-platform-reqs to ignore php, hhvm, lib-* and ext-* platform requirements and force the installation, even if the local..." see [link](https://stackoverflow.com/questions/34637657/is-it-possible-to-ignore-child-dependencies-in-composer-config)

### Session not regenerated after auth attempted

see answer that may help: https://stackoverflow.com/a/71726239
