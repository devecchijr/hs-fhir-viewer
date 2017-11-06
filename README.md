# hs-fhir-viewer
A demo application using the power of Healthshare Information Exchange and FHIR standard

## Setting up Healthshare side

Prerequisite: You'll need a FHIR enabled Information Exchange Installation. 

If you don't have a FHIR access gateway production, you can set this up using the following command:
```
Zn “hslib”
Do ##class(HS.Util.Installer).InstallFHIRAccessGateway(“FHIRAG”)
```
It will create an application with the following URL:
/csp/healthshare/fhirag/fhiraccess:

This is the app to use for FHIR Access Gateway interactions. This app has Password authentication enabled. For demo purposes, you can disabled it.

You will want to point the FHIR AG at your Information Exchange instance.  In the Management Portal for the HSFHIRACCESS namespace, use the Service Registry UI to modify the HSREGISTRY and HSACCESS registry entries to point to your HealthShare IE instance.

## Setting up client side

unzip the dist.zip file to a folder of your choice on your app web server.

Open the yourFolder/assets/demo/data/configProd.json file.

## FHIR URL

In order to point the application at your backend FHIR API, you need set up the following properties: 
Ex:
```
...
  "fhirBaseUrl":"http://localhost:57772/csp/healthshare/fhirag/fhiraccess",
  "fhirAuthorization":"Basic X3N5c3RlbTpzeXM=",
...
```

## Localization

There are some available locales to use in your demo but you can configure your own locale:

To create a new locale json file you can use the samples available at the same folder Ex: (pt-br.json, en.json, fr.json, es-ch.json, etc). Each label corresponds to some piece of content on this application. In order to make the things easier the main part are grouped by component or clinical type.

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

Set the defaultLocale property pointing to your locale file.

Ex:
```
"defaultLocale":"myLocalFile",
...
```
To enable other locales to final user you can work with the localeOptions property.  

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


## Using node js as web server

You can serve this app using node js. For that, unzip the host.zip file to a folder of your choice.

Inside the folder, install the packages needed

```
npm install
```

Open host.js file and point to the index.html app location at the following line: 
```
res.sendFile(path.resolve(__dirname, '../dist/index.html'));
```

If you prefer, you can proxy the backend API to the same port to avoid CORS problems (optional).
```
server.use('/csp', proxy({target: 'http://localhost:57772', changeOrigin: true}));
```

If can also change the listening port:
```
httpServer.listen(3000, () => {
  console.log('Listening on: http://localhost:3000');
});
```

Save your host.js file and run it with node command or if you prefer with nodemon.
```
node host
```




