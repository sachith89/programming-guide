# Springboot Properties

Group properties that we can override in the application context:

- Core properties (logging properties, thread properties)
- Integration properties (RabbitMQ properties, ActiveMQ properties)
- Web properties (HTTP properties, MVC properties)
- Security properties (LDAP properties, OAuth2 properties)

## When Is the Bootstrap Configuration File Used?

We use bootstrap.yml or bootstrap.properties for configuring the bootstrap context. This way we keep the external configuration for bootstrap and main context nicely separated.

The bootstrap context is responsible for loading configuration properties from the external sources and for decrypting properties in the local external configuration files.

When the Spring Cloud application starts, it creates a bootstrap context. The first thing to remember is that the bootstrap context is the parent context for the main application.

Another key point to remember is that these two contexts share the Environment, which is the source of external properties for any Spring application. In contrast with the application context, the bootstrap context uses a different convention for locating the external configuration.

The source of configuration files can be a filesystem or even a git repository, for example. The services use their spring-cloud-config-client dependency to access the configuration server.

To put it in simple words, the configuration server is the point through which we access the application context configuration files.

## Quick Example

```yaml
spring:
  cloud:
    config:
      password: s3cr3t
      username: root
      uri: http://localhost:8888
      fail-fast: 'true'
  application:
    name: config-client
  profiles:
    active: development
management:
  security:
    enabled: 'false'

```
