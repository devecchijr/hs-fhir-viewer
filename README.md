# hs-fhir-viewer
A demo application using the power of Healthshare Information Exchange and FHIR standard

## Setting up Healthshare side

Pre-requesites: You'll need a FHIR enabled Information Exchange Installation. 

If you don't have a FHIR access gateway production, you can set this up using the following command:
```
Zn “hslib”
Do ##class(HS.Util.Installer).InstallFHIRAccessGateway(“FHIRAG”)
```
It will create an application with the following URL:
/csp/healthshare/fhirag/fhiraccess: 

This is the app to use for FHIR Access Gateway interactions.  This app has Password authentication enabled. For demo purposes, you can disabled it.

You will want to point the FHIR AG at your Information Exchange instance.  In the Management Portal for the HSFHIRACCESS namespace, use the Service Registry UI to modify the HSREGISTRY and HSACCESS registry entries to point to your HealthShare IE instance.

## Setting up client side

unzip the dist.zip file to a folder of your choice on your app web server.

Open the yourFolder/assets/demo/data/configProd.json file.

Set the defaultLocale property pointing to your locale file.

Ex:
```
"defaultLocale":"pt-br",
```
To enable other locales you can work with the localeOptions property

Ex:
```
 "localeOptions":[
    {"label": "br portuguese", "value": "pt-br"},
    {"label": "english", "value": "en"},
    {"label": "french", "value": "fr"},
    {"label": "german", "value":"de"},
    {"label": "spanish", "value":"es-ch"},
    {"label": "my locale", "value":"myLocaleJsonFile"},
  ],
```

To create a new locale json file you can use the sample files available at the same folder Ex: (pt-br, en, fr, es-ch, etc). Each label corresponds to some piece of content on this application. In order to make the things easier the main part are grouped by component or clinical type.

Ex:
```
{
  "global_dateFormat": "dd/MM/yyyy",
  "global_datetimeFormat": "dd/MM/yyyy hh:mm",
  "global_datetimeFormat2": "dd/MM/yy hh:mm",
  "global_chartDateFormat": "DD/MM/YY",
  "global_inputDateFormat": "dd/mm/yy",
  "global_calendar_locale":"fr",

  "header_configuration":"Configuration",

  "label_patientSearchTitle": "Recherche de Patient - FHIR PDQm",

  "label_fullname": "Nom",
  "label_address": "Adresse",
  "btn_EHR": "Voir le Dossier Patient",
  "placeholder_firstname": "Prénom",
  "tooltip_firstname": "Prénom du patient",
  "placeholder_birthDate": "Date de naissance",
  ...
  ```



