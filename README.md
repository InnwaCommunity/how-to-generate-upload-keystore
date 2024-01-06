# how-to-generate-upload-keystore


Step (1)
# keytool -genkey -v -keystore Android/upload-keystore.jks -keyalg RSA -keysize 2048 -validity 10000 -alias upload
Initially, enter this command.fill the requirements.

Step(2)
create properties file to add constant value.
# storePassword=<password-from-previous-step>
# keyPassword=<password-from-previous-step>
# keyAlias=upload
# storeFile=<keystore-file-location>

for storeFile,add ../upload-keystore.jks if locate in android file

Step (3)

# def keystoreProperties = new Properties()
#   def keystorePropertiesFile = rootProject.file('key.properties')
#   if (keystorePropertiesFile.exists()) {
#       keystoreProperties.load(new FileInputStream(keystorePropertiesFile))
#   }

get properties values form above codes and then,

#   signingConfigs {
#       release {
#           keyAlias keystoreProperties['keyAlias']
#           keyPassword keystoreProperties['keyPassword']
#           storeFile keystoreProperties['storeFile'] ? file(keystoreProperties['storeFile']) : null
#           storePassword keystoreProperties['storePassword']
#       }
#   }
#   buildTypes {
#       release {
#           signingConfig signingConfigs.release
#       }
#   }

create release mode.
