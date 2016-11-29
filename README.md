# Grunt: Hipchat Notifier
> Send grunt messages to a Hipchat channel

[![Dependency Status](https://david-dm.org/jwalsh/grunt-hipchat-notifier.png)](https://david-dm.org/jwalsh/grunt-hipchat-notifier)
[![devDependency Status](https://david-dm.org/jwalsh/grunt-hipchat-notifier/dev-status.png)](https://david-dm.org/jwalsh/grunt-hipchat-notifier#info=devDependencies)

## Getting Started

This plugin requires Grunt `~1.0.1`

```shell
npm install @jwalsh/grunt-hipchat-notifier --save-dev
```

Once the plugin has been installed, it may be enabled inside your Gruntfile with this line of JavaScript:

```js
grunt.loadNpmTasks('grunt-hipchat-notifier');
```

## The "hipchat_notifier" task

### Overview

In your project's Gruntfile, add a section named `hipchat_notifier` to the data object passed into `grunt.initConfig()`.

```js
grunt.initConfig({
  hipchat_notifier: {

    options: {
      authToken: process.env.HIPCHAT_KEY,
      roomId: process.env.HIPCHAT_ROOM
    },

    // Now create as many messages as you like!

    production: {
      options: {
        message: "Production", // A message to send
        from: "Grunt", // Name for the sender
        color: "green", // Color of the message
        message_format: "html" // 'text' or 'html' 
      }
    }

  },
})
```

### Advanced

```js
grunt.initConfig({
  hipchat_notifier: {

    // You probably want to set your Hipchat options globally...

    options: {
      authToken: "", // Create an authToken at https://hipchat.com/admin/api
      roomId: "" // Numeric Hipchat roomId or room name
    },

    // Now create as many messages as you like!

    hello_grunt: {
      options: {
        message: "Hello!", // A message to send
        from: "Grunt", // Name for the sender
        color: "purple", // Color of the message
        message_format: "html" // Can either be 'text' or 'html' format
      }
    },

    // Send dynamic message based off anything Node/Grunt/Javascript can do!
    
    dynamic_hello_grunt: {
      options: {
        message: function() { // Functions must return a string
          var pkg = grunt.config.data.pkg;
          return 'Running grunt on ' + pkg.name + ' on version ' + pkg.name;
        },
        from: function() {  // Return the run-time user, or something more creative.
          return someUsernameGenerator() || process.env['USER'];
        },
        // Change color dynamically based on some global state, function response, etc
        color: function() {
          return (grunt.config.data.someBoolean && allIsWell()) ? 'green' : 'red';
        }
      }
    }

  },
})
```

## Release History

* 1.0.1 - Updates for Grunt v1
* 0.3.0 - Updated to use new hipchat-client format (deprecated sendRoomMessage) (thanks [@ksykulev](https://github.com/ksykulev)!)
* 0.2.2 - Updated hipchat-client, fixes syntax error in example
* 0.2.1 - Updated hipchat-client - roomId can now be either numeric or room name.
* 0.2.0 - Added support for Hipchat message_format to allow for emoticons and @mentions
* 0.1.1 - Added support for dynamic messaging
* 0.1.0 - First release

