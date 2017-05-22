Google Auth
---------

- As of 5/21/2017, many of the NPM packages and Python examples that try to do this on their own are either out-of-date or in bad shape. Certainly the ones I've tried are.
- It's just easier to punch a hole in your web app and use [Google Sign-In for Websites](https://developers.google.com/identity/sign-in/web/sign-in).
  - You include a `script` tag to pull in Google code (it's 16 KB) that'll look for a `meta` tag with your client id and div with a specific class then wire the div as a button that uses your client id to open an iframe in a *popup* window that'll do the sign in.
  - It'll call a callback on `window` that you specify with a `googleUser` object that has user info methods as well as a `grant` method you can use to ask for additional permissions. e.g.:

        function onSignIn(googleUser) {
          var profile = googleUser.getBasicProfile();
          console.log('Name: ' + profile.getName());
          console.log('Image URL: ' + profile.getImageUrl());

          var options = new gapi.auth2.SigninOptionsBuilder({
            scope: 'https://www.googleapis.com/auth/calendar.readonly'
          });

          googleUser.grant(options).then(grantSucceeded, grantFailed);
        }

        function grantSucceeded(grantResult) {
          // console.log(grantResult);
          accessToken = grantResult.Zi.access_token;
          idToken = grantResult.Zi.id_token;
          // routeState.routeFromHash();
          route();
        }

        function grantFailed(fail) {
          handleError(new Error('Grant failed: ' + JSON.stringify(fail)));
        }

- [Example in where-is-your-time.](https://github.com/jimkang/where-is-your-time/blob/gh-pages/app.js)
