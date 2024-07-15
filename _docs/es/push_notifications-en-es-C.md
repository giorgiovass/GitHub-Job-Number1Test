---
nav_title: Notificaciones push
article_title: Notificaciones push para React Native
platform: Reaccionar nativo
page_order: 2
toc_headers: h2
description: "Este artículo cubre la implementación de notificaciones automáticas en React Native".
channel: empujar

---

# Integración de notificaciones push

> Este artículo de referencia cubre cómo configurar notificaciones automáticas para React Native. La integración de notificaciones push requiere configurar cada plataforma nativa por separado. Siga las guías respectivas enumeradas para finalizar la instalación.

## Paso 1: Complete la configuración inicial

{% tabs %}
{% tab Expo %}
Selecciona el `enableBrazeIosPush` y `enableFirebaseCloudMessaging` opciones en tu `app.json` archivo para habilitar push para iOS y Android, respectivamente. Consulte las instrucciones de configuración [aquí]({{site.baseurl}}/developer_guide/platform_integration_guides/react_native/react_sdk_setup/#step-2-complete-native-setup) para obtener más detalles.

Tenga en cuenta que deberá utilizar estas configuraciones en lugar de las instrucciones de configuración nativas si depende de bibliotecas de notificaciones push adicionales como [Expo Notifications](https://docs.expo.dev/versions/latest/sdk/notifications/).
{% endtab %}

{% tab Android %}
### Paso 1.1: Regístrese para empujar

Regístrese para enviar mensajes utilizando la API Firebase Cloud Messaging (FCM) de Google. Para obtener un tutorial completo, consulte los siguientes pasos de la [guía de integración push nativa de Android]({{site.baseurl}}/developer_guide/platform_integration_guides/android/push_notifications/android/integration/standard_integration/):

1. [Agrega Firebase a tu proyecto]({{site.baseurl}}/developer_guide/platform_integration_guides/android/push_notifications/android/integration/standard_integration/#step-1-add-firebase-to-your-project).
2. [Agregue Cloud Messaging a sus dependencias]({{site.baseurl}}/developer_guide/platform_integration_guides/android/push_notifications/android/integration/standard_integration/#step-2-add-cloud-messaging-to-your-dependencies).
3. [Crea una cuenta de servicio]({{site.baseurl}}/developer_guide/platform_integration_guides/android/push_notifications/android/integration/standard_integration/#step-3-create-a-service-account).
4. [Generar credenciales JSON]({{site.baseurl}}/developer_guide/platform_integration_guides/android/push_notifications/android/integration/standard_integration/#step-4-generate-json-credentials).
5. [Cargue sus credenciales JSON en Braze]({{site.baseurl}}/developer_guide/platform_integration_guides/android/push_notifications/android/integration/standard_integration/#step-5-upload-your-json-credentials-to-braze).

### Paso 1.2: Añade tu ID de remitente de Google

Primero, vaya a Firebase Console, abra su proyecto y luego seleccione <i class="fa-solid fa-gear"></i>**Configuración** > **Configuración del proyecto**.

![The Firebase project with the "Settings" menu open.]({% image_buster /assets/img/android/push_integration/set_up_automatic_token_registration/select-project-settings.png %})

Seleccione **Cloud Messaging**y luego, en **Firebase Cloud Messaging API (V1)**, copie el **ID del remitente** en su portapapeles.

![The Firebase project's "Cloud Messaging" page with the "Sender ID" highlighted.]({% image_buster /assets/img/android/push_integration/set_up_automatic_token_registration/copy-sender-id.png %})

A continuación, abra el archivo de su proyecto. `app.json` archiva y configura tu `firebaseCloudMessagingSenderId` propiedad al ID del remitente en su portapapeles. Por ejemplo:

```
"firebaseCloudMessagingSenderId": "693679403398"
```

### Paso 1.3: Agregue la ruta a su JSON de servicios de Google

En tu proyecto `app.json` archivo, agregue la ruta a su `google-services.json` archivo. Este archivo es necesario al configurar `enableFirebaseCloudMessaging: true` en su configuración.

```json
{
  "expo": {
    "android": {
      "googleServicesFile": "PATH_TO_GOOGLE_SERVICES"
    },
    "plugins": [
      [
        "@braze/expo-plugin",
        {
          "androidApiKey": "YOUR-ANDROID-API-KEY",
          "iosApiKey": "YOUR-IOS-API-KEY",
          "enableBrazeIosPush": true,
          "enableFirebaseCloudMessaging": true,
          "firebaseCloudMessagingSenderId": "YOUR-FCM-SENDER-ID",
          "androidHandlePushDeepLinksAutomatically": true
        }
      ],
    ]
  }
}
```
{% endtab %}

{% tab iOS %}
### Paso 1.1: Cargar certificados APN

Genere un certificado del servicio de notificaciones push (APN) de Apple y cárguelo en el panel de Braze. Para obtener un tutorial completo, consulte [Carga de su certificado APN]({{site.baseurl}}/developer_guide/platform_integration_guides/swift/push_notifications/integration/#step-1-upload-your-apns-certificate).

### Paso 1.2: Elija un método de integración

Si no planea solicitar permisos de inserción cuando se inicie la aplicación, omita el `requestAuthorizationWithOptions:completionHandler:` Llame a su AppDelegate y luego vaya al [Paso 2](#step-2-request-push-notifications-permission). De lo contrario, sigue la [guía de integración nativa de iOS]({{site.baseurl}}/developer_guide/platform_integration_guides/swift/push_notifications/integration/?tab=objective-c#automatic-push-integration).

Cuando haya terminado, continúe con [el Paso 1.3](#step-13-migrate-your-push-key).

### Paso 1.3: Migra tu tecla push

Si anteriormente estaba usando `expo-notifications` para administrar su tecla de pulsación, ejecute `expo fetch:ios:certs` desde la carpeta raíz de su aplicación. Esto descargará su clave de inserción (un archivo .p8), que luego se puede cargar en el panel de Braze.
{% endtab %}
{% endtabs %}

## Paso 2: Solicitar permiso para notificaciones push

Utilizar el `Braze.requestPushPermission()` Método (disponible en v1.38.0 y superiores) para solicitar permiso para notificaciones automáticas del usuario en iOS y Android 13+. Para Android 12 y versiones anteriores, este método no es operativo.

Este método toma un parámetro requerido que especifica qué permisos debe solicitar el SDK al usuario en iOS. Estas opciones no tienen ningún efecto en Android.

```javascript
const permissionOptions = {
  alert: true,
  sound: true,
  badge: true,
  provisional: false
};

Braze.requestPushPermission(permissionOptions);
```

### Paso 2.1: Escuche las notificaciones automáticas (opcional)

Además, puede suscribirse a eventos en los que Braze haya detectado y manejado una notificación push entrante. Utilice la clave de escucha `Braze.Events.PUSH_NOTIFICATION_EVENT`.

{% alert note %}
Los eventos de notificación push de Braze están disponibles tanto en Android como en iOS. Debido a diferencias de plataforma, iOS solo detectará eventos push de Braze cuando un usuario haya interactuado con una notificación.
{% endalert %}

```javascript
Braze.addListener(Braze.Events.PUSH_NOTIFICATION_EVENT, data => {
  console.log(`Push Notification event of type ${data.payload_type} seen. Title ${data.title}\n and deeplink ${data.url}`);
  console.log(JSON.stringify(data, undefined, 2));
});
```

#### Campos de eventos de notificación push

{% alert note %}
Debido a las limitaciones de la plataforma en iOS, Braze SDK solo puede procesar cargas útiles de inserción mientras la aplicación está en primer plano. Los oyentes sólo dispararán para el `push_opened` tipo de evento en iOS después de que un usuario haya interactuado con un push.
{% endalert %}

Para obtener una lista completa de los campos de notificaciones push, consulte la siguiente tabla:

| Nombre del campo         | Tipo      | Descripción |
| ------------------ | --------- | ----------- |
| `payload_type`     | Cadena    | Especifica el tipo de carga útil de notificación. Los dos valores que se envían desde Braze React Native SDK son `push_opened` y `push_received`.  Solo `push_opened` Los eventos son compatibles con iOS. |
| `url`              | Cadena    | Especifica la URL que abrió la notificación. |
| `use_webview`      | Booleano   | Si `true`, la URL se abrirá en la aplicación en una vista web modal. Si `false`, la URL se abrirá en el navegador del dispositivo. |
| `title`            | Cadena    | Representa el título de la notificación. |
| `body`             | Cadena    | Representa el cuerpo o el texto del contenido de la notificación. |
| `summary_text`     | Cadena    | Representa el texto resumido de la notificación. Esto está mapeado desde `subtitle` en iOS. |
| `badge_count`      | Número   | Representa el recuento de insignias de la notificación. |
| `timestamp`        | Número | Representa el momento en que la aplicación recibió la carga útil. |
| `is_silent`        | Booleano   | Si `true`, la carga útil se recibe silenciosamente. Para obtener detalles sobre cómo enviar notificaciones push silenciosas de Android, consulte [Notificaciones push silenciosas en Android]({{site.baseurl}}/developer_guide/platform_integration_guides/android/push_notifications/android/silent_push_notifications). Para obtener detalles sobre cómo enviar notificaciones push silenciosas de iOS, consulte [Notificaciones push silenciosas en iOS]({{site.baseurl}}/developer_guide/platform_integration_guides/swift/push_notifications/silent_push_notifications/). |
| `is_braze_internal`| Booleano   | Esto será `true` si se envió una carga útil de notificación para una función interna del SDK, como sincronización de geocercas, sincronización de indicadores de funciones o seguimiento de desinstalación. La carga útil se recibe de forma silenciosa para el usuario. |
| `image_url`        | Cadena    | Especifica la URL asociada con la imagen de notificación. |
| `braze_properties` | Objeto    | Representa las propiedades de Braze asociadas con la campaña (pares clave-valor). |
| `ios`              | Objeto    | Representa campos específicos de iOS. |
| `android`          | Objeto    | Representa campos específicos de Android. |
{: .reset-td-br-1 .reset-td-br-2}

## Paso 3: Habilitar enlaces profundos (opcional)

Para permitir que Braze maneje enlaces profundos dentro de los componentes de React cuando se hace clic en una notificación push, siga los pasos adicionales.

{% tabs %}
{% tab Expo %}
Nuestra [aplicación de muestra BrazeProject](https://github.com/braze-inc/braze-react-native-sdk/tree/master/BrazeProject) contiene un ejemplo completo de enlaces profundos implementados. Para obtener más información sobre qué son los enlaces profundos, consulte nuestro [artículo de preguntas frecuentes]({{site.baseurl}}/user_guide/personalization_and_dynamic_content/deep_linking_to_in-app_content/#what-is-deep-linking).

{% endtab %}
{% tab Android %}
Para Android, configurar enlaces profundos es idéntico a [configurar enlaces profundos en aplicaciones nativas de Android]({{site.baseurl}}/developer_guide/platform_integration_guides/android/push_notifications/android/integration/standard_integration#step-4-add-deep-links). Si desea que Braze SDK maneje automáticamente los enlaces profundos push, configure `androidHandlePushDeepLinksAutomatically: true` en tus `app.json`.

{% endtab %}
{% tab iOS %}
### Paso 3.1: Agregar capacidades de enlaces profundos

Para iOS, agregue `populateInitialUrlFromLaunchOptions` a su AppDelegate `didFinishLaunchingWithOptions` método. Por ejemplo:

```objc
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
  self.moduleName = @"BrazeProject";
  self.initialProps = @{};

  BRZConfiguration *configuration = [[BRZConfiguration alloc] initWithApiKey:apiKey endpoint:endpoint];
  configuration.triggerMinimumTimeInterval = 1;
  configuration.logger.level = BRZLoggerLevelInfo;
  Braze *braze = [BrazeReactBridge initBraze:configuration];
  AppDelegate.braze = braze;

  [self registerForPushNotifications];
  [[BrazeReactUtils sharedInstance] populateInitialUrlFromLaunchOptions:launchOptions];

  return [super application:application didFinishLaunchingWithOptions:launchOptions];
}
```

### Paso 3.2: Configurar el manejo de enlaces profundos

Utilizar el `Linking.getInitialURL()` método para enlaces profundos que abren su aplicación, y el `Braze.getInitialURL` Método para enlaces profundos dentro de notificaciones push que abren su aplicación cuando no se está ejecutando. Por ejemplo:

```javascript
Linking.getInitialURL()
  .then(url => {
    if (url) {
      console.log('Linking.getInitialURL is ' + url);
      showToast('Linking.getInitialURL is ' + url);
      handleOpenUrl({ url });
    }
  })
  .catch(err => console.error('Error getting initial URL', err));

// Handles deep links when an iOS app is launched from a hard close via push click.
Braze.getInitialURL(url => {
  if (url) {
    console.log('Braze.getInitialURL is ' + url);
    showToast('Braze.getInitialURL is ' + url);
    handleOpenUrl({ url });
  }
});
```
{% alert note %}
Braze proporciona esta solución alternativa ya que la API de enlace de React Native no admite este escenario debido a una condición de carrera al iniciar la aplicación.
{% endalert %}
{% endtab %}
{% endtabs %}

## Etapa 4: Prueba de visualización de notificaciones push

En este punto, debería poder enviar notificaciones a los dispositivos. Siga los siguientes pasos para probar su integración push.

{% alert note %}
A partir de macOS 13, en ciertos dispositivos, puede probar las notificaciones push de iOS en un simulador de iOS 16+ que se ejecuta en Xcode 14 o superior. Para obtener más detalles, consulte las [Notas de la versión de Xcode 14](https://developer.apple.com/documentation/xcode-release-notes/xcode-14-release-notes).
{% endalert %}

1. Establezca un usuario activo en la aplicación React llamando `Braze.changeUserId('your-user-id')` método.
2. Dirígete a **Campañas** y crea una nueva campaña de notificaciones push. Elija las plataformas que le gustaría probar.
3. Redacte su notificación de prueba y diríjase a la pestaña **Prueba** . agregar lo mismo `user-id` como usuario de prueba y haga clic en **Enviar prueba**. Deberías recibir la notificación en tu dispositivo en breve.

![Una campaña push de Braze que muestra que puede agregar su propia ID de usuario como destinatario de prueba para probar su notificación push.][1]

## Reenviar el envío de Android a FMS adicionales

Si desea utilizar un servicio de mensajería Firebase (FMS) adicional, puede especificar un FMS alternativo al que llamar si su aplicación recibe un envío que no proviene de Braze. Por ejemplo:

```json
{
  "expo": {
    "plugins": [
      [
        "@braze/expo-plugin",
        {
          ...
          "androidFirebaseMessagingFallbackServiceEnabled": true,
          "androidFirebaseMessagingFallbackServiceClasspath": "com.company.OurFirebaseMessagingService"
        }
      ]
    ]
  }
}
```

## Configurar extensiones de aplicaciones con Expo

### Habilitación de notificaciones push enriquecidas para iOS

{% alert tip %}
Las notificaciones push enriquecidas están disponibles para Android de forma predeterminada.
{% endalert %}

Para habilitar notificaciones push enriquecidas en iOS usando Expo, configure el `enableBrazeIosRichPush` propiedad a `true` en tus `expo.plugins` objeto en `app.json`:

```json
{
  "expo": {
    "plugins": [
      [
        "@braze/expo-plugin",
        {
          ...
          "enableBrazeIosRichPush": true
        }
      ]
    ]
  }
}
```

Por último, agregue el identificador del paquete para esta extensión de aplicación a la configuración de credenciales de su proyecto: `<your-app-bundle-id>.BrazeExpoRichPush`. Para obtener más detalles sobre este proceso, consulte [Uso de extensiones de aplicaciones con Expo Application Services](#app-extensions).

### Habilitación de historias push para iOS

{% alert tip %}
Las historias push están disponibles para Android de forma predeterminada.
{% endalert %}

Para habilitar historias push en iOS usando Expo, asegúrese de tener un grupo de aplicaciones definido para su aplicación. Para obtener más información, consulte \[Agregar un grupo de aplicaciones][4].

A continuación, configure el `enableBrazeIosPushStories` propiedad a `true` y asigne su ID de grupo de aplicaciones a `iosPushStoryAppGroup` en tus `expo.plugins` objeto en `app.json`:

```json
{
  "expo": {
    "plugins": [
      [
        "@braze/expo-plugin",
        {
          ...
          "enableBrazeIosPushStories": true,
          "iosPushStoryAppGroup": "group.com.company.myApp.PushStories"
        }
      ]
    ]
  }
}
```

Por último, agregue el identificador del paquete para esta extensión de aplicación a la configuración de credenciales de su proyecto: `<your-app-bundle-id>.BrazeExpoPushStories`. Para obtener más detalles sobre este proceso, consulte [Uso de extensiones de aplicaciones con Expo Application Services](#app-extensions).

{% alert warning %}
Si está utilizando Push Stories con los servicios de aplicaciones Expo, asegúrese de utilizar el `EXPO_NO_CAPABILITY_SYNC=1` bandera al correr `eas build`. Hay un problema conocido en la línea de comando que elimina la capacidad de Grupos de aplicaciones del perfil de aprovisionamiento de su extensión.
{% endalert %}

### Uso de extensiones de aplicaciones con Expo Application Services {#app-extensions}

Si está utilizando Expo Application Services (EAS) y ha habilitado `enableBrazeIosRichPush` o `enableBrazeIosPushStories`, deberás declarar los identificadores de paquete correspondientes para cada extensión de aplicación en tu proyecto. Hay varias formas de abordar este paso, dependiendo de cómo esté configurado su proyecto para administrar la firma de código con EAS.

Un enfoque es utilizar el `appExtensions` configuración en su `app.json` archivo siguiendo [la documentación de extensiones de la aplicación](https://docs.expo.dev/build-reference/app-extensions/)de Expo. Alternativamente, puede configurar el `multitarget` configuración en su `credentials.json` archivo siguiendo [la documentación de credenciales locales](https://docs.expo.dev/app-signing/local-credentials/#multi-target-project)de Expo.

[1]: {% image_buster /assets/img/react-native/push-notification-test.png %} "Prueba de campaña de empuje"
[2]: https://braze-inc.github.io/braze-swift-sdk/tutorials/braze/b2-rich-push-notifications/
[3]: https://braze-inc.github.io/braze-swift-sdk/tutorials/braze/b3-push-stories/
[4]: {{site.baseurl}}/developer_guide/platform_integration_guides/swift/push_notifications/push_story/#adding-an-app-group
