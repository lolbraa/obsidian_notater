# TODO
- [ ] Undersøke om folk som kjøper kurs gjennom sailon.no og Vipps får registrert fødselsdato i kurs.sailon.no. Kanskje de blir bedt om å logge inn på nytt?
- [ ] Fikse .env fil og fjerne keys fra GitHub [environment variables - Load a .env file with PHP - Stack Overflow](https://stackoverflow.com/questions/67963371/load-a-env-file-with-php)
- [x] Lage adminpanel-skjelett
- [x] Implementere API-logg
- [ ] Manuell registrering

## Adminstrasjonpanel
### Dokumentasjon
- [Custom Settings Page – Plugin Handbook | Developer.WordPress.org](https://developer.wordpress.org/plugins/settings/custom-settings-page/)
- [5 Ways to Create a WordPress Plugin Settings Page](https://deliciousbrains.com/create-wordpress-plugin-settings-page/)
- [Settings API « WordPress Codex](https://codex.wordpress.org/Settings_API)

- Lage en komplett [sub-menu](https://developer.wordpress.org/plugins/settings/custom-settings-page/) under Settings eller Tools?

### Funskjoner å implementere
- [x] Hente inn API-loggen
	- [x] Scrolling og folding.
- [x] Fjerne "save settings"?
- [ ] Epost for når man må kjøpe nye sertifikater - og link til instruks hvordan
	- [x] Skrive instrukser/informasjon på adminpanelet.
- Enkle tester:
	- [x] Gjøre en enkel API-call mot Sdir for å teste at den er operasjonell.
	- [x] Teste Maskinporten-autentisering.

# Logg og Samtaler med Carl
## 2025.03.31
Ringt Carl for å få verifisert epostaddressen mot Maskinporten-innlogging.
Oppdatert all informasjon på Selvbetjenings-panelet og forlenget levertiden til alle parametre til 3660.
Har tre teorier om hva som var feil:
1. Kontoen var deaktivert på ett eller annet vis, siden de har byttet innloggingssystemer. Dog tok det litt tid før første gikk gjennom.
2. De har endret backend til at man ikke får ha 0 i levetid, og de måtte derfor endres til noe annet.
3. Ett eller annet tull med sommer og vintertid; skiftet var dagen før. Just in case satte jeg de til 3660 = 1 time og ett minutt. Oppdaget at php henter by default UTC-tidssone, så lagt til date_default_timezone_set("Europe/Oslo"); i alle filer.

- ID: ea312148-04bf-4460-81ba-a428efbd0788

![[Kursreg-prosjekt-2025.03.31 16.53.46.png|550]]


## 2025.03.24
Flere problemer
1. Kontaktskjema for hjelp til kursregistrering/manuell melding til oss fungerer ikke! 
   Når jeg sender en test-melding så dukker den verken opp i adminstrasjonspanelet for pluginen eller jeg mottar epost.
Hotfix: Skrev at de må sende epost til post@sailon.no.
Muligens problemer med Sendgrind og gammel API-nøkkel som skal oppdateres og derfor stopper denne pluginen.

2. Autentisering med Maskinporten fungerer ikke med feilmelding "Expired key", og jeg får ikke logget inn på digdir.no. 
Feilmelding i loggen, respons fra Maskinporten.
```
2025-03-24 19:11:01 UserID:783 Error: {
    "headers": {},
    "body": "{\"error\":\"invalid_grant\",\"error_description\":\"Invalid assertion. Client authentication failed. Expired key. (trace_id: 356666143081bbec11d293753e9702ca)\",\"error_uri\":\"https:\/\/maskinporten.no\/errors\/MP-121\"}",
    "response": {
        "code": 400,
        "message": "Bad Request"
    },
    "cookies": [
        {
            "name": "dtCookie",
            "value": "v_4_srv_65_sn_D84AA583E5A49C7F0F9A0C1B3CA24C1D_perc_100000_ol_0_mul_1_app-3A25983732df5fa2ef_0",
            "expires": null,
            "path": "\/",
            "domain": "maskinporten.no",
            "port": null,
            "host_only": false
        },
        {
            "name": "ad909caf6abf5862aa5caccbe674d11d",
            "value": "422fb4022f01854af8c0efedf71603e5",
            "expires": null,
            "path": "\/",
            "domain": "maskinporten.no",
            "port": null,
            "host_only": true
        }
    ],
    "filename": null,
    "http_response": {
        "data": null,
        "headers": null,
        "status": null
    }
}
2025-03-24 19:11:01 UserID:783 Error: Noe galt har skjedd. Kontakt oss og oppgi:. [Sdir-API error: 401 Unauthorized]
API respons body: 
```


Forsøke manuelt:
https://api.sdir.no/aps-course-external/v1/courses/batch"
```
[{
    "personalIdentityNumber": "18020084592",
    "completedAt": "2025-03-24T18:32:25+00:00",
    "organizationNumber": "918391819",
    "courseCode": "HSCLC"
}]
```



Timer
19.40-23.20
Tilpasse nye kontaktskjemaer: Bekreftelse av båtførerbevis og kontakt ved hjelp under kursregistrering mot Sdir. Brukt tid på formatering og testing. Gjort ferdig konfigurasjon av frontend-delen av APIen.

Feilsøking av kurs.sailon.no. Sliter med autentisering mot Maskinporten, error "Expired key". Får ikke logget inn heller. Har de endret innloggingssystem og så går det utover oss? Får 401 på Sdir. Dette gjelder alle sider.
Fjernet vipps-krav på kurs.sailon.no siden det er utelukket.
Fjernet midlertidig kursregistreringen frontenden mot studenten og feilsøkt hvorfor skjema ikke fungerte (kurs.sailon.no).

VIdereutviklet nye funksjoner på staging.sailon.no som skal deployes på sailon.no i nærmeste fremtid: 
Nedtelling/oversikt over når virksomhetssertifikat går ut (2027). 
En knapp som tester autentisering: kjører JWT-generator + forsøker å få access-token fra Maskinporten - enklere feilsøking av hva som er galt. Måtte i den forbindelse omstrukturere backend.php for å hente ut denne funksjonaliteten. 





```
Hei Carl Roar

Jeg vil oppdatere om status på Høyhastighetskurs.


Migrering til ny side

Høyhastighetskurset og APIen er så å si operasjonell på den nye siden, sailon.no. Etter vi fikk på plass epost-tjenesten, har jeg fått portet kontaktskjemaene og funksjonaliteten. Det mangler kun å verifisere at alt er 100%, men det går ikke akkurat nå pga. følgende problem:


Problemer med autentisering mot Maskinporten/DigDir

Maskinporten er Staten/DigDir sin tjeneste for å sikre bruk av APIer mot statlige tjenester. Det er mot denne vi autentiserer med de dyre "Nøklene"/Virksomhetssertifikatene du har kjøpt.

Per nå får vi en feilmelding "Expired key" når serveren vår forsøker å "logge inn"/autentisere.
DigDir har gjort om brukersystemet/-platformen sin, så jeg får ikke logget inn uten din hjelp for å etterforske årsaken til problemene. Jeg trenger hjelp av deg til å verifisere post@sailon.no-brukeren ved å logge inn på adminstrasjonsportalen https://samarbeid.digdir.no/ og trykke på linken på epost. Jeg har passordet til kontoen skrevet ned, så bare ring om du ikke har den tilgjengelig.


To andre notis

Vi hadde et problem (nå er det løst) hvor en kunde ikke fikk registrert seg selv via APIen fordi vi hadde gjort om Vipps-login på kurs.sailon.no. Løsningen var å fjerne sjekken på APIen hvor vi sjekker at personnummeret de oppgir stemmer overens med Vipps-fødselsdato.

Et av kontaktskjemaene på kurs.sailon.no (hjelp eller manuell registrering av høyhastighetskurs) oppfører seg rart og vil ikke behandle innsendinger, men vi mistenker det løser seg når Fredrik fikser ny SendGrind API-nøkkel i morgen. Han skulle ta kontakt med deg for å få 2FA-nøkkel.


Mvh, 

Kristoffer Braa
```


## 2024-04-08
### Adminstrasjonspanelet
- manuell verifisering av d-nummeret som står på båtførerbeviset og hva kursdeltager skrev inn.
	- bilde side om side
	- ocr?
- manuell kursbekreftelse for praktisk del
	- lage nytt Learndash-kurs som et skall og complete gjennom API. Lar den lage sertifikat
- logg over selvregistrerte deltakere gjennom løsningen
	- en knapp for å sende forespørsel til Sdir API om liste over bekreftede deltakere
- felt for å skrive inn variabler brukt mot APIs, og en slider for å gå mellom test og produksjon
- Generell logg over hendelser for debuing (hente inn custom-error log)

### Kryptere bilder???

### Sende kunder mail når 
- teoretisk del er bestått:
1. Kursbekreftelse teori
2. Båtførerbevis opplastet
3. Beskrivelse for hvordan man registrerer bestått teori hos Sdir (videresend denne mailen liksom )
- praktisk del er bestått:
4. Kursbekreftelse teori
5. Båtførerbevis opplastet
6. Kursbekreftelse praktisk del
7. Beskrivelse for hvordan registrere seg til Sdir
	- Det er denne portalen hvor kunder skal søke/laste opp? (Spørre Carl) https://www.sdir.no/fritidsbat/sertifikater/hoyhastighetsbevis/sok-om-hoyhastighetsbevis/

# [Best Practices](https://developer.woocommerce.com/docs/woocommerce-extension-development-best-practices/#0-best-practices)
2. [ ] **The main plugin file should adopt the name of the plugin**. For example: A plugin with the directory name `plugin-name` would have its main file named `plugin-name.php`.
3. [ ] **The text domain should match your plugin directory name**. For example: A plugin with a directory name of `plugin-name` would have the text domain `plugin-name`. Do not use underscores.
4. [ ] **Follow WordPress PHP Guidelines**. WordPress has a [set of guidelines](http://make.wordpress.org/core/handbook/coding-standards/php/) to keep all WordPress code consistent and easy to read. This includes quotes, indentation, brace style, shorthand php tags, yoda conditions, naming conventions, and more. Please review the guidelines.
5. [ ] **Avoid creating custom database tables**. Whenever possible, use WordPress [post types](http://codex.wordpress.org/Post_Types#Custom_Post_Types), [taxonomies](http://codex.wordpress.org/Taxonomies), and [options](http://codex.wordpress.org/Creating_Options_Pages). For more, check out our [primer on data storage](https://developer.woocommerce.com/docs/data-storage-primer/).
6. [ ] **Prevent Data Leaks** by ensuring you aren’t providing direct access to PHP files. [Find out how](https://developer.woocommerce.com/docs/how-to-prevent-data-leaks-in-woocommerce/).
7. [ ] **All plugins need a [standard WordPress README](http://wordpress.org/plugins/about/readme.txt)**. See an example in the [WordPress plugin README file standard](https://wordpress.org/plugins/readme.txt).
8. [ ] **Follow our conventions for your Plugin header comment**. View our [example WordPress plugin header comment](https://developer.woocommerce.com/docs/example-wordpress-plugin-header-comment-for-woocommerce-extensions/) and follow the conventions listed, including: `Author:`, `Author URI:` , `Developer:`, `Developer URI`, `WC requires at least:`and `WC tested up to:`, and `Plugin URI:`.
9. [ ] **Make it extensible**: use WordPress actions and filters to allow for modification/customization, and if your plugin creates a front-end output, we recommend having a templating engine in place so users can create custom template files in their theme’s WooCommerce folder to overwrite the plugin’s template files.For more information, check out Pippin’s post on [Writing Extensible Plugins with Actions and Filters](http://code.tutsplus.com/tutorials/writing-extensible-plugins-with-actions-and-filters--wp-26759).
10. [ ] **Avoid external libraries**. The use of entire external libraries is typically not suggested as this can open up the product to security vulnerabilities. If an external library is absolutely necessary, developers should be thoughtful about the code used and assume ownership as well as of responsibility for it. Try to only include the strictly necessary part of the library, or use a WordPress-friendly version or opt to build your own version. For example, if needing to use a text editor such as TinyMCE, we recommend using the WordPress-friendly version, TinyMCE Advanced.
11. [ ] **Remove unused code**. With version control, there’s no reason to leave commented-out code; it’s annoying to scroll through and read. Remove it and add it back later if needed.
12. [ ] **Use Comments** to describe the functions of your code. If you have a function, what does the function do? There should be comments for most if not all functions in your code. Someone/You may want to modify the plugin, and comments are helpful for that. We recommend using [PHP Doc Blocks](http://en.wikipedia.org/wiki/PHPDoc) similar to [WooCommerce](https://github.com/woocommerce/woocommerce/).
13. [ ] **Avoid God Objects**. [God Objects](http://en.wikipedia.org/wiki/God_object) are objects that know or do too much. The point of object-oriented programming is to take a large problem and break it into smaller parts. When functions do too much, it’s hard to follow their logic, making bugs harder to fix. Instead of having massive functions, break them down into smaller pieces.
14. [ ] **Separate Business Logic & Presentation Logic.** It’s a good practice to separate business logic (i.e., how the plugin works) from [presentation logic](http://en.wikipedia.org/wiki/Presentation_logic) (i.e., how it looks). Two separate pieces of logic are more easily maintained and swapped if necessary. An example is to have two different classes – one for displaying the end results, and one for the admin settings page.
15. [ ] **Use Transients to Store Offsite Information**. If you provide a service via an API, it’s best to store that information so future queries can be done faster and the load on your service is lessened. [WordPress transients](http://codex.wordpress.org/Transients_API) can be used to store data for a certain amount of time.
16. [ ] **Log data that can be useful for debugging purposes**, with two conditions: Allow any logging as an ‘opt in’, and Use the [WC_Logger](https://woocommerce.com/wc-apidocs/class-WC_Logger.html) class. A user can then view logs on their system status page. Learn [how to add a link to logged data](https://developer.woocommerce.com/docs/add-link-to-logged-data/) in your extension.


# Output HTML
Eksempel fra [Woocommerce admin 1](https://github.com/woocommerce/woocommerce/blob/trunk/plugins/woocommerce/includes/admin/class-wc-admin.php#L327) [Wocoomerce admin 2](https://github.com/woocommerce/woocommerce/blob/trunk/plugins/woocommerce/includes/admin/settings/views/html-admin-page-shipping-zones.php)

- [HTML Coding Standards – Coding Standards Handbook \| Developer.WordPress.org](https://developer.wordpress.org/coding-standards/wordpress-coding-standards/html/)
- [PHP Coding Standards – Coding Standards Handbook \| Developer.WordPress.org](https://developer.wordpress.org/coding-standards/wordpress-coding-standards/php/)
- [Best way to output HTML \| WordPress.org](https://wordpress.org/support/topic/best-way-to-output-html/)
- [php - What's a cleaner way to output HTML from a Wordpress plugin? - Stack Overflow](https://stackoverflow.com/questions/30644378/whats-a-cleaner-way-to-output-html-from-a-wordpress-plugin)
- [Escaping Data – Common APIs Handbook \| Developer.WordPress.org](https://developer.wordpress.org/apis/security/escaping/)