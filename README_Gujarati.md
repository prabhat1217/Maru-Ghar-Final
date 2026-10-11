# Maru Ghar — મારું ઘર (Gandhinagar)

આ source bundle માં પસંદ કરેલી premium 3D gold/silver branding, photorealistic property-style homepage, એ જ પસંદ કરેલો app icon, Firebase listing submission અને admin approval page સામેલ છે.

## GitHub repository માં મૂકવા
1. ZIP extract કરો.
2. અંદરના files/folders (`index.html`, `admin.html`, `assets/`, `.github/` વગેરે) repository `prabhat1217/New-maru-Ghar` ના root માં upload કરીને જૂના project files replace કરો.
3. `main` branch પર commit કરો. GitHub Actions માં **Build Maru Ghar Android APK** workflow ચલાવો અથવા push પછી ચાલે તેની રાહ જુઓ.
4. Workflow run માં **Artifacts → MARU-GHAR-ANDROID-APK** માંથી APK ડાઉનલોડ કરો.

## Firebase / admin
- Firebase project: `maru-ghar-gandhinagar-8dbe4`
- Listings collection: `listings`
- Admin page: `/admin.html`
- Admin panel માં Firebase Authentication નું Email/Password account વાપરો. માત્ર UID `yJYiuaUE3KXVLVuWqLyLRH5owQJ3` ને rules માં admin અધિકાર છે.
- `firestore.rules` source file માં સુધારેલી rules છે. આ ZIP મૂકવાથી Firebase Console ની live rules આપમેળે બદલાતી નથી. Live rules અલગથી publish/deploy કરવી જરૂરી છે.
- Firebase Authentication માં Email/Password અને Anonymous providers સક્રિય હોવા જોઈએ.
- Cloudinary unsigned preset `marughar_images` અને cloud name `t5gd6nts` config માં છે. Unsigned preset માટે upload restrictions લગાવેલી હોવી જોઈએ.

## મહત્વની સ્થિતિ
આ source bundle છે, live deployment અથવા successful APK build નો પુરાવો નથી. GitHub Actions run green થયા પછી જ APK build સફળ ગણવો. Firebase Console માં live rules અને test listing/approval ચકાસ્યા પછી જ production-ready ગણવું.


## Admin, sync અને data safety
- હોમપેજના footer માં અને મોબાઇલ હેડર પર `Admin Login / પ્રોપર્ટી મંજૂરી` લિંક છે; તે `admin.html` ખોલે છે. Admin page માંથી પાછા હોમપેજ પર જવા માટે લિંક પણ છે.
- Admin પ્રવેશ Email/Password દ્વારા થાય છે, પરંતુ Admin અધિકાર ફક્ત UID `yJYiuaUE3KXVLVuWqLyLRH5owQJ3` ને જ મળે છે. બીજો વપરાશકર્તા એપ વાપરી શકે, પરંતુ તે listing મંજૂર/ડિલીટ કરી શકતો નથી.
- Listings Firestore ના shared `listings` collection માં અને ફોટા Cloudinary માં રાખવામાં આવે છે; એટલે એ જ Firebase/Cloudinary configuration વાપરતી વેબસાઇટ અને APK cloud data સાથે જોડાય છે. એપ uninstall કરવાથી cloud listing ડિલીટ થતી નથી.
- આ source bundle માં કોડ/Rules/workflow સુધારેલા છે. GitHub પર commit કરવું, GitHub Actions build green કરવો, live Firebase Rules publish/deploy થયાની ખાતરી કરવી અને વાસ્તવિક device પર Admin approval + બીજા device પર listing દેખાય છે તે ચકાસવું હજુ જરૂરી છે. આ તપાસો થયા પહેલાં production-ready હોવાનો દાવો કરવો નહીં.


## આ સુધારામાં વધારાની સુવિધાઓ
- Admin panel માંથી નવી પ્રોપર્ટી ઉમેરવી, સીધી જાહેર કરવી અથવા પેન્ડિંગ રાખવી.
- Admin panel માંથી પેન્ડિંગ/મંજૂર/નામંજૂર લિસ્ટિંગ ડિલીટ કરવી.
- જાહેર પેજમાં એક વખત 24 મંજૂર લિસ્ટિંગ લોડ થાય; “વધુ પ્રોપર્ટી જુઓ” થી આગળની લિસ્ટિંગ લોડ થાય.
- Admin panel એક વખત 100 લિસ્ટિંગ લોડ કરે છે; વધુ જૂની લિસ્ટિંગ માટે આગળનું પેજ લોડ કરી શકાય છે.
- ડિલીટ કરવાથી Firestore લિસ્ટિંગ રેકોર્ડ દૂર થાય છે; Cloudinary પર પહેલેથી અપલોડ થયેલા ફોટા આપમેળે ડિલીટ થતા નથી.
- Firebase/Cloudinaryના મફત પ્લાનમાં મર્યાદાઓ છે; 1,000+ યુઝર્સ માટે ક્ષમતા અને ખર્ચનો વાસ્તવિક ઉપયોગ મુજબ ટેસ્ટ જરૂરી છે. કોઈપણ વેબ/એપ માટે હેંગ ન થવાની 100% ખાતરી આપી શકાતી નથી.

## મફત વેબસાઇટ પ્રકાશન
- `.github/workflows/deploy-web.yml` GitHub Pages પર વેબસાઇટ પ્રકાશિત કરવા માટે છે.
- GitHub repository Settings → Pages માં Source તરીકે **GitHub Actions** પસંદ કરવું જરૂરી હોઈ શકે છે.
- Deploy-Web workflow સફળ થયા પછી GitHub Actionsના deployment output માં વેબસાઇટ લિંક મળશે.


## Firestore Index મહત્વપૂર્ણ

જાહેર લિસ્ટિંગ `status == approved` અને `createdAt desc` query વાપરે છે. તેના માટે `firestore.indexes.json` માં composite index છે. `firestore.rules` અને `firestore.indexes.json` ફક્ત ZIP/GitHubમાં મૂકવાથી Firebase પર લાગુ થતા નથી. Firebase CLIથી યોગ્ય projectમાં બંને deploy કરો (`firebase deploy --only firestore:rules,firestore:indexes`) અથવા Firebase Consoleમાં Rules publish કરીને જરૂરી composite index બનાવો. Live test કર્યા વગર આ પગલું પૂર્ણ માનશો નહીં.
