===
a3m
===

The simplest diagram:

.. uml::

    !include <C4/C4_Context>
    Person(user, "C4 fans", "Hello to Sphinx!")

Web application:

.. uml::

   !include https://raw.githubusercontent.com/plantuml-stdlib/C4-PlantUML/master/C4_Container.puml

   Person(admin, "Administrator")
   System_Boundary(c1, "Sample System") {
      Container(web_app, "Web Application", "C#, ASP.NET Core 2.1 MVC", "Allows users to compare multiple Twitter timelines")
   }
   System(twitter, "Twitter")

   Rel(admin, web_app, "Uses", "HTTPS")
   Rel(web_app, twitter, "Gets tweets from", "HTTPS")
