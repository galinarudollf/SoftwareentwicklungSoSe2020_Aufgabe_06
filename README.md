# SoftwareentwicklungSoSe2020_Aufgabe_06

## Bearbeitungzeit

30. Juni - 17. Juli 2020

## Idee der Übung

Mit dem Aufgabenblatt sollen Ihre Fähigkeiten beim objektorientierten Entwurf und der Implementierung mittels C# weiter trainiert werden. Der Schwerpunkt liegt dabei auf den Delegaten und dem Event-Konzept.

## 1. Delegaten
Das E-Orakel von Freiberg soll für ein Fußballspiel folgende Voraussagen treffen können:

+	das Spielergebnis,
+ ob die Verlängerung (bzw. zwei Verlängerungen) stattfinden werden und
+ die Anzahl der roten Karten für jede Mannschaft.

Aus organisatorischen Gründen werden die Anfragen erst eingereicht, die Aussagen liefert das Orakel dann zum späteren Zeitpunkt flott nacheinander.
Erstellen Sie eine Klasse, die für drei Voraussagen drei static-Methoden definiert. Alle Methoden sollen als Parameter ein string des folgenden Formats bekommen:“Mannschaft1 – Mannschaft2“. Die Methoden haben keinen Rückgabewert, die Voraussagen bzw. Meldungen, dass die Voraussage wegen eines falschen Formats nicht möglich ist, werden innerhalb der jeweiligen Methode ausgegeben.
Benutzen Sie zum Erstellen von Voraussagen die `Random`-Klasse und `HashCode` der Mannschaftsbezeichnungen.

Erstellen Sie für die Methoden einen geeigneten `delegate`-Typ.

In der Main-Methode sind die drei oben beschriebenen Methoden dem delegate hinzuzufügen und mit verschieden Argumenten auszuführen.


## 2. Events
In der digitalisierten Welt funktioniert die Müllentsorgung wie folgt:

Sobald die Mülltonne nicht mehr die zu übernehmende Müllmenge fassen kann, wird ein Event ausgelöst, der das Abtransportieren des Mülls mit einem Müllfahrzeug zufolge hat. Die Tonne wird geleert (der Füllstand der Tonne auf 0 gesetzt) und der Müll wird aus der Tonne in das Fahrzeug übertragen.

Erstellen Sie ein Programm, das u. a. die Klassen `Mülltonne` und `Müllfahrzeug` geinhaltet. Die Klasse Mülltonne soll ein Event enthalten, die Klasse Müllfahrzeug die Methode (bzw. Property), die infolge des Event-Auslösens ausgeführt wird.

 Um den Vorgang entsprechend dem Standard Event Pattern darstellen zu können, wird außerdem eine von der Klasse `EventArgs` abgeleitete Klasse (z.B. `TransportEventArgs`) benötigt. Die Klasse soll über
 + ein Müllmenge-Property und
 + einen passenden Konstruktor verfügen.

Die Klasse Mülltonne enthält
+ die Datenfelder (und evtl. Properties) mit Angaben zu Tonnen-ID, Volumen und Füllstand,
+ die Methode zum Müllaufnehmen (bzw. ein Property), wo die Überprüfung der Müllmenge und das evtl. Auslösen des Events stattfindet und
+ das Event „Abtransport“.

Verwenden Sie zum Definieren des Events den vorhandenen generischen `EventHandler`, z.B.
```C#
public event EventHandler<TransportEventArgs> Transport;
```

Definieren Sie in der Klasse einen passenden Konstruktor und die `ToString`-Methode.

Die Klasse Müllfahrzeug soll:
+	die Angabe zur Müllmenge im Fahrzeug und
+	die Methode zum Abtransportieren (z.B. OnTransport) enthalten.

Die Methode zum Abtransportieren soll folgende Signatur aufweisen, wobei die Bezeichner natürlich frei wählbar sind:

```C
public void OnTransport(object tonne, TransportEventArgs args)
{
  //TODO
}
```

Definieren Sie in der Klasse ebenfalls einen passenden Konstruktor und die `ToString`-Methode.

In der `Main`-Methode einer anderen Klasse sollen in mehrere in einer Liste erfassten Mühltonnen wiederholt verschiedene Müllmengen eingefüllt werden (diese können z.B. zufällig erzeugt werden), sodass dabei immer Mal ein Event ausgelöst wird. Geben Sie die Füllstände der Tonnen und Fahrzeuges nach jedem Füllen und Leeren aus.
