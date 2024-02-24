# how-to-generate-upload-keystore


Step (1)
```bash
    keytool -genkey -v -keystore Android/upload-keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload
    ```

Initially, enter this command.fill the requirements.

Step(2)
create properties file to add constant value.
      ```bash
    storePassword=password-from-previous-step
    keyPassword=password-from-previous-step
    keyAlias=upload
    storeFile=keystore-file-location
    ```
      

fill password that enter in command for storePassword and keyPassword.
For storeFile,add ../upload-keystore.jks if locate in android file

Step (3)
 ```bash
    signingConfigs {
       release {
           keyAlias keystoreProperties['keyAlias']
           keyPassword keystoreProperties['keyPassword']
           storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
           storePassword keystoreProperties['storePassword']
       }
   }
   buildTypes {
       release {
           signingConfig signingConfigs.release
       }
   }
    ```


get properties values form above codes and then,
```bash
    def keystoreProperties = new Properties()
    def keystorePropertiesFile = rootProject.file('key.properties')
      if (keystorePropertiesFile.exists()) {
        keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
      }
    ```
   

create release mode.
