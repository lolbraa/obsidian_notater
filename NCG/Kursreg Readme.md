Les Dokumentasjon.pdf

Krever composer for php-jwt!!! 

Note:
*Den 26.06.2024 installerte jeg Kursreg-v1.0 på www.sailon.no. Denne skal være riktig konfigurert, men jeg måtte fjerne sjekken av fødselsnummer mot Vipps-fødselsdato da jeg ikke klarer å logge inn på www.sailon.no med Vipps-brukeren.*
# Overordnet informasjon
Første steg til en forespørsel er Maskinporten. Her har vi lastet opp den offentlige nøkkelen og har fått tilgang til Sdirs APS Course-scope. 
Når vi gjør en forespørsel lager vi først en JWT-token av vår private nøkkel, samt noe informasjon. Denne tokenen blir sendt til Maskinporten for validering. Tilbake får vi en access token som er godkjent i Sdir sine systemer.

## Prosessflow:
En backend i WordPress-miljøet som lytter etter API-kall, utfører validering og operasjoner, og sender deretter en API-forespørsel til Sdir.

1. Lytt etter API-kall fra JavaScript-blokken
Backend-funksjonen kursreg_api blir kalt når en API-forespørsel sendes fra frontend (JavaScript-blokken).

2. Parse og valider data
Hent Personnummer fra forespørselen og sjekk om det samsvarer med et gyldig format (regex for personnummer).

3. Sikkerhetssjekker
Sjekke om forespørselen er gyldig og om kunden har lov.

4. Generer JWT-token
Bruk jwt-generator.php til å lage et JWT-token som inneholder nødvendige påstander (claims).

5. Send JWT-token til Maskinporten
Utfør en POST-forespørsel til https://maskinporten.no/token med JWT-tokenet.
Motta et svar som inneholder "Access Token" og "Bearer".

6. Utfør kursregistrering
Send en POST-forespørsel til https://api.sdir.no/aps-course-external/v1/courses/batch med nødvendig payload og access_token.

7. Logg vellykket API-kall og oppdater skjema i WordPress
Logg tidspunkt, brukernavn, de første 6 sifrene av personnummeret (varPersonID), og svaret fra API-et til en loggfil.
Returner et svar til frontend for å oppdatere skjemaet med statusen for forespørselen (suksess eller feil).


