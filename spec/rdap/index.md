# RDAP
We use the [RDAP protocol](https://de.wikipedia.org/wiki/Registration_Data_Access_Protocol) to *GET* registration data from registries about domains, IPs and other objects supported by OIDplus.

We bootstrap the root regisries for OID similar like for DNS, while we first query our local registries, then the root nameserver for *validated* OID-roots, like iana-pen and other well-known. Next we fetch and look-up the global OIDplus instances. The RDAP-result object can be extended by Adapters and extensions.
We do **NOT look-up DNS records** in the RDAP query, but instead we can get the authoritive **nameservers** for the ra-tree.

Our [implementation](https://github.com/frdl/rdap-server) is still in ALPHA/BETA status and will be improved.
