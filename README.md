# ARI-CSV

Zeigt die .csv-Dateien, die das ARI ausgibt (aber auch jede andere .csv-datei) an. Die Ausgabe ist sortierbar nach jeder Spalte und 

Ein laufendes Beispiel ist unter http://ari.datenschleuder.de zu finden.

## Gebrauch

#### 1. Dateien

Im Wurzelverzeichnis \

* `index.html` Index-Datei der Startseite
* `README.md` Diese Datei mit den Anleitungen
* `img` Verzeichnis mit den in der Startseite verwendeten Bildern
* `css` Verzeichnis mit .css-Dateien für grundlegende Style-Infos
* `filename_in_URL` Wurzelverzeichnis der Folgeseite, mit der die .csv-Datei dann angezeigt wird 

Im Verzeichnis \filename_in_URL

* `index.html` Index-Datei der '.csv-Dateien-Dartsellungs-Seite'
* `data` Verzeichnis mit Bespiel-.csv-Dateien
* `images`Verzeichnis mit den in der '.csv-Dateien-Dartsellungs-Seite' verwendeten Bildern
* `css`Verzeichnis mit den .css-Dateien zur richtigen Darstellung


#### Wie es funktioniert

Die Datei `index.html` im Wurzelverzeichnis ruft je nach Auswahl die `index.html` der '.csv-Dateien-Dartsellungs-Seite' mit dem Namen der darzustellenden Datei auf.

Beispiele:
`./filename_in_URL/index.html?file=Beispiel-Daten.csv`
`./filename_in_URL/index.html?file=Free.csv`

Dieser Aufruf resultiert aus folgendem Formular:

``` html

    <form action="./filename_in_URL/index.html" method="get" class="formfield">
		<label>Ausw&auml;lbare .csv-Dateien:
			<a class="tooltips2" href="#">
    			<select name="file" size="2">
    				<option>Beispiel-Daten.csv</option>
    				<option>Free.csv</option>
    			</select>
				<span>&nbsp;W&auml;hle die anzuzeigende<br>&nbsp;Datei aus!</span>
			</a>
		</label><br><br>
		<input type="submit" value="Weiter..">
	</form>
```

Der an die `./filename_in_URL/index.html` übergebene Parameter wird mit der Funktion

```html

   function getUrlVars()
	  	{
		 var vars = [], hash;
		 var hashes = window.location.href.slice(window.location.href.indexOf('?') + 1).split('&');
		 for(var i = 0; i < hashes.length; i++)
		 {
		  hash = hashes[i].split('=');
		  vars.push(hash[1]);
		  vars[hash[0]] = hash[1];
		 }
		 return vars; 
		} 

```

ausgelesen und dynamisch in 

```html

    CsvToHtmlTable.init({
		csv_path: 'data/' + urlVars.file,
        element: 'table-container', 
        allow_download: false,
        csv_options: {separator: '|', delimiter: '"'},
        datatables_options: {"paging": false},
		custom_formatting: [[2, format_link]]
      });
      
```

in der Zeile `csv_path: 'data/' + urlVars.file,` gesetzt.


## Wie ARI-CSV eingesetzt werden kann

* Die Funktionalität der Startseite (Auswahl der anzuzeigenden .csv-Datei und aufruf der '.csv-Dateien-Dartsellungs-Seite') müsste im ARI integriert werden.
* Der fest in der `./filename_in_URL/index.html` hinterlegt Pfad der .csv-Dateien ist entweder anzupassen.

Das ist alles.


## Abhängigkeiten

* [Bootstrap](http://getbootstrap.com/) - Responsive HTML, CSS and Javascript framework
* [jQuery](https://jquery.com/) - a fast, small, and feature-rich JavaScript library
* [jQuery CSV](https://github.com/evanplaice/jquery-csv/) - Parse CSV (Comma Separated Values) to Javascript arrays or dictionaries.
* [DataTables](http://datatables.net/) - add advanced interaction controls to any HTML table.


## Copyright

Copyright (c) 2015 Derek Eder. Released under the [MIT License](https://github.com/derekeder/csv-to-html-table/blob/master/LICENSE).
