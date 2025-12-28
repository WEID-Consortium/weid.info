# WEID 2026 Specification DRAFT

ViaThinkSoft Standards Header
=============================

```
VIATHINKSOFT/WEBFAN                           D. Marschall | M. Wehowski
SPECIFICATION No. 3                           ViaThinkSoft |      Webfan
First Draft: 2011                                         1 January 2026


                   === Wehowski Identifier (WEID) ===

Abstract

   This document describes the Wehowski Identifier (WEID) scheme, which
   is an alternative notation of Object Identifiers (OIDs).

Identification of this Document

   Revision:  2026-01-01 (Spec Change 16 as of 2026-01-01)
   State:     In Force
   Filename:  viathinksoft-std-0003-weid.txt
   URN:       urn:x-viathinksoft:std:0003:2026-01-01
   OID:       1.3.6.1.4.1.37553.8.1.8.1.6
              { iso(1) identified-organization(3) dod(6) internet(1)
                private(4) enterprise(1) frdlweb(37553) weid(8) org(1)
                webfan(8) technical-specifications(1) weid-spec(6) }
   WEID:      weid:1-8-1-6-2
   IETF/RFC:  (None)

Attachments

   (None)

Copyright Notice

   Copyright (c) 2011-2026 ViaThinkSoft, Webfan, and the persons
   identified as the document authors.  All rights reserved.

   Licensed under the terms of the Apache 2.0 License.

Terminology

   The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT",
   "SHOULD", "SHOULD NOT", "RECOMMENDED", "NOT RECOMMENDED", "MAY", and
   "OPTIONAL" in this document are to be interpreted as described in
   BCP 14 [RFC2119] [RFC8174] when, and only when, they appear in all
   capitals, as shown here.
```


1\. Introduction / What is a WEID?
==================================

1.  A WEID (WEhowski IDentifier) is a **list of Base36 identifiers** (0..9, A..Z), called arcs, delimited with dashes, and with a Luhn-based check-digit as the last arc.
2.  Examples of WEID are:
    *   `urn:x-weid:HELLO-WORLD-ABC-?`
    *   `urn:x-weid:O-2-RR-?`
    *   `urn:x-weid:D-COM-EXAMPLE-123-?`
