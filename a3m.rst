===
a3m
===

The simplest diagram:

.. uml::

    !include <C4/C4_Context>
    Person(user, "C4 fans", "Hello to Sphinx!")

Web application:

.. uml::

   !include <C4/C4_Container>
   AddElementTag("v1.0", $borderColor="#d73027")
   AddElementTag("v1.1", $fontColor="#d73027")
   AddElementTag("backup", $fontColor="orange")
   AddRelTag("backup", $textColor="orange", $lineColor="orange", $lineStyle = DashedLine())
   Person(user, "Customer", "People that need products")
   Person(admin, "Administrator", "People that administrates the products via the new v1.1 components", $tags="v1.1")
   Container(spa, "SPA", "angular", "The main interface that the customer interacts with via v1.0", $tags="v1.0")
   Container(spaAdmin, "Admin SPA", "angular", "The administrator interface that the customer interacts with via new v1.1", $tags="v1.1")
   Container(api, "API", "java", "Handles all business logic (incl. new v1.1 extensions)", $tags="v1.0+v1.1")
   ContainerDb(db, "Database", "Microsoft SQL", "Holds product, order and invoice information")
   Container(archive, "Archive", "Audit logging", "Stores 5 years", $tags="backup")
   Rel(user, spa, "Uses", "https")
   Rel(spa, api, "Uses", "https")
   Rel_R(api, db, "Reads/Writes")
   Rel(admin, spaAdmin, "Uses", "https")
   Rel(spaAdmin, api, "Uses", "https")
   Rel_L(api, archive, "Writes", "messages", $tags="backup")
   SHOW_LEGEND()

a3m:

.. uml::

   !include <C4/C4_Container>

   Person(archivist1, "Digital Archivist 1")
   Person(archivist2, "Digital Archivist 2")
   System(a3m, "a3m", $type="a3m client")
   System(a3md, "a3md", $type="a3m server")
   Rel(archivist1, a3m, "Uses", "CLI")
   Rel(archivist2, a3md, "Uses", "HTTPS")
   Rel(a3m, a3md, "Uses", "HTTPS")
   SHOW_LEGEND()
