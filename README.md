# Keycloak User Federation From Existing Database

A simple example of creating custom User Federation module for keycloak. Tested on KeyCloak 11.0.2 with Java 8.

## Features
- Can connect with existing database in any database (as long JDBC can connect to it)
- Using Email as Login-name
- Enter query to get password in existing database, based on email
- Enter query to get several user attribute in existing database, based on email


## Build
Use mvn package to build the module into jar file
> mvn package

## Installation into KeyCloak
- Add new jdbc driver and datasource in KeyCloak's Wildfly. For mysql, you can follow these configuration example:
[https://www.tutorialsbuddy.com/keycloak-mysql-setup](https://www.tutorialsbuddy.com/keycloak-mysql-setup)
- Put the .jar file into standalone/deployments folder of keycloak. And then start/restart keycloak

## Configuration in KeyCloak
- Goto your realm, and then choose User Federation
- Choose Add Provider, and select "Federation DB Provider"
- Configure these mandatory settings:
	1. Database JNDI name: The JNDI name of the datasource you want to use (example: java:jboss/datasources/UserDS)
	1. Query to Get Password by Email: The query used to get password from the table. Only one column permitted(example:
select password from wp_users where email=?)
	1. Query to Get User Data: Query to get the user data to be imported to keycloak. Only two columns permitted and the name have to be email and firstName (example:select  email,nama as firstName from wp_users where email=?)
	1. Klik save
	1. It is done, you can try to login in the realm's client with username/password from existing DB  

