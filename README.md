Project waarin er een custom library aan ons gegeven werd. We moesten:

-Een map inladen met terrein, steden en markten op basis van een text file.

-Algoritmes gebruiken om zo snel mogelijk van punt A naar B te gaan, rekening houdend met verschillende terreinen en hoeveel bewegingspunten deze terreinen kosten om doorheen te bewegen.

-Algoritmes gebruiken om de snelste route te berekenen om alle steden 1 keer te bezoeken vanuit een bepaalde stad als startpunt.

-Een eigen algoritme verzinnen om de beste winst te krijgen met een bepaald aantal bewegegingspunten en goud die je krijgt aan het begin van de ronde. De winst kan gemaakt worden doordat er in elke stad een markt aanwezig is met items die je kan kopen en verkopen voor bepaalde prijzen en hoeveelheden.


De README die bij aan het begin van dit project aan ons werd gegeven:

# Game of Trades Student Kit

Game of Trades stelt je in staat om op visuele en spelende wijze kennis te maken met algoritmen.  

## Inhoud

De student kit bestaat uit een Java Maven project met daarin een aantal folders:

* `src/main/java` - hierin moet de bron code komen van de door jullie te maken handelaar. Er staan al wat files voor je klaar. 
* `src/test/java` - hierin moet de bron code komen die de handelaar test. Sommige testen zijn al geschreven, doe er je voordeel mee!
* `src/test/resources` - hierin staan een aantal kant en klare kaarten om te gebruiken.
* `pom.xml` - dit is het bestand dat Maven vertelt hoe het project in elkaar zit en gebouwd moet worden.

De visuele omgeving maakt ook onderdeel uit van de student kit. Zie de 'Starten van de visuele omgeving' verderop.

## Voorbereiding

Om met Game of Trades mee te kunnen doen heb je een werkende Java ontwikkelomgeving nodig. 

Deze bestaat uit de volgende ingrediënten:

