# WEID Specification

An Object Identifier (OID) is an extensively used identification mechanism jointly developed by ITU-T and ISO/IEC for naming any type of object, concept, or "thing" with a globally unambiguous name. (More information about OIDs can be found at [www.oid-info.com](https://www.oid-info.com))

There are three well-known notations for OIDs:

- Dot notation: `2.999`
- ASN.1 notation: `{joint-iso-itu-t(2) example(999)}`
- OID-IRI notation: `/Joint-ISO-ITU-T/Example`

WEID (WEhowski IDentifier) is another notation for OIDs, developed by Till Wehowski and Daniel Marschall:

- WEID notation: `weid:root:2-RR-2`

In the initial version of the WEID specification of 2011, only OIDs below the WEID root arc 1.3.6.1.4.1.37553.8 could be used. In a later definition by Daniel Marschall, any existing OID can be written in WEID notation, by defining sub-namespaces.

The registry of sub-namespaces has currently the following entries:

* Namespace `weid:` (Also called "Class C" WEID)
  * Root OID is `1.3.6.1.4.1.37553.8`
  * Example: OID `1.3.6.1.4.1.37553.8.32488192274` can be written as `weid:EXAMPLE-3` (`3` is the check digit)
  * The registration of WEID Alphanumeric OIDs beneath this arc is managed by Webfan.de in order of FRDLWEB. You can assign as Private WEID by Frdlweb here: https://registry.frdl.de/?goto=com.frdlweb.freeweid


* Sub-Namespace `weid:pen:` (Also called "Class B" WEID)
  * Root OID is `1.3.6.1.4.1`
  * Example: OID `1.3.6.1.4.1.37476.9999` can be written as `weid:pen:SX0-7PR-6` (`6` is the check digit)
  * The registration of Private Enterprise Numbers (PEN) is managed by IANA. You can register a PEN here: 
    [https://pen.iana.org/pen/PenApplication.page](https://pen.iana.org/pen/PenApplication.page)


* Sub-Namespace `weid:root:` (Also called "Class A" WEID)
  * Root OID is the OID tree root
  * Example: OID `2.999` can be written as `weid:root:2-RR-2` (`2` is the check digit)


* More sub-namespaces can be added to this registry in the future. The sub-namespaces must be defined by the [WEID consortium](https://www.startforum.de/s/weid/) (ViaThinkSoft and WebFan) in a [Specification Change](https://registry.frdl.de/?goto=oid%3A1.3.6.1.4.1.37553.8.1.8.1.6.1).



To get an OID in accordance with Recommendation ITU-T X.600 assigned, you need to find a Registration Authority that assigns you an OID. You can obtain an OID as WEID and manage your own arc, e.g. by:

  * [Free OID by Viathinksoft](https://hosted.oidplus.com/viathinksoft/?goto=oidplus%3Acom.viathinksoft.freeoid)
  * ["Public" OID by Frdlweb](https://registry.frdl.de/?goto=oidplus%3Acom.viathinksoft.freeoid)


The construction of a WEID is demonstrated with the example OID 2.999:

- The numeric arcs (e.g. `2` and `999`) are converted from base 10 to base 36, so the arcs become `2` and `RR`.
- The arcs are separated by a hyphen `-`, so we have now `2-RR`.
- Now, an appropriate namespace (and sub-namespace if applicable) will be added. In our case, a fitting (sub-)namespace is `weid:root:`, so we now have `weid:root:2-RR`
- In the end, a Luhn-based check digit (called WeLuhn) is added. If the WEID contains at least one arc, then the check digit is preceded by a hyphen.

  * The WeLuhn algorithm works this way:
  * First, we take the OID in dot notation (e.g. `2.999`)
  * The arcs will be converted from base 10 to base 36, so we have `2-RR`. Padding zeros must not be present and need to be stripped.
  * The hyphens are removed, so we now have `2RR`.
  * `A` will be replaced with `10`, `B` will be replaced with `11`, etc., so we now have `22727`
  * This number is the payload for the normal Luhn algorithm. https://en.wikipedia.org/wiki/Luhn_algorithm which works as follows:

    * Start from the rightmost digit. Moving left, double the value of every second digit (including the rightmost digit).
    * Sum the digits of the resulting value in each position.
    * Sum the resulting values from all positions, `s`.
    * The check digit is calculated by `((10-s mod 10) mod 10)`.
       * In our case, the Luhn checksum is `2`
- Our final WEID notation for OID `2.999` is `weid:root:2-RR-2`.

Recommendations for WEID notation (as of Spec Change 8):

* When choosing a (sub-)namespace, it is recommended to choose a sub-namespace that is closest to the OID you want to describe, producing the shortest WEID therefore. For example, `weid:pen:SX0-7PR-6` should be chosen rather than `weid:root:1-3-6-1-4-1-SX0-7PR-6`
* The arcs in a WEID should be written in upper-case, but lowercase can be interpreted, too.
* The URN namespace (`weid:`, `weid:pen:`, `weid:root:`) is case insensitive, but it is recommended to write it in lowercase.
* Padding with `0` characters is valid (e.g. `weid:000EXAMPLE-3`), but not recommended. The paddings do not count toward the WeLuhn check digit.

Recommendations for WEID notation (as of Spec Change 9):

* In Spec Change 9 (08 March 2022), an alternative syntax of WEIDs is defined. This alternative syntax replaces the checksum with a wildcard in the form of a question mark symbol, for example, `weid:root:2-RR-?` instead of `weid:root:2-RR-2`. One useful scenario can be the documentation of incomplete/template WEIDs. Another usage is converters (like our [online converter](https://weid.info/implementations.html)) which can help you replace the wildcard with the correct checksum.

Changes with [Spec Change 10: Domain-WEID](https://github.com/frdl/weid/issues/3):

* Spec Change 10 (07 August 2023) allows domain names to be used as WEID sub-namespace.
* All WEID sub-namespaces containing at least one dot (`.`) are treated as domain names.
* The notation `weid:example.com:ABC-DEF-?` is equal to `weid:9-DNS-COM-EXAMPLE-ABC-DEF-?`.
* The resulting WEID is called Domain-WEID or "Class D" WEID.
* Note that the check digit is equal for both notations since it is based on the resulting OID.
* TLD-Only domains are not allowed for the purpose of forming a Domain-WEID.
* A Domain-WEID can be converted to Class A/B/C WEID, but the reverse conversion is ambiguous ("*where does the domain name end and the identifier part start?*")

Changes with [Spec Change 11: Proprietary Namespaces](https://github.com/frdl/weid/issues/4):

* Spec Change 11 (07 August 2023) allows custom / vendor-specific WEID sub-namespaces.
* Such namespaces must begin with `x-`, for example:  `weid:x-contoso:ABC-DEF-?` could be a WEID defined by Contoso Ltd.
* As usual for WEID, the namespace is case insensitive.
* To avoid confusion with Spec Change 10 Domain-WEID, the sub-namespace must not contain a dot (`.`).
* The vendor has complete control over the namespace and can define the behavior. However, it is recommended to make use of Base36 and the weLuhn check digit.
* Since the vendor specifies the namespace, it is up to the vendor if they allow the mapping of their WEID-Namespace to the OID-Tree. In comparison to class A/B/C/D WEID which are 100% OID compatible, custom WEID might not be OID-compatible at all.
* Currently, the following custom namespaces are known:

    * `weid:x-frdl:[Base36_NS]-[SubNS]:[Base36_ID]-[CheckDigit]` to be defined/implemented by Frdlweb ([base idea here](https://frdl.de/dynamic-weid-namespace-class)).
    * If you know more namespaces, or if you are the author of a custom namespace, please let us know.

Changes with [Spec Change 12: URN Namespace](https://github.com/ViaThinkSoft/standards/issues/1):

* Spec Change 12 (09 September 2024) defines the Uniform Resource Name (URN) for WEID. In accordiance with RFC3406, the URN namespace of WEID is "urn:x-weid:" (whereas "x-" stands for an unregistered experimental URN). Hence, "weid:2-RR-2" can be written as "urn:x-weid:2-RR-2".

Additional notes:

* Any WEID (except for Custom WEID as defined in Spec Change 11) can be represented by an OID and vice-versa. Therefore, a WEID has all attributes of an OID (e.g. it can be used to generate a Version 5 SHA1 name-based UUID with the Namespace UUID `6ba7b812-9dad-11d1-80b4-00c04fd430c8` according to IETF RFC-4122).
* Please note that some clients handling OIDs cannot handle arcs that have a specific size ([more information here](https://misc.daniel-marschall.de/asn.1/oid_facts.html)). Implementers of WEID strongly encourage allowing arbitrary length arcs (i.e. implementing BigInteger rather than 32-bit integers)
* At www.weid.info you can find more information and announcements of changes.

The current version of the specification is 12, which is identified with the OID 1.3.6.1.4.1.37553.8.1.8.1.6.1.12 (weid:1-8-1-6-1-C-5).

The standard is also released as [ViaThinkSoft/Webfan Standard No. 3](https://www.viathinksoft.de/std/viathinksoft-std-0003-weid.html)

© WEID is developed by [Daniel Marschall](https://www.daniel-marschall.de/) / [ViaThinkSoft](https://www.viathinksoft.com/) and [Melanie Wehowski](https://webfan.de/u/frdl-github-2658030).
