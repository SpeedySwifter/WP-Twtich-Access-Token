# 🛠 WP-Twitch-Access-Token

<div align="center">

![Twitch](https://img.shields.io/badge/Twitch-9146FF?style=for-the-badge&logo=twitch&logoColor=white)
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

[![GitHub Stars](https://img.shields.io/github/stars/SpeedySwifter/WP-Twtich-Access-Token?style=social)](https://github.com/SpeedySwifter/WP-Twtich-Access-Token/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/SpeedySwifter/WP-Twtich-Access-Token?style=social)](https://github.com/SpeedySwifter/WP-Twtich-Access-Token/forks)
[![GitHub Issues](https://img.shields.io/github/issues/SpeedySwifter/WP-Twtich-Access-Token)](https://github.com/SpeedySwifter/WP-Twtich-Access-Token/issues)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

**Ein einfaches, clientseitiges Tool zum Erzeugen von Twitch Access Tokens**

[Installation](#-installation--nutzung) • [Dokumentation](#-dokumentation) • [Code-Beispiele](#-code-beispiele) • [FAQ](#-häufige-fragen-faq)

</div>

---

## 📌 Was ist das?

Dieses Projekt ist ein **leichtgewichtiges Frontend-Tool**, mit dem du schnell und einfach einen **Twitch OAuth Access Token** generieren kannst – perfekt für Entwickler, die mit der Twitch Helix API arbeiten.

### ✨ Features

- ✅ **Keine Installation nötig** – einfach `index.html` im Browser öffnen
- ✅ **Keine Server-Anforderungen** – läuft komplett clientseitig
- ✅ **Kein vollständiges WordPress-Plugin** – nur ein praktisches Hilfstool
- ✅ **Schnelle Token-Generierung** – in Sekunden einsatzbereit
- ✅ **Modernes UI** – responsive Design mit Gradient-Styling
- ✅ **Copy-to-Clipboard** – Token mit einem Klick kopieren
- ✅ **Token-Validation** – prüfe die Gültigkeit deines Tokens

---

## 🎯 Wofür brauche ich einen Access Token?

Die **Twitch Helix API** erfordert bei jeder Anfrage ein gültiges Access Token zur Authentifizierung.

### 📡 Beispiel-Anfrage

```http
GET https://api.twitch.tv/helix/streams?user_login=example
Authorization: Bearer hof5gwx0m8n9m48w4mwuv2xqcv4uu0
Client-Id: uo6dggojyb8d6soh92zknwmi5ej1q2
```

### 🔧 Verwendungszwecke

- Stream-Status abfragen (`/streams`)
- User-Informationen abrufen (`/users`)
- Follower-Listen laden (`/channels/followers`)
- Clips und Videos verwalten
- Chat-Bots authentifizieren
- Webhooks einrichten

---

## 🚀 Installation & Nutzung

### 1️⃣ Repository klonen

```bash
git clone https://github.com/SpeedySwifter/WP-Twtich-Access-Token.git
cd WP-Twtich-Access-Token
```

**Alternative:** [Als ZIP herunterladen](https://github.com/SpeedySwifter/WP-Twtich-Access-Token/archive/refs/heads/main.zip)

### 2️⃣ Twitch App erstellen

<details>
<summary>📸 Schritt-für-Schritt Anleitung (Klicken zum Aufklappen)</summary>

#### Schritt 1: Developer Console öffnen
Gehe zu: [https://dev.twitch.tv/console](https://dev.twitch.tv/console)

#### Schritt 2: Neue Anwendung registrieren
Klicke auf **"Register Your Application"**

#### Schritt 3: Formular ausfüllen
```
Name:                  MeinTwitchTool (oder beliebig)
OAuth Redirect URLs:   http://localhost
Category:              Website Integration
```

#### Schritt 4: Client ID & Secret notieren
Nach dem Speichern werden angezeigt:
- ✅ **Client ID** (öffentlich)
- ✅ **Client Secret** (vertraulich – einmal anzeigen!)

</details>

### 3️⃣ Tool öffnen

```bash
# Im Browser öffnen
open index.html          # macOS
start index.html         # Windows
xdg-open index.html      # Linux
```

Oder: Datei per **Doppelklick** öffnen

### 4️⃣ Token generieren

1. **Client ID** eingeben
2. **Client Secret** eingeben
3. Auf **"Generate Token"** klicken
4. 🎉 **Token kopieren** und verwenden!

---

## 📂 Projektstruktur

```
WP-Twtich-Access-Token/
│
├── 📄 index.html              # Hauptdatei (Tool-Interface)
├── 📁 css/
│   └── 🎨 style.css           # Styling & Responsive Design
├── 📁 js/
│   └── ⚙️ script.js           # Token-Generierung (API-Calls)
├── 📄 README.md               # Diese Datei
└── 📄 LICENSE                 # MIT Lizenz
```

---

## 📖 Dokumentation

### 🔌 API-Endpunkt

Das Tool nutzt den **Client Credentials Flow** von Twitch OAuth:

```javascript
POST https://id.twitch.tv/oauth2/token
Content-Type: application/x-www-form-urlencoded

client_id=<deine_client_id>
&client_secret=<dein_client_secret>
&grant_type=client_credentials
```

### 📤 Response-Beispiel

```json
{
  "access_token": "hof5gwx0m8n9m48w4mwuv2xqcv4uu0",
  "expires_in": 5184000,
  "token_type": "bearer"
}
```

---

## 💻 Code-Beispiele

### JavaScript (Fetch API)

```javascript
async function getTwitchAccessToken(clientId, clientSecret) {
  const response = await fetch('https://id.twitch.tv/oauth2/token', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/x-www-form-urlencoded'
    },
    body: new URLSearchParams({
      client_id: clientId,
      client_secret: clientSecret,
      grant_type: 'client_credentials'
    })
  });

  const data = await response.json();
  return data.access_token;
}

// Verwendung
const token = await getTwitchAccessToken('YOUR_CLIENT_ID', 'YOUR_CLIENT_SECRET');
console.log('Access Token:', token);
```

### PHP (cURL)

```php
<?php
function getTwitchAccessToken($clientId, $clientSecret) {
    $url = 'https://id.twitch.tv/oauth2/token';

    $data = [
        'client_id' => $clientId,
        'client_secret' => $clientSecret,
        'grant_type' => 'client_credentials'
    ];

    $ch = curl_init($url);
    curl_setopt($ch, CURLOPT_POST, true);
    curl_setopt($ch, CURLOPT_POSTFIELDS, http_build_query($data));
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

    $response = curl_exec($ch);
    curl_close($ch);

    $result = json_decode($response, true);
    return $result['access_token'] ?? null;
}

// Verwendung
$token = getTwitchAccessToken('YOUR_CLIENT_ID', 'YOUR_CLIENT_SECRET');
echo "Access Token: " . $token;
?>
```

### Python (Requests)

```python
import requests

def get_twitch_access_token(client_id, client_secret):
    url = 'https://id.twitch.tv/oauth2/token'

    data = {
        'client_id': client_id,
        'client_secret': client_secret,
        'grant_type': 'client_credentials'
    }

    response = requests.post(url, data=data)
    result = response.json()

    return result.get('access_token')

# Verwendung
token = get_twitch_access_token('YOUR_CLIENT_ID', 'YOUR_CLIENT_SECRET')
print(f'Access Token: {token}')
```

### WordPress Integration

```php
<?php
/**
 * Plugin Name: Twitch API Integration
 * Description: Nutzt Twitch Access Token für API-Calls
 */

class TwitchAPI {
    private $client_id = 'YOUR_CLIENT_ID';
    private $client_secret = 'YOUR_CLIENT_SECRET';
    private $access_token = null;

    public function __construct() {
        $this->access_token = $this->getAccessToken();
    }

    private function getAccessToken() {
        // Token aus Transient laden (Cache für 50 Tage)
        $token = get_transient('twitch_access_token');

        if (!$token) {
            $response = wp_remote_post('https://id.twitch.tv/oauth2/token', [
                'body' => [
                    'client_id' => $this->client_id,
                    'client_secret' => $this->client_secret,
                    'grant_type' => 'client_credentials'
                ]
            ]);

            if (!is_wp_error($response)) {
                $data = json_decode(wp_remote_retrieve_body($response), true);
                $token = $data['access_token'];

                // Token für 50 Tage cachen
                set_transient('twitch_access_token', $token, 50 * DAY_IN_SECONDS);
            }
        }

        return $token;
    }

    public function getStreamData($username) {
        $response = wp_remote_get("https://api.twitch.tv/helix/streams?user_login={$username}", [
            'headers' => [
                'Authorization' => 'Bearer ' . $this->access_token,
                'Client-Id' => $this->client_id
            ]
        ]);

        if (!is_wp_error($response)) {
            return json_decode(wp_remote_retrieve_body($response), true);
        }

        return null;
    }
}

// Verwendung
$twitch = new TwitchAPI();
$stream_data = $twitch->getStreamData('example');
print_r($stream_data);
?>
```

---

## 🔒 Sicherheitshinweise

### ⚠️ WICHTIG: Client Secret schützen!

```diff
- ❌ NIEMALS Client Secret in öffentlichen Repositories committen
- ❌ NIEMALS Client Secret im Frontend-Code hardcoden
- ❌ NIEMALS Client Secret in JavaScript-Dateien speichern
+ ✅ Nur für lokale Entwicklung nutzen
+ ✅ In Produktion: Token serverseitig generieren
+ ✅ Umgebungsvariablen verwenden (.env)
```

### 🛡️ Best Practices

```bash
# .gitignore Beispiel
.env
config.php
credentials.json
*.secret
```

```php
// Sichere Konfiguration in WordPress
define('TWITCH_CLIENT_ID', getenv('TWITCH_CLIENT_ID'));
define('TWITCH_CLIENT_SECRET', getenv('TWITCH_CLIENT_SECRET'));
```

---

## ❓ Häufige Fragen (FAQ)

<details>
<summary><b>Wie lange ist der Token gültig?</b></summary>

Der Token ist standardmäßig **ca. 60 Tage (5.184.000 Sekunden)** gültig. Die genaue Dauer wird im `expires_in`-Feld der Response angezeigt.

**Token erneuern:**
```javascript
// Nach Ablauf einfach neuen Token generieren
if (tokenExpired) {
  const newToken = await getTwitchAccessToken(clientId, clientSecret);
}
```
</details>

<details>
<summary><b>Kann ich das in WordPress einbinden?</b></summary>

**Ja!** Siehe [WordPress Integration](#wordpress-integration) oben.

Empfohlene Plugins für Twitch-Integration:
- [Twitch Embed](https://wordpress.org/plugins/twitch-embed/)
- [StreamWeasels Twitch Integration](https://wordpress.org/plugins/streamweasels-twitch-integration/)
</details>

<details>
<summary><b>Funktioniert das mit User Access Tokens?</b></summary>

**Nein**, dieses Tool generiert nur **App Access Tokens** (Client Credentials Flow).

Für **User Access Tokens** benötigst du:
- Authorization Code Flow
- User-Login via OAuth
- Redirect URL Handling

📖 [Twitch User Authentication Docs](https://dev.twitch.tv/docs/authentication/getting-tokens-oauth/#authorization-code-grant-flow)
</details>

<details>
<summary><b>Warum läuft das nicht serverseitig?</b></summary>

Das Tool ist für **schnelle lokale Tests** gedacht.

**Für Production:**
```php
// Serverseitiger Token-Request (sicher)
$token = getTwitchTokenFromServer(); // ✅

// Clientseitiger Token-Request (unsicher)
const token = getTwitchTokenFromBrowser(); // ❌
```
</details>

<details>
<summary><b>Wie validiere ich einen Token?</b></summary>

```javascript
async function validateToken(token) {
  const response = await fetch('https://id.twitch.tv/oauth2/validate', {
    headers: {
      'Authorization': `OAuth ${token}`
    }
  });

  return response.ok;
}
```
</details>

<details>
<summary><b>Rate Limits beachten?</b></summary>

**Ja!** Twitch hat Rate Limits:

| Endpoint | Limit |
|----------|-------|
| Standard | 800 Anfragen / Minute |
| Mit Token | 800 Anfragen / Minute |
| Ohne Token | 30 Anfragen / Minute |

📖 [Rate Limits Documentation](https://dev.twitch.tv/docs/api/guide#rate-limits)
</details>

---

## 🛠️ Technologie-Stack

<div align="center">

| Technologie | Version | Zweck |
|------------|---------|-------|
| ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white) | 5 | Struktur |
| ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white) | 3 | Styling |
| ![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black) | ES6+ | Logik |
| ![Twitch API](https://img.shields.io/badge/Twitch_API-9146FF?style=flat&logo=twitch&logoColor=white) | Helix | OAuth 2.0 |

</div>

---

## 🤝 Beitragen (Contributing)

Contributions sind herzlich willkommen! 🎉

### Mitmachen in 5 Schritten

```bash
# 1. Forke das Repository
# 2. Clone deinen Fork
git clone https://github.com/DEIN_USERNAME/WP-Twtich-Access-Token.git

# 3. Erstelle einen Feature-Branch
git checkout -b feature/AwesomeFeature

# 4. Commit & Push
git add .
git commit -m "Add: Awesome new feature"
git push origin feature/AwesomeFeature

# 5. Öffne einen Pull Request
```

### 📋 Contribution Guidelines

- ✅ Beschreibe deine Changes im PR
- ✅ Halte dich an den bestehenden Code-Stil
- ✅ Teste deine Änderungen gründlich
- ✅ Aktualisiere die README falls nötig

---

## 🐛 Bug Reports

Fehler gefunden? [Erstelle ein Issue](https://github.com/SpeedySwifter/WP-Twtich-Access-Token/issues/new)

**Template:**
```markdown
**Beschreibung:**
[Kurze Beschreibung des Problems]

**Schritte zum Reproduzieren:**
1. Gehe zu...
2. Klicke auf...
3. Siehe Fehler...

**Erwartetes Verhalten:**
[Was sollte passieren?]

**Screenshots:**
[Falls vorhanden]

**Browser:**
- [ ] Chrome
- [ ] Firefox
- [ ] Safari
- [ ] Edge

**Version:** [z.B. 1.0.0]
```

---

## 📚 Weitere Ressourcen

### 🔗 Offizielle Twitch Docs
- [Twitch API Reference](https://dev.twitch.tv/docs/api/)
- [OAuth Client Credentials](https://dev.twitch.tv/docs/authentication/getting-tokens-oauth/#client-credentials-grant-flow)
- [Helix API Endpoints](https://dev.twitch.tv/docs/api/reference)
- [Webhooks & EventSub](https://dev.twitch.tv/docs/eventsub)

### 🎓 Tutorials & Guides
- [Twitch API Quickstart](https://dev.twitch.tv/docs/api/get-started)
- [Authentication Guide](https://dev.twitch.tv/docs/authentication)
- [Best Practices](https://dev.twitch.tv/docs/api/guide)

### 🔧 Tools & Libraries
- [Twitch CLI](https://github.com/twitchdev/twitch-cli)
- [TwitchIO (Python)](https://github.com/TwitchIO/TwitchIO)
- [TMI.js (JavaScript)](https://github.com/tmijs/tmi.js)

### 🌐 Community
- [Twitch Dev Discord](https://link.twitch.tv/devchat)
- [Twitch API Forums](https://discuss.dev.twitch.tv/)
- [r/Twitch](https://reddit.com/r/Twitch)

---

## 📜 Lizenz

Dieses Projekt ist unter der **MIT License** lizenziert – siehe [LICENSE](LICENSE) Datei für Details.

```
MIT License

Copyright (c) 2024 SpeedySwifter

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software...
```

---

## 👤 Autor

<div align="center">

**SpeedySwifter**

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/SpeedySwifter)
[![Twitter](https://img.shields.io/badge/Twitter-1DA1F2?style=for-the-badge&logo=twitter&logoColor=white)](https://twitter.com/SpeedySwifter)
[![Twitch](https://img.shields.io/badge/Twitch-9146FF?style=for-the-badge&logo=twitch&logoColor=white)](https://twitch.tv/SpeedySwifter)

</div>

---

## ⭐ Support

<div align="center">

**Hat dir dieses Projekt geholfen?**

Gib dem Repository einen ⭐ Stern auf GitHub!

[![GitHub Stars](https://img.shields.io/github/stars/SpeedySwifter/WP-Twtich-Access-Token?style=social)](https://github.com/SpeedySwifter/WP-Twtich-Access-Token/stargazers)

### 💖 Sponsor werden

[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-FFDD00?style=for-the-badge&logo=buy-me-a-coffee&logoColor=black)](https://buymeacoffee.com/speedyswifter)
[![PayPal](https://img.shields.io/badge/PayPal-00457C?style=for-the-badge&logo=paypal&logoColor=white)](https://paypal.me/speedyswifter)

</div>

---

## 📊 Statistiken

<div align="center">

![GitHub repo size](https://img.shields.io/github/repo-size/SpeedySwifter/WP-Twtich-Access-Token)
![GitHub commit activity](https://img.shields.io/github/commit-activity/m/SpeedySwifter/WP-Twtich-Access-Token)
![GitHub last commit](https://img.shields.io/github/last-commit/SpeedySwifter/WP-Twtich-Access-Token)

</div>

---

## 🗺️ Roadmap

- [x] Basic Token Generator
- [x] Copy-to-Clipboard Funktion
- [x] Responsive Design
- [ ] Token Validation
- [ ] Token Revocation
- [ ] Multi-Language Support (DE/EN)
- [ ] Dark Mode
- [ ] Token History (LocalStorage)
- [ ] Desktop App (Electron)
- [ ] Browser Extension

---

## 📝 Changelog

### Version 1.0.0 (2024-01-XX)
- 🎉 Initial Release
- ✨ Token Generation Feature
- 🎨 Modern UI Design
- 📱 Responsive Layout
- 📋 Copy-to-Clipboard

---

<div align="center">

**Made with 💜 for the Twitch Developer Community**

---

⭐ **Star dieses Repo wenn es dir geholfen hat!** ⭐

</div>
