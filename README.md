[![Apache Sling](https://sling.apache.org/res/logos/sling.png)](https://sling.apache.org)

&#32;[![Build Status](https://ci-builds.apache.org/job/Sling/job/modules/job/sling-org-apache-sling-scripting-java/job/master/badge/icon)](https://ci-builds.apache.org/job/Sling/job/modules/job/sling-org-apache-sling-scripting-java/job/master/)&#32;[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=apache_sling-org-apache-sling-scripting-java&metric=coverage)](https://sonarcloud.io/dashboard?id=apache_sling-org-apache-sling-scripting-java)&#32;[![Sonarcloud Status](https://sonarcloud.io/api/project_badges/measure?project=apache_sling-org-apache-sling-scripting-java&metric=alert_status)](https://sonarcloud.io/dashboard?id=apache_sling-org-apache-sling-scripting-java)&#32;[![JavaDoc](https://www.javadoc.io/badge/org.apache.sling/org.apache.sling.scripting.java.svg)](https://www.javadoc.io/doc/org.apache.sling/org-apache-sling-scripting-java)&#32;[![Maven Central](https://maven-badges.herokuapp.com/maven-central/org.apache.sling/org.apache.sling.scripting.java/badge.svg)](https://search.maven.org/#search%7Cga%7C1%7Cg%3A%22org.apache.sling%22%20a%3A%22org.apache.sling.scripting.java%22)&#32;[![Contrib](https://sling.apache.org/badges/status-contrib.svg)](https://github.com/apache/sling-aggregator/blob/master/docs/status/contrib.md)&#32;[![scripting](https://sling.apache.org/badges/group-scripting.svg)](https://github.com/apache/sling-aggregator/blob/master/docs/group/scripting.md) [![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://www.apache.org/licenses/LICENSE-2.0)

# Apache Sling Scripting Java Support

This module is part of the [Apache Sling](https://sling.apache.org) project.

This module implements a script engine for java servlets, that are compiled
on the fly by Sling.

To test it:

1. Install this bundle in Sling, for example with

  mvn -P autoInstallBundle clean install -Dsling.url=http://localhost:8080/system/console
  
If Sling is running with the launchpad/testing setup.

2. Create /apps/foo/foo.java in your repository (via WebDAV for example), with this code:

package apps.foo;

import java.io.IOException;
import javax.servlet.ServletException;
import org.apache.sling.api.SlingHttpServletRequest;
import org.apache.sling.api.SlingHttpServletResponse;
import org.apache.sling.api.servlets.SlingSafeMethodsServlet;

public class foo extends SlingSafeMethodsServlet {
    
    protected void doGet(SlingHttpServletRequest request, SlingHttpServletResponse response) 
    throws ServletException, IOException {
        response.setContentType("text/plain");
        response.getWriter().write("Response from " + getClass().getName() + " at " + new java.util.Date());
    }
}   

3. Request http://localhost:8080/content/foo/*.html which should display something like

  Response from apps.foo.foo at Tue Nov 18 14:49:14 CET 2008
  
4. The servlet code should be automatically recompiled after any changes.
  
