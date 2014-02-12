# Introduction

The **Library Service Ontology** is an Ontology to define a classification of
conventional services provided by libraries. The Ontology is related to the
[GoodRelations Ontology], to the [Service Ontology], to the [Document Service
ontology] and to the [vCard Ontology].  The current version of this ontology is
a preliminary draft as part of a Bachelor Thesis.  This is Version {VERSION},
last modified at {GIT_REVISION_DATE}.

[GoodRelations Ontology]: http://www.heppnetz.de/projects/goodrelations/
[Service Ontology]: http://purl.org/ontology/service
[Document Service ontology]: http://purl.org/ontology/dso
[vCard Ontology]: http://www.w3.org/TR/vcard-rdf/

# Namespaces and Ontology

The URI namespace of the Library Service Ontology is
<http://purl.org/ontology/libso#>.  The namespace prefix `lso` is recommended.
The URI of this ontology as a whole is <http://purl.org/ontology/libso>.

The following namespace prefixes are used to refer to related ontologies:

    @prefix a: <http://protege.stanford.edu/system#> .
    @prefix dct: <http://purl.org/dc/terms/> .
    @prefix dcterms: <http://purl.org/dc/terms/> .
    @prefix dso: <http://purl.org/ontology/dso#> .
    @prefix foaf: <http://xmlns.com/foaf/0.1/> .
    @prefix geo: <http://www.w3.org/2003/01/geo/wgs84_pos#> .
    @prefix gr: <http://purl.org/goodrelations/v1#> .
    @prefix lso: <http://purl.org/ontology/libso#> .
    @prefix org: <http://www.w3.org/ns/org#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .
    @prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
    @prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
    @prefix s: <http://schema.org/> .
    @prefix schema: <http://schema.org/> .
    @prefix service: <http://purl.org/ontology/service#> .
    @prefix vann: <http://purl.org/vocab/vann/> .
    @prefix vcard: <http://www.w3.org/2006/vcard/ns#> .
    @prefix voaf: <http://purl.org/vocommons/voaf#> .
    @prefix xml: <http://www.w3.org/XML/1998/namespace> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

The Library Service Ontology is defined in RDF/Turtle as following:

    @prefix a: <http://protege.stanford.edu/system#> .
    @prefix dct: <http://purl.org/dc/terms/> .
    @prefix vann: <http://purl.org/vocab/vann/> .
    @prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
    @prefix voaf: <http://purl.org/vocommons/voaf#> .
    @prefix owl: <http://www.w3.org/2002/07/owl#> .

    <http://purl.org/ontology/libso> a voaf:Vocabulary,
        owl:Ontology ;
        dct:creator "Matthias Letsch" ;
        dct:description "An Ontology to define a classification of conventional services provided by libraries." ;
        dct:modified "{GIT_REVISION_DATE}"^^xsd:date ;
        dct:title "Library [Service Ontology]"@en ;
        vann:preferredNamespacePrefix "lso" ;
        vann:preferredNamespaceUri "http://purl.org/ontology/libso#" ;
        owl:versionInfo "{VERSION}" .

# Overview

The ontology defines the core class [LibraryService] representing the set of
possible services provided by libraries. To connect the LSO to existing
Vocabularies, [LibraryService] is a subclass of [Service] as defined in the
[Service Ontology]. The possible services are divided into local Services
(Class [Local]) and web based Services (Class [WebBased]) due to describe their
specific access options. To link the services to providing libraries, the Class
[ServiceProvider] and the inverse properties [provides] and [providedBy] as
defined in the Service Ontology are used. These properties are automatically
inherited in any subclass of [Service]. The Library Service Ontology also
provides terms for describing contact options to the staff, opening times and
price specifications by resorting to selected properties and classes from the
[vCard Ontology] and the [GoodRelations Ontology].

[Service]: http://purl.org/ontology/service#Service
[provides]: http://purl.org/ontology/service#provides
[providedBy]: http://purl.org/ontology/service#providedBy

[LibraryService]: #
[Local]: #
[Webbased]: #

# Original Concepts

## Classes

A library service is a kind of service provided by a library or a related
Institution. The core class is lso:LibraryService. Each instance of
lso:LibraryService is also an instance of service:Service, gr:ProductOrService
or dctype:Service. For some possible connections to a Service also see the
[Service Ontology]. Each Service can be connected to a staff contact option via
[vCard Ontology] terms. Each local Service can be connected to an opening time
specification via GoodRelations Ontology terms. Each web based Service must
have an URI for the access. Some services can have price specifications via
GoodRelations Ontology terms or other terms of use via lso:Condition. Some of
the classes are re-used classes from the [Document Service Ontology] in order
to define the services without generating redundant vocabulary.

    lso:LibraryService a rdfs:Class ;
        rdfs:label "Bibliotheksdienstleistung"@de, "Library Service"@en ;
        rdfs:comment "A kind of service provided by a library or a related Institution." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf service:Service ;
        a:role "abstract" .

