---
stand_alone: true
docname: draft-iab-iotsi-workshop
cat: info
submissiontype: IETF
pi:
  compact: 'yes'
  text-list-symbols: o*+-
  subcompact: 'no'
  sortrefs: 'yes'
  symrefs: 'yes'
  strict: 'yes'
  toc: 'yes'
title: Report from the Internet of Things (IoT) Semantic Interoperability (IOTSI)
  Workshop 2016
abbrev: draft-iab-iotsi-workshop
date: 2017-08-28
author:
- ins: J. Jimenez
  name: Jaime Jimenez
  org: Ericsson
  email: jaime.jimenez@ericsson.com
- ins: H. Tschofenig
  name: Hannes Tschofenig
  org: ARM
  email: hannes.tschofenig@arm.com
- ins: D. Thaler
  name: Dave Thaler
  org: Microsoft
  email: dthaler@microsoft.com
informative:
  RFC3444:
  Allseen-Plugin:
    title: Using the AllJoyn Studio Extension
    author:
    - ins: B. Rockwell
      name: B. Rockwell
      org: ''
    date: 2016
  HATEOAS:
    title: Semantic Interoperability Requires Self-describing Interaction Models
      - HATEOAS for the Internet of Things
    author:
    - ins: M. Kovatsch
      name: M. Kovatsch
      org: ''
    date: 2016
    seriesinfo:
      Proceedings: of the IoT Semantic Interoperability Workshop 2016
  IOTSIAG:
    target: https://www.iab.org/activities/workshops/iotsi/agenda/
    title: IoT Workshop for Semantic Interoperability (IOTSI) - Agenda and Slides
    author:
    - org: IAB
    date: 2016
  IOTSIGIT:
    target: https://github.com/iotsi/iotsi
    title: Github Collaborative Repository
    author:
    - org: IOTSI
    date: 2016
  IOTSIWS:
    target: https://www.iab.org/activities/workshops/iotsi/
    title: IoT Workshop for Semantic Interoperability (IOTSI) 2016 - Main Page and
      Position Papers
    author:
    - org: IAB
    date: 2016
  LWM2M-Schema:
    title: OMA LWM2M XML Schema
    author:
    - org: OMA
    date: 2016
  OMA-Editor:
    title: OMA LWM2M Object and Resource Editor
    author:
    - org: OMA
    date: 2016
  OMNA:
    title: OMNA Lightweight M2M (LWM2M) Object & Resource Registry
    author:
    - org: OMA
    date: 2016
  PYANG:
    title: An extensible YANG validator and converter in python
    author:
    - ins: M. Bjorklund
      name: M. Bjorklund
      org: ''
    date: 2016
  UDI:
    title: Object Oriented Approach to IoT Interoperability
    author:
    - ins: M. Kohanim
      name: M. Kohanim
      org: ''
    date: 2016
    seriesinfo:
      Proceedings: of the IoT Workshop for Semantic Interoperability (IOTSI)
  nRF-Sniffer:
    title: nRF Sniffer - Smart/Bluetooth low energy packet sniffer
    author:
    - org: Nordic Semiconductor
    date: 2016
  AllJoynExplorer:
    title: AllJoyn Explorer
    author:
    - org: Microsoft
    date: 2016
  OpenDOF:
    target: https://opendof.org
    title: The OpenDOF Project
    author:
    - org: OpenDOF
    date: 2015

--- abstract


This document provides a summary of the 'Workshop on Internet of
Things (IoT) Semantic Interoperability (IOTSI)',
which took place in Santa Clara, CA, on March 17-18, 2016.  The main
goal of the workshop was to foster a discussion on the different
approaches used by companies and standards developing organizations
to accomplish interoperability at the application layer.  This report
summarizes the discussions and lists recommendations to the standards
community.  The views and positions in this report are those of the
workshop participants and do not necessarily reflect those of the
authors and the Internet Architecture Board (IAB), which organized
the workshop.

--- middle

# Introduction {#section-1}

