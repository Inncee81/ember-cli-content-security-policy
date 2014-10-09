# ember-cli-content-security-policy

This addon adds the `Content-Security-Policy` header to response sent from the Ember CLI Express server.
Clearly, Ember CLI's express server is not intended for production use, and neither is this addon. This is intended as a
tool to ensure that CSP is kept in the forefront of your thoughts while developing an Ember application.

## Options

This addon is configured via your applications `config/environment.js` file. Two specific properties are
used from your projects configuration:

* `contentSecurityPolicyHeader` -- The header to use for CSP (**default: `Content-Security-Policy-Report-Only`**)
* `contentSecurityPolicy` -- This is an object that is used to build the final header value. Each key/value
  in this object is converted into a key/value pair in the resulting header value.

The default `contentSecurityPolicy` value is:

```javascript
  contentSecurityPolicy: {
    'default-src': "'none'",
    'script-src': "'self'",
    'font-src': "'self'",
    'connect-src': "'self'",
    'img-src': "'self'",
    'style-src': "'self'",
    'media-src': "'self'"
  }
```

Which is translated into:

```
default-src 'none'; script-src 'self'; connect-src 'self'; img-src 'self'; style-src 'self';
```

*Please note*:
+ when running `ember serve` with live reload enabled, we also add the `liveReloadPort` to
the `connect-src` and `script-src` whitelists.
+ when running in development we add `'unsafe-eval'` to the `script-src`. This is to allow the `wrapInEval`
functionality that ember-cli does by default (as a sourcemaps "hack").
+ when setting the values on `contentSecurityPolicy` object to 'self', 'none', 'unsafe-inline','unsafe-eval','inline-script' or 'eval-script', you must include the single quote as shown in the default value above.

## Installation

```bash
npm install --save-dev ember-cli-content-security-policy
```

## Resources:

* http://www.w3.org/TR/CSP/
* http://content-security-policy.com/
* https://developer.mozilla.org/en-US/docs/Web/Security/CSP/Using_Content_Security_Policy