**Components of Services:** A subservice is a single component of a
higher-level service.

    lso:SubService a rdfs:Class ;
        rdfs:label "Dienstleistungsbestandteil"@de, "Service Component"@en ;
        rdfs:comment "Defines a single component of a higher-level service" ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LibraryService .

**Local Services:** A local service is a kind of service that is offered on
site at the library.  Local services can have an opening hour specification and
several contact options to the staff. Some of them, e.g. interlibrary loans,
also can have price specifications.

    lso:Local a rdfs:Class ;
        rdfs:label "Lokale Dienstleistung"@de, "Local Service"@en ;
        rdfs:comment "A kind of service that is offered on site at the library." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LibraryService .

**Local Services for providing collection usage:** A local usage service is a
kind of service provided to take use of the library’s media collection.

    lso:LocalUsage a rdfs:Class ;
        rdfs:label "Lokale Bestandsbenutzung"@de, "Local Usage Service"@en ;
        rdfs:comment "A kind of service provided to take use of the library’s media collection." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:Local ;
        owl:sameAs dso:documentService .

**Loan:** A loan is a typical library loan service. The class dso:loan is part
of the [Document Service Ontology].

    dso:loan a rdfs:Class ;
        rdfs:label "Fernleihe"@de, "Interloan"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/dso> ;
        rdfs:subClassOf dso:DocumentService, lso:LocalUsage .

**Interlibrary Loan:** An interlibrary loan is a typical library service to
provide access to physical documents from other libraries. The class
dso:interloan is part of the Document Service ontology.

    dso:InterLoan a rdfs:Class ;
        rdfs:label "Fernleihe"@de, "Interloan"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/dso> ;
        rdfs:subClassOf dso:DocumentService,
        lso:LocalUsage .

**Research Station:** A research station is a PC-Station provided for research
within the library’s media collection.

    lso:ResearchStation a rdfs:Class ;
        rdfs:label "Rechercheplatz"@de, "Research Station"@en ;
        rdfs:comment "A PC-Station provided for research within the library’s media collection." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LocalUsage .

**Presentation:** A Presentation is a service to provide space to use the media
collection on site at the library, e.g. in a reading room.

    dso:Presentation a rdfs:Class ;
        rdfs:label "Präsenzansicht"@de, "Presentation"@en ;
        rdfs:comment "A service to provide space to use the media collection on site at the library, e.g. in a reading room." ;
        rdfs:isDefinedBy <http://purl.org/ontology/dso> ;
        rdfs:subClassOf dso:documentService, lso:LocalUSage .

**Local Services for Information Transfer:** A local information service is a
kind of ser- vice provided to inform the library users on site in the library.

    lso:LocalInformation a rdfs:Class ;
        rdfs:label "Lokale Informationsvermittlung"@de, "Local Information Service"@en ;
        rdfs:comment "A kind of service provided to inform the library users on site in the library." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:Local .

**Information Counter:** An information Counter service is a service provided
to inform the library users at a service counter.

    lso:InformationCounter a rdfs:Class ;
        rdfs:label "Informationstheke"@de, "Information Counter"@en ;
        rdfs:comment "A service provided to inform the library users at a service counter." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LocalInformation .

**Library Tour:** A library tour is a service provided to guide the users
through the library building and to show them the potential uses.

    lso:LibraryTour a rdfs:Class ;
        rdfs:label "Bibliotheksführung"@de, "Library Tour"@en ;
        rdfs:comment "A service provided to guide the users through the library building and to show them the potential uses." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LocalInformation .

**User Training:** User training is a service provided to train the users in
research and use of the library’s media collection.

    lso:UserTraining a rdfs:Class ;
        rdfs:label "Nutzerschulung"@de, "User Training"@en ;
        rdfs:comment "A service provided to train the users in research and use of the library’s media collection." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LocalInformation .

**Registration:** A registration is an action to register a person as a library
user and inform it about usage opportunities and conditions.

    lso:Registration a rdfs:Class ;
        rdfs:label "Nutzeranmeldung"@de, "User Registration"@en ;
        rdfs:comment "An action to register a person as a library user and inform it about usage opportunities and conditions." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LocalInformation .

**Local Services for providing work space and aids:** A local work service is a
service for providing working space and opportunities to the users.

    lso:LocalWork a rdfs:Class ;
        rdfs:label "Lokales Arbeiten"@de, "Local Work"@en ;
        rdfs:comment "A service for providing working space and opportunities to the users." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:Local .