The Internet Architecture Board (IAB) holds occasional workshops
designed to consider long-term issues and strategies for the
Internet, and to suggest future directions for the Internet
architecture.  The investigated topics often require coordinated
efforts of many organizations and industry bodies to improve an
identified problem.  One of the targets of the workshops is to
establish communication between relevant organizations, especially
when the topics are out of the scope for the Internet Engineering
Task Force (IETF).  This long-term planning function of the IAB is
complementary to the ongoing engineering efforts performed by working
groups of the IETF.

With the expansion of the Internet of Things (IoT), interoperability 
becomes more and more important. Standards-developing organizations 
have done a tremendous amount of work to standardize protocols to 
simplify implementation and to lower the cost of IoT products. As a 
result, new protocols were developed, existing protocols were combined 
in new ways, and lightweight profiles were defined.

At the application layer, interoperability is not yet mature; the 
work on data formats (in the form of data models and information 
models) has not seen the same level of consistency throughout various 
standardization groups. 

One common problem is the lack of an encoding-independent standardization 
of the information, the so-called information model. Another problem is 
the strong relationship with the underlying communication architecture, 
such as an RPC or a RESTful design. Furthermore, different groups develop 
similar concepts that only differ slightly, leading to interoperability 
problems. Finally, some groups favor different encodings for use with 
various application layer protocols.

Thus, the IAB decided to organize a workshop to reach out to relevant
stakeholders to explore the state-of-the-art and to identify
communality and gaps {{IOTSIAG}}, {{IOTSIWS}}. In particular, the IAB was
interested to learn about the following aspects:

* What is the state of the art in data and information models? What should 
  an information model look like?

* What is the role of formal languages, such as schema languages, in 
  describing information and data models?

* What is the role of metadata, which is attached to data to make it self-describing?

* How can we achieve interoperability when different organizations, companies 
  and individuals develop extensions?

* What is the experience with interworking various data models developed
  from different groups, or with data models that evolved over time?

* What functionality should online repositories for sharing schemas have?

* How can existing data models be mapped against each other to offer interworking?

* Is there room for harmonization, or are the use cases of different groups 
  and organizations so unique that there is no possibility for cooperation?

* How can organizations better work together to increase awareness and information sharing?

# Terminology {#section-2}

The first roadblock to semantic interoperability is the lack of a
common vocabulary to start the discussion.
{{RFC3444}} provides a starting point by separating conceptual models for designers,
or "information models", from concrete detailed definitions for implementers, or
"data models". There are concepts that are
undefined in that RFC and elsewhere, such as the interaction with the
resources of an endpoint, or "interaction model".  Therefore the three
"main" common models that were identified were:

{: hangIndent='3'}
Information Model
: An information model defines an environment at the highest level of abstraction, they
  express the desired functionality.
  They can be defined informally (e.g., in plain English) or more
  formally (e.g., UML, Entity-Relationship Diagrams, etc.).
  Implementation details are hidden.
{: vspace='0'}

{: hangIndent='3'}
Data Model
: A data model defines concrete data representations at a lower level of
  abstraction, including implementation and protocol-specific details.
  Some examples are: SNMP Management Information
  Base (MIB) modules, W3C Thing Description (TD) Things, YANG models, LWM2M
  Schemas, OCF Schemas and so on.
{: vspace='0'}

{: hangIndent='3'}
Interaction Model
: An interaction model defines how data is accessed and retrieved from the endpoints,
  being therefore tied to the specific
  communication pattern that the system has (e.g., REST methods,
  Publish/Subscribe operations, or RPC calls).
{: vspace='0'}

Another identified terminology issue is the semantic meaning overload
that some terms have.  The meaning can vary depending on the context in which the
term is used.  Some examples of such terms are: semantics, models,
encoding, serialization format, media types or encoding types.  Due
to time constraints, no concrete terminology was agreed upon, but
work will continue within each organization to create various
terminology documents.  The participants agreed to set up a github repository
{{IOTSIGIT}} for sharing information.

# Architecture {#section-3}

