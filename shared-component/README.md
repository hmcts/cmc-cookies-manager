# CMC Cookie Manager
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Cookie Manager is a Javascript library for dealing with cookie compliance.

It can handle removing cookies which the user does not consent to or those that are not defined in the manifest.
It can also handle the storing of user preferences when it comes to cookies, and includes the functionality to display a banner when no
preferences have been set.

## Programing langualge

* [Nunjucks](https://mozilla.github.io/nunjucks/)
* [JavaScript](https://www.javascript.com/)

## Dependencie / Prerequisites 

* [govuk-frontend](https://www.npmjs.com/package/govuk-frontend) ^3.11.0

```bash
npm install govuk-frontend --save
```

Make sure `serviceName` nunjucksEnv is avalable in your application

```typescript
nunjucksEnv.addGlobal('serviceName', `Money Claims`)
```

## Installation

NPM

```bash
npm i github:hmcts/cmc-cookies-manager#2.0.0
```
**** Always use the latest release in above npm command (insted of #2.0.0 use latest release version).

## Usage

Update the gulp file to import the *.njk and javascript files into your project.

example :

```javascript
function copyCookieBanner() {
  gulp.src([
    `./node_modules/cmc-cookies-manager/components/cookie-manager/**/*.js`
  ])
    .pipe(gulp.dest(`${assetsDirectory}/js/`))

  gulp.src([
    `./node_modules/cmc-cookies-manager/components/cookie-manager/**/*.njk`
  ])
    .pipe(gulp.dest(`${appDirectory}/cookie-manager/`))

  gulp.src([
    `./node_modules/cmc-cookies-manager/components/cookie-banner/**/*.*`
  ])
    .pipe(gulp.dest(`${appDirectory}/cookie-banner/`))
}
```

Include the `cookie-manager.js` script on your web pages:

```html
<script src="{{ asset_paths['js'] }}/cookies-manager.js"></script>
```

Include the `cookie-banner.njk` on your web pages:

| Preferably include it in your govukTemplate.njk

```html
  <div>
    <link href="/stylesheets/govuk-frontend-3.11.0.min.css" media="screen" rel="stylesheet" type="text/css"/>
    {% include "../common/components/imported/cookie-manager/cookie-banner.njk" %}
  </div>
```

CMC-COOKIES-MANAGER has three major activits:

1. Display the cookie banner
2. Provide cookies preference and details page
3. JavaScript for managing the cookies

Including / importing `cookie-banner.njk` will enable the cookie banner in your webpage. Now we should need to create tow new pages wich will act as cookie-preference page (preference page will allow you to update your cookies preference) and cookies details page (will explai different type of cokies in your application).

Create a new webpage called `cookies.njk` and include `cookie-preferences.njk` this will enable cookies preference page

```html
  <div class="grid-row">
    <div class="govuk-!-margin-left-4">
      {% include "../common/components/imported/cookie-manager/cookie-preferences.njk" %}
    </div>
  </div>
```

Now your application is fully configured.

### Cookies Preference details
| Option | Description | Default Value |
| --- | --- | --- |
| cookies_policy | Name of cookie which stores cookie preferences | 'cm-user-preferences' |
| cookies_preferences_set | Name of cookie which stores details regarding cookie preferences is set by user or not | true / false |
| user-preference-cookie-expiry-days | Expiry time of cookie manager preference cookie (in days) | 365 |

If `cookies_preferences_set` cookie is `false` then the `cookie-manager.js` will enable the cookies banner which all user to accept or rectect the cookies preferences. You can get the user selected cookies preferences from the `cookies_policy` cookies, based on the value you have to implement service releated operations (eg: turn on or off the google analytics).


## Authors

* [Prathap Mathiyalagan](https://github.com/pradhap87)
* [OCMC Team](https://github.com/orgs/hmcts/teams/cmc)

## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

## License
[MIT](https://choosealicense.com/licenses/mit/)