**Copier Or Scanner:** A copier or a scanner is a service provided to enable
users making personal copies or scans of documents.

    lso:CopierOrScanner a rdfs:Class ;
        rdfs:label "Kopierer oder Scanner"@de, "Copier or Scanner"@en ;
        rdfs:comment "A service provided to enable users making personal copies or scans of documents." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LocalWork .

**Black and white Copier**

    lso:CopierBlack a rdfs:Class ;
        rdfs:label "Schwarz-Weiß-Kopierer"@de, "Black and White Copier"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:CopierOrScanner .

**Color Copier**

    lso:CopierColor a rdfs:Class ;
        rdfs:label "Farbkopierer"@de, "Color Copier"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:CopierOrScanner .

**Scanner Only (Digitization)**

    dso:Digitization a rdfs:Class ;
        rdfs:label "Scanner"@en ;
        a:role "concrete" ;
        rdfs:isDefinedBy <http://purl.org/ontology/dso> ;
        rdfs:subClassOf lso:CopierOrScanner .

**Working Space for Groups:** A group work space is a service to provide
working space for groups of users.

    lso:GroupWorkSpace a rdfs:Class ;
        rdfs:label "Gruppenarbeitsraum"@de, "Group Work Room"@en ;
        rdfs:comment "A service to provide working space for groups of users." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LocalWork .

**Individual Work Space:** An individual work space is a service to provide the
opportunity for individual work for a single user.

    lso:IndividualWorkSpace a rdfs:Class ;
        rdfs:label "Einzelarbeitsplatz"@de, "Individual Work Space"@en ;
        rdfs:comment "A service to provide the opportunity for individual work for a single user." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LocalWork .

**PC Work Station:** A PC work station is a service to provide the opportunity to do work on a PC.

    lso:PCWorkStation a rdfs:Class ;
        rdfs:label "PC-Arbeitsplatz"@de, "PC Work Station"@en ;
        rdfs:comment "A service to provide the opportunity to do work on a PC." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LocalWork .

**Photo Service:** A photo service is a service provided to generate photographs for the users.

    lso:PhotoService a rdfs:Class ;
        rdfs:label "Fotodienst"@de, "Photo Service"@en ;
        rdfs:comment "a service provided to generate photographs for the users." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LocalWork .

**Web Based Services:** A web based service is a kind of online service provided on the library’s website.

    lso:WebBased a rdfs:Class ;
        rdfs:label "Internetbasierte Dienstleistung"@de, "Web Based Service"@en ;
        rdfs:comment "A kind of online service provided on the library’s website."
        ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:LibraryService .

**Web Based Services for Providing Collection Usage:** A web based usage
service is a kind of online service provided to gain access to parts of the
media collection on the web.

    lso:WebBasedUsage a rdfs:Class ;
        rdfs:label "Internetbasierte Bestandsbenutzung"@de,
            "Web Based Usage Service"@en ;
        rdfs:comment "A kind of online service provided to gain access to parts of the media collection on the web." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:WebBased .

**Catalogue**

    lso:Catalogue a rdfs:Class ;
        rdfs:label "Katalog"@de, "Catalogue"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:WebBasedUsage .

**Database**

    lso:Database a rdfs:Class ;
        rdfs:label "Datenbank"@de, "Database"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:WebBasedUsage .

**Open Access:** The Open Access service class is part of the Document Service
Ontology.  It implies to free accessibility of a document without any
restrictions by the service provider.

    dso:OpenAccess a rdfs:Class ;
        rdfs:label "Open Access"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/dso> ;
        rdfs:subClassOf dso:DocumentService,
        lso:WebBasedUsage .

**Recommendation:** A recommendation service provides the ability for the user
to issue a purchase recommendation.

    lso:Recommendation a rdfs:Class ;
        rdfs:label "Anschaffungsempfehlung"@en, "Purchase Recommendation"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:WebBasedUsage .

**Web Based Services for Information Transfer:** A web based information
service is a kind of online service provided to inform the users on the web via
chat, email or online tutorials.

    lso:WebBasedInformation a rdfs:Class ;
        rdfs:label "Internetbasierter Auskunftsdienst"@de,
            "Web Based Information Service"@en ;
        rdfs:comment "a kind of online service provided to inform the users on the web." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:WebBased .

**Online Information**

    lso:OnlineInformation a rdfs:Class ;
        rdfs:label "Internetbasierter Auskunftsdienst"@de, "Online Information"@en ;
        rdfs:comment "a kind of online service provided to inform the users on the web via chat or email etc." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:WebBasedInformation .

## Adjusted classes from related ontologies

