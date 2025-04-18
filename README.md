# moje.cert.pl API Postman Collection
Kolekcja w wersji 2.1 dla aplikacji Postman z zestawem zapytań do API moje.cert.pl

## 📚 Spis treści

- [📌 zmienne](#-zmienne)
- [🔑 jak uzyskać klucz API](#-jak-uzyskać-klucz-api)
- [🆔 jak uzyskać ID organizacji](#-jak-uzyskać-id-organizacji)
- [🌐 jak znaleźć dostępne domeny w organizacji](#-jak-znaleźć-dostępne-domeny-w-organizacji)

## 📌 zmienne

```json
  "variable": [
    {
      "key": "HTTP_HOST",
      "value": "moje.cert.pl"
    },
    {
      "key": "API_KEY",
      "value": "Token <klucz_API>",
      "type": "string"
    },
    {
      "key": "ORG_SLUG",
      "value": "<id_organizacji>",
      "type": "string"
    },
    {
      "key": "DOMAIN_NAME",
      "value": "<nazwa_domeny>",
      "type": "string"
    }
  ]
```

## 🔑 jak uzyskać klucz API

Klucz API jest niepowtarzalny dla każdego kontekstu użytkownika. Jednocześnie kluczy API można utworzyć więcej niż jeden, ale każdy z nich będzie przypisany do Twojego kkontekrtu użytkownika i uprawnień jakie posiadasz. 

Żeby uzyskać klucz API należy zalogować się do portalu, kliknąć "hamburger menu" ☰ w prawym górnym rogu, bezpośrednio za swoim adresem e-mail.

Następnie wybrać [Ustawienia], a w prawym menu [Twoje tokeny API] i postępować zgodnie z instrukcją. 

  ![moj cert pl_get_api_key](https://github.com/user-attachments/assets/1e34c03c-d2a5-48fb-82a6-9975f1eca2f0)

Pamiętaj, że wartość zmiennej API_KEY w której znajsuje się klucz musi poprzedzać słowo "Token"



## 🆔 jak uzyskać ID organizacji

W celu pobrania ID organizacji, czyli tak organization slug (ORG_SLUG), należy wykonać request oznaczony w kolekcji jako GET organization list all:

📤 GET {{HTTP_HOST}}/api/v1/organizations/

W odpowiedzi otrzymamy JSON zawierajacy polę slug. wartością będzie nazwa organizacji, pisana z małych liter, zdefiniowana w portalu wraz z losowym sufixem.

Jeśli posiadasz dostęp do wielu organizacji, otrzymasz w wyniku listę wszystkich dostępnych organizacji dla Twojego kontekstu użytkownika. 

```json
{
    "count": 1,
    "next": null,
    "previous": null,
    "results": [
        {
            "name": "MOJA ORGANIZACJA",
            "slug": "moja-organizacja-p4nit7m0",
            "nip": "",
            "regon": "",
            "krs": "",
            "address": "",
            "city": "",
            "postal_code": "",
            "contact_emails": []
        }
    ]
}
```
Uzyskaną wartość wstawiamy jako wartość zmiennej ORG_SLUG

## 🌐 jak znaleźć dostępne domeny w organizacji

Mając wartość ORG_SLUG możesz wykonać kolejny request GET organizations retrieve

📤 GET {{HTTP_HOST}}/api/v1/organizations/{{ORG_SLUG}}/

W wyniku otrzymasz listę wszystkich domen dodanych do organizacji, w raz z podstawowymi informacjami odnośnie ostatniego skanowania i wycieków związanych z domeną.

```json
{
    "name": "MOJA ORGANIZACJA",
    "slug": "moja-organizacja-p4nit7m0",
    "nip": "",
    "regon": "",
    "krs": "",
    "address": "",
    "city": "",
    "postal_code": "",
    "contact_emails": [],
    "domains": [
        {
            "domain_name": "mojadomena.pl",
            "creation_time": "2025-02-18T12:54:51.832141+01:00",
            "last_scan": {
                "creation_time": "2025-04-15T06:13:04.695633+02:00",
                "finish_time": null,
                "is_finished": false,
                "num_vulnerabilities_high": 0,
                "num_vulnerabilities_medium": 0,
                "num_vulnerabilities_low": 1
            },
            "leak_data": {
                "latest_date": "2025-04-11",
                "count": 10
            }
        },
        {
            "domain_name": "mojadomena.eu",
            "creation_time": "2025-02-18T15:03:33.656418+01:00",
            "last_scan": {
                "creation_time": "2025-04-02T14:42:19.298941+02:00",
                "finish_time": "2025-04-02T19:26:45.421707+02:00",
                "is_finished": true,
                "num_vulnerabilities_high": 0,
                "num_vulnerabilities_medium": 0,
                "num_vulnerabilities_low": 0
            },
            "leak_data": {
                "latest_date": "2025-04-14",
                "count": 10
            }
        }
    ]
}
```

wybraną domenę z pola "domain_name", definjujesz jako wartość zmiennej DOMAIN_NAME




