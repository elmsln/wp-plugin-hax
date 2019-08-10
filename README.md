## HAX
Bringing the HAX block editor to ClassicPress & WordPress. [HAX](https://haxtheweb.org/) is short for headless authoring experience, meaning that it is a block editor that is disconnected from the CMS its used in. HAX recognizes editable blocks by using the [web component standard](https://webcomponents.org/) and a small piece of abstracted JSON Schema called [HAX Schema](https://haxtheweb.org/hax-schema) in order to know what's editable. HAX provides all of the editing capabilities in a way that attempts to write clean HTML markup the same way an expert end-user could, but without ever touching code.

## Dependencies
- You'll also need the [Webcomponents plugin](https://github.com/elmsln/wp-plugin-webcomponents) to use HAX.
- If using WordPress, you'll need to get the [Classic Editor plugin](https://wordpress.org/plugins/classic-editor/)
  - ClassicPress does not have this dependency

## Usage

This should give you the dependencies you need to get going.
1. Download this plugin and place it in wp-content/plugins/hax
2. Download the Webcomponents plugins and place it in wp-content/plugins/webcomponents
3. If using WordPress you'll also need the Classic Editor plugin; and then you'll also have to enable it as the default editor (wp-admin/options-writing.php)
4. Enable the Plugins (wp-admin/plugins.php)
5. Go to edit or create a new page / post
6. Enjoy HAX'ing the web

## Note on usage
The default is to serve the Javascript required for HAX and its web components from a CDN. We default to a Penn State mirror of the required assets so you can get up and running quickly. We recommend that if you choose to go into production with HAX, that you look at doing a build routine locally (outlined below) in order to reduce your reliance on our CDN as well as give you a specific version of the assets.

## Hooking up additional "apps" in the "Find" area
To connect to popular services like YouTube, Flickr, and Vimeo you'll need an API key. You can find details on how to get these keys as well as where to put them on the General Settings (wp-admin/options-general.php) page.

### Developer functions
By default, the auto-loaded elements (things you make with HAX and hit save) need to have the website taught how to render. This means that their web component JS files will be added to the site in order for them to render for users. This list can be modified on the General Settings page wp-admin/options-general.php.

# Front end Developers
You may build HAX from source if needed. HAX defaults to use CDNs which will effectively point to
this directory or some mutation of it -- https://github.com/elmsln/HAXcms/tree/master/build

If you want to build everything from source, your welcome to use yarn / npm to do so though our
build routine effectively will end in the same net result.  If you want to do custom build routines
such as rollup or webpack and not use our prebuilt copies / split build approaches, then your welcome
to check the box related to not loading front end assets in the settings page in order to tailor
the build to your specific needs.

## Getting dependencies
You need polymer cli (not polymer but the CLI library) in order to interface with web components in your site. Get polymer cli installed prior to usage of this (and (yarn)[https://yarnpkg.com/lang/en/docs/install/#mac-stable] / an npm client of some kind)
```bash
$ yarn global add polymer-cli
```
Perform this on your computer locally, this doesn't have to be installed on your server.

## Usage

- Find `CopyThisStuff` directory in `/wp-content/plugins/webcomponents`.
- create a `/wp-content/webcomponents` directory
- copy the files from `CopyThisStuff` into `/wp-content/webcomponents`

Then run the following (from the directory you copied it over to) in order to get dependencies:
```bash
$ yarn install
```
Now run `polymer build` and you'll have files in `build/` which contain everything you'll need to get wired up to web components in your site. Modifying build.js or package.json can be used in order to get new elements and have them be implemented.

### Shouldn't I put web components in my theme?
We don't think so. While it may seem counter intuitive, the theme layer should be effectively implementing what the site is saying is available. If you think of standard HTML tags are being part of this (p, div, a, etc) then it makes a bit more sense. You don't want functional HTML components to ONLY be supplied if your theme is there, you want your theme to implement and leverage the components.

## New to web components?
We built our own tooling to take the guess work out of creating, publishing and testing web components for HAX and other projects. We highly recommend you use this tooling though it's not required:
- https://open-wc.org - great, simple tooling and open community resource
- https://github.com/elmsln/wcfactory - Build your own web component library
- https://github.com/elmsln/lrnwebcomponents - Our invoking of this tooling to see what a filled out repo looks like