The Library Service classes can be linked to other kinds of classes to express certain
relations. Where possible, use is made of existing ontologies in order to make certain
statements without generating redundant vocabulary.

**Condition:** The Condition class defines terms of use for a service, e.g.
price specifications or periods.

    lso:Condition a rdfs:Class ;
        rdfs:label "Nutzungskondition"@de, "Condition"@en ;
        rdfs:comment "Defines the terms of use for a service." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        owl:sameAs service:ServiceLimitation .

**Point Of Service:** The Point of Service class defines a physical site where
a local service is available.

    lso:PointOfService a rdfs:Class ;
        rdfs:label "Servicepunkt"@de, "Point of Service"@en ;
        rdfs:comment "defines a physical site where a local service is available." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf org:OrganizationalUnit .

**Point Of Service: Organizational Unit:** The POS Unit Class defines an
organizational unit as a point of service.

    lso:POSUnit a rdfs:Class ;
        rdfs:label "Teilorganisation als Servicepunkt"@de,
            "Organizational Unit as Point Of Service"@en ;
        rdfs:comment "defines an organizational unit as a physical site where a local service is available." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:PointOfService,
        org:OrganizationalUnit .

**Point Of Service:** Building: The POS Building Class defines a building as a
point of service.

    lso:POSBuilding a rdfs:Class ;
        rdfs:label "Gebäude als Servicepunkt"@de, "Building as Point Of Service"@en ;
        rdfs:comment "defines a building as a physical site where a local service is available." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:PointOfService,
        org:OrganizationalUnit .

**Point Of Service:** Department: The POS Department Class defines a department
within an organizational unit or a building as a point of service.

    lso:POSDepartment a rdfs:Class ;
        rdfs:label "Abteilung als Servicepunkt"@de, "Department as Point Of Service"@en ;
        rdfs:comment "defines a department as a physical site where a local service is available." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:PointOfService,
        org:OrganizationalUnit .

**Licence:** The Licence class defines conditions for access to databases given
by licenses through predefined Instances.

    lso:Licence a rdfs:Class ;
        rdfs:label "Lizenz"@de, "Licence"@en ;
        rdfs:comment "class defines conditions for access to databases given by licenses." ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:subClassOf lso:Condition .

**Predefined Instances:**

**Licence: Free access**

        lso:Free a lso:Licence ;
        rdfs:Label "Frei im Web verfügbar"@de, "Free Online Access"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> .

**Licence: External Access for registered Users**

    lso:ExternalAccess a lso:Licence ;
        rdfs:Label "Externer Zugang für angemeldete Nutzer"@de,
            "External Access for registered Users"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> .

**Licence: National Licence**

    lso:NationalLicence a lso:Licence ;
        rdfs:Label "Nationallizenz"@de, "National Licence"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> .

**Licence: Single User**

    lso:SingleUser a lso:Licence ;
        rdfs:Label "Einzelplatzversion"@de, "Sinlge User Version"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> .

**Licence: Pay Per Use**

    lso:PayPerUse a lso:Licence ;
        rdfs:Label "Kostenpflichtiges Angebot"@de, "Paid Offer"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> .

## Properties

**Has Point of Service:** This property is used to link local services to a
physical point of service. It is only usable in connection with service
entities of a lso:Local subclass (see rdfs:domain).

    lso:hasPointOfService a rdf:Property ;
        rdfs:label "verfügbar am Standort"@de, "has point of service"@en ;
        rdfs:domain lso:Local ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:range lso:PointOfService .

**Has Access URL:** This property is used to define an URL for the access to a
web based Service. It is only usable in connection with service entities of a
lso:WebBased subclass (see rdfs:domain).

    lso:hasAccessURL a rdf:Property ;
        rdfs:label "Zugang über URL"@de, "has access URL"@en ;
        rdfs:domain lso:WebBased ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:range rdfs:Literal .

**Has Optional Web Access:** This property is used to define an optional web
access to a local service in principle.

    lso:hasOptionalWebAccess a rdf:Property ;
        rdfs:label "Alternativer Internetzugang"@de, "has optional web access"@en ;
        rdfs:domain lso:Local ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:range lso:WebBased .

**Has Condition:** This property is used to define one or more condition terms for the use
of a certain service.

    lso:hasCondition a rdf:Property ;
        rdfs:label "Nutzungskonditionen"@de, "has condition"@en ;
        rdfs:domain lso:LibraryService ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:range lso:Condition .

**Related Document:** This property is used to link a condition of
lso:Condition to an URL of a related document.

    lso:relatedDocument a rdfs:Property ;
        rdfs:label "Zugehöriges Dokument"@de,
        "related Document"@en ;
        rdfs:domain rdfs:Condition ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:range rdfs:Literal .