Various architectures follow different design patterns. Some are REST-
oriented with a limited set of standard methods to find and manipulate resources on
endpoints.  Others are RPC-like, with a rich set of methods that may vary by 
resource type. Still others are more
Publish/Subscribe-oriented that focus on the flow of information
based on the topics of the information that is being shared.  

TODO: The 3 items below need to be rewritten, perhaps as normal paragraphs,
as they're hard to follow and it's unclear what the purpose of the "list" is.

{: hangIndent='3'}
Thing-hub-cloud
: Things talk to some type of hub or gateway, which talks back to them and
  to the cloud.  There is a spectrum of emphasis on the hub vs. the
  cloud.  For some, the hub is simply an IP router that connects different link
  layer technologies, but for others it
  is a critical place for maintaining local control.
{: vspace='0'}

{: hangIndent='3'}
Meta Thing
: Some things are actually a composite of other things, like an alarm composed
  of a clock, lights, and thermostat.
{: vspace='0'}

{: hangIndent='3'}
Nearby things
: Some things may be geospatially related even if they
  are not on the same network or within the same administrative
  domain.
{: vspace='0'}

Current data models and definitions for "things" often focus on
defining actual physical devices and representing their state.  That
focus should perhaps be shifted into a more holistic or user-oriented
perspective, defining abstract concepts as well.  On the other hand, a lot
of focus is placed on human interaction with physical devices, while
IoT may often be more focussed on interaction between "things" instead.

Those things should be designed to be multi-purpose, keeping in
mind that solutions should be open-ended to facilitate new usages and
new future domains of operation. This pattern has already happened, where
devices that were intended for one purpose ended up being used for a
different one given the right context (e.g., a smart phone LED light
was used as a heartrate monitor).

# What Problems to Solve {#section-4}

The participants agreed that there is not simply a single problem to be solved, but
rather a range. At least the following problems were discussed:

* Formal Languages for Documentation Purposes

To simplify review and publication, standardization organizations are in 
need of a more formal description of their information and data models.
For example, the Open Mobile Alliance (OMA)
used an XML schema {{LWM2M-Schema}} to describe their object
definitions (i.e., data model) and the actual object definitions are available
for download as XML instance documents.  These XML
documents offer an alternative way of describing objects compared to
the tabular representation found in the specification itself.  The
XML files of standardized objects are available for download at
{{OMNA}}.  Furthermore, a tool is offered to define new objects and
resources.  The online editor tool can be found at {{OMA-Editor}}.

TODO: It might appear unfair to just call out a single organization above, which
implies that mechanism is somehow better than the other organizations present
that have other formal languages, especially when the workshop mentioned
multiple.  W3C uses RDF, OCF uses JSON+RAML, AllSeen uses XML with a specific XSD, etc.
Should either use multiple examples, or no examples.

* Formal Languages for Code Generation

Code generation tools that use formal data and information modelling languages
are needed by developers. For example, the Allseen Visual Studio
Plugin {{Allseen-Plugin}} offers a wizard to generate code based on
the formal description of the data model.  Another example of a data
modelling language that can be used for code generation is YANG.  A
popular tool to help with code generation of YANG modules is pyang {{PYANG}}.
An example of a tool that can do code generation for different ecosystems is
OpenDOF {{OpenDOF}}. Use cases discussed for code generation included easing
development of server-side device functionality, clients, and compliance tests.

* Debugging Support

Debugging tools are needed that implement generic object browsers, which
use standard data models and/or retrieve formal language descriptions
from the devices themselves. As one example, the
NRF Bluetooth Smart sniffer from Nordic Semiconductor {{nRF-Sniffer}} can be
used to display services and characteristics defined by the Bluetooth SIG.
As another example, AllJoyn Explorer {{AllJoynExplorer}} can be used to browse
and interact with any resource exposed by an AllJoyn device, including both 
standard and vendor-defined data models, by retrieving the formal descriptions
from the device at runtime.

* Translation

Gateways and other similar devices need to dynamically
translate (or map) one data model to another one.  An example of this
idea can be found in {{UDI}}.

TODO: Probably need to list other examples discussed in the workshop as well.

* Runtime Discovery