3.  The check-digit can either be calculated (see chapter 4), or it can be replaced with a `?` which denotes a check-digit wildcard. One useful scenario can be the documentation of incomplete/template WEIDs. Another usage is converters (like our [online converter](https://weid.info/implementations.html)), which can help you replace the wildcard with the correct checksum.
4.  A WEID begins with the unofficial URN namespace `urn:x-weid:` (in accordance with [IETF RFC 3406](https://www.rfc-editor.org/rfc/rfc3406), `x-` stands for an unregistered experimental URN). The URN namespace (`urn:x-weid:`) is case-insensitive, but it is recommended to write it in lowercase.
5.  WEID are only valid if they are registered at the [Frdlweb Registration Authority](https://registry.frl.de/), or if one of the standard schemas (see chapter 2) is used.
6.  WEID has support for namespace-internal NSS qualifiers, expressed as colon-separated suffixes. For example, `urn:x-weid:ABC-DEF-?:xyz123:456:/789` defines a qualifier `xyz123:456:/789` that is meaningful for an application that knows how to handle `urn:x-weid:ABC-DEF-?`.
7.  Every WEID (excluding the information in NSS qualifiers) can be converted to an OID and vice versa using mappings (see chapter 3)
8.  The arcs in a WEID should be written in upper-case, but lowercase can be interpreted, too.
9.  Padding with `0` characters is valid (e.g., `urn:x-weid:000EXAMPLE-?`), but not recommended. The paddings do not count towards the WeLuhn check digit.

2\. Acquiring a WEID
====================

### (2.1) WEID based on Object Identifiers (OID)

If you own an OID or want to have a WEID that describes an OID, then you may use the root `urn:x-weid:O-...`. The arcs of the OID are converted from Base10 to Base36.

For example: The OID `2.999` will become `urn:x-weid:O-2-RR-?`.

To receive an OID in accordance with Recommendation ITU-T X.600, you need to find a Registration Authority that assigns you an OID. You can obtain an OID as WEID and manage your own arc, e.g., by:

*   [Free OID by Viathinksoft](https://hosted.oidplus.com/viathinksoft/?goto=oidplus%3Acom.viathinksoft.freeoid)
*   [Public OID by Frdlweb](https://registry.frdl.de/?goto=oidplus%3Acom.viathinksoft.freeoid)

### (2.2) WEID based on Object Identifiers (OID) inside the IANA PEN root

Since many OIDs are inside the IANA PEN root `1.3.6.1.4.1`, a shortcut has been established to ensure shorter identifiers. The WEID root is `urn:x-weid:P-...`, followed by the PEN and any other OID arcs that are converted from Base10 to Base36.

For example, PEN 37476 will become `urn:x-weid:P-SX0-?` and the OID `1.3.6.1.4.1.37476.9999` will become `urn:x-weid:P-SX0-7PR-?`.

You can register a PEN here: [https://pen.iana.org/pen/PenApplication.page](https://pen.iana.org/pen/PenApplication.page)

### (2.3) WEID based on Universally Unique Identifier (UUID)

If you want to create a WEID based on a UUID, then you may use the root `urn:x-weid:U-...`. The next arc will be the UUID converted from Base128 to Base36. (This means, the numeric value which would be below OID `2.25`, just coded as Base36 instead of Base10).

For example, the UUID `271b73c9-2b52-4581-8d71-b4a02d55813c` will become `urn:x-weid:U-2BCJZ644V24W81UOAX4BK4QWS-?` which is equal to OID `2.25.51982432266164560271085076081362174268`.

Any other WEID arcs are synchronous to the OID arcs, just converted between base10 and base36.

For example, `urn:x-weid:U-2BCJZ644V24W81UOAX4BK4QWS-7PR-?` is equal to OID `2.25.51982432266164560271085076081362174268.9999`.

UUIDs can be created with a lot of tools, for example: [https://misc.daniel-marschall.de/tools/uuid\_mac\_decoder/](https://misc.daniel-marschall.de/tools/uuid_mac_decoder/)

### (2.4) WEID based on Domain Name System (DNS) names

If you own a DNS name (e.g., a domain name) or want to have a WEID based on a DNS name, then you may use the root `urn:x-weid:D-...`. The next arcs will be the DNS name in reverse order, encoded in (NOT converted to!) Base36.

For example, `example.com` will become `urn:x-weid:D-COM-EXAMPLE-?`.

Any other WEID arcs are synchronous to the OID arcs, just converted between base10 and base36.

For example, `urn:x-weid:D-COM-EXAMPLE-7PR-?` is equal to OID `1.3.6.1.4.1.37553.8.13.16438.32488192274.9999`.

TLD-Only domains ARE allowed for the purpose of forming a Domain-WEID.

### (2.5) Other WEID

Any other WEID (such as `urn:x-weid:EXAMPLE`) needs a registration/request at registry.frl.de. During that registration/request, an entry in the WEID root (together with an OID and, if required, an OID redirection) will be added.

3\. Mapping a WEID to the OID tree
==================================

*   Each WEID (except the deprecated fully proprietary WEID) can be represented by an OID and vice versa. Therefore, a WEID has all attributes of an OID (e.g., it can be used to generate a Version 5 SHA1 name-based UUID with the Namespace UUID `6ba7b812-9dad-11d1-80b4-00c04fd430c8` according to [IETF RFC 9562](https://www.rfc-editor.org/rfc/rfc9562)).
*   By default, the root of WEIDs is mapped to the OID tree at OID `1.3.6.1.4.1.37553.8`. This means that `urn:x-weid:?` equals OID `1.3.6.1.4.1.37553.8`.
*   The Base36 arcs of a WEID are converted to Base10 and are then added to the OID tree below the arc `1.3.6.1.4.1.37553.8`. The check-digit (last arc of the WEID) is NOT used for the mapping to the OID tree.
    For example, `urn:x-weid:EXAMPLE-ABC-3` is mapped to `1.3.6.1.4.1.37553.8.32488192274.13368`.
*   During the registration of a WEID, an alternative OID root (also called redirection) may be defined. Currently, the following redirections are defined:
    *   `urn:x-weid:O-?` is usually mapped to `1.3.6.1.4.1.37553.8.24`, however, there will be a redirection to the OID tree root.
    *   `urn:x-weid:P-?` is usually mapped to `1.3.6.1.4.1.37553.8.25`, however, there will be a redirection to OID `1.3.6.1.4.1`.
    *   `urn:x-weid:U-9-?` is usually mapped to `1.3.6.1.4.1.37553.8.30`, however, there will be a redirection to OID `2.25`.
    *   Other WEID arcs (such as `urn:x-weid:D-?`) do not have an OID redirection. They will be mapped to the OID tree through `1.3.6.1.4.1.37553.8`.
    *   Future alternative mapping may be announced via a [WEID Specification Change](https://registry.frdl.de/?goto=oid%3A1.3.6.1.4.1.37553.8.1.8.1.6.1) by the WEID Consortium.
*   The WeLuhn check-digit (see chapter 4) is based on the default OID, NOT on the redirection target OID. Hence, the checksum can be calculated/verified without knowing the OID mapping.
*   In case namespace-internal NSS qualifiers (such as `:foobar` in `urn:x-weid:P-SX0-?:foobar`) are used, the information of the qualifier is not mapped to the OID tree.
*   Please note that some clients handling OIDs cannot handle arcs that have a specific size ([more information here](https://misc.daniel-marschall.de/asn.1/oid_facts.html)). Implementers of WEID strongly encourage allowing arbitrary-length arcs (i.e., implementing BigInteger rather than 32-bit integers).

4\. Calculation of the WeLuhn check-digit
=========================================

The WeLuhn check digit of `urn:x-weid:P-SX0-?` is calculated as follows:

*   The URN prefix (`urn:x-weid:`) is removed, as well as 0-paddings (`001` shall be `1`) and hyphens, so we now have `PSX0`.
*   `136141SZ58` will be added to the front, so we have `136141SZ58PSX0`. (Note that this prefix resembles the OID that points to the WEID root. No OID redirection must be applied for calculating the check-digit.)
*   Then, `A` will be replaced with 10, `B` will be replaced with `11`, etc., so we now have `1361412835582528330`. This number is the payload for the standard Luhn algorithm, which works as follows:
    *   Start from the rightmost digit. Moving left, double the value of every second digit (including the rightmost digit).
    *   Sum the digits of the resulting value in each position.
    *   Sum the resulting values from all positions, `s`.
    *   The check digit is calculated by `((10-s mod 10) mod 10)`.
*   In our case, the Luhn check digit is `0`, resulting in the WEID `urn:x-weid:P-SX0-0`

The [online converter](https://weid.info/implementations.html) can be used to calculate the check digit (enter a WEID that ends with `-?` and receive the calculated check digit).

5\. Deprecated notations
========================

The following notations are deprecated, but are still valid for backwards compatibility:

*   **(5.1) `weid:`** is a deprecated notation of `urn:x-weid:`
*   **(5.2) `urn:x-weid:pen:<pen-as-base36>-<base36>-?`** is a deprecated alternative notation of OID `1.3.6.1.4.1.<base10>.<base10>`, for example `urn:x-weid:pen:SX0-7PR-?` is equal to OID `1.3.6.1.4.1.37476.9999`.
*   **(5.3) `urn:x-weid:pen:<pen-as-base10>:<base36>-?`** is a deprecated alternative notation of OID `1.3.6.1.4.1.<base10>.<base10>`, for example `urn:x-weid:pen:37476:7PR-?` is equal to OID `1.3.6.1.4.1.37476.9999`.
*   **(5.4) `urn:x-weid:uuid:<uuid-as-base36>-<base36>-?`** is a deprecated alternative notation of OID `2.25.<base10>.<base10>`. For example, `urn:x-weid:uuid:3D576PEXUZ1EVVF3MKRKOTYB-7PR-?` is equal to OID `2.25.2098739235139107623796528785225371043.9999`.
*   **(5.5) `urn:x-weid:uuid:<uuid-as-split-base16>:<base36>-?`** is a deprecated alternative notation of OID `2.25.<base10>.<base10>`. For example, `urn:x-weid:uuid:019433d5-535f-7098-9e0b-f7b84cf74da3:7PR-?` is equal to OID `2.25.2098739235139107623796528785225371043.9999`.
*   **(5.6) `urn:x-weid:root:?`** is a deprecated alternative notation of the OID root. For example, `urn:x-weid:root:2-RR-?` is equal to OID `2.999`.
*   **(5.7) `urn:x-weid:<domain.tld>:?`** is a deprecated alternative notation of `urn:x-weid:9-DNS-<tld>-<domain>-?`. (Note that the current definition for DNS-based WEID uses the root `urn:x-weid:D-?` instead of `urn:x-weid:9-DNS-?`.) In this NSS prefix, TLD-Only domains ARE NOT allowed for the purpose of forming a Domain-WEID, since it may collide with other NSS prefixes.
*   **(5.8) `urn:x-weid:x-weid:x-...:`**, i.e., NSS prefixes starting with `x-` and not containing a dot (`.`), is a deprecated feature called "vendor-specific WEID", creating WEID that are fully proprietary with custom rules, and they may or may not have a representation as OID. The only use was `urn:x-weid:x-frdl:[Base36_NS]-[SubNS]:[Base36_ID]-[CheckDigit]` to be defined/implemented by Frdlweb ([base idea here](https://frdl.de/dynamic-weid-namespace-class)). Instead of using a fully proprietary WEID, please use a regular WEID and add a namespace-internal NSS qualifier to that WEID.

6\. Additional notes
====================

At [www.weid.info](http://www.weid.info), you can find more information and announcements of changes.

At [https://weid.info/implementations.html](https://weid.info/implementations.html), you can find an online converter that converts WEID to OID and vice versa, which can also calculate check-digits (enter a WEID with `-?` suffix, and you will get the correct check digit back).

The current version of the specification is 16, which is identified with the OID `1.3.6.1.4.1.37553.8.1.8.1.6.1.16` (`urn:x-weid:1-8-1-6-1-G-?`).

The standard is also released as [ViaThinkSoft/Webfan Standard No. 3](https://www.viathinksoft.de/std/viathinksoft-std-0003-weid.html)

7\. Security Considerations
===========================

None.

8\. RA Considerations
=====================

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6**<br>
ASN1: `{ iso(1) identified-organization(3) dod(6) internet(1) private(4) enterprise(1) frdlweb(37553) weid(8) org(1) webfan(8) technical-specifications(1) weid-spec(6) }`<br>
IRI: `/.../weid/Organization/Webfan/1/6`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1**<br>
ASN1: `{ ... weid-spec-changes(1) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.1**<br>
ASN1: `{ ... weid-spec-change-2013-6-27-1-identifier(1) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.2**<br>
ASN1: `{ ... weid-spec-change-2013-6-27-2-weix-canceled-and-replaced(2) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.3**<br>
ASN1: `{ ... weid-spec-change-2013-6-27-3-rooting-url-look-up-url-meaning-revision(3) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.4**<br>
ASN1: `{ ... weid-spec-change-2013-0-1-commercial-repository(4) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.5**<br>
ASN1: `{ ... weid-spec-change-2013-6-27-4-determine-seperator-colon(5) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.6**<br>
ASN1: `{ ... weid-spec-change-2013-10-2-camel-case-identifier(6) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.7**<br>
ASN1: `{ ... weid-spec-change-2013-10-2-thesaurus(7) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.8**<br>
ASN1: `{ ... weid-spec-change-2021-12-8-marschall-indi-version(8) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.9**<br>
ASN1: `{ ... weid-spec-change-2022-03-08-marschall-checksum-wildcard(9) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.10**<br>
ASN1: `{ ... weid-spec-change-2023-08-07-domain-weid(10) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.11**<br>
ASN1: `{ ... weid-spec-change-2023-08-07-custom-namespace(11) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.12**<br>
ASN1: `{ ... weid-spec-change-2024-09-09-urn(12) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.13**<br>
ASN1: `{ ... weid-spec-change-2025-01-01-uuid(13) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.14**<br>
ASN1: `{ ... weid-spec-change-2025-01-06-uuid-update1(14) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.15**<br>
ASN1: `{ ... weid-spec-change-2025-01-06-uuid-update2(15) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.1.6.1.16**<br>
ASN1: `{ ... weid-spec-change-2026-01-01-revamp(16) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.4**<br>
ASN1: `{ ... dns(4) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.24**<br>
ASN1: `{ ... oid(24) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.25**<br>
ASN1: `{ ... pen-oid(25) }`

**OID: 1.3.6.1.4.1.37553.8.1.8.30**<br>
ASN1: `{ ... uuid-oid(30) }`

9\. References
==============

9.1 Normative References
------------------------

\[RFC2119\] Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", [BCP 14](https://datatracker.ietf.org/doc/html/bcp14), [RFC 2119](https://datatracker.ietf.org/doc/html/rfc2119), DOI 10.17487/RFC2119, March 1997, <[https://www.rfc-editor.org/info/rfc2119](https://www.rfc-editor.org/info/rfc2119)\>.

\[RFC3406\] Daigle, L., van Gulik, D., Iannella, R., and P. Faltstrom, "Uniform Resource Names (URN) Namespace Definition Mechanisms", [RFC 3406](https://datatracker.ietf.org/doc/html/rfc3406), DOI 10.17487/RFC3406, October 2002, <[https://www.rfc-editor.org/info/rfc3406](https://www.rfc-editor.org/info/rfc3406)\>.

9.2 Informative References
--------------------------

\[RFC4122\] Leach, P., Mealling, M., and R. Salz, "A Universally Unique IDentifier (UUID) URN Namespace", [RFC 4122](https://datatracker.ietf.org/doc/html/rfc4122), DOI 10.17487/RFC4122, July 2005, <[https://www.rfc-editor.org/info/rfc4122](https://www.rfc-editor.org/info/rfc4122)\>.

10\. Acknowledgements
=====================

I would like to thank Melanie Wehowski for her long-time support in OIDplus and WEID projects. Thanks to the authors of these free tools that did a good job in validating various contents of this document:

This document was written in Nroff Internet Draft Editor by 3xA Security. [https://aaa-sec.com/nroffedit/](https://aaa-sec.com/nroffedit/) [https://misc.daniel-marschall.de/patches/nroffedit/](https://misc.daniel-marschall.de/patches/nroffedit/) ("year 2020" patch)

11\. Authors' Addresses
=======================

Daniel Marschall<br>
Postfach 11 53<br>
69243 Bammental<br>
Germany

Email: [daniel-marschall@viathinksoft.de](mailto:daniel-marschall@viathinksoft.de)<br>
URI: [https://www.viathinksoft.com/](https://www.viathinksoft.com/)

Appendix A: Specification Change Changelog
==========================================

The following change log entries are just for information. They might contain features that are already deprecated. Hence, only information outside the "Changelog" chapter may be used for implementations.

Changes as of Spec Change 1 - 7
-------------------------------

In the initial version of the WEID specification of 2011, only OIDs below the WEID root arc `1.3.6.1.4.1.37553.8` could be used. In a later definition by Daniel Marschall, any existing OID can be written in WEID notation.

The detailed descriptions of the changes of Spec Change 1 through 7 are not available anymore. Only a short description from the OID RA exists:

1.  `weid-spec-change-2013-6-27-1-identifier`
2.  `weid-spec-change-2013-6-27-2-weix-canceled-and-replaced`
3.  `weid-spec-change-2013-6-27-3-rooting-url-look-up-url-meaning-revision`
4.  `weid-spec-change-2013-0-1-commercial-repository`
5.  `weid-spec-change-2013-6-27-4-determine-seperator-colon`
6.  `weid-spec-change-2013-10-2-camel-case-identifier`
7.  `weid-spec-change-2013-10-2-thesaurus`

Changes as of Spec Change 8: NSS prefixes (also called sub-namespaces)
----------------------------------------------------------------------

*   Besides the classic `weid:` namespace (that represents OID `1.3.6.1.4.1.37553.8`), new namespaces `weid:root:` (which represents the root OID) and `weid:pen:` (which represents OID `1.3.6.1.4.1`) are introduced.
*   When choosing a (sub-)namespace, it is recommended to choose an NSS prefix that is closest to the OID you want to describe, producing the shortest WEID, therefore. For example, `weid:pen:SX0-7PR-6` should be chosen rather than `weid:root:1-3-6-1-4-1-SX0-7PR-6`.
*   The arcs in a WEID should be written in upper-case, but lowercase can be interpreted, too.
*   The URN namespace (`weid:`, `weid:pen:`, `weid:root:`) is case insensitive, but it is recommended to write it in lowercase.
*   Padding with `0` characters is valid (e.g., `weid:000EXAMPLE-3`), but not recommended. The paddings do not count toward the WeLuhn check digit.

Changes as of Spec Change 9: Wildcard check digit
-------------------------------------------------

*   In Spec Change 9 (08 March 2022), an alternative syntax of WEIDs is defined. This alternative syntax replaces the checksum with a wildcard in the form of a question mark symbol, for example, `weid:root:2-RR-?` instead of `weid:root:2-RR-2`. One useful scenario can be the documentation of incomplete/template WEIDs. Another usage is converters (like our [online converter](https://weid.info/implementations.html)), which can help you replace the wildcard with the correct checksum.

Changes with [Spec Change 10: Domain-WEID](https://github.com/frdl/weid/issues/3)
---------------------------------------------------------------------------------

*   Spec Change 10 (07 August 2023) allows domain names to be used as NSS prefixes.
*   All NSS prefixes containing at least one dot (`.`) are treated as domain names.
*   The notation `weid:example.com:ABC-DEF-?` is equal to `weid:9-DNS-COM-EXAMPLE-ABC-DEF-?`.
*   The resulting WEID is called Domain-WEID or "Class D" WEID.
*   Note that the check digit is equal for both notations since it is based on the resulting OID.
*   TLD-Only domains are not allowed for the purpose of forming a Domain-WEID, since it may collide with other NSS prefixes.
*   A Domain-WEID can be converted to Class A/B/C WEID, but the reverse conversion is ambiguous ("_where does the domain name end and the identifier part start?_")

Changes with [Spec Change 11: Proprietary Namespaces](https://github.com/frdl/weid/issues/4)
--------------------------------------------------------------------------------------------

*   Spec Change 11 (07 August 2023) allows custom / vendor-specific NSS prefixes.
*   Such namespaces must begin with `x-`, for example: `weid:x-contoso:ABC-DEF-?` could be a WEID defined by Contoso Ltd.
*   As usual for WEID, the namespace is case-insensitive.
*   To avoid confusion with Spec Change 10 Domain-WEID, the NSS prefix must not contain a dot (`.`).
*   The vendor has complete control over the namespace and can define the behavior. However, it is recommended to make use of Base36 and the weLuhn check digit.
*   Since the vendor specifies the namespace, it is up to the vendor if they allow the mapping of their WEID-Namespace to the OID-Tree. In comparison to Class A/B/C/D WEID, which are 100% OID compatible, a custom WEID might not be OID-compatible at all.
*   Currently, the following custom namespaces are known:
    *   `weid:x-frdl:[Base36_NS]-[SubNS]:[Base36_ID]-[CheckDigit]` to be defined/implemented by Frdlweb ([base idea here](https://frdl.de/dynamic-weid-namespace-class)).
    *   If you know more namespaces, or if you are the author of a custom namespace, please let us know.

Changes with [Spec Change 12: URN Namespace](https://github.com/ViaThinkSoft/standards/issues/1)
------------------------------------------------------------------------------------------------

*   Spec Change 12 (09 September 2024) defines the Uniform Resource Name (URN) for WEID. In accordance with [IETF RFC 3406](https://www.rfc-editor.org/rfc/rfc3406), the URN namespace of WEID is `urn:x-weid:` (whereas `x-` stands for an unregistered experimental URN). Hence, `weid:2-RR-2` can be written as `urn:x-weid:2-RR-2`.

Changes with [Spec Change 13: UUID WEID](https://github.com/WEID-Consortium/weid.info/issues/1)
-----------------------------------------------------------------------------------------------

*   Spec Change 13 (1 January 2025) defines the WEID namespaces, which contain a UUID. The notation `weid:uuid:<uuid-base16>:...` (Also called "Class B / UUID" WEID) is equal to `weid:root:2-P-<uuid-base36>:...` which is equal to the root OID `2.25.<uuid-base10>...`.

Changes with [Spec Change 14: UUID WEID Update](https://github.com/WEID-Consortium/weid.info/issues/2)
------------------------------------------------------------------------------------------------------

*   Spec Change 14 (6 January 2025) defines the special case `weid:uuid:?` to be an alias of `weid:root:2-P-3`, which is OID `2.25`.

Changes with [Spec Change 15: UUID+PEN WEID Update](https://github.com/WEID-Consortium/weid.info/issues/3)
----------------------------------------------------------------------------------------------------------

*   Spec Change 15 (6 January 2025) defines `weid:uuid:(uuid-base16):xxx-?` to be an alias of `weid:uuid:(uuid-base36)-xxx-?` (which itself is an alias of `weid:root:2-P-(uuid-base36)-xxx-?`) which represents OID `2.25.(uuid-base10).xxx`.
*   It also defines `weid:pen:(pen-base10):xxx-?` to be an alias of `weid:pen:(pen-base36)-xxx-?` (which itself is an alias of `weid:root:1-3-6-1-4-1-(pen-base36)-xxx-?`) which represents OID `1.3.6.1.4.1.(pen-base10).xxx`.

Changes with [Spec Change 16: Large revamp of WEID](https://github.com/WEID-Consortium/weid.info/issues/4)
----------------------------------------------------------------------------------------------------------

*   Deprecating NSS prefixes (e.g., `pen:`, `uuid:`, `root:`, `example.com:`, `x-...:`), as they are confusing. Instead, let everything be a normal WEID (e.g., `weid:P-...`), just with different OID mappings based on the WEID arc.
    *   `weid:root:2-RR-?` will become `weid:O-2-RR-?` which is mapped to `2.999`.
    *   `weid:pen:SX0-?` and its alternative notation `weid:pen:37476:?` will become `urn:x-weid:P-SX0-?` and will be mapped to `urn:oid:1.3.6.1.4.1.37476`.
    *   `weid:uuid:2BCJZ644V24W81UOAX4BK4QWS-?` and its alternative notation `weid:uuid:271b73c9-2b52-4581-8d71-b4a02d55813c:?` will become `urn:x-weid:U-2BCJZ644V24W81UOAX4BK4QWS-?` and will be mapped to `urn:oid:2.25.51982432266164560271085076081362174268`.
    *   `weid:example.com:?` and its alternative WEID `weid:9-UUID-COM-EXAMPLE-?` will become `urn:x-weid:D-COM-EXAMPLE-?` and will be mapped to the OID tree like a normal WEID (below `1.3.6.1.4.1.37553.8`).
*   Deprecated vendor-specific WEID (such as `weid:x-foobar:anything-here`), as they don't have a standardized way to be mapped to the OID tree and need a spec change to be supported.
*   Added support for namespace-internal NSS qualifiers, expressed as colon-separated suffixes (e.g., `urn:x-weid:EXAMPLE-?:/foobar`). In other words, any WEID can now have its own NSS qualifiers, e.g., `urn:x-weid:P-SX0` can be extended to `urn:x-weid:P-SX0:foo:bar:/anything?p=1` (this way, proprietary things can be done).
*   The terminology "Class A", "Class B", "Class C", and "Class D" is deprecated. It was earlier defined as:
    *   "Class A" (was `weid:root:`)
    *   "Class B" (was `weid:pen:` and `weid:uuid:`, as they are below "Class A" `weid:root:`)
    *   "Class C" (was `weid:`, because it was below "Class B" `weid:pen:`)
    *   "Class D" (anything below "Class C" `weid:`, such as `weid:example.com:`)
    *   Now everything is "Class D" (e.g., `weid:O-?` is below "Class C" `weid:?`)
*   The use of the `weid:` namespace is deprecated. Instead, use `urn:x-weid:`.
    (In accordance with RFC 3406, the URN namespace of WEID is `urn:x-weid:`, whereas `x-` stands for an unregistered experimental URN).
*   Although this change is subtle, the new definition of a WEID is independent of the OID tree. Previously, a WEID was defined as an alternate notation of an OID. Now, a WEID is defined as a list of Base36 arcs with a check-digit, and the OID mapping (or redirection) is a feature of the WEID.

Appendix B: Future changes for consideration
===========================================

*   Removal of check-digit, as it is often confused with an arc, and is seldom calculated and usually written as wildcard `-?`.
*   Replacing `urn:x-weid` (WEhowski IDentifier) with `urn:x-mwid` (Marschall Wehowski IDentifier) due to the incompatibility that would arise by removing the check-digit.