**Has Period Time:** This property is used to define a period for a Condition of lso:Condition for a certain service.

    lso:hasPeriodTime a rdfs:Property ;
        rdfs:label "zugehörige Frist"@de, "has Period Time"@en ;
        rdfs:domain lso:Condition ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:range rdfs:Literal .

**Has Licence:** This property is used to link a web based service of lso:WebBased
to a licence of lso:Licence.

    lso:hasLicence a rdfs:Property ;
        rdfs:label "unter Lizenz"@de,"has Licence"@en ;
        rdfs:domain lso:WebBasedUsage ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:range lso:Licence .

**Staff Contact:** This property is used to link a service to a responsible person or depart-
ment of vcard:Individual or vcard:Organization.

    lso:staffContact a rdfs:Property ;
        rdfs:label "Kontakt zum Personal"@de, "staff Contact"@en ;
        rdfs:domain lso:LibraryService ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:range vcard:Individual,
        vcard:Organization .

**Floor:** This property is used to define a floor for a service point of lso:POSDepartment.

    lso:floor a rdfs:Property ;
        rdfs:label "Etage oder Ebene"@de, "floor"@en ;
        rdfs:domain lso:POSDepartment ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:range rdfs:Literal .

**Room:** This property is used to define a room number for a service point of lso:POSDepartment.

    lso:room a rdfs:Property ;
        rdfs:label "Zimmernummer"@de,
        "room number"@en ;
        rdfs:domain lso:POSDepartment ;
        rdfs:isDefinedBy <http://purl.org/ontology/libso> ;
        rdfs:range rdfs:Literal .

# Parts from related Ontologies

## Classes from the Service Ontology

**Service:** The Service Provider class is part of the [Service Ontology]. A
service is some action that is done for someone.

    service:Service a owl:Class ;
        rdfs:label "Service"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/service> ;
        rdfs:seeAlso schema:Product,
        schema:Service ;
        rdfs:subClassOf dct:Service, gr:ProductOrService .

**Service Provider:** The Service Provider class is part of the Service
Ontology. A service provider is an entity that is responsible for providing a
Service. In the present case, the entity is primarily a library providing one
or more of the formerly defined library services.

    service:ServiceProvider a rdfs:Class ;
        rdfs:label "ServiceProvider"@en ;
        rdfs:isDefinedBy <http://purl.org/ontology/service> ;
        rdfs:seeAlso dct:agent,
            gr:BusinessEntity,
            schema:Organization,
            schema:person,
            foaf:agent .

## Classes from GoodRelations Ontology

**Opening Hours Specification:** The Opening Hours Specification class from the
GoodRelations Ontology is used to define opening times for local services. It
is linked to the Day of Week class in order to define the days on which a
service is accessible.

    gr:OpeningHoursSpecification a rdfs:Class ;
        rdfs:label "Opening hours specification"@en ;
        rdfs:comment "This is a conceptual entity that holds together all information about the opening hours on a given day (gr:DayOfWeek)." ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1#> .

**Day of Week**

    gr:DayOfWeek a rdfs:Class ;
        rdfs:label "Day of Week"@en ;
        rdfs:comment "The day of the week, used to specify to which day the opening hours of a gr:OpeningHoursSpecification refer." ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1#> .

**Day of Week: Predefined Instances**

    gr:Monday a gr:DayOfWeek .
    gr:Tuesday a gr:DayOfWeek .
    gr:Wednesday a gr:DayOfWeek .
    gr:Thursday a gr:DayOfWeek .
    gr:Friday a gr:DayOfWeek .
    gr:Saturday a gr:DayOfWeek .
    gr:Sunday a gr:DayOfWeek .

**Unit Price Specification:** The Unit Price Specification class from the Good
Relations Ontology is used to define the price for the use of a certain
service.

    gr:UnitPriceSpecification a rdfs:Class ;
        rdfs:label "Unit price specification"@en ;
        rdfs:comment """A unit price specification is a conceptual entity that 
            specifies the price asked for a given gr:Offering by the respective gr:Business
            Entity. An offering may be linked to multiple unit price specifications that
            specify alternative prices for non-overlapping sets of conditions (e.g. 
            quantities or sales regions) or with differing validity periods...""" ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1#> .

## Classes from the vCard Ontology

**Individual:** The Individual Class is part of the vCard Vocabulary. In the
present case, it is used to represent a contactable person responsible for a
certain service.

    vcard:Individual a owl:Class ;
        rdfs:label "Individual"^^xsd:string ;
        rdfs:comment "An object representing a single person or entity"^^xsd:string ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:subClassOf vcard:Kind ;
        owl:disjointWith vcard:Location,
        vcard:Organization .

