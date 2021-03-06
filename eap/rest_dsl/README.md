JAX-RS Consumer with the Camel REST DSL
=======================================

This example deploys a basic Rest service using Rest DSL with JAX-RS in EAP with the Camel Subsystem.

### Requirements:

 * Red Hat Fuse 7.6.0
 * JBoss EAP 7.2.5
 * Maven 3.0 or Greater (http://maven.apache.org/)
 * Java 8

Building
--------
To build the project.

     mvn clean install

This will build the war including the dependencies.

Building and Deploying to JBoss EAP
-----------------------------------

To start up EAP browse to your EAP install directory. Then run

     /bin/standalone.sh

This will bring up EAP. Once you see logging like this, EAP is up:

     11:08:55,464 INFO  [org.jboss.as] (Controller Boot Thread) JBAS015874: JBoss EAP 6.4.0.GA started in 10870ms - 
     Started 151 of 189 services (56 services are lazy, passive or on-demand)

If you do not already have a user set up for the JBoss Management console you can set one up buy running `$EAP_HOME/bin/add-user.sh` in a separate window. It will walk you through the process. Select 'Management user' when given the option. One this is done and EAP is up, navigate to `http://localhost:9990`  and login with your newly created user. 

### To deploy your war:

From the management console navigate to the Runtime tab and select 'Management Deployments' on the left hand side. Once here, select 'Add' and browse to your war file. You can either use the one in your .m2 directory or the one in `fuse-quickstarts/eap/rest_dsl/target`. After choosing the war file, click the 'En/Disable' button to start it.

Alternatively you can deploy your code using the jboss-as-maven-plugin. To do so go into `eap/parent/pom.xml` and change the configuration of the `jboss-as-maven-plugin` to use your management user's `username` and `password` and switch `<skip>` to `false`.  Then run:

     mvn clean install


Results
-----------------------
Once you have the war deployed with the routes started, you should be able to use the Rest services with a Rest client (Postman).

### Base Path

    http://localhost:8080/eap-rest-dsl-7.6/rest/

### Rest Services

Method | URL               | Descripción
-------|-------------------|----------------------------------------------------
GET    | /user             | Returns the users
GET    | /user/{id}        | Returns a user by id
POST   | /user             | Creates a user
PUT    | /user             | Updates a user
DELETE | /user/{id}        | Deletes a user by id

Example of a JSON User object (to use with the POST and PUT methods):

    {
        "id": 1,
        "username": "leandro"
    }

