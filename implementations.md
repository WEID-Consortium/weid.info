<script src="WeidOidConverter.js"></script>
<script>
	function oidInputChanged() {
		var tmp = WeidOidConverter.oid2weid('urn:oid:' + document.getElementById('oid').value);
		if ((tmp === false) || (tmp.weid === false) || (tmp.oid === false)) {
			document.getElementById('weid2a').innerHTML = '<font color="red">Invalid input</font>';
			document.getElementById('oid2a').innerHTML = '&nbsp;';
		} else {
			document.getElementById('weid2a').innerHTML = 'urn:x-weid:' + tmp.weid.replace(/^weid:/, '').replace(/^urn:x-weid:/, '');
			document.getElementById('oid2a').innerHTML = 'urn:oid:' + tmp.oid.replace(/^urn:oid:/, '');
		}
	}
	function weidInputChanged() {
		var tmp = WeidOidConverter.weid2oid('urn:x-weid:' + document.getElementById('weid').value);
		if ((tmp === false) || (tmp.weid === false) || (tmp.oid === false)) {
			document.getElementById('weid2b').innerHTML = '<font color="red">Invalid input</font>';
			document.getElementById('oid2b').innerHTML = '&nbsp;';
		} else {
			document.getElementById('weid2b').innerHTML = 'urn:x-weid:' + tmp.weid.replace(/^weid:/, '').replace(/^urn:x-weid:/, '');
			document.getElementById('oid2b').innerHTML = 'urn:oid:' + tmp.oid.replace(/^urn:oid:/, '');
		}
	}
</script>

<a name="service"></a>

### Service
You can obtain an OID as WEID and manage your own arc, e.g. by:
* Free OID by [ViaThinkSoft](https://hosted.oidplus.com/viathinksoft/?goto=oidplus%3Acom.viathinksoft.freeoid)
* Private [WEID](https://registry.frdl.de/?goto=com.frdlweb.freeweid) by Frdlweb
* Public [OID](https://registry.frdl.de/?goto=oidplus%3Acom.viathinksoft.freeoid) by Frdlweb


<a name="code"></a>

### Code
* JavaScript (supports Spec Change 16): [WeidOidConverter.js](https://github.com/WEID-Consortium/weid.info/blob/gh-pages/WeidOidConverter.js)
* PHP (supports Spec Change 15): [WeidOidConverter.php](https://github.com/WEID-Consortium/weid.info/blob/gh-pages/WeidOidConverter.php)
* Delphi (supports Spec Change 15): [WEID_Delphi.pas](https://github.com/danielmarschall/oidplus_nostalgia/tree/master/DOS/WEID_Delphi.pas)
* Turbo Pascal (supports Spec Change 15): [WEID.pas](https://github.com/danielmarschall/oidplus_nostalgia/tree/master/DOS/WEID.PAS) and [VTSFUNCS.pas (Dependency)](https://github.com/danielmarschall/oidplus_nostalgia/tree/master/DOS/VTSFUNCS.PAS)


<a name="software"></a>

### Software
We recommend the software [OIDplus](https://oidplus.com/) if you like to run your own (OID/)WEID-Registry.

<a name="convert"></a>

### Online OID/WEID Converter
You can use our online converter to test the conversion between OID/WEID:

<h4>Convert OID to WEID</h4>
<p><b>Input:</b> urn:oid:<input type="text" value="2.999" name="oid" id="oid" oninput="oidInputChanged();" style="width:500px"></p>
<p><b>Output:</b></p>
<div id="weid2a"></div>
<div id="oid2a"></div>
<br>
<h4>Convert WEID to OID</h4>
<p><b>Input:</b> urn:x-weid:<input type="text" value="EXAMPLE-?" name="weid" id="weid" oninput="weidInputChanged();" style="width:500px"></p>
<p><b>Output:</b></p>
<div id="weid2b"></div>
<div id="oid2b"></div>
<br><br>	

<!--
<a name="test"></a>
<h3>Online OID/WEID-Converter (Beta)</h3>
<p>You can use our online converter to test the conversion between OID/WEID:</p>
<frdlweb-oid2weid></frdlweb-oid2weid>
<br /><strong frdl-if-js-remove="2000">Loading...</strong>
<br /><br />
-->

<script>
oidInputChanged();
weidInputChanged();
</script>
<script>