**Organization:** The Organization Class is part of the vCard Vocabulary. In the present
case, it is used to represent a contactable department responsible for a certain service.

    vcard:Organization a owl:Class ;
        rdfs:label "Organization"^^xsd:string ;
        rdfs:comment """An object representing an organization. An organization
            is a single entity, and might represent a business or government, a department
            or division within a business or government, a club, an association, or the
            like."""^^xsd:string;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:subClassOf vcard:Kind .

**Email:** The Email Class is part of the vCard Vocabulary. In the present case, it is used to
link an email address to a person or department responsible for a certain service.

    vcard:Email a owl:Class ;
        rdfs:label "Email"^^xsd:string ;
        rdfs:comment """To specify the electronic mail address for communication
            with the object the vCard represents. Use the hasEmail object property."""^^xsd:string ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        owl:deprecated true .

**Voice:** The Voice Class is part of the vCard Vocabulary. In the present case, it is used to
link a telephone number to a person or department responsible for a certain service.

    vcard:Voice a owl:Class ;
    rdfs:label "Voice"^^xsd:string ;
    rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
    rdfs:subClassOf vcard:TelephoneType .

**Fax:** The Fax Class is part of the vCard Vocabulary. In the present case, it is used to link
a fax number to a person or department responsible for a certain service.

    vcard:Fax a owl:Class ;
        rdfs:label "Fax"^^xsd:string ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:subClassOf vcard:TelephoneType .

**Address:** The Address Class is part of the vCard Vocabulary. In the present
case, the Address Class is used to define a address to a physical site for any
service point of lso:PointOfService.

    vcard:Address a owl:Class ;
        rdfs:label "Address"^^xsd:string ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:comment "To specify the components of the delivery address for the object"^^xsd:string .

## Location Class from the Basic Geo Vocabulary

**Location:** The Location Class from the Basic Geo Vocabulary is used to
define coordinates for service points of lso:PointOfService.

    geo:Location a rdfs:Class .

## Classes from the Organization Ontology

**Organization:** The Organization Class from the Organization Ontology is used
to define service providers of service:ServiceProvider as Organizations.

    org:Organization a rdfs:Class, owl:Class ;
        rdfs:label "Organization"@en ;
        rdfs:comment """Represents a collection of people organized together into a
            community or other social, commercial or political structure. The group has
            some common purpose or reason for existence which goes beyond the set of
            people belonging to it and can act as an Agent. Organizations are often 
            decomposable into hierarchical structures. It is recommended that SKOS lexical labels
            should be used to label the Organization. In particular `skos:prefLabel` for
            the primary (possibly legally recognized name), `skos:altLabel` for alternative
            names (trading names, colloquial names) and `skos:notation` to denote a
            code from a code list. Alternative names: _Collective_ _Body_ _Org_ _Group_"""@en ;
        rdfs:isDefinedBy <http://www.w3.org/ns/org> ;
        rdfs:subClassOf foaf:Agent ;
        owl:equivalentClass foaf:Organization ;
        owl:hasKey ( org:identifier ) .

**Organizational Unit:** The Organizational Unit Class from the Organization
Ontology is used to define service points of lso:PointOfService as Units of
Instances of service:ServiceProvider.

    org:OrganizationalUnit a rdfs:Class, owl:Class ;
        rdfs:label "OrganizationalUnit"@en ;
        rdfs:comment """An Organization such as a University Support Unit which is
            part of some larger FormalOrganization and only has full recognition within
            the context of that FormalOrganization, it is not a Legal Entity in its own
            right. Units can be large and complex containing other Units and even
            FormalOrganizations. Alternative names: _OU_ _Unit_ _Department_"""@en ;
        rdfs:isDefinedBy <http://www.w3.org/ns/org> ;
        rdfs:subClassOf org:Organization .

**Site:** The Site Class from the Organization Ontology is used to represent a
physical site for any service point of lso:PointOfService.

    org:Site a rdfs:Class, owl:Class ;
        rdfs:label "Site"@en ;
        rdfs:comment """An office or other premise at which the organization is
            located. Many organizations are spread across multiple sites and many sites will
            host multiple locations. In most cases a Site will be a physical location.
            However, we don't exclude the possibility of non-physical sites such as a
            virtual office with an associated post box and phone reception service. 
            Extensions may provide subclasses to denote particular types of site."""@en ;
        rdfs:isDefinedBy <http://www.w3.org/ns/org> .

## Properties from the Service Ontology

The properties from the [Service Ontology] are used to link a
service:ServiceProvider to a lso:LibraryService.