Allow IoT devices to exchange information, potentially along with the
data exchange, to discover meta-data about the data and, potentially,
even a self-describing interaction model.  An example of such an
approach has been shown with HATEOAS {{HATEOAS}}.

TODO: Probably need to list other examples discussed in the workshop as well.
For example, AllJoyn introspection.

# Translation {#section-5}

In an ideal world where organizations and companies cooperate and agree on a
single data model standard, there is no need for gateways that translate from one data model
to the other one. However, this is far from reality today, and there are many
proprietary data models in addition to the already standardized ones. There
are analogies with gateways back in the 1980s that were used to
translate between network layer protocols.  Eventually IP took over, providing
the necessary end-to-end interoperability at the network layer. Unfortunately,
the introduction of translation gateways that lead to the loss of expressiveness 
due to the translation between data models seems unavoidable.

TODO: add discussion of the "red star" diagram

TODO: add key point discussed that translation between two standard data models requires specific code,
it cannot be algorithmically derived based on the two formal descriptions.  It can only be
algorithmically done when the actual data model on one side is actually algorithmically derived
from the one on the other side.  This is called a "derived model".

Translation can happen in two flavours, namely:

a)  Translating formal descriptions between data models: a translation between data model
descriptions, such as translating a YANG model to a RAML/JSON model,
can be performed once such as during design time.
A single information model can be mapped to a number of different data models.
b)  Translating data between data models: this flavour implies doing translation at
runtime.

TODO: more info was summarized on the slides and in the notes about three types of
runtime interactions discussed in the papers (and at the workshop): 

In one sense, these distinctions affect when the relevant translation is
performed.  It can be done at "design time" when the information
model is done, or it can be done at runtime for a concrete data model
and it can be done depending on the actual serialization.

Yet another distinction will appear depending on the requirements
from the application protocols. RPC-style ones might require a
slightly different data model than RESTful ones for similar operations. For
example, SNMP-traps could be similar to CoAP-Observations but not
quite the same.  It is easier to translate between systems that
follow the same architecture/design pattern than across
architectures, and sometimes a full translation might not even be possible (e.g.,
stateless vs stateful systems).

# Dealing with change {#section-6}

A large part of the workshop was dedicated to the evolution of
devices and server side applications.  Multiple of the participating
groups have defined data formats for data representation.
Interactions between devices and services and how their relationship
evolves over time is more related to their respective interaction models.

The workshop discussed various approaches to dealing with change.  In the most primitive case, a
developer might use a description of an API and implement whichever
are the protocol steps.  In some cases the information model itself
can be used to generate some of the code stubs.  Subsequent changes to an API
require changes on the clients to upgrade to the new version, which
requires some development of new code to satisfy the needs of the new
API.

These interactions could be made machine-understandable in the first place,
enabling for changes to happen at runtime.
In that scenario, a machine client could discover the possible interactions with a
service, adapting to changes as they occur without specific code
being developed to adapt to them.

The challenge seems to be to define the human-readable parts as
machine-readable.  Machine-readable languages require a shared vocabulary to
give meaning to the tags.

These types of interactions are often based on the REST architectural
style. Its principle is that a device or endpoint only needs a
single entry point with a host providing descriptions of the API
in-band by means of web links and forms.

By defining IoT-specific relation types, it is possible to drive
interactions through links instead of hardcoding URIs into the
client, thus making the system flexible enough for later changes.
The definition of the basic hypermedia formats for IoT is still work
in progress, however some of the existing mechanisms can be reused,
such as resource discovery, forms, or links.

# Security Considerations {#section-7}

There were two types of security considerations discussed: use of formal data 
models for security configuration, and security of data and data models in general.

It was observed that the security assumptions and configuration, or "security model", varies by ecosystem today,
making the job of a translator difficult.  For example, the types of security
principals (e.g., user vs. device vs. application), the use of ACLs vs. capabilities,
and what types of policies can be expressed, all vary by ecosystem.  As a result,
the security model architecture generally dictates where translation can be done.

