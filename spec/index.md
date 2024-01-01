# Protocols and specifications

## WEID notation
+ **WEID** is a specification to write OID identifiers in a different notation. Its status is stable and it is ready to use. [Read the spec](weid-notation/)

## Related Topics:

#### Objectmodel-, Registration Authority and Allocation look-up
+ **RDAP** is a protocol to look-up registration data for domains, IPs, networks or other objects like e.g. OID or WEID. We try to implement OID and WEID and other look-ups as part of RDAP. Its status is BETA, you can use it but it will be improved or changed. [Read more](rdap/)
+ **OID-IP** is a protocol developed by ViaThinkSoft. It can be used to query OID registries similar to DNS Nameservers. [Join the space](https://startforum.de/s/oid-ip/)

#### OID with DNS - Domain-, Address- and Identity- Binding
We are thinking about to use the domain name system for OID resolution.
+ **ORS** is a protocol to write an OID as a hostname and look its DNS up in DNS nameservers autoritativ for OID.
+ **DNS** is the resolution system we all know well already. After a lttle reading and testing OID-RAs with domains and nameservers and the ORS,
  I do not find the need to declare a *new* specification. I believe we can implement ORS by just the "normal" DNS and protocols we just have,
  BUT to ensure the conformance of applications we need registries.+ 
+ **Application Schema Registry** could specify how a systems can use ORS/DNS in a reasonable way.
 
