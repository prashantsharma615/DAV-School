# DAV Class 4 Study Helper: Android app

An Android app where DAV Class 4 students log in and find questions and answers for their whole syllabus: English, Hindi, Maths, Science, Social Science and Computer (84 chapters, about 390 questions).

## Get the app

- **Website (open on any phone):** https://prashantsharma615.github.io/DAV-School/
- **Android APK:** https://github.com/prashantsharma615/DAV-School/releases/latest. Download `DAV-Class4-Study-Helper.apk` and open it on the phone to install.

Every time you change anything in this repo, GitHub automatically rebuilds the APK and the website (see the **Actions** tab).

## Logins

| Who | Login ID | Password |
|---|---|---|
| Admin (teacher) | `ADMIN` | `admin123` (**change this** in the Admin Panel after the first login) |
| Demo student | `DAV4-001` | `learn123` |

**Student IDs work like this**
1. Log in as ADMIN and create each student's login (name, section, ID, password).
2. Click **Export student list** to download `students.js`.
3. Replace `www/students.js` with the downloaded file, then build a new version of the app (steps below). Every phone with that version can now use those logins.

> Logins you create in the Admin Panel are saved only on that phone until you export them and rebuild the app. If you want to add students live, with no rebuild, the next step is to connect a free online database such as Firebase.

## Make the Android app (on your Windows or Mac computer)

**Install once:** [Node.js (LTS)](https://nodejs.org) and [Android Studio](https://developer.android.com/studio).

Open a terminal (Command Prompt) inside this folder and run:

```bash
npm install
npx cap add android        # only the first time
npx cap sync android
npx cap open android       # opens the project in Android Studio
```

In Android Studio:
- **To test on a phone:** connect the phone with USB debugging on and press ▶ Run.
- **To make the Play Store file:** go to **Build → Generate Signed App Bundle / APK → Android App Bundle**, create a keystore (save that file and its password safely, because every future update needs them) and build. You'll get an `.aab` file.

**App icon:** `www/icon.png` is ready. In Android Studio, right-click `app/res`, choose **New → Image Asset**, and pick that file.

## Publish on the Google Play Store
1. Create a Google Play Developer account at https://play.google.com/console (one-time US$25 fee).
2. **Create app**, then upload the `.aab` file.
3. Fill in the store listing, privacy policy, content rating and the **Target audience** section. Because the app is for children under 13, choose those age groups. Google's *Families* policies then apply: no ads that aren't child-safe, and you need a clear privacy policy.
4. Submit for review.

## Updating content
All questions and answers are in `www/data/` (one file per subject). Each chapter looks like this:

```js
{ title: "Chapter name", summary: "One line about the chapter", qa: [
  ["Question?", "Answer."],
  ["Question 2?", "Answer 2."]
]}
```

Add or edit lines, then run `npx cap sync android` and build again.

## Important notes
- The answers are original. They follow the DAV Class 4 chapter list (DAV CMC books, 2026-27 syllabus), but the text and answer keys of the DAV books are **not** copied, because those books are copyrighted. Teachers should check the answers against the book and edit `www/data/` wherever the school's book differs.
- For English Reader lessons, only story notes are included (Lilliput, King Thrushbeard, Kanyakumari). Exercise answers that depend on the book's text should be added by the teacher.
- Chapter lists can differ slightly between DAV zones. Check them against your school's syllabus.
- Don't use "DAV" in the Play Store app name or logo without the school's or DAV CMC's permission.
