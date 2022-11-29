# Prepara DUST Mobile Apps PWA and Deployment

## Deployment

1. Setup a netlify.toml file to specify how the site should be build

```toml
[build]
  command = "npm run build"
  publish = "dist"
  environment = { NODE_VERSION = "18.8.0", NPM_VERSION = "8.18.0" }
```

2. Fix the refresh on `/about` (basically surfing directly to routes in SPA's)

You can create a file called `_redirects` in `dist` (needs to be taken into account when building the app) with the content below:

```
# Fixing Single Page Web app routes
/*    /index.html   200
```

Or you can add the redirect to the `netlify.toml` file:

```toml
[[redirects]]
  from = "/*"
  to = "/index.html"
  status = 200
  force = false
```

More info @ [https://docs.netlify.com/routing/redirects/](https://docs.netlify.com/routing/redirects/),

### Fixing CORS on Netlify

Source: [https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS](https://developer.mozilla.org/en-US/docs/Web/HTTP/CORS)

I expected us to get CORS problems here, but we don't. Backend is configured to allow all cors but that was not enough in the past.

Anyways, if problems would arise here is a Netlify solution.

```toml
[[redirects]]
  from = "/api/*"
  to = "https://dust.devbitapp.be/api"
  status = 200
  force = true
```

**Make sure to place this before the `/*` redirect!**

More info @ [https://docs.netlify.com/configure-builds/file-based-configuration/#redirects](https://docs.netlify.com/configure-builds/file-based-configuration/#redirects).