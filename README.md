<p align="center"><img src="https://i.imgur.com/lfe9Emp.png" align="center"></p>

This repo contains CSS tweaks and modifications for [Mastodon](https://joinmastodon.org), a libre micro-blogging social server whose default web frontend is similar to Tweetdeck. These mods can be used to create custom themes by admins for their Mastodon instances, or imported into userstyle extensions by users.

# Instructions for admins
Download this repo and copy the files into your Mastodon deployment. If I can figure out the git commands to fetch the files without messing up your existing Mastodon deployment, I'll add them here.

Let's use the Linernotes Dark theme as an example. Per [these olds docs](https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Customizing.md), to enable a new theme, you need to do the following:

1. **Fetch the files.** Add your desired custom CSS/SCSS to `app/javascript/styles`. You can copy/merge the entire `app` folder from the root of this repo into the root of your Mastodon deployment.

```
app/
  javascript/
    styles/
      contrast/
        ...
      fonts/
        ...
      linernotes_dark/                            | **new**
        overrides.scss                            | **new**
        palette.scss                              | **new**
      mastodon-light/
        ...
      mastodon/
        ...
      mfc/                                        | **new**
        mastodonFlat.css                          | **new**
        variables.scss                            | **new**
      mods/                                       | **new**
        avatars_circle.css                        | **new**
        columns_gettingstarted.css                | **new**
        ...                                       | **new**
        misc_elefriend.css                        | **new**
      application.scss
      contrast.scss
      linernotes_dark.scss                        | **new**
      mailer.scss
      mastodon-light.scss
```


2. **Add your theme to the config.** This is what [the default themes.yml](https://github.com/tootsuite/mastodon/blob/master/config/themes.yml) looks like in Mastodon. To make your custom theme visible in settings, you need to add a new line in the form `themeName: path/to/theme.scss`. For example, the linernotes_dark theme would require adding `linernotes_dark: styles/linernotes_dark.scss` as a new line. 

```
default: styles/application.scss
contrast: styles/contrast.scss
mastodon-light: styles/mastodon-light.scss
linernotes_dark: styles/linernotes_dark.scss      | **new**
```

3. **Add a human-friendly name for the theme (optional).** You can edit each desired language's locale file in `config/locales/[lang].yml` to add a localized string name for your theme's `themeName` as added in the previous step. For example, [the default `config/locales/en.yml`](https://github.com/tootsuite/mastodon/blob/041ff5fa9a45f7b8d1048a05a35611622b6f5fdb/config/locales/en.yml#L942-L945) contains localizations for the three default themes that ship with Mastodon, into the `en`glish language. You need to do this for every language you expect your users to use, or else they will see the unlocalized `themeName` directly.

```
  themes:
    contrast: Mastodon (High contrast)
    default: Mastodon (Dark)
    mastodon-light: Mastodon (Light)
    linernotes_dark: Linernotes Dark              | **new**
```

4. **Compile theme assets and restart.** Run `RAILS_ENV=production bundle exec rails assets:precompile` and restart your Mastodon instance for the changes to take effect.

# Instructions for users

**If your admin has installed a theme:**
1. Go to your instance's Settings/Preferences.
2. Scroll down to the "Web" section.
3. Click the "Site theme" dropdown and select your desired theme.
4. Save changes, and start using the Mastodon webapp with your newly selected theme!

**If your admin has not installed a theme:**

Copy and paste desired CSS tweaks into your user-style manager. If you don't have one, use Stylus:

[![stylus icon](https://addons.cdn.mozilla.net/user-media/addon_icons/814/814814-64.png)](https://add0n.com/stylus.html)
[![firefox](https://static.filehorse.com/icons-mac/browsers-and-plugins/firefox-icon-32.png)](https://addons.mozilla.org/en-US/firefox/addon/styl-us/)
[![opera](https://static.filehorse.com/icons-mac/browsers-and-plugins/opera-icon-32.png)](https://addons.opera.com/en/extensions/details/stylus/)
[![chrome](https://static.filehorse.com/icons/browsers-and-plugins/google-chrome-icon-32.png)](https://chrome.google.com/webstore/detail/stylus/clngdbkpkpeebahjckkjfobafhncgmne)
[![source code](https://github.githubassets.com/favicon.ico)](https://github.com/openstyles/stylus/)

Another way to get some of these tweaks... | Help
--- | ---
A distribution of Mastodon Flat CSS is available at https://userstyles.org/styles/153362 and contains many of these tweaks through the "Customize settings" menu. | ![image](https://i.imgur.com/5FpYwlQ.png)

The base MFC userstyle can be found at `app/javascript/styles/mfc/mastodonFlat.css`. You can load a theme into Stylus like so:

1. Navigate to your Mastodon instance.
2. Click the Stylus extension's icon in your browser and find the section that says "Write style for:"
3. Hover over the website's domain name (e.g. `mastodon.social`) and click just that part, in order to write a new style that will be applied to the entire website.
4. Copy and paste the contents of `mastodonFlat.css` into your new userstyle.
5. Copy and paste any desired mods into your new userstyle.
6. Name your userstyle, then click "Save" and close the popup window.

# Other info
Prior work | Preview
--- | ---
This work is heavily based on (and an extension of) my earlier work on [Mastodon Flat CSS](https://github.com/trwnh/mastodon-flat-css), and its child theme [Linernotes Mastodon Themes](https://github.com/trwnh/linernotes_mastodon_themes). I grew tired of having to maintain what was essentially the same code in multiple different places, so this repo was created to be a more modular way of managing code snippets after I learned enough about how importing works. | ![mfc preview](https://raw.githubusercontent.com/trwnh/mastodon-flat-css/master/mfc.png)
linernotes_dark is an admin-installable theme that was commissioned for linernotes.club. Because the base MFC theme is adaptable, it is not too difficult to build your own theme on top of it. See the source code for comments and documentation. | ![linernotes preview](https://raw.githubusercontent.com/trwnh/mastomods/master/.PREVIEWS/linernotes_dark.png) 

# Support
[![mastodon](https://i.imgur.com/ahOT5QI.png)](https://mastodon.social/@trwnh) Contact/follow me: [mastodon.social/@trwnh](https://mastodon.social/@trwnh)

[![email](https://cdn0.iconfinder.com/data/icons/woocons1/Mail.png)](mailto:a@trwnh.com) Email/XMPP: a@trwnh.com
[![xmpp online status](http://trwnh.com:5280/status_alt/a)](xmpp:a@trwnh.com)

[![paypal](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRGOZY1FoaRFdYzeDvRKK3aFHmPnFYMmgd8K3UuZhab-exTZfCc4g)](https://paypal.me/trwnh) Tip me: [paypal.me/trwnh](https://paypal.me/trwnh)

[![liberapay](https://i.imgur.com/B8RZn2y.png)](https://liberapay.com/trwnh) Recurring patronage: [liberapay.com/trwnh](https://liberapay.com/trwnh)
