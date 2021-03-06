# Grunt-sync

A [grunt](http://github.com/gruntjs/grunt/) task to keep directories in sync.
It is very similar to [grunt-contrib-copy](https://github.com/gruntjs/grunt-contrib-copy) but
tries to copy only those files that has actually changed.

## Usage

```bash
npm install grunt-sync --save
```

Within your grunt file:

```javascript
  grunt.initConfig({

    sync: {
      main: {
        files: [{
          cwd: 'src',
          src: [
            '**', /* Include everything */
            '!**/*.txt' /* but exclude txt files */
          ],
          dest: 'bin',
        }],
        pretend: true, // Don't do any IO. Before you run the task with `updateAndDelete` PLEASE MAKE SURE it doesn't remove too much.
        verbose: true // Display log messages when copying files
      }
    }

  });

  grunt.loadNpmTasks('grunt-sync');
  grunt.registerTask('default', 'sync');
```

## More examples
```javascript
sync: {
  main: {
    files: [
      {src: ['path/**'], dest: 'dest/'}, // includes files in path and its subdirs
      {cwd: 'path/', src: ['**/*.js', '**/*.css'], dest: 'dest/'}, // makes all src relative to cwd
    ],
    verbose: true,
    pretend: true, // Don't do any disk operations - just write log
    ignoreInDest: "**/*.js", // Never remove js files from destination
    updateAndDelete: true // Remove all files from desc that are not found in src

  }
}
```

## Installation
```
npm install grunt-sync --save
```

## Changelog
* 0.2.0 - Default configuration will not remove any files any more. You have to specify `updateAndDelete` option to remove any files from destination.
* 0.1.2 - Deleting all files in destination on Windows solved.
* 0.1.1 - Fixed issue with trailing slash in destination.
* 0.1.0 - Files missing that are not in `src` are deleted from `dest` (unless you specify `updateOnly`)

## Migration 0.1.x -> 0.2.x
In version 0.2 you have to explicitly specify that you want the plugin to remove files from destination. See `updateAndDelete` option and run with `pretend:true` first to make sure that it doesn't remove any crucial files. You can tune what files should be left untouched with `ignoreInDest` property.

If you have `updateOnly:true` in your 0.1 config you can remove this option. For those who used `updateOnly:false` you have to include `updateAndDelete:true` in 0.2 config to keep the same behavior.

## TODO
Research if it's possible to have better integration with `grunt-contrib-watch` - update only changed files instead of scanning everything.
