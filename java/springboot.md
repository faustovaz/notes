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















