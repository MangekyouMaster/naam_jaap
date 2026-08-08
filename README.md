# नाम जाप — Play Store तक पहुँचाने का पूरा रास्ता

ये folder एक पूरी PWA (Progressive Web App) है। Play Store पर डालने के लिए 3 पड़ाव हैं:

## पड़ाव 1 — App को Online Host करो (ज़रूरी है, PWABuilder को एक live link चाहिए)

**सबसे आसान तरीका: GitHub Pages (मुफ़्त, हमेशा के लिए)**

1. github.com पर मुफ़्त account बनाओ (अगर नहीं है)
2. नया repository बनाओ, नाम दो जैसे `naam-jaap`
3. इस folder की सारी files (`index.html`, `manifest.json`, `service-worker.js`, तीनों icon `.png`) उस repo में upload करो ("Add file → Upload files")
4. repo की **Settings → Pages** में जाओ → Branch: `main`, folder: `/ (root)` चुनकर Save करो
5. 1-2 मिनट बाद आपको एक link मिलेगा: `https://<तुम्हारा-username>.github.io/naam-jaap/`
6. वो link खोलकर चेक करो कि app सही चल रही है

## पड़ाव 2 — APK बनाओ (टेस्ट करने के लिए, आज ही)

1. [pwabuilder.com](https://www.pwabuilder.com) खोलो
2. ऊपर वाला link (पड़ाव 1 से) paste करो, "Start" दबाओ
3. ये अपने-आप manifest और icons detect कर लेगा (green checkmarks दिखेंगे)
4. "Package for stores" → **Android** चुनो
5. Download होगा एक `.zip` — उसमें एक **signed APK** (टेस्ट के लिए सीधा install करने वाली) और एक **AAB** file (Play Store के लिए) दोनों मिलेंगी
6. वो APK अपने phone में भेजो (WhatsApp/Drive/USB), "Settings → अज्ञात स्रोतों से install करने की अनुमति दो" ऑन करो, और install कर लो — अब ये बिल्कुल एक असली app जैसा चलेगा, अपने icon के साथ

## पड़ाव 3 — Play Store पर डालना (जब तैयार हो)

1. [play.google.com/console](https://play.google.com/console) पर **Google Play Developer account** बनाओ (एक बार का ₹2000 के लगभग / $25 शुल्क)
2. "Create app" → app का नाम, category (Lifestyle), description भरो
3. पड़ाव 2 से मिली **AAB file** upload करो (APK नहीं, Play Store AAB मांगता है)
4. Screenshots (अपने phone से app के 2-3 screenshots लो), app icon (यहाँ मौजूद `icon-512.png`), privacy policy link (PWABuilder एक basic policy generate करने में भी मदद करता है) जोड़ो
5. Review के लिए submit करो — आमतौर पर कुछ दिनों में approve हो जाता है

## ज़रूरी बातें
- हर बार जब आप app में कुछ नया feature जोड़ोगे, बस GitHub पर files फिर से upload करनी होंगी — PWABuilder से दोबारा package बनाना पड़ेगा अगर बड़ा बदलाव है।
- Data अभी हर user के अपने phone/browser में ही save होता है (कोई common server नहीं) — friends के बीच एक-दूसरे का data शेयर नहीं होगा, हर किसी का अपना अलग count रहेगा।
- अगर आगे चलकर चाहो कि सबका data cloud में sync हो (जैसे leaderboard), तो उसके लिए backend जोड़ना होगा — वो अगला कदम हो सकता है, बता देना।
