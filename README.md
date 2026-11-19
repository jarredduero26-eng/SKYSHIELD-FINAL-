# SkyShield AI (Bootstrap 5.3.3)

**SKYSHIELD AI: An Intelligent Weather Risk Prediction and Personalized Preparedness System for Students**
Group 5: Jarred D. Duero, Angel May E. Guibelondo, Princess Jewel Salon

A fully offline website built on our subject teacher's Bootstrap template. Students can sign up, log in, check weather risk, read alerts, view the study, and open their school location and route. Weather is simulated in JavaScript, so no API keys are needed.

**Pages included:** Home, Login, Sign Up, Dashboard (Weather Risk, Alerts, About the Study, Literature, Evaluation & Team, Location & Route).

---

## Table of Contents

1. [Quick Start](#1-quick-start)
2. [Project Structure](#2-project-structure)
3. [Dashboard Pages](#3-dashboard-pages)
4. [How the Offline Login Works](#4-how-the-offline-login-works)
5. [How the Risk Score Works](#5-how-the-risk-score-works)
6. [Location and Route](#6-location-and-route)
7. [Buttons and UI Features](#7-buttons-and-ui-features)
8. [Bootstrap Components Used](#8-bootstrap-components-used)
9. [How to Edit](#9-how-to-edit)
10. [Test Checklist](#10-test-checklist)
11. [Common Mistakes and Fixes](#11-common-mistakes-and-fixes)
12. [Limitations and Credits](#12-limitations-and-credits)

---

## 1. Quick Start

1. Open the project folder in **VS Code**.
2. Right-click `index.html` and choose **Open with Live Server** (or double-click it).
3. Click **Sign Up**, create an account, and the dashboard opens.
4. Change something, save, and refresh (**Ctrl + F5**).

---

## 2. Project Structure

```
skyshield-ai/
├── index.html               Home page
├── pages/
│   ├── login.html           Login page
│   ├── signup.html          Sign up page
│   └── dashboard.html       Student dashboard (all app pages)
├── assets/
│   ├── css/
│   │   ├── bootstrap.min.css        Bootstrap styles (do NOT edit)
│   │   ├── bootstrap-icons.min.css  Icon styles (do NOT edit)
│   │   ├── fonts/                   Icon fonts
│   │   └── style.css                OUR custom styles (edit this one)
│   ├── js/
│   │   ├── bootstrap.bundle.min.js  Bootstrap JavaScript (do NOT edit)
│   │   └── app.js                   OUR logic: accounts, risk engine, alerts, evaluation
│   └── images/                      Photos and favicon
└── README.md
```

**Rule of thumb:** edit the HTML files, `style.css` and `app.js`. Do not edit `.min.css` or `.min.js` files.

---

## 3. Dashboard Pages

The sidebar (or the menu button on phones) switches between pages without reloading.

| Page | What it does |
|------|--------------|
| **Weather Risk** | Preset buttons (Heavy Rainfall, Thunderstorm, Extreme Heat, Clear Weather) and a custom check. Shows temperature, rainfall, heat, wind, a 0-100 score, a Low / Moderate / High badge and personalized recommendations. |
| **Alerts** | Live feed with Simulate Incoming Alert, Acknowledge, Acknowledge All, Clear All and filters by risk level. Includes the official-advisory disclaimer. |
| **About the Study** | Background and Problem, Objectives, Significance (filter by group), Scope (6 features) and Limitations (7). |
| **Literature** | Search and Local / Foreign filters for the 9 studies, each expandable. |
| **Evaluation & Team** | Functionality and usability form with a live score summary, and credits for Group 5. |
| **Location & Route** | Opens the saved school location and route, copies the link, and shows route advice for the current risk level. |

---

## 4. How the Offline Login Works

- Accounts are saved in the browser's **localStorage**, so no internet or server is needed.
- Sign Up stores your name, email and a hashed password. Login compares the hash.
- **Remember me** keeps you logged in after closing the browser.
- The Dashboard is protected. Opening it without logging in sends you to Login.
- Alerts and evaluation responses are saved per account. **Delete my account** removes them.
- The profile menu (click your name) lists every **saved account** on this device with a check mark on the one you are using. Accounts stay in the list until they are deleted. Clicking another account opens Login with that email filled in, and you type its password. **Add another account** opens Sign Up.

Note: accounts exist only in the browser and device where they were created. The simple hash is for learning and is not real security.

---

## 5. How the Risk Score Works

Score = rainfall + lightning + heat + travel mode + trip time + electronics, capped at 100.

| Factor | Points |
|--------|--------|
| Rainfall (mm/h) | 50 for 30+, 35 for 15+, 22 for 7.5+, 10 for 2.5+, 5 for any rain |
| Lightning nearby | 30 |
| Heat feels like | 45 for 41C+, 30 for 36C+, 12 for 32C+ |
| Travel | Walking 10, Bicycle/motorcycle 20, Covered 0 |
| Trip time | over 30 min: 15, over 10 min: 8, otherwise 3 |
| Electronics in rain or storm | 5 |

**70+ = High**, **40-69 = Moderate**, **below 40 = Low**. The logic follows our C program (RainReady 2.0).

---

## 6. Location and Route

The route opens Google Maps directions to the school (University of Science and Technology of Southern Philippines, Cagayan de Oro):

`https://www.google.com/maps/dir/?api=1&destination=University%20of%20Science%20and%20Technology%20of%20Southern%20Philippines%2C%20Cagayan%20de%20Oro`

It appears on the Home page, the Weather Risk page and the Location & Route page. To change it, search for `google.com/maps` in `index.html` and `pages/dashboard.html`, and change `ROUTE_URL` in `assets/js/app.js`. Opening the map needs internet. Everything else works offline.

---

## 7. Buttons and UI Features

- All buttons share one style: rounded corners, a gradient on main buttons, a lift on hover, a press effect and a clear keyboard focus ring.
- Weather preset buttons stay highlighted when selected.
- Buttons show a small spinner while working (Login, Sign Up, Analyze Custom Conditions).
- Show / hide password buttons on Login and Sign Up.
- Copy Link shows "Copied!" after copying.
- A Back to top button appears when you scroll down.
- The Home navbar highlights the section you are reading.
- The profile menu has your email, saved accounts, Dashboard, Usability Survey and Log out.
- The three clickable arrows (Who benefits?, Limitations and the profile menu) use our own code in `app.js`, so they open and close even if Bootstrap's JavaScript fails to load. Press **Esc** or click outside to close the menu.

---

## 8. Bootstrap Components Used

| Component | Found in |
|-----------|----------|
| Navbar | `index.html` |
| Hero, cards, grid | `index.html`, `dashboard.html` |
| Form, input group, range | `login.html`, `signup.html`, `dashboard.html` |
| Offcanvas | `dashboard.html` (phone menu) |
| Dropdown | `dashboard.html` (profile menu) |
| Progress bar, table, badge, alert | `dashboard.html` |

---

## 9. How to Edit

- **Brand color:** `--brand` and `--brand-dark` at the top of `style.css`.
- **Score weights:** `score()` and `LV()` in `app.js`.
- **Advice text:** `recs()` in `app.js`.
- **Literature, objectives, limitations:** the `LIT`, `OBJ`, `SCOPE` and `LIM` lists in `app.js`.
- **Hero image:** replace `assets/images/hero.jpg`.

---

## 10. Test Checklist

- [ ] All pages open without errors
- [ ] Sign Up, Logout and Login work; wrong password shows an error
- [ ] Opening `pages/dashboard.html` while logged out goes to Login
- [ ] Every preset and the custom check update the risk result
- [ ] Alerts: simulate, filter, acknowledge, clear
- [ ] About tabs, Literature search and filters, Evaluation score
- [ ] Route buttons open the link; Copy Link says "Copied!"
- [ ] Accordion, profile menu and Back to top button work
- [ ] Looks good on phone size (**F12**, then **Ctrl + Shift + M**)
- [ ] Works with the internet turned off (except the map link)

---

## 11. Common Mistakes and Fixes

| Problem | Likely cause | Fix |
|---------|--------------|-----|
| Page has no styling | Wrong CSS path | Check `assets/` vs `../assets/` |
| Icons show as empty squares | `fonts/` folder missing | Keep `bootstrap-icons.min.css` and `css/fonts/` together |
| Hamburger menu or phone side menu does nothing | `assets/js/bootstrap.bundle.min.js` is missing or was replaced by `app.js` code | Keep the real Bootstrap file there. `app.js` is a separate file |
| Buttons on the dashboard do nothing | `app.js` missing | Keep `assets/js/app.js` and its `<script>` line |
| Account disappeared | Different browser or data cleared | Sign up again |
| Changes do not appear | File not saved or cached | Save, then **Ctrl + F5** |

---

## 12. Limitations and Credits

- Weather values are simulated, not live data. SKYSHIELD AI is a supplementary tool and does not replace official advisories from authorized government agencies.
- Bootstrap 5.3.3 and Bootstrap Icons 1.11.3 (MIT License)
- Photos from Unsplash (Unsplash License)
- Based on the teacher's Bootstrap template and our Group 5 Concept Paper.