* Java 8 Development Kit (JDK) 
* [Apache Maven 3.3+](https://maven.apache.org/download.cgi) - [installatie tips](https://maven.apache.org/install.html), [installatie op ubuntu](http://www.mkyong.com/maven/how-to-install-maven-in-ubuntu/)
* IDE naar keuze (intelliJ, eclipse, netbeans)
* Git   

## Clonen van de Student Kit

Clone je eigen project, niet de algemene student kit!

```
> git clone https://github.com/gameoftrades/<git repo van mijn team>.git

Cloning into 'gameoftrades-student-kit'...
remote: Counting objects: 87, done.
remote: Compressing objects: 100% (51/51), done.
remote: Total 87 (delta 13), reused 79 (delta 8), paRck-reused 0eceiving objects:  13% (12/87)
Receiving objects: 100% (87/87), 15.60 KiB | 0 bytes/s, done.
Resolving deltas: 100% (13/13), done.
Checking connectivity... done.
```

In de `gameoftrades-student-kit` folder staat nu de student kit, klaar om geïmporteerd te worden in je IDE.

## Team Specifieke Aanpassingen

Omdat ieder team uniek is maar je net een algemene repository hebt gecloned is het _noodzakelijk_ om een aantal team specifieke aanpassingen te maken.

* In de `pom.xml` pas de waarde van de `artifactId` tag aan naar `got-teamNN` waarbij NN dan het team nummer (2 digits) is. Is het team nummer kleiner dan 10, plak er dan een 0 voor. Wat het moet worden is <artifactId>got-teamNN</artifactId> dus NIET de naam van de tag veranderen van artifactId naar iets anders.

```xml
    <!-- Change Me -->
    <artifactId>gameoftrades-student-kit</artifactId> <!-- got-teamNN -->
    <!-- --> 
```

* In je ontwikkelomgeving, hernoem de package `studentNN`. Ook hier moet NN het team nummer worden. 
   
## Op te leveren artifacten voor beoordeling

Er moeten twee bestanden worden opgeleverd voor de beoordeling van de algoritme implementaties:

* De zip file van de broncode, inclusief testen en pom.xml

* Een jar file met daarin de uitvoerbare (gecompileerde) code.

Deze jar file kun je maken door het uitvoeren van een `mvn clean install`.
Wanneer dit gelukt is vindt je in de `target` folder de jar file (got-teamNN-1.0.jar). 

Mochten je tests falen en je toch een jar willen maken dan kan dat met `mvn clean install -DskipTests`

## Herkansingsopdracht

Voor de mensen die dit blok nogmaals moeten doen is er een speciale [herkansingsopdracht](OPDRACHT-Herkansing.md).

# FAQ / How to

## Hoe begin ik?

* Zorg eerst dat je een werkende ontwikkelomgeving hebt en de student-kit kunt bouwen.
* Bestudeer het [gameoftrades-library project](https://github.com/gameoftrades/gameoftrades-library); deze bevat het domein model van de handels wereld. 
* Rename het artifactId en de packagenaam naar die van je team.
* Run de WereldLaderTest in je IDE en zorg dat alle testen gaan slagen door de WereldLaderImpl.java aan te passen.
* Start de StudentUI en aanschouw de wereld.
* Implementeer nu opdracht 2, 3 en 4. 

## Bouwen van de Student Kit (vanaf de command line)

Bouwen zonder de testen uit te voeren:
```
> mvn clean install -DskipTests
```

Bouwen en wel de testen uitvoeren:
```
> mvn clean install
```

Alleen compileren:
```
> mvn compile
```

Uitvoeren van de testen:
```
> mvn test
```
## Wat is een `interface`? Wat betekent `implements`?

Een Interface beschrijft een contract waaraan een klasse zich kan conformeren door deze interface te implementeren.

Dat wil zeggen dat de methoden genoemd in de interface ook moeten voorkomen in de klasse. 
Dit is Java zijn manier voor multiple inheritance.

Doe de tutorial [voor meer inzicht](https://docs.oracle.com/javase/tutorial/java/concepts/interface.html).

## Starten van de visuele omgeving.

In de `src/test/java` folder, in de `nl.gameoftrades.ui` package staat een klasse `StudentUI`. Deze start de visuele omgeving.

Let op: De visuele omgeving is afhankelijk van jouw implementatie van Handelaar. Zonder WereldLader kan hij de kaart niet tonen!   

## Hoe maak ik mijn Algoritme visueel debugbaar?

Door de interface `io.gameoftrades.debug.Debuggable` te implementeren in je Algoritme klasse.

Deze zorgt er voor dat de methode `setDebugger(Debugger debugger)` in het Algoritme geïmplementeerd moet worden.

Als je dit als volgt doet dan heb je bij default een `DummyDebugger` (die niets doet) maar kan de gebruikersinterface de `GuiDebugger` zetten en jij, als je dat zou willen, de `AsciiArtDebugger` die naar de console debug uitvoer stuurt.

```
public class MijnSnelstePadAlgoritme implements SnelstePadAlgoritme, Debuggable {

    private Debugger debug = new DummyDebugger();
    
    @Override
    public void setDebugger(Debugger debugger) {
        this.debug = debugger;
    }
    
```

In de `Debugger` interface zitten verschillende methoden die domein objecten en andere data-structuren zichtbaar maken in de gebruikersinterface.
Door een van deze methoden aan te roepen tijdens de uitvoering van je algoritme wordt dit in de gebruikersinterface zichtbaar gemaakt als Stap.


## Format van het kaart bestand

```$xslt
<breedte>,<hoogte>
<map>
<Aantal steden>
<X stad 1>,<Y stad 1>,<Naam stad 1>
<X stad 2>,<Y stad 2>,<Naam stad 2>
etc.
<Aantal handels>
<Stadsnaam>,<BIEDT/VRAAGT>,<Naam product>,<Prijs>
```
