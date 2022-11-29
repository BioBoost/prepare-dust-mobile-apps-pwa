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

Create a file `_redirects` and redirect all routes to `index.html`

```
# Fixing Single Page Web app routes
/*    /index.html   200
```

### Fixing CORS on Netlify

I expected us to get CORS problems here, but we don't. Backend is configured to allow all cors but that was not enough in the past.

Anyways, if problems would arise here is a Netlify solution.

