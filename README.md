## Como configurar

1. Se crea la api key de [theMovieDb] para poder configurar las peliculas y series de la aplicación.
2. Crear `secrets.xml` in `res/values` y agregar la key generada.
```xml
    <?xml version="1.0" encoding="utf-8"?>
    <resources>
        <string name="movieKey">XXXX</string>
    </resources>
```
3. Luego de generar la key se procede a instalar firebase, para esto utilizamos android estudio para implementar en android.
4. Crearemos una cuenta de firebase, donde agregaremos los siguientes campos para poder configurarlo.
 - Nombre del paquete de Android (`de.cineaste.android`) y certificado de firma SHA-1 luego damos en ingresar.
5. Luego descargamos el archivo google-services.json y lo pondremos en la raiz de la aplicación.
6. Una vez tenemos el archivo de google services procedemos a importar librerias a tus archivos Gradle.

`(build.gradle) en raiz `
```  
buildscript {
  repositories {
   google()
  }
  dependencies {
    classpath 'com.google.gms:google-services:4.3.4'
  }
}
allprojects {
    repositories {
        google()
    }

    dependencies {
      implementation platform('com.google.firebase:firebase-bom:26.3.0')
      implementation 'com.google.firebase:firebase-analytics-ktx'
      implementation 'com.google.firebase:firebase-auth-ktx'
      implementation 'com.google.firebase:firebase-firestore-ktx'
    }
}
```
`(app/build.gradle) `
``` 
apply plugin: 'com.android.application'
apply plugin: 'com.google.gms.google-services' 
``` 
 
7. Ya luego de esto podemos instanciar en las actividades el objeto FirebaseAnalytics y logEvent() para empezar a enviar eventos a Google Analytics.

- `private lateinit var firebaseAnalytics: FirebaseAnalytics` (importamos el objeto) en MainActivity
- `firebaseAnalytics = Firebase.analytics` (instanciamos el objeto) en onCreate() metodo encargado de iniciar firebase.

8. Ya con firebase instalado podemos proceder a implementar las etiquetas para mejor eventos en nuestra aplicación, teniendo en cuenta que existe etiquetas por deferecto.
  Para crear una etiqueta lo hacemos de la siguiente forma:
  
``` 
firebaseAnalytics.logEvent("addToWhislist") {
    param("nombre", name)
    param("calificacion", text)
}
 ``` 
 

