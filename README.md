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