One approach discussed was whether two endpoints might be able to use some overlay
security model, across a translator between two ecosystems, which only works if
the two endpoints agree on a common data model for their communication.  Another approach
discussed was simply having a translator act as a trusted intermediary, which allows
the translator to be able to translate between different data models.

One suggestion discussed was potentially adding metadata into either the
formal data model language, or accompanying the data values over the wire, tagging
the data with privacy levels.  However, sometimes even the privacy level of information
might itself be sensitive.  Still, it was observed that being able to dynamically
learn security requirements might help provide better UIs and translators.

# Collaboration {#section-8}

The participants discussed how best to share information among their various organizations.
One discussion was around having joint meetings. One current challenge reported was that
organizations were not aware of when and where each others' meetings were scheduled,
and sharing such information could help organizations better colocate meetings.
To facilitate this exchange, the participants agreed to add links to their respective
meeting schedules from a common page in the IOTSI repository {{IOTSIGIT}}.

Another challenge reported was that organizations did not know how to find each others'
published data models, and sharing such information could better facilitate reuse of the
same information model.  To facilitate this exchange, this participants discussed whether
a common repository might be used by multiple organizations.  The OCF's OneIoTa repository
was discussed as one possibility but it was reported that its Terms of Use at the time
of the workship prevented this.  The OCF agreed to take this back and look at updating
the Terms of Use to allow other organizations to use it too, as the restriction was not
the intent.  Schema.org was discussed as another possibility.  In the meantime, the
participants agreed to add links to their respective repositories from a common page in
the IOTSI repository {{IOTSIGIT}}.

It was also agreed that the iotsi@iab.org mailing list would remain open and available
for sharing information between all relevant organizations.

# Acknowledgements {#section-9}

We would like to thank all paper authors and participants for their
contributions, and Ericsson for hosting the workshop.

# Appendix A: Program Committee {#section-8}

This workshop was organized by the following individuals: Jari Arkko,
Ralph Droms, Jaime Jiménez, Michael Koster, Dave Thaler, and Hannes
Tschofenig.

# Appendix B: Accepted Position Papers {#section-9}

