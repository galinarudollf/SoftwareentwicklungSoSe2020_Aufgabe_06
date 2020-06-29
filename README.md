# SoftwareentwicklungSoSe2020_Aufgabe_06

## Bearbeitungzeit

30. Juni - 17. Juli 2020

## Idee der Übung

Mit dem Aufgabenblatt sollen Ihre Fähigkeiten beim objektorientierten Entwurf auf der Basis 
+ von generischen Klassen und Collections sowie 
+ der Delegaten und dem Event-Konzept
weiter verbessert werden. 

Organisieren Sie Ihre Mini-Projekte jeweils in separaten Ordnern.

## 1. Generische Collections
Erstellen Sie die generische Klasse `Set` zum Verwalten von Elementen einer Menge.
Die Klasse soll die Properties und Methoden des Interfaces `ICollection<T>` implementieren:

Properties:

  + `int Count` gibt die Anzahl der Elemente an , die in der Collection enthalten sind
  + `bool IsReadOnly` gibt an, ob die Collection schreibgeschützt ist

Methoden:

  + `void Add(T)` fügt der Collection ein Element hinzu
  + `bool Remove(T)` entfernt das erste Vorkommen eines angegebenen Objekts aus der Collection
  + `void Clear()` entfernt alle Elemente aus der Collection
  + `bool Contains(T)` ermittelt, ob die Collection einen bestimmten Wert enthält
  + `void CopyTo(T[], Int32)` kopiert die Elemente der Collection in ein Array, beginnend bei einem bestimmten Array-Index
  + `IEnumerator<T> GetEnumerator()` gibt einen Enumerator zurück, der die Collection durchläuft
  + `IEnumerator GetEnumerator()` gibt einen Enumerator zurück, der die Collection durchläuft

Verwenden Sie in der Klasse zum Speichern der Elemente ein  privates Feld vom Typ `List<T>`, zum Verwalten von Elementen die angegebenen Methoden bzw. weitere sinnvolle Methoden. Nutzen Sie in den Methoden der Klasse die von der Klasse `List` zur Verfügung stehenden Properties und Methoden: `Count`, `Contains`, `Add`, `CopyTo`, `Remove`. Beachten Sie beim Implementieren der Methoden, dass alle Elemente einer Menge unterschiedlich sein müssen.

Tipps:
  + Für die generische `GetEnumerator`-Methode bietet sich die `yield return` - Anweisung an.
  + Die nichtgenerische `IEnumerable.GetEnumerator()`-Methode ist "historisch gewachsen" und wird nicht mehr verwendet, muss aber trotzdem implementiert werden. Im einfachsten Fall delegieren Sie an die generische Version: `System.Collections.IEnumerator System.Collections.IEnumerable.GetEnumerator() => GetEnumerator();`

Definieren Sie in der Klasse weitere Properties und Methoden, z.B.:
`Cardinality`, `IsEmpty`, `IsSubsetOf()`, `Intersection()`, `Union()`
Testen Sie die Klasse in der `Main`-Methode, indem Sie die Mengen mit Elementen unterschiedlicher Datentypen erstellen, z.B. `int` und Stöckchen-Zahlen aus der Aufgabe 4.2.

## 2. Type constraints
Die Klasse `Set` soll so verändert werden, dass sie nur Instanzen von Typen aufnehmen kann, die das Interface `ISuitable` implementieren.

Erstellen Sie bitte das Interface `ISuitable` mit der Methode `bool Suit()`.

Erstellen Sie eine andere Klasse, die das Interface `ISuitable` implementiert, oder ergänzen Sie einfach die Stöckchen-Zahlen-Klasse um die `ISuitable`- Implementierung.

Die Methode `Suit()` kann z.B. überprüfen, ob die Zahlen eine bestimmte Größe nicht überschreiten. Passen Sie die Methoden der Klasse `Set` so an, dass nur "geeignete" Elemente (solche mit `element.Suit() == true`) hinzugefügt werden.


