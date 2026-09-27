# Grand Café Hostinger Deployment — One npm install

This edition has been flattened into a single-root Node.js application. It does **not** use npm workspaces and it does **not** have separate client/server package files.

## 1. Upload the project

Upload the complete project folder to Hostinger or connect the complete Git repository.

The root must contain:

```text
package.json
server.js
vite.config.js
client/
server/
```

## 2. Node.js version

Select Node.js **20.x or 22.x**.

## 3. Environment variables

Add these in Hostinger:

```env
NODE_ENV=production
MONGODB_URI=mongodb+srv://YOUR_USER:YOUR_PASSWORD@YOUR_CLUSTER.mongodb.net/grand_cafe?retryWrites=true&w=majority&appName=GrandCafe
MONGODB_DB=grand_cafe
JWT_SECRET=use-a-long-random-secret-at-least-32-characters
PUBLIC_ORIGIN=https://yourdomain.com
```

`PORT` is normally assigned by Hostinger automatically.

Optional:

```env
UPLOAD_DIR=/absolute/writable/persistent/path/uploads
```

If `UPLOAD_DIR` is omitted, uploads are kept in `server/uploads`.

## 4. Install once

From the project root:

```bash
npm install
```

That one command installs React, Vite, Express, MongoDB/Mongoose and every other dependency. It also automatically runs `npm run build` because the root `package.json` contains a `postinstall` script.

Do **not** run `npm install` inside `client`.
Do **not** run `npm install` inside `server`.

## 5. Startup

Use either of these Hostinger settings:

Startup file:

```text
server.js
```

or start command:

```bash
npm start
```

The Express server serves `client/dist`, so frontend and backend run from the same Hostinger Node.js app and the same domain.

## 6. Verify

Open:

```text
https://yourdomain.com/api/health
```

Expected database status:

```json
{
  "ok": true,
  "brand": "Grand Café",
  "database": "mongodb-connected"
}
```

Then open `/admin` and create the first admin account.

## Updating later

When you upload a newer project version, keep the same MongoDB URI. Menu changes, admin accounts, orders and reservations remain in MongoDB Atlas.

If uploaded menu images matter, use a persistent `UPLOAD_DIR` and back it up before replacing deployment files.
