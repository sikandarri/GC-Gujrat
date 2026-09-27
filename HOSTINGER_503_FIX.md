# Hostinger 503 checklist

Use the project root that contains `package.json` and `server.js`.

## Hostinger settings

- Node.js: 20.x or 22.x
- Build command: `npm install` (the project postinstall runs the Vite build)
- Start command: `npm start`
- Port: `3000`

## Required environment variables

```env
NODE_ENV=production
PORT=3000
MONGODB_URI=mongodb+srv://...
MONGODB_DB=grand_cafe
JWT_SECRET=your-64-byte-random-secret
PUBLIC_ORIGIN=https://your-domain.com
```

Do not include a trailing slash in `PUBLIC_ORIGIN`.

## MongoDB Atlas

Make sure the Atlas database user is valid and Network Access allows the Hostinger server to connect. For a temporary connectivity test you can allow `0.0.0.0/0`, then narrow it later if you have a stable outgoing IP.

## Verification

After deployment open:

`https://your-domain.com/api/health`

The app should respond even while MongoDB is reconnecting. When connected, `database` becomes `mongodb-connected`.

If the site still fails, open Hostinger Dashboard > Deployments > the current deployment > Runtime logs and copy the first error line.
