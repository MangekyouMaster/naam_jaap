# नाम जाप — पूरा Setup Guide (Login + Database + Play Store)

## पड़ाव 1 — Firebase Project बनाओ (Login + Database के लिए)

1. [console.firebase.google.com](https://console.firebase.google.com) खोलो, Google account से login करो
2. "Add project" → नाम दो (जैसे `naam-jaap`) → आगे बढ़ो (Analytics ऑफ कर सकते हो, ज़रूरी नहीं)
3. बाईं तरफ **Build → Authentication** → "Get started" → **Sign-in method** टैब में:
   - "Email/Password" पर क्लिक करके Enable करो
   - "Google" पर क्लिक करके Enable करो (support email चुनना होगा — अपना ईमेल चुन लो)
4. बाईं तरफ **Build → Firestore Database** → "Create database" → **Production mode** चुनो → कोई भी नज़दीकी region (जैसे `asia-south1`) चुनकर बना लो
5. Firestore के **Rules** टैब में जाकर, `firestore.rules` file का पूरा content copy-paste करो और **Publish** दबाओ (इससे हर user सिर्फ़ अपना ही data देख/बदल पाएगा — किसी और का नहीं)
6. Project Settings (⚙️ आइकॉन) → नीचे स्क्रॉल करो → "Your apps" → वेब आइकॉन (`</>`) पर क्लिक करो → app का nickname दो → "Register app"
7. अब जो `firebaseConfig` कोड दिखेगा (apiKey, authDomain, आदि), उसे copy करो

## पड़ाव 2 — Config को App में डालो

1. `index.html` फ़ाइल किसी text editor (Notepad, या GitHub पर सीधे edit) में खोलो
2. शुरुआत में `const firebaseConfig = { ... }` ढूंढो
3. वहाँ की values (`YOUR_API_KEY` वगैरह) को Firebase से मिली असली values से बदल दो
4. Save करो

## पड़ाव 3 — Online Host करो

पहले जैसे ही: GitHub पर नया repo बनाओ, इस folder की सारी files (index.html, manifest.json, service-worker.js, firestore.rules नहीं चाहिए यहाँ — वो सिर्फ़ Firebase console में paste करने के लिए था, बाकी सब files + icons) upload करो, Settings → Pages से enable करो। एक live link मिलेगा।

**ज़रूरी:** Firebase console में **Authentication → Settings → Authorized domains** में अपना GitHub Pages वाला domain (`username.github.io`) जोड़ना मत भूलना, वरना Google Sign-In काम नहीं करेगा।

## पड़ाव 4 — APK बनाओ और Test करो

pwabuilder.com पर वही link डालो → Android package बनाओ → APK मिलेगा → फ़ोन में install करके test करो।

## "App के अंदर browser जैसा bar दिख रहा है" — इसे कैसे हटाएं

जब आप PWABuilder से पहली बार Android package बनाते हो, तो ऊपर एक address-bar जैसी पट्टी दिख सकती है। इसे हमेशा के लिए हटाने के लिए **Digital Asset Links verify** करना होता है — यानी अपनी website को अपनी Android app से "जोड़ना" पड़ता है ताकि Android को पता चले कि ये आपकी ही app है:

1. PWABuilder Android package के साथ एक `assetlinks.json` फ़ाइल भी बनकर आती है (या instructions में एक SHA-256 fingerprint दिया होता है)
2. इस repo में मौजूद `assetlinks.json` template लो, उसमें `package_name` और `sha256_cert_fingerprints` की जगह PWABuilder से मिली असली values डालो
3. उसे अपनी website पर बिल्कुल इसी path पर रखो: `https://username.github.io/.well-known/assetlinks.json`
   (GitHub repo में एक `.well-known` नाम का folder बनाना होगा, उसके अंदर ये file)
4. App को दोबारा install करो — अब bar गायब होकर पूरी तरह fullscreen native app जैसी चलेगी

## पड़ाव 5 — Play Store पर Publish

play.google.com/console पर developer account (~$25 एक बार) बनाओ, AAB file upload करो, screenshots और description भरो, submit करो।

## अभी App में क्या-क्या नया है
- **Email/Password Sign-In** — कोई भी अपना खाता बना सकता है
- **Google Sign-In** — एक टैप में login
- **Firestore Database** — हर user का data (नाम, count, तस्वीरें, भजन) cloud में अलग-अलग सुरक्षित रहता है, नया फ़ोन लेने पर भी login करते ही सब वापस आ जाएगा
- **Sign out** — ऊपर दाईं तरफ़ अपने avatar पर टैप करके

## आगे की संभावनाएं (अगर चाहो तो बताना)
- सबका मिला-जुला leaderboard (कौन सबसे ज़्यादा जाप कर रहा है)
- Friends को जोड़कर साथ में group challenge
- Push notifications (रोज़ाना याद दिलाने के लिए)
