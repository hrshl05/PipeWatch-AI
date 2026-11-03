# PipeWatch AI

A software-based underground water pipeline leakage reporting and monitoring platform. PipeWatch AI helps communities submit suspected leakage reports with GPS coordinates and photo evidence, then view shared reports on an interactive map and dashboard.

## Features

- Firebase email/password authentication
- Shared community leakage reports for all signed-in users
- Submit suspected underground pipeline leakage reports
- Attach photo evidence (JPG, PNG, or WebP; up to 8 MB before browser-side compression)
- Capture and display GPS coordinates
- Interactive map and report visualizations
- Responsive dashboard for desktop and mobile
- Author-controlled report deletion through Firestore security rules

## Technology stack

- HTML, CSS, JavaScript
- Firebase Authentication
- Cloud Firestore
- Leaflet maps
- Tailwind CSS
- Font Awesome

## Project structure

```text
PipeWatch-AI/
├── index.html
├── README.md
├── firebase.json
├── .firebaserc
├── .gitignore
└── firestore.rules
```

## Run locally

Because the app uses browser modules and Firebase, run it through a local web server rather than opening `index.html` directly.

For example, with Python installed:

```bash
python -m http.server 8000
```

Then open `http://localhost:8000` in your browser.

## Firebase setup

1. Create or select a Firebase project.
2. Enable **Authentication → Sign-in method → Email/Password**.
3. Add the domain serving the website under **Authentication → Settings → Authorized domains**.
4. Create a Cloud Firestore database.
5. Publish the rules in `firestore.rules` using **Firestore Database → Rules**.
6. Verify the Firebase web-app configuration in `index.html` matches your project.

The included `.firebaserc` currently targets the Firebase project `roadvision-ai-4e1ea`. Change it if you are deploying to a different Firebase project.

## Deploy to Firebase Hosting

Install/use the Firebase CLI, sign in, and run these commands from the project directory:

```bash
npx firebase-tools login
npx firebase-tools deploy --only hosting,firestore:rules
```

## Data access and security

- User profile documents under `users/{uid}` are private to their owner.
- Legacy reports under `users/{uid}/reports/{reportId}` remain owner-only.
- Community reports are stored under the top-level `reports` collection.
- Any authenticated user can read community reports and submit a report.
- A report author can delete their own community report; updates are disabled by the included rules.
- Passwords are managed by Firebase Authentication and are not stored in Firestore.

Review and test Firestore rules in your own Firebase project before public deployment. The Firebase web configuration embedded in a browser app identifies the project; it is not a substitute for security rules. Never commit service-account private keys, admin credentials, or other server-side secrets.

## Important project scope

PipeWatch AI is a software-based, user-reporting and location-mapping platform. It displays suspected underground pipeline leakage observations submitted by users, supported by photos and GPS coordinates. It does **not** autonomously sense underground pipes or independently confirm a leak. Hardware sensors are not required for this software-only version.

## License

No license has been specified yet. Add a license file if you want to define how others may use, modify, and distribute this project.