**Provides**

    service:provides a owl:ObjectProperty ;
        rdfs:label "provides"@en ;
        rdfs:domain service:ServiceProvider ;
        rdfs:isDefinedBy <http://purl.org/ontology/service> ;
        rdfs:range service:Service ;
        owl:inverseOf service:providedBy .

**Provided By**

    service:providedBy a owl:ObjectProperty ;
        rdfs:label "providedBy"@en ;
        rdfs:domain service:Service ;
        rdfs:isDefinedBy <http://purl.org/ontology/service> ;
        rdfs:range service:ServiceProvider ;
        rdfs:seeAlso schema:provider ;
        owl:inverseOf service:provides .

## Properties from the GoodRelations Ontology

The Properties from the [GoodRelations Ontology] are used to define opening
hours for local services and any price specifications.

**Opening Hours Specification Properties:** The Opening Hours Specification
properties are used to define opening hours for local services. For an optimal
integration into the LSO vocabulary the domain of the
gr:hasOpeningHoursSpecification element has been modified slightly. Comments
are partially shortened compared to the original.

**Has Opening Hours Specification**

    gr:hasOpeningHoursSpecification a rdf:Property ;
        rdfs:label "has opening hours specification (0..*)"@en ;
        rdfs:comment "For use in LSO: This property links a lso:Local to a gr:OpeningHoursSpecification.",
            "This property links a gr:Location to a gr:OpeningHoursSpecification." ;
        rdfs:domain gr:Location,
        lso:Local,
        schema:Place ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1#> ;
        rdfs:range gr:OpeingHoursSpecification .

**Opens**

    gr:opens a rdf:Property ;
        rdfs:label "opens (1..1)"@en ;
        rdfs:comment "The opening hour of the gr:Location on the given gr:DayOf- Week..." ;
        rdfs:domain gr:OpeningHoursSpecification ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1#> ;
        rdfs:range xsd:time .

**Closes**

    gr:closes a rdf:Property ;
        rdfs:label "closes (1..1)"@en ;
        rdfs:comment "The closing hour of the gr:Location on the given gr:DayOfWeek..." ;
        rdfs:domain gr:OpeningHoursSpecification ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1#> ;
        rdfs:range xsd:time .
        
**Has Opening Hours Day of Week**

    gr:hasOpeningHoursDayOfWeek a rdf:Property ;
        rdfs:label "has opening hours day of week (1..*)"@en ;
        rdfs:comment "This specifies the gr:DayOfWeek to which the gr:OpeningHoursSpecification is related..." ;
        rdfs:domain gr:OpeningHoursSpecification ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1#> ;
        rdfs:range gr:DayOfWeek .

**Price Specification Properties:** These properties are used to define price
specifications for certain library services. For an optimal integration into
the LSO vocabulary the domain of the gr:hasPriceSpecification element has been
modified slightly. Comments are partially shortened compared to the original.

**Has Price Specification**

    gr:hasPriceSpecification a rdf:Property ;
        rdfs:label "has price specification (0..*)"@en ;
        rdfs:comment "For use in LSO: This property links a lso:LibraryService to a gr:PriceSpecification.",
        "This links a gr:Offering to a gr:PriceSpecification or specifications..." ;
        rdfs:domain gr:Offering,
        lso:LibraryService,
        schema:Offer ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1#> ;
        rdfs:range gr:PriceSpecification .

**Has Currency**

    gr:hasCurrency a rdf:Property ;
        rdfs:label "has currency (1..1)"@en ;
        rdfs:comment "The currency for all prices in the gr:PriceSpecification given using the ISO 4217 standard (3 characters)." ;
        rdfs:domain gr:PriceSpecification ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1#> ;
        rdfs:range xsd:string .

**Has Currency Value**

    gr:hasCurrencyValue a rdf:Property ;
        rdfs:label "has currency value (0..1)"@en ;
        rdfs:comment """This property specifies the amount of money for a price per
        unit, shipping charges, or payment charges. The currency and other relevant
        details are attached to the respective gr:PriceSpecification etc...""" ;
        rdfs:domain gr:PriceSpecification ;
        rdfs:isDefinedBy <http://purl.org/goodrelations/v1#> ;
        rdfs:range xsd:float .

## Properties from the vCard Ontology

The Properties from the vCard Vocabulary are used to define contact options to
persons and departments responsible for a service and address information to
service points.  Contact Properties: These properties are used to define
contact options.  Formatted Name: This property is used to give a name to an
individual person responsible for a service.

    vcard:fn a owl:DatatypeProperty ;
        rdfs:label "formatted name"^^xsd:string ;
        rdfs:comment "The formatted text corresponding to the name of the object" ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:range xsd:string .