# Installasjon
0. Det kan hende du må øke `upload_max_filesize` directive in php.ini.   [How to fix “the uploaded file exceeds the upload\_max\_filesize directive in php.ini.” error - SiteGround KB](https://www.siteground.com/kb/the-uploaded-file-exceeds-the-upload_max_filesize-directive-in-php-ini-error/). I plesk gjøres det under PHP.
	   
1. Installer zip-filen i WordPress som en plugin
	1. Endre eventuelle verdier i PHP-dokumentene.
	2. ``inline.html`` er HTML-koden som plasseres på en side (i en kodeblokk) som brukergrensesnitt.
	3. Det er altså noen tekster/sider som behøves i kurset for en fullstendig brukeropplevelse. Blant annet forms hvor kunder laster opp båtførerprøve og hvor de tar kontakt ved problemer
2. PHP Composer for JWT-generering
	1. Kopier ``composer.json`` til HTTPDOCS-rootfolder.
	2. Gå til Composer i Plesk og trykk SCAN.
	3. Man skal finne filen, og da kan man trykke INSTALLER.

```
Package: firebase/php-jwt
Folder: /kurs.sailon.no/wp-content/plugins/kursreg/vendor

composer.json:
{
    "require": {
        "firebase/php-jwt": "^6.10"
    }
}

```

## Produksjon
Gå fra test til produksjon
1. Endre verdier for sertifikat og endepuntker i jwt-generator.php
2. Endre verdier for Sdir-endepunkter i kursreg-backend.php
3. Legge til Sdir-produksjonsscope på digdir.no https://sjolvbetjening.samarbeid.digdir.no/integrations/ea312148-04bf-4460-81ba-a428efbd0788

# Dokumentasjon om Sjøfartsdirektoratets API
Docs: https://developer.sdir.no/rest-api/qualifications/course/
Dev-docs: https://sdir-t-apim-common.developer.azure-api.net/api-details#api=sdir-t-api-aps-course-external&operation=v1_externalcourse_postcoursecompletions__courseRegistrations__post

# Dokumentasjon om Maskinporten-integrasjon
 - Virksomhetessertifikat/Enterprise Certificate fra Buypass. 
     - Steg 0: Offentlig nøkkel legges inn i Selvbetjeningen-portalen til Maskinporten
     - Steg 1: Hver gang man trenger å autentisere seg overfor Maskinporten, lager man en JWT-token lokalt som signeres med den private nøkkelen. Maskinporten sjekker signaturen mot den offentlig nøkkelen.
	     - Denne pluginen bruker firebase/php-jwt for å lage JWT-tokens.
         - Kan alternativt lage JWT-token med plugin i WordPress (da forblir virksomhetssertifikatet lokalt) og hente med en API, eller putte sertifikatet/nøkkelen som plain-tekst i Zapier. 
     - Steg 2: Tilbake får man access_token med levetid (satt til 300). Vi bruker ikke refresh-token.
- Steg 3: Subscription key fra Sdir + access_token brukes til å autentisere hvert API-kall mot Sjøfartsdirektoratet.
	- Vi har kun tilgang til "Create passed course participants." på https://sdir-t-apim-common.azure-api.net/aps-course-external/v1/courses/batch. Her legges access_token som en header.

https://docs.digdir.no/docs/Maskinporten/maskinporten_guide_apikonsument
https://docs.digdir.no/docs/Maskinporten/maskinporten_protocol_token
https://docs.digdir.no/docs/Maskinporten/maskinporten_protocol_jwtgrant
- client_name: Kursreg mot Sdir
- client_id: ea312148-04bf-4460-81ba-a428efbd0788

## JWT-tokens
[Generere JWT-token ifølge denne guiden](https://developer.sdir.no/get-started/token/). Det er bare en innføring. guiden er lastet ned lokalt som en fil i mappestrukturen her.

### Ved installasjon av nye sertifikat
Hvert sertifikat går ut etter 5 år (?). Et sertifikat består av en privat og en offentlig nøkkel og må kjøpes av Buypass.

Ved utvikling hadde vi to sertifikater, test og produksjon. Ved fornyelse trenger vi kun produksjon.

1. Sertifikatet som blir sendt fra Buypass må dekrypteres. Følg instruksjoner og sørg for å lagre krypteringsnøkkel!
	1. Bruk gjerne [Keystore Explorer](https://keystore-explorer.org/) og lag et keystore som sdir_keys.jks under mappen Virksomhetssertifikat.
	2. Eksporter offentlig og privat nøkkel i PEM-format, ukryptert. Det kan hende det må til prøving og feiling til.
2. Legg til offentlig nøkkel/virksomhetssertifikat i Selvbetjeningen til Digdir ([direktelenke](https://sjolvbetjening.samarbeid.digdir.no) eller [min-side](https://minside-samarbeid.digdir.no/)). Se "Integrasjon-betjening for Maskinporten med Public Key lastet opp sjolvbetjening.samarbeid.digdir.no.png" for hint. 
	1. Ta vare på: KID for opplastet nøkkel og integrasjons-id Maskinporten har gitt. Disse må oppdateres i jwt-generator.php.
3. Legg til nøkkel og informasjon i jwt-generator.php.

  

### Sertifikat i bruk nå, frem til 2027
```
{"keys":[{"kty":"RSA","x5t#S256":"Zk3m9T221aBl1z0EAswIkBrwe-ATPRCpWbwfOcNw9R0","e":"AQAB","use":"sig","kid":"333479588311127117992779","x5c":["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"],"alg":"RS256","n":"4oLlTwpPro1b4uQR0fQCLwAbWAXf0JHBIqp785L-NsceZw_p47wZnG0U_2SDS0cjga_5gZx7n4dX0z7C2ccakycLA4aUCD4yap0_V7VllOaK9yl9wOVKuV4TPRJJ3ySJcO7WHzCRmn7DREm-JfnKDLuU8hvkT5_GqzvcX7He9g-XS9egj-sDWLT66cMFiL2di9eCfuywtnKblXtSlExnv-6Xx67Wylgg4bu3IFbo77z8QNRIXvuCZKTtpfMA0mEQi2CG7zHmK-NvHK4m7sCVHn2xag0DZ63nDwVcSYD0NjJ35mTEcSnojSp0L_Mvbw6jea84RUFK6Yjg_osQIHbAAV4aAPiaIoREu9spxvMxKAa82ZzRmsu_BW9dwUyYJsmYWPjPmmX5FluAMD5CBMoPFnEv3r_vfvFq4NWIpW5NkRf_chIeSQObXjXn3d61SELpigTXJkmDZluynshxe6GC7DR019nk6FXpGyKNQdk7BPw2x8ukCWbwdntd-dnqjKSn","exp":1741427391}],"created":"2024-03-13 10:49:52","last_updated":"2024-03-13 10:49:52"}
```

Virksomhetssertifikat - sertifikatene/offentlige nøkler

Sertifikat 1:
```
-----BEGIN CERTIFICATE-----
MIIGFDCCA/ygAwIBAgIKRpxGUJaZrStZSDANBgkqhkiG9w0BAQsFADBoMQswCQYD
VQQGEwJOTzEYMBYGA1UEYQwPTlRSTk8tOTgzMTYzMzI3MRMwEQYDVQQKDApCdXlw
YXNzIEFTMSowKAYDVQQDDCFCdXlwYXNzIENsYXNzIDMgQ0EgRzIgU1QgQnVzaW5l
c3MwHhcNMjQwMzEyMTMzMDQ2WhcNMjcwMzEyMjI1OTAwWjBRMQswCQYDVQQGEwJO
TzETMBEGA1UECgwKU0FJTCBPTiBBUzETMBEGA1UEAwwKU0FJTCBPTiBBUzEYMBYG
A1UEYQwPTlRSTk8tOTE4MzkxODE5MIIBojANBgkqhkiG9w0BAQEFAAOCAY8AMIIB
igKCAYEAtC8pZhLfW6JV8W3pcd9/Z3+mSALfUdwjt982V87G9x0fAexen4+mAqu/
CnAl2iUfVhnCpZGPxoFq7GGkOY5VeSHZ066fCds+ky8RxX9k4PWpJDvYGqw6K0Zj
PNM28dJzSLJSDlE22SzTbKrnlCJw/HWJrI3nAzbEuurH0RuZr79RgozOKu9PwouX
wQ2Upcd0n3kpOitv03k8L375jKAEVZYcejTELWijxxrzPIsdCtKu8uqQ7R1cnWlk
hIsCj/hsqmcJA6M3jeNgCFu9+ZImTFvMbY3zIzjLCql/o9jRh+HhMdWGpfWh6fEF
upCEuI49DQ2iK/V68q/sIAyndDjY0ppEpXZFRSqTkDxotE85d/5/zWgBxOVN7lw0
HFUeAbUEqwd9I8Cq/b7NiAOg+9jLxIQc+3tj10T5qC9mh123LTqQmM2nvxB75tks
/5GVdN7Vnz8gLC372lLMpdCLTS7KQK3uM3UXdaVju6aM33Cg7Ky8Wc9iGX80FKvd
sRPco8ZbAgMBAAGjggFVMIIBUTAJBgNVHRMEAjAAMB8GA1UdIwQYMBaAFIFFnCmV
Zjg37TtUTo4y5ZYhedVkMB0GA1UdDgQWBBS2WpSO3yQqXrCp3+vDbWoviCxTXDAO
BgNVHQ8BAf8EBAMCBaAwHwYDVR0gBBgwFjAKBghghEIBGgEDAjAIBgYEAI96AQEw
OwYDVR0fBDQwMjAwoC6gLIYqaHR0cDovL2NybC5idXlwYXNzY2EuY29tL0JQQ2wz
Q2FHMlNUQlMuY3JsMG8GCCsGAQUFBwEBBGMwYTAnBggrBgEFBQcwAYYbaHR0cDov
L29jc3Bicy5idXlwYXNzY2EuY29tMDYGCCsGAQUFBzAChipodHRwOi8vY3J0LmJ1
eXBhc3NjYS5jb20vQlBDbDNDYUcyU1RCUy5jZXIwJQYIKwYBBQUHAQMEGTAXMBUG
CCsGAQUFBwsCMAkGBwQAi+xJAQIwDQYJKoZIhvcNAQELBQADggIBAJiOlfnUaTTH
47jenA4qHXIGraeGgFqmMfsN0w8qIT+TACBnOLyRI/+inQabjfMDVxLsYY/FYJMt
p5Lz1o5H9b1fQbwVBoAKtdE9uUV2bMNzU3P+eB/UyxM9+R3XGGlMZvCWB9zZ9hEh
HlhroK9kpwbIFt8AjlPwBtBQj7XlpYo4ozhJnyCKN9JMUNzRiNrn/R99TNmURVRQ
j+fMC2NkaSNZDZQyJguJ1gBlFhdxVGl+d/2oNdKoU4tX9+9ba+6vJpXw/02XpgiJ
M6hxcnxbFcIZFd2we5nS6v1cHxalRm9zfKwdqk5p3wBz8IMGe/guacAYATp57RAr
rA35oNmmNHP3VUuogj6m1c+dPVD6ZYPDLNpCT7YAgdu5JFxfCLvnw76pMXOr/JqB
2R+Bm+x+bQponOtIbKrwVKBq/4Vqz9t1T85LWa00nDTMCjBkFP2SsSmAJdpRp5H9
TSz3yn/XO21ncKSF/hgck33oWLDw9uqXfbT+Yh3AHqTwpMH9NkPuta/un9+PoxL1
HAZAfET5kkmpj1M3DdOQHU5k6AYFZJ1ej9OznFxsGaUhil1ACJGC/MCuGBUuEAbA
M6rMaPPJtaB1iSOwURnGWPVkvO0qBDKpJTTv76HVmVxaMrFq5vmcMnPVbkAz4+dN
W4xJsyicXrj/l44QnJJcDpZ/mRu2MBwG
-----END CERTIFICATE-----
```


Sertifikat 2:
```
-----BEGIN CERTIFICATE-----
MIIGFDCCA/ygAwIBAgIKRp329v5jL4MTSzANBgkqhkiG9w0BAQsFADBoMQswCQYD
VQQGEwJOTzEYMBYGA1UEYQwPTlRSTk8tOTgzMTYzMzI3MRMwEQYDVQQKDApCdXlw
YXNzIEFTMSowKAYDVQQDDCFCdXlwYXNzIENsYXNzIDMgQ0EgRzIgU1QgQnVzaW5l
c3MwHhcNMjQwMzEyMTMzMDQ2WhcNMjcwMzEyMjI1OTAwWjBRMQswCQYDVQQGEwJO
TzETMBEGA1UECgwKU0FJTCBPTiBBUzETMBEGA1UEAwwKU0FJTCBPTiBBUzEYMBYG
A1UEYQwPTlRSTk8tOTE4MzkxODE5MIIBojANBgkqhkiG9w0BAQEFAAOCAY8AMIIB
igKCAYEA4oLlTwpPro1b4uQR0fQCLwAbWAXf0JHBIqp785L+NsceZw/p47wZnG0U
/2SDS0cjga/5gZx7n4dX0z7C2ccakycLA4aUCD4yap0/V7VllOaK9yl9wOVKuV4T
PRJJ3ySJcO7WHzCRmn7DREm+JfnKDLuU8hvkT5/GqzvcX7He9g+XS9egj+sDWLT6
6cMFiL2di9eCfuywtnKblXtSlExnv+6Xx67Wylgg4bu3IFbo77z8QNRIXvuCZKTt
pfMA0mEQi2CG7zHmK+NvHK4m7sCVHn2xag0DZ63nDwVcSYD0NjJ35mTEcSnojSp0
L/Mvbw6jea84RUFK6Yjg/osQIHbAAV4aAPiaIoREu9spxvMxKAa82ZzRmsu/BW9d
wUyYJsmYWPjPmmX5FluAMD5CBMoPFnEv3r/vfvFq4NWIpW5NkRf/chIeSQObXjXn
3d61SELpigTXJkmDZluynshxe6GC7DR019nk6FXpGyKNQdk7BPw2x8ukCWbwdntd
+dnqjKSnAgMBAAGjggFVMIIBUTAJBgNVHRMEAjAAMB8GA1UdIwQYMBaAFIFFnCmV
Zjg37TtUTo4y5ZYhedVkMB0GA1UdDgQWBBR4qbV493PoB3pybOq+fL/HQfzlGjAO
BgNVHQ8BAf8EBAMCBkAwHwYDVR0gBBgwFjAKBghghEIBGgEDAjAIBgYEAI96AQEw
OwYDVR0fBDQwMjAwoC6gLIYqaHR0cDovL2NybC5idXlwYXNzY2EuY29tL0JQQ2wz
Q2FHMlNUQlMuY3JsMG8GCCsGAQUFBwEBBGMwYTAnBggrBgEFBQcwAYYbaHR0cDov
L29jc3Bicy5idXlwYXNzY2EuY29tMDYGCCsGAQUFBzAChipodHRwOi8vY3J0LmJ1
eXBhc3NjYS5jb20vQlBDbDNDYUcyU1RCUy5jZXIwJQYIKwYBBQUHAQMEGTAXMBUG
CCsGAQUFBwsCMAkGBwQAi+xJAQIwDQYJKoZIhvcNAQELBQADggIBALld72oMkliv
B37BWte+0Q91pGKqC6tAIFltUHv3ce11EI08SEoKYDSaWmaVjup8B+m50BD6Nvcy
jOtKy6Pb1etOBogwBymtTn4PsOB9eke8MH3mqfsiom9tJM+yUW+xazbRxYbqysGd
4y5u6lpHYI+ZRWjvJmmRzruOqA11JlC37cAcR8pg5LQ8MnRQAmBr1SRwGJCZe8Bf
JLIro7I1uCWnhbC9cPD0UegYtA9aZ/kNLu7xeFhkpvvDPB2hu2xXRTAuGAHN91Kd
LN0v2YRkUfcoRYu4Bi95In8wKlSEP3QEJYLebDMLlbU+NHdh0OqnQ2qjJEDEUtGB
YDsPSP02JLAmvYix5kCUBJ8/cJ/fuuIhc66L+xRG2aNVDxOHnjKdmSOgK36qHBQQ
ZShP8OHvaeEPItg+NxXbqq2EIfxKS4XBuNUhFqhs1vF3JrhXNaVV9biPpPo3J3m8
fgbxQOIld3NBoyWb6KpJYya9dM3SGjTc60qaNL1ziVNkQzK/PCHAXLT8zSpjzMN/
sV1A9DkuwGtp6hAAuaYP1JlYP8WbEI5yWLH+Qv4GpctiZUh1ogCJ2i1tFr9V+m9H
fp8UhXWu7keW7/l3lJslJqpsunV7NmTwsofb0Wk6Gtn5nHIZmTGbfafh0GG59v7Y
7b0uGJT949GKZAORhzfTdtY18toWS/9t
-----END CERTIFICATE-----
```


Mellomliggende CA-sertifikat (Subordinate CA Certificate) for Buypass Class 3 CA G2 ST Business:

```
-----BEGIN CERTIFICATE-----
MIIGezCCBGOgAwIBAgILANcF2TfqKJjzbYgwDQYJKoZIhvcNAQENBQAwZDELMAkG
A1UEBhMCTk8xGDAWBgNVBGEMD05UUk5PLTk4MzE2MzMyNzETMBEGA1UECgwKQnV5
cGFzcyBBUzEmMCQGA1UEAwwdQnV5cGFzcyBDbGFzcyAzIFJvb3QgQ0EgRzIgU1Qw
HhcNMjAxMTEwMTIxMTEzWhcNNDAxMTEwMTIxMTEzWjBoMQswCQYDVQQGEwJOTzEY
MBYGA1UEYQwPTlRSTk8tOTgzMTYzMzI3MRMwEQYDVQQKDApCdXlwYXNzIEFTMSow
KAYDVQQDDCFCdXlwYXNzIENsYXNzIDMgQ0EgRzIgU1QgQnVzaW5lc3MwggIiMA0G
CSqGSIb3DQEBAQUAA4ICDwAwggIKAoICAQDqw8/QQ+dL0Niv6BfiM8VRtO7EtgZq
K3Qkm5fJBq1OxSSMTG9VwC4gLOvMrfL42IuLVw8ktwGGKdgWoHNPDVCN0lnILsNC
sB2um1ItX5WkTnv6rpi1dcFFigUAQpRe0WadeW2QXsAV0PYdtkEuiowhIVIR25PT
v+9t2pEc5iJ27Y1jLsua6UxIb+EINymtTqgJkc3prggRi6DpeFfgCGewEvccJeQr
EuP+yt2ldHOda2+EWOLGUIcTNQWepTX4dboard7xIoPwPlknIPASp0M8tL/XLhrI
gxow2cz8yqgZnxFfu6kpwWqg/9UQQTaJE0bT4kdp0325qt38yyzxflVXpWgB56K3
+1WP1oi8to1c32AYr48/T6G8jelu0LFvEq1eaijpeklrSiAlms7mERudnrokZCKR
j+2SQ5f0b5y/D45N2OghAPxz4v8IfHI/jns7UXnF5pBbwZNRYgCTgAlEO9vk0Y8l
dQsXfOUF+IpYPCMfIZv17pCE9sjMT74J8nfbFC/viaxI5b+CpBgp7XIQDCyVNDUJ
MLvSoH0V7QpXJuU2jsuqc2vsPjORdTZKO++cPC5yw4zWbz8rycW3ii4D2WDhMR9M
tj1W43mY9lbguQ6uG2Z5xEqwLL+Gs9o6gqkAaYwC3yn8M+gZgV46WW8QJ2wlPcyk
cCDmFBhWb8BSVQIDAQABo4IBKDCCASQwDwYDVR0TAQH/BAUwAwEB/zAfBgNVHSME
GDAWgBQXU4UmZpfHJhINn97MtEQy6pTU0TAdBgNVHQ4EFgQUgUWcKZVmODftO1RO
jjLlliF51WQwDgYDVR0PAQH/BAQDAgEGMBEGA1UdIAQKMAgwBgYEVR0gADA9BgNV
HR8ENjA0MDKgMKAuhixodHRwOi8vY3JsLmJ1eXBhc3NjYS5jb20vQlBDbDNSb290
Q2FHMlNULmNybDBIBggrBgEFBQcBAQQ8MDowOAYIKwYBBQUHMAKGLGh0dHA6Ly9j
cnQuYnV5cGFzc2NhLmNvbS9CUENsM1Jvb3RDYUcyU1QuY2VyMCUGCCsGAQUFBwED
BBkwFzAVBggrBgEFBQcLAjAJBgcEAIvsSQECMA0GCSqGSIb3DQEBDQUAA4ICAQB5
jLdhzRbmm6hRX9yDwlHCM7Hd9gslAkhfvHvnElRxM9e9tt1c6xFO88qqYfTRmEDh
jEC0o/3OrhcMnuT7Jm/jncqGe8dfiHKj5jzXi/zqGdPhnOmm39bzPhI2uvY4AWKr
XN1badgUs7XePcmAtvJDhA0G1CjKyUN+2sO63wh5CLJrRi9TWfkiTD/bQIUMcDQl
sJDRWIkekidVm5qq0/zlQM1jz2QVGJcM8e8xjlfb/reUF9VSdzFpuOJh00fc+h7X
wzOtAhaiiUnu2DK1O9B0GE7ZP9AuH67NODBKCVqkGIZ87U/jnZYujSJ6ivMJOvwf
eiXeQgUrpHyKWV7jYAo+4SMHBTXXR1WcN8Eu8wAuahSQ5XCwdYxt/TnvRqY8bpQ0
yQPScksc7y/IrZv2Wvk45XCobaESx2wmrSf4jXxEWVbA25+6q57H3sKDxfgDxU0r
W5ZNLUN1k0FsVBvncwDuXK0B3zdvqEMvRFgdQfLF+djdACGshzD8r9fMw7qvY5EP
cU/mDVq3tgfRftdsiw2ON2ud4kjspcSkhk7PRq+V+JZ1/cHysdzop+S1oP0a5ctQ
bH0v5nS8lrdnoK9JAY0ISOsZ6eFqfNiEJnhEzBzwd2fi/kK9gMvJxcjbBFvATKUp
EY2Xf4cOziOshH6UwF5z9UrIFAfYmHI30mJqp0VlLA==
-----END CERTIFICATE-----
```