## 3. Delegaten
Das E-Orakel von Freiberg soll für ein Fußballspiel folgende Voraussagen treffen können:

  +	das Spielergebnis,
  + ob die Verlängerung (bzw. zwei Verlängerungen) stattfinden werden
  + die Anzahl der roten Karten für jede Mannschaft.

Aus organisatorischen Gründen werden die Anfragen erst eingereicht, die Aussagen liefert das Orakel dann zum späteren Zeitpunkt flott nacheinander.
Erstellen Sie eine Klasse, die für die drei Arten von Voraussagen je eine `static`-Methode definiert. Alle Methoden sollen als Parameter einen String des folgenden Formats bekommen: “Mannschaft1 – Mannschaft2“. Die Methoden haben keinen Rückgabewert, die Voraussagen bzw. Meldungen, dass die Voraussage wegen eines falschen Formats nicht möglich ist, werden innerhalb der jeweiligen Methode auf der Konsole ausgegeben.
Benutzen Sie zum Erstellen von Voraussagen die `Random`-Klasse und die `GetHashCode()`-Methode der Mannschaftsbezeichnungen.

Erstellen Sie für die Methoden einen geeigneten `delegate`-Typ.

In der `Main`-Methode sind die drei oben beschriebenen Methoden dem Delegaten hinzuzufügen und mit verschieden Argumenten auszuführen.


## 4. Events
In der digitalisierten Welt funktioniert die Müllentsorgung wie folgt:

Sobald die Mülltonne nicht mehr die zu übernehmende Müllmenge fassen kann, wird ein Event ausgelöst, das das Abtransportieren des Mülls mit einem Müllfahrzeug zufolge hat. Die Tonne wird geleert (der Füllstand der Tonne auf 0 gesetzt) und der Müll wird aus der Tonne in das Fahrzeug übertragen.

Erstellen Sie ein Programm, das u. a. die Klassen `Mülltonne` und `Müllfahrzeug` beinhaltet. Die Klasse `Mülltonne` soll ein Event enthalten, die Klasse `Müllfahrzeug` die Methode (bzw. Property), die infolge des Event-Auslösens ausgeführt bzw. modifiziert wird.

 Um den Vorgang entsprechend dem Standard Event Pattern darstellen zu können, wird außerdem eine von der Klasse `EventArgs` abgeleitete Klasse (z.B. `TransportEventArgs`) benötigt. Die Klasse soll über
  + ein Müllmenge-Property und
  + einen passenden Konstruktor verfügen.

Die Klasse Mülltonne enthält
  + die Datenfelder (und evtl. Properties) mit Angaben zu Tonnen-ID, Volumen und Füllstand,
  + die Methode zum Müllaufnehmen (bzw. ein Property), wo die Überprüfung der Müllmenge und das evtl. Auslösen des Events stattfindet
  + das Event (z.B. „Abtransport“).

Verwenden Sie zum Definieren des Events den vorhandenen generischen `EventHandler`-Delegattypen, z.B.
```C#
public event EventHandler<TransportEventArgs> Transport;
```

Definieren Sie in der Klasse einen passenden Konstruktor und die `ToString`-Methode.

Die Klasse `Müllfahrzeug` soll:
 +	die Angabe zur Müllmenge im Fahrzeug und
 +	die Methode zum Abtransportieren (z.B. `OnTransport`) enthalten.

Die Methode zum Abtransportieren soll folgende Signatur aufweisen, wobei die Bezeichner natürlich frei wählbar sind:

```C#
public void OnTransport(object tonne, TransportEventArgs args)
{
  //TODO
}
```

Definieren Sie in der Klasse ebenfalls einen passenden Konstruktor und die `ToString`-Methode.

In der `Main`-Methode einer anderen Klasse sollen in mehrere Mülltonnen (z.B. `List` oder `Array`) wiederholt verschiedene Müllmengen eingefüllt werden (diese können z.B. zufällig erzeugt werden), sodass dabei in regelmäßigen Abständen ein Event ausgelöst wird. Geben Sie die Füllstände der Tonnen und Fahrzeuges nach jedem Füllen und Leeren aus.
