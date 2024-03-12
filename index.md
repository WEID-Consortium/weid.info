# WEID Consortium
The WEID Consortium is a group of IT-workers and companies leaded by Frdlweb and ViaThinkSoft who work on network and internet protocols, specially identifiers, look-ups and registries.

Responsible owner: Till Wehowski ([Frdlweb/Webfan Homepagesystem](https://registry.frdl.de/?goto=oid%3A1.3.6.1.4.1.37553))
Technical management: Daniel Marschall ([ViaThinkSoft](https://hosted.oidplus.com/viathinksoft/?goto=oid%3A1.3.6.1.4.1.37476))

Organisation Entity: [co@weid.info](https://weid.info/)

# WEID Community
Read the talk, ask questions, or apply to join the [WEID Consortium](https://www.startforum.de/s/weid) and contribute or vote for changes.
Contribute to several related projects, read the documentations get news in the [WEID Frdlweb Group](https://frdl.de/groups/profile/152/weid-consortium).
You can contact the Org e.g. via our shared cloud account [@weid@webfan.de](https://webfan.de/u/weid).

# WEID Chapters
We currently work on:
+ **WEID Notation** is a specification to write OID identifiers in a different notation. Its status is stable and it is ready to use.
+ **RDAP** is a protocol to look-up registration data for domains, IPs, networks or other objects like e.g. OID or WEID. We try to implement OID and WEID and other look-ups as part of RDAP. Its status is BETA, you can use it but it will be improved or changed (see *OID-Connect* below...).
+ **OID-IP** is a protocol developed by ViaThinkSoft. It can be used to query OID registries similar to DNS Nameservers.
+ **OIDplus** is a system to manage objects in a registry. It is developed and maintained by Daniel Marschall (ViaThinkSoft).

# WEID Notation
Read the [specification](spec.html) of the WEID Notation, the first specification in place and complete which was developed by the WEID Consortium.

**The Status of the following Chapters is Alpha, they are not ready but will be implemented soon probably...**

We further plan to develop, or we plan to work with:
+ **ORS** is a protocol to write an OID as a hostname and look its DNS up in DNS nameservers autoritativ for OID.
+ Frdlweb wants to define a **.well-known and defined set** of apps,successors/protocols/tools in something like WEID+ to implement implementations like Frdlweb code or OIDplus, for example to create federations of registries like OIDplus systems.
+ A **nameserver system and protocol** with (root-)registries similar to the domain name system connecting OIDs to physical hosts/services.
+ A well defined set of **registration policies** to register and hand-out subordinates and/or identifiers like **IPs, domains, services related and connected to OID registries**.
+ Defining a bootstrap of trusted **default roots and OID trees** where you can **register** well-known OIDs like IANA PEN, FreeOID by Viathinksoft and registered and connected sub-registries like e.g. OIDplus instances.

# OID-Connect
Successor of a set of our protocols for registration, provisioning, accreditation, binding, managing, connecting and extending the registration, delegation, signing and validation of OID allocations, its registrants, registrars and registries.
- [Protocol Registry](1.3.6.1.4.1.37553.8.1.8.1.33061)
- [WEID OID-Connect Service Provider](https://connect.oid.zone/)

# WEID Software
Working on software implementing the WEID protocols, like e.g. OIDplus.
Successors of the WEID Software Chapter will be (soon):
- Source code registries and development packages collections
- Applications registries and app setup/installer marketplaces
- Code less interoperational protocols and interfaces registry, significantly referred to as **OIDminus**  

# WEID RA and WEID Business
Wehowski and Marschall will enable and administer the commercial market to sub-delegate and resell roots, trees and subzones and connect internet services like webhosting or emails to it and to other services following our protocols. They may provide a biz/shop to (re-)sell webhosting, domains, services, servers and other products.
