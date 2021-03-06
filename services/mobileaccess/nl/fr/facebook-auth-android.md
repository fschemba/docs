---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

# Activation de l'authentification Facebook pour les applications Android
{: #facebook-auth-android}

Dernière mise à jour : 4 août 2016
{: .last-updated}


Pour utiliser Facebook comme fournisseur d'identité dans vos applications Android, ajoutez et configurez la plateforme Android pour votre application
Facebook sur le site Facebook for Developers.
{:shortdesc}

## Avant de commencer
{: #facebook-auth-android-before}
Vous devez disposer des éléments suivants :
* Un projet Android qui est configuré pour fonctionner avec Gradle. Le projet n'a pas besoin d'être instrumenté avec un SDK client de {{site.data.keyword.amashort}}.  
* Une instance d'une application {{site.data.keyword.Bluemix_notm}} qui est protégée par le service {{site.data.keyword.amashort}}. Pour plus d'informations sur la création d'un système de back end {{site.data.keyword.Bluemix_notm}}, voir [Initiation](index.html).
* Une application Facebook avec une plateforme Android sur le site Facebook for Developers (https://developers.facebook.com).

**Important :** il n'est pas nécessaire d'installer séparément le SDK Facebook (`com.facebook.FacebookSdk`). Celui-ci est installé automatiquement par Gradle quand vous ajoutez le SDK client Facebook de {{site.data.keyword.amashort}}. Vous
pouvez ignorer cette étape si vous ajoutez la plateforme Android sur le site Facebook for Developers.

## Configuration d'une application Facebook pour la plateforme Android
{: #facebook-auth-android-config}
Depuis le site Facebook for Developers (https://developers.facebook.com) :

1. Connectez-vous à votre compte sur le site Facebook for Developers.
2. Ajoutez ou configurez la plateforme Android. Plus d'informations figurent dans les étapes suivantes.
1. Entrez le nom du package de votre application Android dans l'invite Google Play Package Name (Nom du package Google Play). Pour identifier le nom de
package de votre application Android, recherchez l'entrée `<manifest ..... package="{nom_votre_package}">` dans le
fichier `AndroidManifest.xml` de projet Android Studio.

1. Entrez le nom de la classe de votre activité principale dans l'invite **Class Name (Nom de classe)**. Le nom de classe est la valeur de
la propriété `android:name` dans la section activity. Si plusieurs activités sont répertoriées dans le fichier
`AndroidManifest.xml`, recherchez celle contenant l'entrée `<intent-filter>`:

	```XML
	<activity
		android:name=".MainActivity"
		android:label="@string/app_name">
		<intent-filter>
			<action android:name="android.intent.action.MAIN"/>
			<category android:name="android.intent.category.LAUNCHER"/>
		</intent-filter>
	</activity>
	```

1. Pour que Facebook puisse vérifier l'authenticité de votre applications, vous devez spécifier le hachage SHA1 de votre certificat de développeur.

	**Au sujet de la sécurité Android :** Sur le système d'exploitation Android, toutes les applications installées sur un périphérique Android doivent être signées à l'aide d'un certificat de développeur. L'application Android peut être générée dans deux modes : Debug (débogage) et Release (publication). <br/>
  Utilisez des certificats différents pour ces deux modes.  Les certificats utilisés pour signer les applications Android en mode Debug sont fournies avec le SDK Android, qui est généralement installé automatiquement par Android Studio. Au moment de publier votre appli dans le magasin Google Play, vous devez la signer avec un autre certificat, généralement généré par vous. <br/>Facebook
vous permet d'entrer deux ensembles de hachages de clé : un pour les applications générées en mode Debug avec un certificat de débogage et un autre pour
les applications générées en mode Release avec un certificat à cet effet. Pour plus d'informations, voir [Signing your Android applications](http://developer.android.com/tools/publishing/app-signing.html).

1. Le magasin de clés qui contient le certificat que vous utilisez pour l'environnement de développement est stocké dans le fichier `~/.android/debug.keystore`. Le mot de passe du magasin de clés par défaut est : `android`. Utilisez ce certificat pour générer des applications en mode Debug.

1. Extrayez le hachage de clé du certificat du mode Debug :

	```XML 	keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore | openssl sha1 -binary | openssl base64
	```

	**Astuce** : Vous pouvez utiliser la même syntaxe pour extraire le hachage de clé du certificat du mode Release. Remplacez l'alias et le chemin du magasin de clés dans la commande.

1. Copiez et collez le hachage de clé obtenu avec la commande **keytool** dans une invite
Development/Release Key Hashes sur le site Facebook for Developers.

	**Astuce** : Vous pouvez activer l'authentification unique (SSO) si vous prévoyez d'utiliser cette fonction.

1. Cliquez sur **Save Settings (Sauvegarder les paramètres)**.

## Configuration de {{site.data.keyword.amashort}} pour l'authentification Facebook
{: #facebook-auth-android-mca}
Une fois que vous disposez de l'ID d'application Facebook et avez configuré votre application Facebook pour servir les clients
Android, vous pouvez activer l'authentification Facebook depuis le tableau de bord {{site.data.keyword.amashort}}.

1. Ouvrez votre appli dans le tableau de bord {{site.data.keyword.Bluemix_notm}}.

1. Cliquez sur **Options pour application mobile** et notez la valeur de **Route** (`applicationRoute`)
et **Identificateur global unique de l'application** (`applicationGUID`). Vous aurez besoin de ces valeurs lors de l'initialisation du SDK.

1. Cliquez sur la vignette {{site.data.keyword.amashort}}. Le tableau de bord {{site.data.keyword.amashort}} se charge.

1. Cliquez sur le bouton **Configurer** dans le panneau **Facebook**.

1. Entrez l'ID d'application Facebook et cliquez sur **Sauvegarder**.

## Configuration du SDK client de {{site.data.keyword.amashort}} pour Android
{: #facebook-auth-android-sdk}
Pour configurer le SDK client pour Android, utilisez le gestionnaire de dépendances Gradle dans Android Studio.

1.  Ouvrez le fichier `build.gradle` du module de votre appli.
Votre projet Android peut comporter deux fichiers `build.gradle` : un pour le projet et l'autre pour le module de l'application. Utilisez le fichier du module de l'application.

1. Localisez la section des dépendances dans le fichier `build.gradle` et ajoutez une nouvelle dépendance de compilation pour le SDK client :

	```Gradle
	dependencies {
		compile group: 'com.ibm.mobilefirstplatform.clientsdk.android',
        name:'facebookauthentication',
        version: '2.+',
        ext: 'aar',
        transitive: true
    	// autres dépendances
	}
```

	**Remarque :** vous pouvez retirer la dépendance sur le module `core` du groupe `com.ibm.mobilefirstplatform.clientsdk.android`, si elle figure dans votre fichier. Le module `facebookauthentication` télécharge le module `core` automatiquement, ainsi que le propre SDK de Facebook.

  Une fois que vous avez enregistré vos mises à jour, le module `facebookauthentication` télécharge et installe tous les SDK nécessaires dans votre projet Android.


1. Synchronisez votre projet avec Gradle. Cliquez sur **Tools (Outils) > Android > Sync project with Gradle Files (Synchroniser le projet avec les fichiers Gradle)**.

1. Ouvrez le fichier `res/values/strings.xml` et ajoutez une chaîne `facebook_app_id` contenant l'ID de votre application
Facebook :

	```XML
	<resources>
		<string name="app_name">HelloWorld</string>
		<string name="action_settings">Settings</string>
		<string name="facebook_app_id">522733366802111</string>
	</resources>
```

1. Dans le fichier `AndroidManifest.xml` de votre projet Android :
   1. Ajoutez le droit d'accès à Internet sous l'élément `<manifest>` :

	```XML
	<uses-permission android:name="android.permission.INTERNET" />
```
  2. Ajoutez les métadonnées requises pour le SDK Facebook à l'élément `<application>` :

	```XML
	<application .......>

		<meta-data
			android:name="com.facebook.sdk.ApplicationId"
			android:value="@string/facebook_app_id"/>

		<activity ...../>
		<activity ...../>
	</application>
```

   1. Ajoutez un élément Facebook activity sous vos activités existantes :

	```XML
	<application .....>
		<activity ...../>
		<activity ...../>

		<activity 	android:name="com.facebook.FacebookActivity"
					android:configChanges=
						"keyboard|keyboardHidden|screenLayout|screenSize|orientation"
					android:theme="@android:style/Theme.Translucent.NoTitleBar"
					android:label="@string/app_name" />

	</application>
```

1. Initialisez le SDK client et enregistrez le gestionnaire d'authentification Facebook. Initialisez le SDK client de {{site.data.keyword.amashort}} en transmettant les paramètres de contexte, d'identificateur unique global de l'application (`applicationGUID`) et de route (`applicationRoute`).<br/>
 Il est courant d'insérer le code d'initialisation dans la méthode `onCreate` de l'activité principale de l'application Android, bien que ceci ne soit pas impératif.<br/>
 Remplacez *applicationRoute* et *applicationGUID* par les valeurs de **Route** et de **Identificateur global
unique de l'application** dans le menu **Options pour application mobile** sur la page principale de votre application
dans le tableau de bord Bluemix.

	```Java 	BMSClient.getInstance().initialize(getApplicationContext(), 					"applicationRoute", 					"applicationGUID", 					BMSClient.REGION_UK);

	BMSClient.getInstance().setAuthorizationManager(
					MCAAuthorizationManager.createInstance(this));

	FacebookAuthenticationManager.getInstance().register(this);
```
   Remplacez `BMSClient.REGION_UK` par la région appropriée  Pour afficher votre région {{site.data.keyword.Bluemix_notm}}, cliquez sur l'icône **Avatar**  ![icône Avatar](images/face.jpg "icône Avatar")  dans la barre de menu pour ouvrir le widget **Compte et support**.
   
  **Remarque :** si votre application Android a pour cible Android version 6.0 (API niveau 23) ou supérieure, vous devez vous assurer que l'application dispose d'un appel `android.permission.GET_ACCOUNTS` avant d'appeler `register`. Pour plus d'informations, voir [https://developer.android.com/training/permissions/requesting.html](https://developer.android.com/training/permissions/requesting.html){: new_window}.
					


1. Ajoutez le code suivant à votre activité :

	```Java 	@Override 	protected void onActivityResult(int requestCode, int resultCode, Intent data) {
		super.onActivityResult(requestCode, resultCode, data);
		FacebookAuthenticationManager.getInstance()
			.onActivityResultCalled(requestCode, resultCode, data);
	}
```

## Test de l'authentification
Une fois que le SDK client est initialisé et que le gestionnaire d'authentification Facebook est enregistré, vous pouvez commencer à envoyer des
demandes à votre back end mobile.

### Avant de commencer
{: #facebook-auth-android-testing-before}
Vous devez utiliser le conteneur boilerplate {{site.data.keyword.mobilefirstbp}} et disposer déjà d'une ressource protégée par
{{site.data.keyword.amashort}} sur le noeud final `/protected`. Pour configurer un noeud final `/protected`, voir la rubrique [Protection des ressources](https://console.{DomainName}/docs/services/mobileaccess/protecting-resources.html).

1. Essayez d'envoyer depuis votre navigateur une requête à un noeud final protégé de votre nouvelle application back end mobile. Ouvrez l'URL suivante :
`{applicationRoute}/protected`. Par exemple : `http://my-mobile-backend.mybluemix.net/protected`
<br/>Le noeud final `/protected` d'une application back end mobile créée avec le conteneur boilerplate MobileFirst Services Starter est
protégé par {{site.data.keyword.amashort}}. Un message signalant l'interdiction d'accéder au site (`Unauthorized`) est renvoyé au navigateur. Ce message est renvoyé car ce noeud final n'est accessible qu'aux applications mobiles instrumentées avec le SDK client de {{site.data.keyword.amashort}}.

1. A l'aide de votre application Android, envoyez une demande au même noeud final. Ajoutez le code ci-dessous après avoir initialisé
le client `BMSClient` et enregistré le gestionnaire d'authentification Facebook (`FacebookAuthenticationManager`).

	```Java
	Request request = new Request("/protected", Request.GET);
	request.send(this, new ResponseListener() {
		@Override
		public void onSuccess (Response response) {
			Log.d("Myapp", "onSuccess :: " + response.getResponseText());
			Log.d("MyApp", AuthorizationManager.getInstance().getUserIdentity().toString());
		}
		@Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
			if (null != t) {
				Log.d("Myapp", "onFailure :: " + t.getMessage());
			} else if (null != extendedInfo) {
				Log.d("Myapp", "onFailure :: " + extendedInfo.toString());
			} else {
				Log.d("Myapp", "onFailure :: " + response.getResponseText());
			}
		}
	});
```

1. Lancez votre application. Un écran de connexion à Facebook s'affiche.

	![image](images/android-facebook-login.png)

	Cet écran peut être légèrement différent si l'appli Facebook n'est pas installée sur votre périphérique, ou si vous n'y êtes pas connecté.

1. Cliquez sur **OK** pour autoriser {{site.data.keyword.amashort}} à utiliser votre ID utilisateur Facebook pour l'authentification.

1. 	Lorsque votre demande aboutit, la sortie suivante figure dans l'utilitaire LogCat :

	![image](images/android-facebook-login-success.png)

 Vous pouvez également ajouter une fonctionnalité de déconnexion en ajoutant le code suivant :

 ```
FacebookAuthenticationManager.getInstance().logout(getApplicationContext(), listener);
 ```

 Si vous appelez ce code lorsqu'un utilisateur est connecté via Facebook, l'utilisateur est déconnecté de Facebook. Lorsque l'utilisateur tente de se
reconnecter, il doit à nouveau soumettre ses données d'identification Facebook.

 La valeur `listener` transmise à la fonction de déconnexion peut être `null`.
