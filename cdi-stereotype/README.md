# cdi-stereotype: Example Using CDI Stereotype.

Author: Ievgen Shulga  
Level: Intermediate  
Technologies: JPA, JSF, EJB  
Summary: The `cdi-stereotype` quickstart demonstrates how to apply CDI stereotypes to beans to encapsulate CDI interceptor bindings and CDI alternatives.  
Target Product: JBoss EAP  
Source: <https://github.com/jbossas/eap-quickstarts/>  

## What is it?

The `cdi-stereotype` quickstart is an extension of the [cdi-interceptors](../cdi-interceptors/README.md) quickstart and demonstrates how to use a CDI stereotype in Red Hat JBoss Enterprise Application Platform.

A stereotype is an annotation, annotated `@Stereotype`, that packages several other annotations. Stereotypes allow a developer to declare common metadata for beans in a central place.

In this example, the stereotype encapsulates the following :

* All beans with this stereotype inherit the following interceptor bindings: `@Logging` and `@Audit`
* All beans with this stereotype are alternatives

This quickstart defines stereotype with 2 interceptors bindings (`@Logging` and `@Audit`) to be inherited by all beans with that stereotype. It also indicates that all beans to which it is applied are `@Alternatives`. An alternative stereotype lets us classify beans by deployment scenario.
Arquillian tests added in [cdi-interceptors](../cdi-interceptors/README.md) quickstart.

_Note: This quickstart uses the H2 database included with Red Hat JBoss Enterprise Application Platform 7.1. It is a lightweight, relational example datasource that is used for examples only. It is not robust or scalable, is not supported, and should NOT be used in a production environment!_

_Note: This quickstart uses a `*-ds.xml` datasource configuration file for convenience and ease of database configuration. These files are deprecated in JBoss EAP and should not be used in a production environment. Instead, you should configure the datasource using the Management CLI or Management Console. Datasource configuration is documented in the [Configuration Guide](https://access.redhat.com/documentation/en/red-hat-jboss-enterprise-application-platform/) for Red Hat JBoss Enterprise Application Platform._


## System Requirements

The application this project produces is designed to be run on Red Hat JBoss Enterprise Application Platform 7.1 or later.

All you need to build this project is Java 8.0 (Java SDK 1.8) or later and Maven 3.3.1 or later. See [Configure Maven for JBoss EAP 7.1](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/CONFIGURE_MAVEN_JBOSS_EAP7.md#configure-maven-to-build-and-deploy-the-quickstarts) to make sure you are configured correctly for testing the quickstarts.


## Use of EAP7_HOME

In the following instructions, replace `EAP7_HOME` with the actual path to your JBoss EAP installation. The installation path is described in detail here: [Use of EAP7_HOME and JBOSS_HOME Variables](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/USE_OF_EAP7_HOME.md#use-of-eap_home-and-jboss_home-variables).


## Start the JBoss EAP Server

1. Open a command prompt and navigate to the root of the JBoss EAP directory.
2. The following shows the command line to start the server:

        For Linux:   EAP7_HOME/bin/standalone.sh
        For Windows: EAP7_HOME\bin\standalone.bat


## Build and Deploy the Quickstart

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. Type this command to build and deploy the archive:

        mvn clean install wildfly:deploy

4. This will deploy `target/cdi-stereotype.war` to the running instance of the server.


## Access the Application

The application will be running at the following URL <http://localhost:8080/cdi-stereotype/>

You can now comment out classes in the `WEB-INF/beans.xml` file to disable one or both of the interceptors or alternative stereotype and view the results.

* Comment the `<class>org.jboss.as.quickstarts.cdi.interceptor.AuditInterceptor</class>` and you will no longer see the audit history on the browser page.
* Comment the `<class>org.jboss.as.quickstarts.cdi.interceptor.LoggingInterceptor</class>` and you will no longer see the log messages in the server log.
* Comment the `<stereotype>org.jboss.as.quickstarts.cdi.interceptor.ServiceStereotype</stereotype>` and you no longer see ItemAlternativeServiceBean implementation invoked.

In this quickstart, in order to switch back to the default implementation,
uncomment the `<interceptors>` and `<stereotype>` block in the `WEB-INF/beans.xml` file and redeploy the quickstart.


## Server Log: Expected Warnings and Errors

_Note:_ You will see the following warnings in the server log. You can ignore these warnings.

    WFLYJCA0091: -ds.xml file deployments are deprecated. Support may be removed in a future version.

    HHH000431: Unable to determine H2 database version, certain features may not work

## Undeploy the Archive

1. Make sure you have started the JBoss EAP server as described above.
2. Open a command prompt and navigate to the root directory of this quickstart.
3. When you are finished testing, type this command to undeploy the archive:

        mvn wildfly:undeploy


## Run the Quickstart in Red Hat JBoss Developer Studio or Eclipse

You can also start the server and deploy the quickstarts or run the Arquillian tests from Eclipse using JBoss tools. For general information about how to import a quickstart, add a JBoss EAP server, and build and deploy a quickstart, see [Use JBoss Developer Studio or Eclipse to Run the Quickstarts](https://github.com/jboss-developer/jboss-developer-shared-resources/blob/master/guides/USE_JBDS.md#use-jboss-developer-studio-or-eclipse-to-run-the-quickstarts).


## Debug the Application

If you want to debug the source code of any library in the project, run the following command to pull the source into your local repository. The IDE should then detect it.

        mvn dependency:sources