**Organization Name:** This property is used to give a name to a department responsible for a service.

    vcard:organization-name a owl:DatatypeProperty ;
        rdfs:label "organization name"^^xsd:string ;
        rdfs:comment "To specify the organizational name associated with the object" ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:range xsd:string .

**Has Email:** This property is used to add an email address to a person or department.

    vcard:hasEmail a owl:ObjectProperty ;
        rdfs:label "has email"^^xsd:string ;
        rdfs:comment "To specify the electronic mail address for communication with the object"^^xsd:string ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:range vcard:Email .

**Has Telephone:** This property is used to add a telephone or fax number to a person or department.

    vcard:hasTelephone a owl:ObjectProperty ;
        rdfs:label "has telephone"^^xsd:string ;
        rdfs:comment "To specify the telephone number for telephony communication with the object"^^xsd:string ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        owl:equivalentProperty vcard:tel .

**Has Value:** This property is used to define a certain value for an email address, telephone or fax number

    vcard:hasValue a owl:ObjectProperty ;
        rdfs:label "has value"@en ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:comment "Used to indicate the resource value of an object property that requires property parameters"^^xsd:string .

Address Information Properties: These properties are used to define address
information to physical sites of service points.

**Has Address**

    vcard:hasAddress a owl:ObjectProperty ;
        rdfs:label "has address"^^xsd:string ;
        rdfs:comment "To specify the components of the delivery address for the object"^^xsd:string ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:range vcard:Address .

**Country Name**

    vcard:country-name a owl:DatatypeProperty ;
        rdfs:label "country name"^^xsd:string ;
        rdfs:comment "The country name associated with the address of the object" ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:range xsd:string .

**Locality**

    vcard:locality a owl:DatatypeProperty ;
        rdfs:label "locality"^^xsd:string ;
        rdfs:comment "The locality (e.g. city or town) associated with the address of the object" ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:range xsd:string .

**Postal Code**

    vcard:postal-code a owl:DatatypeProperty ;
        rdfs:label "postal code"^^xsd:string ;
        rdfs:comment "The postal code associated with the address of the object" ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:range xsd:string .

**Street Address**

    vcard:street-address a owl:DatatypeProperty ;
        rdfs:label "street address"^^xsd:string ;
        rdfs:comment "The street address associated with the address of the object" ;
        rdfs:isDefinedBy <http://www.w3.org/2006/vcard/ns> ;
        rdfs:range xsd:string .

## Properties from the Basic Geo Vocabulary

The properties from the Basic Geo Vocabulary are used to define coordinates for
a site of a service point.

**Location:** This property is used to link a site of a service point to
concrete coordinates.

    geo:location a rdfs:Property ;
        rdfs:domain org:Site ;
        rdfs:range geo:Location .

**Latitude**

    geo:lat a rdfs:Property ;
        rdfs:domain geo:Location ;
        rdfs:range rdfs:Literal .

**Longitude**

    geo:long a rdfs:Property ;
        rdfs:domain geo:Location ;
        rdfs:range rdfs:Literal .

## Properties from the Organization Ontology

The properties from the Organization Ontology are used to define the
relationships be- tween service points and service providers and to link them
to a physical Site.

**Has Unit**

    org:hasUnit a rdf:Property,
        owl:ObjectProperty ;
        rdfs:label "has Unit"@en ;
        rdfs:comment """Indicates a unit which is part of this Organization, e.g. a
            Department within a larger FormalOrganization. Inverse of `org:unitOf`."""@en ;
        rdfs:domain org:FormalOrganization ;
        rdfs:isDefinedBy <http://www.w3.org/ns/org> ;
        rdfs:range org:OrganizationalUnit ;
        rdfs:subPropertyOf org:hasSubOrganization .

**Unit Of**

    org:unitOf a rdf:Property,
        owl:ObjectProperty ;
        rdfs:label "unit Of"@en ;
        rdfs:comment """Indicates an Organization of which this Unit is a part, e.g.
        a Department within a larger FormalOrganization. This is the inverse of
        `org:hasUnit`."""@en ;
        rdfs:domain org:OrganizationalUnit ;
        rdfs:isDefinedBy <http://www.w3.org/ns/org> ;
        rdfs:range org:FormalOrganization ;
        rdfs:subPropertyOf org:subOrganizationOf .

**Has Site**

    org:hasSite a rdf:Property,
        owl:ObjectProperty ;
        rdfs:label "has site"@en ;
        rdfs:comment """Indicates a site at which the Organization has some presence
        even if only indirect (e.g. virtual office or a professional service which is
        acting as the registered address for a company). Inverse of `org:siteOf`."""@en ;
        rdfs:domain org:Organization ;
        rdfs:isDefinedBy <http://www.w3.org/ns/org> ;
        rdfs:range org:Site .

