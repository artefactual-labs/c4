===
a3m
===

.. uml::

    @startuml
    !theme spacelab
    !include <C4/C4_Container>
    Person(archivist, "Digital Archivist", "A digital archivist utilizing a3m manages, preserves, and curates digital collections, ensuring their long-term accessibility and integrity through systematic archival processes and state-of-the-art digital preservation techniques.")
    System_Boundary(a3m, "a3m") {
        Container(a3m_client, "Client", "Python", "The client can operate as a command-line interface or a gRPC client over the wire.")
        Container(a3m_api, "gRPC API", "Python", "The gRPC server is a core component of the a3m server, providing processing status details and basic actions such as transfer submission.")
        Container(a3m_engine, "Workflow engine", "Python", "The workflow engine is a core component that orchestrates the tasks needed during processing by looking up the workflow document.")
        Container(a3m_workflow, "Workflow document", "JSON-encoded DSL", "It describes the processing steps.")
        Container(a3m_pool, "Thread pool", "Python", "It maintains a pool of system threads used to execute the tasks defined in the workflow document.")
        Container(a3m_client_modules, "Client modules", "Python", "Executable modules, e.g. file format identification, normalization, storage, etc...")
        ContainerDb(a3m_db, "Database", "SQLite", "The database is used to store processing state and information about the packages.")
    }
    System_Ext(blobstore, "S3", "The blobstore used to store AIPs. It can be configured to notify other systems for further work, e.g. reporting.")
    Rel(archivist, a3m_client, "Uses")
    Rel(a3m_client, a3m_api, "Uses", "gRPC")
    Rel(a3m_api, a3m_engine, "Uses", "Internal")
    Rel_Left(a3m_engine, a3m_workflow, "Reads workflow from")
    Rel_Neighbor(a3m_engine, a3m_pool, "Runs tasks with")
    Rel_Neighbor(a3m_engine, a3m_db, "Reads and writes to")
    Rel(a3m_client_modules, a3m_db, "Reads and writes to")
    Rel(a3m_pool, a3m_client_modules, "Executes")
    Rel(a3m_client_modules, blobstore, "Sends AIPs")
    SHOW_LEGEND()
    @enduml
