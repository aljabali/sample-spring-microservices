Enabling Eureka and services

Enabling SSL /Https using self -sign certificate for microservice using Spring Cloud, Eureka and Zuul

Original article can be found here (https://piotrminkowski.wordpress.com/2017/02/05/part-1-creating-microservice-using-spring-cloud-eureka-and-zuul/)

All what i did is to enable ssl for both Eureka+Zuul and services

simply follow these steps

# run eureka first

# Import certificate in your local keystore
https://www.grim.se/guide/jre-cert

i.e. Ubuntu
keytool -import -alias alias -keystore /etc/ssl/certs/java/cacerts -file localhost.crt


Configuration changes are
1- add ssl to all configurations of servers
  ssl:
    key-store: keystore.jks
    key-store-password: password
    key-password: password

2- change eureka url in all config files to https
      defaultZone: ${DISCOVERY_URL:https://localhost:8761}/eureka/


3- add ribbon config in gateway

  TrustStore: keystore.jks
  TrustStorePassword : password
  ReadTimeout: 60000
  IsSecure: true
  MaxAutoRetries: 1

