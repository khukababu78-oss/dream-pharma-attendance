# Dream Pharma Attendance

Staff check in and out with a selfie and GPS location. The owner sees details, a monthly summary and a salary sheet.

Files
- `index.html` is the whole app (host it on GitHub Pages).
- `firestore.rules` goes into Firebase (Firestore Database > Rules).

## 1. Firebase (backend)

1. Go to console.firebase.google.com and click Add project. Name it, for example, `dream-pharma-attendance`. Google Analytics can stay off.
2. Build > Authentication > Get started. In Sign-in method, turn on **Anonymous** and **Email/Password**.
3. Authentication > Users > Add user. Enter your own email (lowercase) and a strong password. This is the admin login.
4. Build > Firestore Database > Create database. Choose a region close to Bangladesh (asia-south1 Mumbai or asia-southeast1 Singapore) and start in production mode.
5. Firestore > Rules. Delete everything, paste the contents of `firestore.rules`, replace `OWNER_EMAIL_HERE` with the admin email from step 3 (lowercase), then Publish.
6. Project settings (gear icon) > General > Your apps > click the web icon `</>`. Register an app and copy the `firebaseConfig` values.
7. Open `index.html` in a text editor. Near the top, replace the four `PASTE_...` values (apiKey, authDomain, projectId, appId) with your config. Save.

The apiKey in a web app is not a secret. Your data is protected by the Firestore rules.

## 2. GitHub Pages (hosting)

1. Create a new repository on github.com, for example `dream-pharma-attendance`. Public is fine; Pages on a free account needs a public repo.
2. Add file > Upload files. Upload `index.html` (with your config filled in) and `README.md`. Commit.
3. Settings > Pages. Under Build and deployment choose Deploy from a branch, Branch `main`, folder `/ (root)`, Save.
4. After a minute the site is live at `https://YOUR-USERNAME.github.io/dream-pharma-attendance/`.
5. Back in Firebase: Authentication > Settings > Authorized domains > Add domain, and add `YOUR-USERNAME.github.io` (no https, no path).

## 3. First use

1. Open the link on your phone. Go to Settings and sign in with the admin email and password.
2. Stand inside the shop and tap "Use my current location as the shop".
3. Set shift start time, grace minutes, weekly off day and the late rule.
4. Add each staff member with a monthly salary and an optional 4 digit PIN.
5. Share the link with staff. They pick their name, take a selfie and check in. Allow Camera and Location when the browser asks.

## Notes

- GPS and camera need HTTPS. GitHub Pages and Firebase Hosting both provide it.
- Photos are stored as small images inside Firestore, so Firebase Storage is not needed.
- Staff can only create their own check-in and add check-out details. Only the admin can list records, edit staff, settings and salary adjustments.
- A phone with a wrong clock can send a wrong time. The server time is saved in each record as `serverAt` for checking.
