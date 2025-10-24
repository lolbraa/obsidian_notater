[ePayment API \| Vipps MobilePay Developer Docs](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/) er den aktuelle?



# Oversikt
## Roadmap
- [x] 1.0 - Fundamentalt fungerende plugin, men mangler quality of life og sikringer ift. betalinger.
- [x] 1.1 - Admistrasjonspanel: eget Vipps panel med payment status hentet fra API
- [x] 1.2 - Polling (i tillegg til Webhooks) av get payment status / capture payment. 
- [ ] 1.x - Støtte Paymenter v1.3. CanUseGateway og Credits.
- [ ] 1.x - Støtte andre valutaer. ePayment og Recurring støtter NOK, DKK og EUR ? [ePayment API \| Vipps MobilePay Developer Docs](https://developer.vippsmobilepay.com/api/epayment/#tag/CreatePayments/operation/createPayment) [Recurring Payments Merchant API \| Vipps MobilePay Developer Docs](https://developer.vippsmobilepay.com/api/recurring/#tag/Agreement-v3-endpoints/operation/DraftAgreementV3)
- [ ] 2.x Støtte MobilePay? Vipps' kortbetaling "Freestanding card"? [How ePayment works with freestanding cards \| Vipps MobilePay Developer Docs](https://developer.vippsmobilepay.com/docs/APIs/epayment-api/how-it-works/freestanding-cards/)
- [ ] 2.x - Recurring og bruke Laravels HTTP-klient.
	- [ ] cancel og refund - bruker ikke tid på nå, siden man manuelt kan gjøre det i portalen
- [ ] Automatisk regnskapsføring; transaksjonsdata sendes til Conta, enten rett fra Paymenter eller via Vipps
- [ ] Vipps Login, samt SSO for både Paymenter OG Pterodactyl
- [ ] 

### Før oppdatering:
I testmiljø:
1. Ingen feilmeldinger ved boot
2. Kan gjennomføre kjøp
3. canUseGateway fungerer som det skal
4. Sjekke logs
Produksjon:
5. git pull, sjekke at filene faktisk er endret
6. Sørge for composer er riktig, composer install vipps liksom
7. gjennomføre et kjøp
8. sjekke logs

## TODO
- [x] Pay
	- [x] Sjekke om valuta er NOK med canUseGateway
		- [x] Cart: Implementert
		- [x] Invoice: Implementert
		- [ ] Credits: Får ikke hentet items, så hvordan gjøre dette!? Implementert midlertidig sjekk av brukerens default valuta
		- [ ] Kan vi bruke andre valutaer enn NOK? SEK?
	- [x] referanse nummer, metadata, osv.
		- [x] Bruke transaction ID som referansenummer??
		- [x] Mobilnummer: Teste grundig!
	- [x] return url
		- [x] Return URL for mobil !?! [Landing page \| Vipps MobilePay Developer Docs](https://developer.vippsmobilepay.com/docs/knowledge-base/landing-page/) - Virker som det fungerer utmerket by default
	- [x] receipt etter kjøp/for å fullføre kjøp
		- [x] Fullføre/Teste TAX. Hvordan hente inn MVA informasjon!?
		- [ ] Coupons?
		- [ ] Credits?
- [x] Webhooks
	- [x] [Webhooks API guide \| Vipps MobilePay Developer Docs](https://developer.vippsmobilepay.com/docs/APIs/webhooks-api/api-guide/)
	- [x] checkPayment=true
- [x] Polling [Polling guidelines \| Vipps MobilePay Developer Docs](https://developer.vippsmobilepay.com/docs/knowledge-base/polling-guidelines/)
	- [ ] Scheduled tasks er vanskelig å få til. Paymenter implementerer selv kun en daglig cronjob (cronjob.php) som sjekker noen ting ift. fakturaer og slikt, men Vipps foreslår allerede etter 5 minutter.
	- [x] Dispatche jobb/queue
- [x] Capture
	- [x] Capture direkte etter authenticated
	- [x] Dispatche jobb
	- [ ] Schedule en manuell sjekk i console.php. Lese lagrede verdier, ala. punkt lenger nede?
	- [ ] Capture etter at serveren er opprettet
		- [ ] Hooke inn på createjob som kjøres når den skal lage en server? 
			- https://github.com/Paymenter/Paymenter/tree/master/app/Jobs/Server 
			- [Paymenter/app/Jobs/Server/CreateJob.php at master · Paymenter/Paymenter · GitHub](https://github.com/Paymenter/Paymenter/blob/master/app/Jobs/Server/CreateJob.php#L30)
			- Ser bort fra dette da alle forsøkene mine på å lytte til jobber ikke returnerer denne jobben...
		- [ ] Kan også hooke inn på cronjob, daglig?
			- Finner ikke en måte å hooke seg inn uten å endre kildekode
	- [ ] Partial capture - vits i å støtte?
- [ ] Cancel - Hvor hooker man seg inn i Paymenter?
- [ ] Refund - Paymenter støtter ikke?
- [x] Vipps branding
	- [x] egen theme [Theme \| Paymenter](https://paymenter.org/development/theme/) ofr å importere det "overalt"?
	- [x] Valg mellom betalingsløsninger med bilder og radio-knapper
	- [ ] logo footer - bruke Vipps sitt library?

- [ ] Lagre informasjon om Vipps transaksjoner og status, først og fremst transaksjoner som er authenticated, men ikke captured
	- [ ] Kan se på en annen plugin, Announcements, for tips om implementasjon [Paymenter/extensions/Others/Announcements/database/migrations/](https://github.com/Paymenter/Paymenter/blob/master/extensions/Others/Announcements/database/migrations/2024_10_19_095356_create_ext_announcements_table.php)


- [x] Oversikt over Vipps-transaksjoner og status
	- [x] Mot bruker: Implementere via theme
	- [x] Mot adminstrator
		- [ ] ~~Lage en egen side [Pages - Panels - Filament](https://filamentphp.com/docs/3.x/panels/pages)~~
		- [x] Hooke inn med renderhooks! [Render hooks - Core Concepts - Filament](https://filamentphp.com/docs/3.x/support/render-hooks)
			- [ ] ~~Renderhooks støtter ikke utvidelse av resources (som er standard måte å lage en table), for det er ment for full page?~~
			- [ ] ~~Kan lage widgets, men det er ikke vits i i dette tilfellet? [Table widgets - Widgets - Filament](https://filamentphp.com/docs/3.x/widgets/tables)~~
			- [ ] ~~Kan lage en livewire-komponent og putte en filament-table i det - virker som det beste [Adding a table to a Livewire component - Tables - Filament](https://filamentphp.com/docs/3.x/tables/adding-a-table-to-a-livewire-component)~~
			- [ ] ~~Filament Tables er kun for databaseoperasjoner? Endte med å bruke samme greie som på brukersiden.~~
			- [x] Filament View og render hook
				- [x] Funksjoner for å hente informasjon om transaksjoner fra Vipps
					- [x] Get payment events [ePayment API \| Vipps MobilePay Developer Docs](https://developer.vippsmobilepay.com/api/epayment/#tag/QueryPayments/operation/getPayment)
					- [x] Get payment (detaljer for en transaksjon; er den fullført?)
					- [x] Hva hvis det er obvious at det ikke er en Vipps-transaksjon?
> [!NOTE]- Filament-hook
> ```
> \Filament\Support\Facades\FilamentView::registerRenderHook(
> 	PanelsRenderHook::PAGE_END,
> 	fn() => '<div>Injected at the end of the page!</div>'
> );
> 
> examples:
> hook: fn(array $scopes): string => json_encode($scopes),
>         view('gateways.vipps::debug-page')
> ```

- [ ] Recurring [Quick start for the Recurring API \| Vipps MobilePay Developer Docs](https://developer.vippsmobilepay.com/docs/APIs/recurring-api/recurring-api-quick-start/)
	- [ ] Lagre informasjon om agreements i databasen? Eller polle Vipps for 
	- [ ] Logikk for abonnement (kreve betalinger og oppdatere) kan kjøres daglig?
		- [ ] Hooke seg på Laravels schedules? Hooke seg på Paymenters daglige schedule? Ett eller annet med jobs?
		- [ ] Jeg tror det er best å lage en egen vipps-cron.php som kjøres av Laravels schedule med gitt intervall.
- [ ] Gå bort fra SDK; bruke Laravels HTTP-klient.
	- [ ] så api-requests dukker opp i HTTP-logs [Proservere Dev](https://paymenterdev.brill-goblin.ts.net/admin/http-logs)
	- [ ] "Alltid ha med HTTP-headers" [HTTP headers \| Vipps MobilePay Developer Docs](https://developer.vippsmobilepay.com/docs/knowledge-base/http-headers/)

- [ ] Vipps login
	- [ ] SSO sammen med Ptero?


Forslag: Side-plugins
- så man kan lage det som er proservere.com 
- Egen side lagt til i navigasjonsbaren - Discord (dette er for brukere)

## API-nøkler – test
Paymenter 
MSN
373370

client_id
bace39a9-ce96-4b02-8f58-1a4c6614b224

client_secret
1Vj8Q~yqVu~5uuin9qRqIya7foCYEvRSE3YdVcne

Ocp-Apim-Subscription-Key (primær)
41f3ceb2f43d4fab85ca9810d43339a7

Ocp-Apim-Subscription-Key (sekundær)
6f4858879a0d43d286684f669444ff16

Testbruker (05108307252)
40947803
+47 40 94 78 03

## API-nøkler - produksjon
MSN
835992

client_id
69f0338e-cd9e-45aa-b4a3-ef904b854892

client_secret
ID28Q~h5Qc0gB_6~LcNHhRchPVCkjnvFkQQbdbe_

Ocp-Apim-Subscription-Key (primær)
a50a92f44f444741ad0ec6226e5c663b

Ocp-Apim-Subscription-Key (sekundær)
f145cd6e71244b74a0ae7c684cc8ffc4

Testbruker
40947803
+47 40 94 78 03

# Tips Laravel
log
```sh
paymenterdev@paymenterdev:~$ php artisan app:upgrade
```
vardump
```php
dd($invoice);
dump()
```

```php
return view('gateways.vipps::debug', ['result' => $result]);
----
<div class="container">
<h2>Vipps Debug Output</h2>
<pre style="background:#222;color:#eee;padding:1em;border-radius:6px;overflow:auto;">
{{ var_export($result, true) }}
</pre>
</div>
```

Hvis jeg skal implementere APIen selv med HTTP, ikke PHP-SDK, så burde jeg bruke dette for å catche errors ???
```php
try {
}
catch (\Exception $e) {
	/* var_dump($e->getMessage());
	var_dump($e->getTraceAsString()); */
	throw new \Exception('Vipps API error: ' . $e->getMessage());
}
```
## Objekter

> [!NOTE]- Invoice
> 
> ```json
> App\Models\Invoice {#4331 ▼ // extensions/Gateways/Vipps/Vipps.php:201
>   #connection: "mariadb"
>   #table: "invoices"
>   #primaryKey: "id"
>   #keyType: "int"
>   +incrementing: true
>   #with: []
>   #withCount: []
>   +preventsLazyLoading: false
>   #perPage: 15
>   +exists: true
>   +wasRecentlyCreated: false
>   #escapeWhenCastingToString: false
>   #attributes: array:8 [▼
>     "id" => 3
>     "number" => "3"
>     "status" => "pending"
>     "due_at" => "2025-06-03"
>     "currency_code" => "NOK"
>     "user_id" => 1
>     "created_at" => "2025-05-27 22:36:40"
>     "updated_at" => "2025-05-27 22:36:40"
>   ]
>   #original: array:8 [▼
>     "id" => 3
>     "number" => "3"
>     "status" => "pending"
>     "due_at" => "2025-06-03"
>     "currency_code" => "NOK"
>     "user_id" => 1
>     "created_at" => "2025-05-27 22:36:40"
>     "updated_at" => "2025-05-27 22:36:40"
>   ]
>   #changes: []
>   #casts: array:1 [▼
>     "due_at" => "date"
>   ]
>   #classCastCache: []
>   #attributeCastCache: []
>   #dateFormat: null
>   #appends: []
>   #dispatchesEvents: []
>   #observables: []
>   #relations: array:2 [▼
>     "items" => Illuminate\Database\Eloquent\Collection {#2117 ▶}
>     "transactions" => Illuminate\Database\Eloquent\Collection {#4055 ▼
>       #items: []
>       #escapeWhenCastingToString: false
>     }
>   ]
>   #touches: []
>   #relationAutoloadCallback: null
>   +timestamps: true
>   +usesUniqueIds: false
>   #hidden: []
>   #visible: []
>   #fillable: array:5 [▼
>     0 => "number"
>     1 => "user_id"
>     2 => "currency_code"
>     3 => "due_at"
>     4 => "status"
>   ]
>   #guarded: array:1 [▼
>     0 => "*"
>   ]
>   +send_create_email: true
> }
> ```

> [!NOTE]- Items (cart)
> ```json
> Illuminate\Support\Collection {#3908 ▼ // extensions/Gateways/Vipps/Vipps.php:151
>   #items: array:1 [▼
>     0 => {#2348 ▼
>       +"product": App\Models\Product {#3784 ▶}
>       +"plan": App\Models\Plan {#2454 ▶}
>       +"configOptions": Illuminate\Database\Eloquent\Collection {#3644 ▼
>         #items: []
>         #escapeWhenCastingToString: false
>       }
>       +"checkoutConfig": {#3668}
>       +"price": App\Classes\Price {#2684 ▼
>         +price: 12
>         +currency: {#3447 ▼
>           +"code": "USD"
>           +"prefix": "$"
>           +"suffix": ""
>           +"format": "1.000,00"
>         }
>         +setup_fee: 0
>         +has_setup_fee: false
>         +is_free: null
>         +dontShowUnavailablePrice: false
>         +formatted: {#1973 ▶}
>         +tax: 0
>         +setup_fee_tax: 0
>         +discount: 0
>         +original_price: 12
>         +original_setup_fee: 0
>       }
>       +"quantity": 1
>     }
>   ]
>   #escapeWhenCastingToString: false
> }
> 
> "cart" // extensions/Gateways/Vipps/Vipps.php:151
> 
> 
> ```




# PHP-SDK
```sh
composer require zaporylie/vipps:^3.x-dev
```
mode: test
client_id:
client_secret:
subscription_key:
merchant_serial_number:

## HTTP client
Laravel's built-in HTTP client (`Illuminate\Support\Facades\Http`) is not compatible with the Vipps SDK because Vipps requires a PSR-18 HTTP client (implements `Psr\Http\Client\ClientInterface`), while Laravel's HTTP client does not.

**Why?**
- Laravel's HTTP client is a wrapper around Guzzle, but it is not itself a PSR-18 client.
- The Vipps SDK expects a PSR-18 compatible client, such as `GuzzleHttp\Client`.

## Snippets

> [!NOTE]- Svar fra en payment forespørsel
>
> ```
> \zaporylie\Vipps\Model\EPayment\v1\CreatePaymentResponse::__set_state(array(
>    'redirectUrl' => 'https://apitest.vipps.no/dwo-api-application/v1/deeplink/vippsgateway?v=2&token=eyJraWQiOiJqd3RrZXkiLCJhbGciOiJSUzI1NiJ9.eyJhcHAiOiJlUGF5bWVudCIsInN1YiI6ImYwMTQyYj.....',
>    'reference' => 'test-12121212-5',
> ))
> ```

> [!NOTE]- Dump fra en payment forespørsel
> * Trying 51.105.193.254:443... 
> - Connected to apitest.vipps.no (51.105.193.254) port 443 (#0) 
> - ALPN, offering http/1.1 
> - CAfile: /etc/ssl/certs/ca-certificates.crt 
> - CApath: /etc/ssl/certs 
> - SSL connection using TLSv1.3 / TLS_AES_256_GCM_SHA384 
> - ALPN, server accepted to use http/1.1 
> - Server certificate: 
> - subject: C=NO; L=Oslo; O=Vipps Mobilepay AS; CN=apitest.vipps.no 
> - start date: Jan 8 00:00:00 2025 GMT 
> - expire date: Jan 20 23:59:59 2026 GMT 
> - subjectAltName: host "apitest.vipps.no" matched cert's "apitest.vipps.no" 
> - issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1 
> - SSL certificate verify ok. > POST /accesstoken/get HTTP/1.1 Host: apitest.vipps.no Content-Length: 0 User-Agent: GuzzleHttp/7 Ocp-Apim-Subscription-Key: 41f3ceb2f43d4fab85ca9810d43339a7 Merchant-Serial-Number: 373370 Vipps-System-Name: Paymenter Vipps-System-Version: 0.1 Vipps-System-Plugin-Name: zaporylie/vipps (PHP) Vipps-System-Plugin-Version: 3.x-dev client_id: bace39a9-ce96-4b02-8f58-1a4c6614b224 client_secret: 1Vj8Q~yqVu~5uuin9qRqIya7foCYEvRSE3YdVcne 
> - old SSL session ID is stale, removing 
> - Mark bundle as not supporting multiuse < HTTP/1.1 200 OK < Date: Wed, 28 May 2025 21:40:04 GMT < Content-Type: application/json < Content-Length: 1543 < Connection: keep-alive < server: Kestrel < strict-transport-security: max-age=63072000; preload < x-request-id: 7404198e-bd03-114f-4092-fceeb0e4e951 < 
> - Connection #0 to host apitest.vipps.no left intact 
> - Found bundle for host apitest.vipps.no: 0x5639fd0ade10 [serially] 
> - Re-using existing connection! (#0) with host apitest.vipps.no 
> - Connected to apitest.vipps.no (51.105.193.254) port 443 (#0) > POST /epayment/v1/payments HTTP/1.1 Host: apitest.vipps.no User-Agent: GuzzleHttp/7 
> - Ocp-Apim-Subscription-Key: 41f3ceb2f43d4fab85ca9810d43339a7 Merchant-Serial-Number: 373370 Vipps-System-Name: Paymenter Vipps-System-Version: 0.1 Vipps-System-Plugin-Name: zaporylie/vipps (PHP) Vipps-System-Plugin-Version: 3.x-dev Authorization: 
> * Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6IkNOdjBPSTNSd3FsSEZFVm5hb01Bc2hDSDJYRSIsImtpZCI6IkNOdjBPSTNSd3FsSEZFVm5hb01Bc2hDSDJYRSJ9.eyJhdWQiOiJiYWNlMzlhOS1jZTk2LTRiMDItOGY1OC0xYTRjNjYxNGIyMjQiLCJpc3MiOiJodHRwczovL3N0cy53aW5kb3dzLm5ldC9lNTExNjUyNi01MWRjLTRjMTQtYjA4Ni1hNWNiNDcxNmJjNGIvIiwiaWF0IjoxNzQ4NDY4MTA0LCJuYmYiOjE3NDg0NjgxMDQsImV4cCI6MTc0ODQ3MjAwNCwiYWlvIjoiazJSZ1lGalJ3MkhyUG5mK1FiUG9MMDBLNjUyWUFBPT0iLCJhcHBpZCI6ImJhY2UzOWE5LWNlOTYtNGIwMi04ZjU4LTFhNGM2NjE0YjIyNCIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0L2U1MTE2NTI2LTUxZGMtNGMxNC1iMDg2LWE1Y2I0NzE2YmM0Yi8iLCJvaWQiOiJlNDI5MGU5NS02MGM5LTRmMGEtODI3Yy02ODc5Nzc1NDkzOGEiLCJyaCI6IjEuQVNBQUptVVI1ZHhSRkV5d2hxWExSeGE4UzZrNXpycVd6Z0pMajFnYVRHWVVzaVE5QVFBZ0FBLiIsInN1YiI6ImU0MjkwZTk1LTYwYzktNGYwYS04MjdjLTY4Nzk3NzU0OTM4YSIsInRpZCI6ImU1MTE2NTI2LTUxZGMtNGMxNC1iMDg2LWE1Y2I0NzE2YmM0YiIsInV0aSI6IkVSajY2d3ZTQzBPZ2dLTk9Nb0VsQUEiLCJ2ZXIiOiIxLjAiLCJ4bXNfZnRkIjoiWUh5enZsNXY5TndodjRZcmF6RjZDd2o0REdXU0ZCRFNBSUoxVHczZ0FfZ0JaWFZ5YjNCbGJtOXlkR2d0WkhOdGN3In0.Zx21H0keKcQ2ND5pAhm_EqxcMT-Q0Ohq7R78j6He1ANdU4a69vNWy8Pk4hykJGcuC-bcIqElSTcyiqGP-rjmpezjAl7eAOPoJok6b9W93-6zFpuiKMvPd_V82aqbZRqw_eqa5dpxlVvbv7zlBu3oYAoBzEZfLmTX3goTiCd5Z_Jrw_fr1BR3sRT5YAeFxahvU3UKddZnB0rly9j_1X04iTuxGUEXFuvvEltN1YBhx-KUKm7eAX-IUy8QmVlcufhzRNnvDBebB7ONb5mUtwRcXS064Lo6PHmINrP1rIyqRNej_BInmWVc2pAmFqj9nBYQRqTA3juOrkvwp7wVCCfLjw Content-Type: application/json Idempotency-Key: costam5 Content-Length: 203 * Mark bundle as not supporting multiuse < HTTP/1.1 409 Conflict < 
> * Date: Wed, 28 May 2025 21:40:06 GMT < Content-Type: application/problem+json; charset=utf-8 < Content-Length: 282 < Connection: keep-alive < Request-Context: appId=cid-v1:a93a792c-9572-4c72-8702-1275fd168921 < * Connection #0 to host apitest.vipps.no left intact



```
sudo tailscale funnel -bg 80
```
> [!NOTE]- Svar fra en webhook register
> 
> ```json
> zaporylie\Vipps\Model\Webhook\v1\RegisterWebhookResponse {#3661 ▼ // extensions/Gateways/Vipps/Vipps.php:354
>   #id: "e1e888a8-8fd1-4f4f-ac6a-5963d72d58bb"
>   #secret: "vbvUfM3TGn1m64trISiPTPhy4ZSFRMp0enrXEf5jb1Vaw7k6K5UhAYSpu50EpvOygHCkDkyAN8pjaqBm88b3kg=="
> }
> ```






# Paymenter-greier
[Extensions \| Paymenter](https://paymenter.org/development/extensions/#configs)
![[Paymenter-Vipps-2025.06.07 18.13.24.png]]
```
sudo chown -R www-data:www-data /var/www/paymenter/storage /var/www/paymenter/bootstrap/cache
sudo chmod -R 755 /var/www/paymenter/storage /var/www/paymenter/bootstrap/cache
```

Mange mapper er det ikke write-permission på. Helst bruk sudo for å flytte/endre filer, men man kan også gjøre mappa skrivbar:
```
sudo chmod -R 770 /var/www/paymenter/extensions/Gateways
```

## theme
[Theme \| Paymenter](https://paymenter.org/development/theme/)
[Building assets \| Paymenter](https://paymenter.org/development/theme/assets)
```
npm run build vipps-theme
```


[Asset Bundling (Vite) - Laravel 12.x - The PHP Framework For Web Artisans](https://laravel.com/docs/12.x/vite#working-with-blade-and-routes)t
```sh
sudo systemctl stop nginx
composer run dev
```
ENVFIL: APP_URL=http://paymenterdev.brill-goblin.ts.net/

## Events

> [!NOTE]- Events
> paymenterdev@paymenterdev:/var/www/paymenter$ php artisan event:list
>   App\Events\Auth\Login ..............................................................................................................  
>   ⇂ App\Listeners\SendMailListener@handle  
>   App\Events\Invoice\Creating ........................................................................................................  
>   ⇂ App\Listeners\InvoiceCreatingListener@handle  
>   App\Events\Invoice\Finalized .......................................................................................................  
>   ⇂ App\Listeners\SendMailListener@handle  
>   App\Events\Invoice\Paid ............................................................................................................  
>   ⇂ App\Listeners\InvoicePaidListener@handle  
>   App\Events\Order\Finalized .........................................................................................................  
>   ⇂ App\Listeners\SendMailListener@handle  
>   App\Events\ServiceCancellation\Created .............................................................................................  
>   ⇂ Closure at: /extensions/Gateways/Vipps/Vipps.php:72  
>   ⇂ App\Listeners\CancellationCreatedListener@handle (ShouldQueue)  
>   App\Events\ServiceCancellation\Deleted .............................................................................................  
>   ⇂ Closure at: /extensions/Gateways/Vipps/Vipps.php:78  
>   App\Events\Service\Created .........................................................................................................  
>   ⇂ Closure at: /extensions/Gateways/Vipps/Vipps.php:59  
>   App\Events\Service\Deleted .........................................................................................................  
>   ⇂ Closure at: /extensions/Gateways/Vipps/Vipps.php:65  
>   App\Events\Service\Updated .........................................................................................................  
>   ⇂ Closure at: /extensions/Gateways/Stripe/Stripe.php:25  
>   App\Events\TicketMessage\Created ...................................................................................................  
>   ⇂ App\Listeners\TicketMessageCreatedListener@handle  
>   App\Events\User\Created ............................................................................................................  
>   ⇂ App\Listeners\SendMailListener@handle  
>   App\Events\User\Updated ............................................................................................................  
>   ⇂ Closure at: /extensions/Gateways/Vipps/Vipps.php:52  
>   Filament\Events\ServingFilament ....................................................................................................  
>   ⇂ Closure at: /vendor/filament/filament/src/FilamentServiceProvider.php:89  
>   Illuminate\Auth\Events\Logout ......................................................................................................  
>   ⇂ Closure at: /vendor/laravel/passport/src/PassportServiceProvider.php:369  
>   Illuminate\Auth\Events\Registered ..................................................................................................  
>   ⇂ Illuminate\Auth\Listeners\SendEmailVerificationNotification  
>   Illuminate\Console\Events\CommandFinished ..........................................................................................  
>   ⇂ Closure at: /vendor/laravel/framework/src/Illuminate/Foundation/Providers/FoundationServiceProvider.php:212  
>   Illuminate\Database\Events\QueryExecuted ...........................................................................................  
>   ⇂ Closure at: /vendor/laravel/framework/src/Illuminate/Foundation/Exceptions/Renderer/Listener.php:60  
>   ⇂ Spatie\LaravelIgnition\Recorders\QueryRecorder\QueryRecorder@record  
>   Illuminate\Foundation\Events\LocaleUpdated .........................................................................................  
>   ⇂ Closure at: /vendor/nesbot/carbon/src/Carbon/Laravel/ServiceProvider.php:57  
>   Illuminate\Foundation\Http\Events\RequestHandled ...................................................................................  
>   ⇂ Closure at: /vendor/livewire/livewire/src/Features/SupportAutoInjectedAssets/SupportAutoInjectedAssets.php:24  
>   Illuminate\Http\Client\Events\ConnectionFailed .....................................................................................  
>   ⇂ App\Listeners\RequestListener@handle  
>   Illuminate\Http\Client\Events\ResponseReceived .....................................................................................  
>   ⇂ App\Listeners\RequestListener@handle  
>   Illuminate\Log\Events\MessageLogged ................................................................................................  
>   ⇂ Spatie\LaravelIgnition\Recorders\LogRecorder\LogRecorder@record  
>   Illuminate\Queue\Events\JobAttempted ...............................................................................................  
>   **⇂ Closure at: /vendor/laravel/framework/src/Illuminate/Foundation/Providers/FoundationServiceProvider.php:217**  
>   **Illuminate\Queue\Events\JobExceptionOccurred .......................................................................................**  
>   **⇂ Spatie\LaravelIgnition\Recorders\JobRecorder\JobRecorder@record**  
>   **Illuminate\Queue\Events\JobFailed ..................................................................................................**  
>   **⇂ Closure at: /app/Providers/AppServiceProvider.php:71**  
>   **Illuminate\Queue\Events\JobProcessed ...............................................................................................**  
>   **⇂ Closure at: /vendor/laravel/framework/src/Illuminate/Foundation/Exceptions/Renderer/Listener.php:33**  
>   **⇂ Closure at: /vendor/spatie/laravel-ignition/src/IgnitionServiceProvider.php:262**  
>   **⇂ Closure at: /app/Providers/AppServiceProvider.php:61**  
>   **Illuminate\Queue\Events\JobProcessing** ..............................................................................................  
>   ⇂ Closure at: /vendor/laravel/framework/src/Illuminate/Log/Context/ContextServiceProvider.php:42  
>   ⇂ Closure at: /vendor/laravel/framework/src/Illuminate/Foundation/Exceptions/Renderer/Listener.php:33  
>   ⇂ Closure at: /vendor/spatie/laravel-ignition/src/IgnitionServiceProvider.php:256  
>   Paymenter\Extensions\Gateways\Vipps\Updated ........................................................................................  
>   ⇂ Closure at: /extensions/Gateways/Vipps/Vipps.php:85  
>   SocialiteProviders\Manager\SocialiteWasCalled ......................................................................................  
>   ⇂ Closure at: /app/Providers/AppServiceProvider.php:47  


## payment log

> [!NOTE]-
> ```
> array:2 [▼ // extensions/Gateways/Vipps/Vipps.php:850
>   0 => zaporylie\Vipps\Model\EPayment\v1\EventLog {#1877 ▼
>     #reference: "transaction-210420-1"
>     #pspReference: "b4776b69-f5a0-40ba-99ae-5a162fa47f6f"
>     #name: "CREATED"
>     #amount: zaporylie\Vipps\Model\EPayment\v1\Amount {#2881 ▼
>       #currency: "NOK"
>       #value: 120
>     }
>     #timestamp: DateTime @1749495126 {#2123 ▼
>       date: 2025-06-09 18:52:06.139061 UTC (+00:00)
>     }
>     #idempotencyKey: "68472d55e2bbc4.15747361"
>     #success: true
>   }
>   1 => zaporylie\Vipps\Model\EPayment\v1\EventLog {#4095 ▼
>     #reference: "transaction-210420-1"
>     #pspReference: "b4776b69-f5a0-40ba-99ae-5a162fa47f6f"
>     #name: "ABORTED"
>     #amount: zaporylie\Vipps\Model\EPayment\v1\Amount {#1833 ▼
>       #currency: "NOK"
>       #value: 120
>     }
>     #timestamp: DateTime @1749495142 {#2475 ▼
>       date: 2025-06-09 18:52:22.923936 UTC (+00:00)
>     }
>     #idempotencyKey: "68472d55e2bbc4.15747361"
>     #success: true
>   }
> ]
> 
> ```

  
## Utvikling: Flere hooks, spesielt i adminpanelet
Legge inn hooks, feks. på invoice-siden så man kan vise Vipps-eventlogg. Se over.

## Bug: canUseGateway for credits
Dropdown menyen for gateways henter bare alle gateways, men man burde kanskje bruke getCheckoutGateways, og gjøre en oppdatert sjekk for hver gang man oppdaterer valuta? 
## Bug: canUseGateway for invoice og generelt
Han har nemlig laget klar en funksjon som en gateway kan bruke for å verifisere at den kan brukes, kalt canUseGateway(). Denne funksjonen mottar alle varelinjene og kontekst for hvor den ble kallet fra. Den tenker jeg å bruke for å sjekke at ordren skjer i NOK, ikke USD eller andre valutaer.
Men de gatewayene han har utviklet støtter jo mange valutaer, så han har ikke brukt den - og dermed tydeligvis heller ikke testet at den fungerer. 

Det er flere scenarier der denne funksjonen kalles, spesielt ved checkout og invoices/fakturaer. 
1. Ved invoices så passerer han ingen varelinjer, bare "null", for det virker som han har skrevet en attribute ved objektet "products" som ikke finnes. Se bilde 1
2. Logikken som skulle sjekke hvilke gateways som rapporterer at de er riktige, hadde en brist; den passerte et helt objekt istedet for en string til videre i logikken. Altså ble det bare feilmeldinger.

![[Paymenter-Vipps-2025.05.29 19.22.02.png|550]]
![[Paymenter-Vipps-2025.05.29 19.22.02-1.png|550]]

[fix: couple of bugs when payment gateway implements canUseGateway() by lolbraa · Pull Request #810 · Paymenter/Paymenter · GitHub](https://github.com/Paymenter/Paymenter/pull/810)


## Theme
```
paymenterdev@paymenterdev:/var/www/paymenter$ php artisan app:theme:create

 ┌ What should be the Theme's name? ────────────────────────────┐
 │ Vipps Theme                                                  │
 └──────────────────────────────────────────────────────────────┘

 ┌ Who is the author of this theme? ────────────────────────────┐
 │ Kristoffer Braa                                              │
 └──────────────────────────────────────────────────────────────┘

[1/4] Copied files from `default` theme.
[2/4] Replaced path values in vite.config.js.
[3/4] Replaced variables in `theme.php`.
[4/4] Theme "vipps-theme" created successfully.

You can now start developing your theme by running:
    `npm run dev vipps-theme`
After you have finished developing, you can build your theme by running:
    `npm run build vipps-theme`
```


## Adminpage
```sh
paymenterdev@paymenterdev:/var/www/paymenter$ php artisan make:filament-page VippsAdminPage

 ┌ Which resource would you like to create this in? ────────────┐
 │ Gateway                                                      │
 └──────────────────────────────────────────────────────────────┘

 ┌ Which type of page would you like to create? ────────────────┐
 │ View                                                         │
 └──────────────────────────────────────────────────────────────┘

 ┌ Which namespace would you like to create this in? ───────────┐
 │ Paymenter\Extensions\Gateways\Vipps\Admin\Resources          │
 └──────────────────────────────────────────────────────────────┘

   INFO  Filament page [extensions/Gateways/Vipps/Admin/Resources/GatewayResource/Pages/VippsAdminPage.php] created successfully.  

   INFO  Make sure to register the page in `GatewayResource::getPages()`.
```

# Webhook
[401 Unauthorized — httpstatuses.io](https://httpstatuses.io/401)
> [!NOTE]- Respons (logg) under testing av webhook
> ```log
> [2025-05-31 19:30:34] local.INFO: Vipps webhook authentication succeeded {"ip":"127.0.0.1","headers":{"accept-encoding":["gzip"],"x-vipps-authorization":["HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature=kU1pibAdUMLtzcZwTaQqK2/MRgmaebmX2flv4igy/9k="],"x-ms-date":["Sat, 31 May 2025 17:30:33 GMT"],"x-ms-content-sha256":["kQSmDK2O2OZoefs7WJBmm2OR4kuoPtDMNGGmh0QVvtA="],"x-forwarded-proto":["https"],"x-forwarded-host":["paymenterdev.brill-goblin.ts.net"],"x-forwarded-for":["51.105.193.245"],"webhook-id":["39c2fb44-7107-45cd-b3b3-657c3202ed84"],"tailscale-funnel-request":["?1"],"content-type":["application/json; charset=utf-8"],"authorization":["HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature=kU1pibAdUMLtzcZwTaQqK2/MRgmaebmX2flv4igy/9k="],"content-length":["256"],"user-agent":["Vipps MobilePay/1.0 Webhooks/1.0"],"host":["paymenterdev.brill-goblin.ts.net"]},"body":"{\"msn\":\"373370\",\"reference\":\"inv-8-attempt-2\",\"pspReference\":\"740e7483-c083-4b95-9246-a37299ad53b7\",\"name\":\"CREATED\",\"amount\":{\"currency\":\"NOK\",\"value\":12100},\"timestamp\":\"2025-05-31T17:29:23.358Z\",\"idempotencyKey\":\"683b3c72858e20.24358952\",\"success\":true}"} 
> [2025-05-31 19:32:39] local.WARNING: Vipps webhook authentication failed {"ip":"127.0.0.1","headers":{"accept-encoding":["gzip"],"x-vipps-authorization":["HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature=FKFaajI6zuCXqYtw0XZvRfAH0pGK2tlSCK/2LJ7+yko="],"x-ms-date":["Sat, 31 May 2025 17:32:38 GMT"],"x-ms-content-sha256":["kQSmDK2O2OZoefs7WJBmm2OR4kuoPtDMNGGmh0QVvtA="],"x-forwarded-proto":["https"],"x-forwarded-host":["paymenterdev.brill-goblin.ts.net"],"x-forwarded-for":["51.105.193.245"],"webhook-id":["39c2fb44-7107-45cd-b3b3-657c3202ed84"],"tailscale-funnel-request":["?1"],"content-type":["application/json; charset=utf-8"],"authorization":["HMAC-SHA256 SignedHeaders=x-ms-date;host;x-ms-content-sha256&Signature=FKFaajI6zuCXqYtw0XZvRfAH0pGK2tlSCK/2LJ7+yko="],"content-length":["256"],"user-agent":["Vipps MobilePay/1.0 Webhooks/1.0"],"host":["paymenterdev.brill-goblin.ts.net"]},"body":"{\"msn\":\"373370\",\"reference\":\"inv-8-attempt-2\",\"pspReference\":\"740e7483-c083-4b95-9246-a37299ad53b7\",\"name\":\"CREATED\",\"amount\":{\"currency\":\"NOK\",\"value\":12100},\"timestamp\":\"2025-05-31T17:29:23.358Z\",\"idempotencyKey\":\"683b3c72858e20.24358952\",\"success\":true}"} 
> ```

> [!NOTE]- Track Vipps references unique
> I am implementing Vipps payment gateway, and to make sure the user has the possibility to start multiple transactions, and maybe stop halfway through some, I need to call the Vipps API with unique references. As of right now I store the unique references in cache like this: ->setReference(reference: 'inv-' . $invoice->id . '-attempt-' . ( \Cache::forever( key: 'vipps_attempt_' . $invoice->id, value: ($attempt = (\Cache::get('vipps_attempt_' . $invoice->id, default: 0) + 1)) ) ? $attempt : 1 Is it possible to attach and keep track of each payment-attempt (and its reference) in the invoice-class, or in some other way?
> 
> ### Copilot said: Yes, you can improve the way you
> 
> Yes, you can improve the way you track payment attempts and their unique references by storing this information in your database, associated with each invoice, instead of relying solely on the cache. This ensures that the data is persistent (survives cache clears and server restarts) and is more easily queryable and maintainable.
> 
> Here are some approaches you can take:
> 
> ---
> 
> ### **1. Create a Dedicated PaymentAttempt Model and Table**
> 
> **a. Migration Example:**
> 
> PHP
> 
> ```
> // database/migrations/xxxx_xx_xx_create_payment_attempts_table.php
> 
> use Illuminate\Database\Migrations\Migration;
> use Illuminate\Database\Schema\Blueprint;
> use Illuminate\Support\Facades\Schema;
> 
> class CreatePaymentAttemptsTable extends Migration
> {
>     public function up()
>     {
>         Schema::create('payment_attempts', function (Blueprint $table) {
>             $table->id();
>             $table->foreignId('invoice_id')->constrained()->onDelete('cascade');
>             $table->string('reference')->unique();
>             $table->string('status')->nullable(); // e.g. pending, completed, failed, cancelled
>             $table->timestamps();
>         });
>     }
> 
>     public function down()
>     {
>         Schema::dropIfExists('payment_attempts');
>     }
> }
> ```
> 
> **b. PaymentAttempt Model:**
> 
> PHP
> 
> ```
> // app/Models/PaymentAttempt.php
> 
> namespace App\Models;
> 
> use Illuminate\Database\Eloquent\Model;
> 
> class PaymentAttempt extends Model
> {
>     protected $fillable = ['invoice_id', 'reference', 'status'];
> 
>     public function invoice()
>     {
>         return $this->belongsTo(Invoice::class);
>     }
> }
> ```
> 
> **c. Invoice Relationship:**
> 
> PHP
> 
> ```
> // app/Models/Invoice.php
> 
> public function paymentAttempts()
> {
>     return $this->hasMany(PaymentAttempt::class);
> }
> ```
> 
> **d. Usage Example:**
> 
> PHP
> 
> ```
> // When starting a new payment attempt
> $attemptNumber = $invoice->paymentAttempts()->count() + 1;
> $reference = 'inv-' . $invoice->id . '-attempt-' . $attemptNumber;
> 
> $paymentAttempt = $invoice->paymentAttempts()->create([
>     'reference' => $reference,
>     'status' => 'pending',
> ]);
> 
> // Use $paymentAttempt->reference for the Vipps API
> ```


# Dokumentasjon

## Informasjon mot adminstrator og kunder
> [!NOTE]- Statusoppdatering om utvikling
> En av begrensningene som har vært litt tungvint er at hver ordre bærer ikke så veldig mye informasjon, og man kan heller ikke utvide så enkelt. Feks. kan en ordre kun ha status pending, cancelled eller paid - mens Vipps bruker 8-10 per transaksjon.
> 
> En av kravene til Vipps er at man lager en ny referanse for hver eneste gang man gjør et forsøk på å betale, altså hvis kunden starter en betalingsprosess, avbryter, og så starter en ny, må nr. 2 ha en unik referanse. Og denne må man jo lagre.
> 
> Jeg forsøkte først å bare cache det, men fant ut av at det burde lagres ordentlig i databasen sammen med ordren. En litt halvveis måte jeg landet på var å lage en ny "transaction" for hver gang man starter en betalingsprosess, men setter summen på hver transaksjon til 0 - frem til Vipps sier at betalingen er godkjent av brukeren, da settes summen inn og fakturaen merkes som betalt. 
> Det gir på en måte mening, men kan være veldig forvirrende mot sluttbruker. Derfor har jeg hatt lyst til å utvide transaksjonstabellen med den mer nyanserte informasjonen fra Vipps, noe jeg nå har fått til. Den informasjonen som er vist på bildet er alt for mye da, så jeg skal fjerne mye og gjøre det penere.
> 
> Jeg har også lagt til denne type informasjon for en faktura på adminpanelet. Dermed kan man som adminstrator faktisk holde oversikt med om Vipps-pluginen fungerer og har TRUKKET beløpet - det er nemlig ingen enkel måte å sjekke det på, foruten at man aldri får utbetalt penger fra DNB.
> Jeg skal implementere logikk med schedule som sjekker dette og sørger for at ting blir trukket, men det er søren ikke lett slik Paymenter er satt opp, uten å endre kjernefiler.![[Paymenter-Vipps-2025.06.11 21.34.41.png|550]]
> 
> ![[Paymenter-Vipps-2025.06.11 21.34.42.png]]
> 
> ![[Paymenter-Vipps-2025.06.11 21.34.42-1.png|550]]

## Produksjon V1
> [!NOTE]-  Statusoppdatering trukket i produksjon
>
> ![[Paymenter-Vipps-2025.06.11 21.36.51.png]]
> 
> ![[Paymenter-Vipps-2025.06.11 21.36.52.png|550]]
> 
> ![[Paymenter-Vipps-2025.06.11 21.36.52-1.png|550]]
> 
> ![[Paymenter-Vipps-2025.06.11 21.36.52-2.png|550]]
> 
> ![[Paymenter-Vipps-2025.06.11 21.36.52-3.png|550]]
> Testet produksjon nå. Fant så ut at man ikke kan trekke beløp under 1 NOK, men 1kr går akkurat :P
> ![[Paymenter-Vipps-2025.06.11 21.36.53.png|550]]

## Theme: Radioknapper i stedet for selection
> [!NOTE]- Statusoppdatering
> Har brukt alt for lang tid på å lage en egen "theme" for å kunne gjøre ting som dette; en meny for å velge betalingsløsning som ikke bare er en dropdown-meny
> 
> ![[Paymenter-Vipps-2025.06.11 21.38.07.png]]
> 
> ![[Paymenter-Vipps-2025.06.11 21.38.07-1.png|550]]



# Annet
OBS: I produsjon, hver dag (?) kommer denne feilmeldingen ![[Paymenter-Vipps-2025.08.01 21.41.24.png|550]]. Har testet at det fungerer med en ordentlig transaksjon.
EDIT: Bare en bug i paymenter



# Regnskapsføring
Hva som trengs å føres:
- Kundedata
	- Navn, adresse, epost
- Dato
- Sum
- Avgift
- Typenummer


> [!NOTE]- Diskusjon og research om Vipps->Conta
> Kristoffer
> > Kan @Martin og evt du, Fredrik, lage en liste over hvilken informasjon og hvilke API-kall som må gjøres mellom Vipps og Conta?
> > Basert på endepunktene og det som er listet som nødvendig informasjon
> > Husk at mitt største problem er at jeg ikke har noen innsikt i regnskapsføring
> > [Get started with Conta's API \| Conta Hjelp](https://hjelp.conta.no/api/)
> > [Report API \| Vipps MobilePay Developer Docs](https://developer.vippsmobilepay.com/api/report/#tag/reportv2ledgers/paths/~1report~1v2~1ledgers~1%7BledgerId%7D~1%7Btopic%7D~1dates~1%7BledgerDate%7D/get)
> 
> Fredrik
> > https://hjelp.conta.no/regnskap/hvordan-bokfore-innbetalinger-fra-vipps-og-zettle-i-conta/
> 
> Martin
> > ![[Paymenter-Vipps-2025.08.27 17.14.24.webp|550]]
> > Må faktisk dokumentere kunde, vare, dato, sum, salgskonto. Optimalt kobles opp mot Proservere under avdeling
> > Er ett alternativt, vis paymenter kan eksportere i riktig format
> > eksportere til SAF-T
> > https://hjelp.conta.no/regnskap/bilag/hvordan-bokfore-salg-fra-nettbutikk/
> 
> 
> 
> Martin
> > Om paymenter oppfyller alle krav til kundereskonto, og kan eksportere data som SAF-T, så tror jeg det bare er standard bokføring. Altså, bilag
> 
> Fredrik
> > Skal være faktura per kjøp ja aka bilag
> 
> Kristoffer
> > Så vidt jeg vet kan du kun generere en pdf-faktura. Går sikkert an å mekke noe i annet format som en plugin, men da må man jo spørre seg hvilken av løsningene man faktisk ønsker seg.
> > 
> > Direkte i Paymenter vil jo dekke alle salg (?) for Proservere, mens Vipps er en mye mer generell løsning for alle slags salg - hvis vi skulle selge gjennom annet enn Paymenter
> 
> Martin
> > Mtp hvordan det må bokføres, så tror jeg kanskje vipps recuring må på plass før conta api'en kan lages, siden vi egent trenger:
> > Paymenter oppretter kunde, når kunde oppretter bruker på paymenter.
> > Faktura opprettes i paymenter -> Oppretter faktura i conta.
> > Betaling gjennomføres, og betaling + avgift bokføres i conta. 
> > Kunde betaler ikke, kreditnota opprettes i conta (Kanselering av en faktura)
> > Vis man ikke får navn, addresse, epost osv igjennom vipps da