* Jari Arkko, "Gadgets and Protocols Come and Go, Data Is Forever"
* Carsten Bormann, "Noise in specifications hurts"
* Benoit Claise, "YANG as the Data Modelling Language in the IoT space"
* Robert Cragie, "The ZigBee Cluster Library over IP"
* Dee Denteneer, Michael Verschoor, Teresa Zotti, "Fairhair: interoperable IoT services for major Building Automation and Lighting Control ecosystems"
* Universal Devices, "Object Oriented Approach to IoT Interoperability"
* Bryant Eastham, "Interoperability and the OpenDOF Project"
* Stephen Farrell, Alissa Cooper, "It's Often True: Security's Ignored (IOTSI) - and Privacy too"
* Christian Groves, Lui Yan, ang Weiwei, "Overview of IoT semantics landscape"
* Ted Hardie, "Loci of Interoperability for the Internet of Things"
* Russ Housley, "Vehicle-to-Vehicle and Vehicle-to-Infrastructure Communications"
* Jaime Jimenez, Michael Koster, Hannes Tschofenig, "IPSO Smart Objects"
* David Jones, IOTDB - "Interoperability Through Semantic Metastandards"
* Sebastian Kaebisch, Darko Anicic, "Thing Description as Enabler of Semantic Interoperability on the Web of Things"
* Achilleas Kemos, "Alliance for Internet of Things Innovation Semantic Interoperability Release 2.0, AIOTI WG03 - IoT Standardisation"
* Ari Keraenen, Cullen Jennings, "SenML: simple building block for IoT semantic interoperability"
* Dongmyoung Kim, Yunchul Choi, Yonggeun Hong, "Research on Unified Data Model and Framework to Support Interoperability between IoT Applications"
* Michael Koster, "Model-Based Hypertext Language"
* Matthias Kovatsch, Yassin N.  Hassan, Klaus Hartke, "Semantic Interoperability Requires self describing Interaction Models"
* Kai Kreuzer, "A Pragmatic Approach to Interoperability in the Internet of Things"
* Barry Leiba, "Position Paper"
* Marcello Lioy, "AllJoyn"
* Kerry Lynn, Laird Dornin, "Modeling RESTful APIs with JSON Hyper-Schema"
* Erik Nordmark, "Thoughts on IoT Semantic Interoperability: Scope of security issues"
* Open Geospatial Consortium, "OGC SensorThings API: Communicating "Where" in the Web of Things"
* Jean Paoli, Taqi Jaffri, "IoT Information Model Interoperability: An Open, Crowd-Sourced Approach in Three Parallel Parti"
* Joaquin Prado, "OMA Lightweight M2M Resource Model"
* Dave Raggett, Soumya Kanti Datta, "Input paper for IAB Semantic Interoperability Workshop"
* Pete Rai, Stephen Tallamy, "Semantic Overlays Over Immutable Data to Facilitate Time and Context Specific Interoperability"
* Jasper Roes, Laura Daniele, "Towards semantic interoperability in the IoT using the Smart Appliances REFerence ontology (SAREF) and its extensions"
* Max Senges, "Submission for IAB IoT Sematic Interoperability workshop"
* Bill Silverajan, Mert Ocak, Jaime Jimenez, "Implementation Experiences of Semantic Interoperability for RESTful Gateway Management"
* Ned Smith, Jeff Sedayao, Claire Vishik, "Key Semantic Interoperability Gaps in the Internet-of-Things Meta-Models"
* Robert Sparks and Ben Campbell, "Considerations for certain IoT based services"
* J.  Clarke Stevens, "Open Connectivity Foundation oneIoTa Tool"
* J.  Clarke Stevens, Piper Merriam, "Derived Models for Interoperability Between IoT Ecosystems"
* Ravi Subramaniam, "Semantic Interoperability in Open Connectivity Foundation (OCF) - formerly Open Interconnect Consortium (OIC)""
* Andrew Sullivan, "Position paper for IOTSI workshop"
* Darshak Thakore, "IoT Security in the context of Semantic Interoperability"
* Dave Thaler, "IoT Bridge Taxonomy"
* Dave Thaler, S"ummary of AllSeen Alliance Work Relevant to Semantic Interoperability"
* Mark Underwood, Michael Gruninger, Leo Obrst, Ken Baclawski, Mike Bennett, Gary Berg-Cross, Torsten Hahmann, Ram Sriram, "Internet of Things: Toward Smart Networked Systems and Societies"
* Peter van der Stok, Andy Bierman, "YANG-Based Constrained Management Interface (CoMI)"

# Appendix C: List of Participants {#section-10}

* Andy Bierman, YumaWorks
* Carsten Bormann, Uni Bremen/TZI
* Ben Campbell, Oracle
* Benoit Claise, Cisco
* Alissa Cooper, Cisco
* Robert Cragie, ARM Limited
* Laura Daniele, TNO
* Bryant Eastham, OpenDof
* Christian Groves, Huawei
* Ted Hardie, Google
* Yonggeun Hong, ETRI
* Russ Housley, Vigil Security
* David Janes, IOTDB
* Jaime Jimenez, Ericsson
* Shailendra Karody, Catalina Labs
* Ari Keraenen, Ericsson
* Michael Koster, SmartThings
* Matthias Kovatsch, Siemens
* Kai Kreuzer, Deutsche Telekom
* Barry Leiba, Huawei
* Steve Liang, Uni Calgary
* Marcello Lioy, Qualcomm
* Kerry Lynn, Verizon
* Mayan Mathen, Catalina Labs
* Erik Nordmenk, Arista
* Jean Paoli, Microsoft
* Joaquin Prado, OMA
* Dave Raggett, W3C
* Max Senges, Google
* Ned Smith, Intel
* Robert Sparks, Oracle
* Ram Sriram, NIST
* Clarke Stevens
* Ram Subramanian, Intel
* Andrew Sullivan, DIN
* Darshak Thakore, Cablelabs
* Dave Thaler, Microsoft
* Hannes Tschofenig, ARM Limited
* Michael Verschoor, Philips Lightning

--- back
