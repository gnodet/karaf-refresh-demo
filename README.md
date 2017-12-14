Start Karaf and copy following commands into console:

feature:repo-add mvn:org.apache.aries.jpa/jpa-features/2.7.0-SNAPSHOT/xml/features
feature:repo-add mvn:com.eclipsesource.jaxrs/features/5.3/xml/features
feature:repo-add mvn:com.example/jersey-features/2.2.2-SNAPSHOT/xml/features
feature:repo-add mvn:com.example/module-features/1.0.0-SNAPSHOT/xml/features
feature:install module-liquibase
feature:install module-part1
feature:install module-part2

You will notice, that installing subsequent modules trigger restarting previous ones. 

The offending lines look like that:
2017-12-14T12:17:33,400 | INFO  | features-1-thread-1 | FeaturesServiceImpl              | 9 - org.apache.karaf.features.core - 4.1.2 | Stopping bundles:
2017-12-14T12:17:33,401 | INFO  | features-1-thread-1 | FeaturesServiceImpl              | 9 - org.apache.karaf.features.core - 4.1.2 |   org.apache.aries.transaction.manager/1.3.3
2017-12-14T12:17:33,432 | INFO  | features-1-thread-1 | FeaturesServiceImpl              | 9 - org.apache.karaf.features.core - 4.1.2 |   org.apache.aries.jpa.javax.persistence_2.1/2.7.0.SNAPSHOT
2017-12-14T12:17:33,433 | INFO  | features-1-thread-1 | FeaturesServiceImpl              | 9 - org.apache.karaf.features.core - 4.1.2 |   org.apache.aries.jpa.eclipselink.adapter/2.6.1
2017-12-14T12:17:33,435 | INFO  | features-1-thread-1 | FeaturesServiceImpl              | 9 - org.apache.karaf.features.core - 4.1.2 |   com.eclipsesource.jaxrs.publisher/5.3.1.201602281253

