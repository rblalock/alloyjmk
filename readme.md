# alloy.jmk

## Why?

This was an experiement to solve an issue I have with an app (or series of apps) built from a single code base. I first attempted to solve it with [TiCh](https://github.com/jasonkneen/tich) which kind of works, but isn't great when it comes to having Android sections in the Tiapp.xml file.

The issue I had with this is that I had to keep changing the alloy theme, then rememebring to copy the relevant file over, and do this for each build - very easy to make mistakes and I did!

### What it does

alloy.jmk is a build file that runs before compilation of an Alloy project - it's a standard part of alloy and allows you to run tasks  after and before compilation, the latter being the perfect time to **swap the tiapp.xml with another** based on an Alloy theme!

Download the jmk and drop it in your Alloy app folder (same folder as the config.json).

(remember to do a ti clean before each build)

My config.json looks like this:

```JSON
{
    "global": {
        "appConfig": {            
            "ios": {
                "default": "tiapp_default.xml",
                "app2": "tiapp_app2.xml",
                "app3": "tiapp_app3.xml"
            },
            "android": {
                "default": "tiapp_default.xml",
                "app2": "tiapp_app2.xml",
                "app3": "tiapp_app3.xml"
            }
        },
        "theme": "app2"
    },
    "env:development": {},
    "env:test": {},
    "env:production": {},
    "os:android": {},
    "os:blackberry": {},
    "os:ios": {},
    "os:mobileweb": {},
    "dependencies": {}
}
```

The key things here are the "theme" reference and the "appConfig" section. In my example, the appIds for the apps I'm building are different (legacy thing), so I need a need a different tiapp.xml for each app *and* platform. (in the example above I use the same one for iOS and Android but they can be different).

My workaround is to have the default tiapp.xml (where no theme is specified) copied to **tiapp_default.xml**, I then create variations of this as **tiapp_app1.xml** etc *and* I set git to ignore the tiapp.xml file I don't get crazy commits going on.

The result is that if I simply change the theme to "app1" and build the app, it'll automatically copy the relevant tiapp.xml in place before Alloy starts, so my app is built with the theme specified and using the tiapp.xml I wanted.

:)

## To add

* a "common" setting if you don't want to specify platforms
* more error handling / help

Work in progress. Happy to look at any PRs though! ;)

## License

<pre>
Copyright 2015 Jason Kneen

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
</pre>
