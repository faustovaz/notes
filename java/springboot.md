# Spring Boot

### Profiles

Spring boot offers the possibility of configure multiple profiles, so it's possible to use different configuration for different environments. If not specified Spring Boot will look for configuration in the default file `application.properties`. To specify a profile, let's say dev profile, it's necessary to have a file called `application-dev.properties`, for production `application-production.properties`, an so on. (So the pattern is `application-{env}.properties`)

To activate a profile using gradle, do one of the following:

- `$ SPRING_PROFILES_ACTIVE=dev gradle build`
- `$ SPRING_PROFILES_ACTIVE=prod gradle bootRun`
- `$ gradle bootRun` (in case of using the default profile)

To execute the jar, do one of the following:

- `$ SPRING_PROFIES_ACTIVE=dev java -jar myapp.jar`
- `$ java -jar -Dspring.profiles.active=dev myapp.jar`
- `$ java -jar myapp.jar` (using default profile)

### Using self-signed certificate

To generate a certificate using keytool:
```bash
$ keytool -genkeypair -keyalg RSA --keysize 2048 -storetype PKCS12 -keystore keystore.p12 -validity 10 
-storepass testing -alias aliastest
```
where
     - `genkeypair`: what is to be done (in the example, generate a key pair using the given algorithm);
     - `keyalg`: the chosen algorithm (RSA for example);
     -` keysize`: the size of the key;
     - `storetype`: the type of file which will be used as the certificate;
     - `keystore`: the name of the file;
     - `validity`: the number (in days) to expire the certificate;
     - `storepass`: the password used 
     - `alias`: alias

Remember to use `localhost` for the first question (`What is your first and last name?`) if the plans are to use the selfsigned certificate at localhost.
With the self signed certificate, we can use it to test https connections with our Spring boot app by copying the certificate file to the resources folder (`src/main/resources`) and referencing it in the application.properties file:

```java
server.ssl.key-store=src/main/resources/keystore.p12
server.ssl.key-store-password=testing
server.ssl.key-store-type=PKCS12
server.ssl.key-alias=aliastest

```