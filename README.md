# První cvičení – C# konzolová aplikace (.NET 9)

> Kompletní didaktický průvodce pro studenty: od založení projektu, přes Git, až po základy programování v C# s ukázkami kódu.

---

## Obsah

1. [Založení projektu ve Visual Studio 2022](#1-založení-projektu-ve-visual-studio-2022)
2. [Git – co to je a základní pojmy](#2-git--co-to-je-a-základní-pojmy)
3. [Git ve Visual Studio 2022](#3-git-ve-visual-studio-2022)
4. [Git pomocí aplikace Fork](#4-git-pomocí-aplikace-fork)
5. [Komentáře v kódu](#5-komentáře-v-kódu)
6. [Metoda Main – vstupní bod aplikace](#6-metoda-main--vstupní-bod-aplikace)
7. [Proměnné a datové typy](#7-proměnné-a-datové-typy)
8. [Práce s třídou Math a přetypování](#8-práce-s-třídou-math-a-přetypování)
9. [Výpis do konzole a interpolace řetězců](#9-výpis-do-konzole-a-interpolace-řetězců)
10. [Typ string (řetězec)](#10-typ-string-řetězec)
11. [Seznam (List) – dynamické pole](#11-seznam-list--dynamické-pole)
12. [Třída (class) – co to je a proč ji vytvořit](#12-třída-class--co-to-je-a-proč-ji-vytvořit)
13. [Konstruktor](#13-konstruktor)
14. [Vytváření instancí (objektů)](#14-vytváření-instancí-objektů)
15. [Přístup k vlastnostem objektu (tečková notace)](#15-přístup-k-vlastnostem-objektu-tečková-notace)
16. [Seznam instancí (List objektů)](#16-seznam-instancí-list-objektů)
17. [Cyklus foreach](#17-cyklus-foreach)
18. [Metody ve třídě](#18-metody-ve-třídě)
19. [Rychlý tahák](#19-rychlý-tahák)

---

## 1) Založení projektu ve Visual Studio 2022

### Krok za krokem

1. **Spusť Visual Studio 2022** (Community edice je zdarma).
2. Na úvodní obrazovce klikni na **„Create a new project"** (Vytvořit nový projekt).
3. V seznamu šablon vyhledej **„Console App"** (Konzolová aplikace).
   - Ujisti se, že vybraná šablona má popisek **C#** a **Windows / Linux / macOS**.
   - **Nevybírej** šablonu „Console App (.NET Framework)" – ta je starší.
4. Klikni **Next** (Další).
5. Vyplň:
   - **Project name** (Název projektu): např. `PrvniCviceni`
   - **Location** (Umístění): zvol složku, kam chceš projekt uložit
   - **Solution name** (Název řešení): obvykle stejný jako název projektu
6. Klikni **Next**.
7. Vyber **Framework**: `.NET 9.0` (nebo nejnovější dostupná verze).
8. **Zaškrtni** volbu **„Do not use top-level statements"** – díky tomu uvidíš kompletní strukturu programu včetně `namespace`, `class Program` a metody `Main`.
9. Klikni **Create** (Vytvořit).

### Co se vytvořilo?

```
PrvniCviceni/                   ← složka řešení (Solution)
├── PrvniCviceni.sln            ← soubor řešení (Solution file)
└── PrvniCviceni/               ← složka projektu
    ├── PrvniCviceni.csproj     ← soubor projektu (konfigurace, .NET verze)
    ├── Program.cs              ← hlavní soubor s kódem
    └── obj/                    ← dočasné soubory (neverzujeme v Gitu)
```

### Spuštění aplikace

- **Ctrl + F5** – spustí aplikaci **bez debuggeru** (konzole zůstane otevřená).
- **F5** – spustí aplikaci **s debuggerem** (lze krokovat kód, sledovat proměnné).

> **Tip:** Po každé úpravě kódu zkus aplikaci spustit a ověřit, že funguje správně. Průběžné testování je základ!

---

## 2) Git – co to je a základní pojmy

**Git** je systém pro správu verzí kódu. Umožňuje:
- Sledovat historii změn (kdo, co a kdy změnil).
- Vrátit se k předchozí verzi kódu.
- Spolupracovat v týmu bez vzájemného přepisování práce.

**GitHub** je webová služba, která hostuje Git repozitáře online (vzdálené úložiště).

### Slovníček pojmů

| Pojem | Co to je | K čemu to je |
|---|---|---|
| **Repository (repozitář)** | Složka s projektem sledovaná Gitem | Uchovává veškerou historii změn projektu |
| **Commit** | Uložení změn do **místního** repozitáře s popisem | Vytvoří záchytný bod – lze se k němu vrátit |
| **Push** | Odeslání commitů na **GitHub** (vzdálený server) | Zpřístupní tvoje změny ostatním |
| **Fetch** | Zjištění, co je nového na GitHubu **bez** změny souborů | Bezpečná kontrola – nic se ti nezmění |
| **Pull** | Stažení a **aplikování** změn z GitHubu (= Fetch + Merge) | Dostaneš se na aktuální stav týmu |
| **Branch (větev)** | Oddělená linie vývoje | Bezpečně zkoušíš úpravy mimo hlavní větev |
| **Merge** | Sloučení jedné větve do druhé | Zapracuješ hotovou práci do hlavní větve |
| **Clone** | Stažení celého vzdáleného repozitáře na tvůj počítač | Poprvé získáš projekt z GitHubu |
| **Pull Request (PR)** | Návrh na sloučení větve na GitHubu | Týmová kontrola před Merge |
| **.gitignore** | Soubor se seznamem ignorovaných souborů/složek | Git nebude sledovat `bin/`, `obj/`, `.vs/` apod. |

### Pravidla pro psaní commit zpráv

Dobrá zpráva u commitu šetří čas celému týmu – z historie musí být **jasné co a proč**.

- Řádek 1: **stručný titulek do ~50 znaků** v rozkazovacím způsobu.
- Nepiš „update" nebo „oprava" – buď konkrétní.
- Komituj **malé logické celky** (častěji a menší balíčky).
- Nepoužívej diakritiku.

```
Špatně:  Update
Dobře:   Pridej tridu Student a metodu Popis()

Špatně:  Oprava věcí
Dobře:   Oprava diakritiku ve výpise Student.Popis()
```

---

## 3) Git ve Visual Studio 2022

### 3.1 Vytvoření Git repozitáře pro existující projekt

1. Otevři projekt ve Visual Studio.
2. Přejdi na **Git → Create Git Repository…**
3. Vyber **GitHub** (nebo **Existing remote** pokud máš repozitář vytvořený).
4. Vyplň název repozitáře, popis, zvol veřejný/soukromý.
5. Klikni **Create and Push** – VS vytvoří repozitář a nahraje kód na GitHub.

> Pokud chceš pouze lokální repozitář (bez GitHubu), vyber **Local only**.

### 3.2 Commit a Push (uložení a odeslání změn)

1. Ulož změny v kódu (**Ctrl+S**).
2. Otevři **View → Git Changes** (nebo panel „Git Changes" v pravém dolním rohu).
3. Uvidíš seznam změněných souborů.
4. Do pole **Message** napiš popis commitu (co jsi změnil a proč).
5. Klikni **Commit All** (uloží lokálně) nebo **Commit All and Push** (uloží a rovnou odešle na GitHub).
6. Pokud jsi dal jen Commit All, dokonči odeslání klikem na **Push** (šipka nahoru v panelu Git Changes nebo **Git → Push**).

> **Tip:** První odeslání nové větve bývá **Publish Branch** – VS ji vytvoří i na GitHubu.

### 3.3 Fetch a Pull (načtení změn od ostatních)

- **Fetch:** **Git → Fetch** – jen zjistí, co je nového na GitHubu (nic se nezmění v tvém kódu).
- **Pull:** **Git → Pull** – stáhne a zapracuje změny do tvých souborů.

> Máš-li **lokální necommitnuté změny**, nejdřív je **Commitni**, teprve pak dělej Pull – předejdeš konfliktům.

### 3.4 Branch (větve)

1. **Vytvoření:** **Git → New Branch…** → název např. `feature/student-class` → **Create**.
2. **Přepnutí:** Klikni na název větve v **dolní stavové liště** VS a vyber jinou větev.
3. **Smazání:** **Git → Manage Branches…** → pravým klikem na větev → **Delete**.

### 3.5 Merge (sloučení)

1. Přepni se na cílovou větev (typicky `main`).
2. **Git → Manage Branches…** → pravým klikem na `main` → **Merge From…**
3. Vyber zdrojovou větev → **Merge**.
4. Pokud vzniknou **konflikty**, VS je ukáže – vyber správné části a ulož.
5. **Commit** výsledku → **Push** na GitHub.

---

## 4) Git pomocí aplikace Fork

### 4.1 Co je Fork?

**Fork** je grafická aplikace (GUI klient) pro práci s Gitem. Je přehlednější než příkazový řádek a nabízí vizuální zobrazení větví, commitů a změn.

### 4.2 Stažení a instalace

1. Přejdi na web: **[https://git-fork.com/](https://git-fork.com/)**
2. Klikni na **Download for Windows** (nebo macOS).
3. Spusť stažený instalátor a postupuj podle pokynů.
4. Po instalaci spusť Fork a při prvním spuštění nastav své **jméno** a **e-mail** (budou použity v commitech).

### 4.3 Klonování repozitáře (Clone)

1. Na GitHubu otevři repozitář → klikni na zelené tlačítko **Code** → zkopíruj URL (HTTPS).
2. Ve Forku: **File → Clone…**
3. Vlož URL repozitáře do pole **Repository URL**.
4. Vyber složku, kam se má projekt stáhnout (**Parent folder**).
5. Klikni **Clone** – Fork stáhne celý repozitář na tvůj počítač.

### 4.4 Commit (uložení změn)

1. V levém panelu Forku klikni na **Changes** – uvidíš seznam změněných souborů.
2. Zaškrtni soubory, které chceš commitnout (nebo klikni **Stage All** pro všechny).
3. Do pole **Commit Message** napiš popis změn.
4. Klikni **Commit**.

### 4.5 Push (odeslání na GitHub)

1. Po commitu klikni na tlačítko **Push** (šipka nahoru) v horní liště.
2. Vyber větev a klikni **Push**.

### 4.6 Fetch a Pull

- **Fetch:** Klikni na tlačítko **Fetch** v horní liště – zjistí nové změny na GitHubu.
- **Pull:** Klikni na **Pull** – stáhne a zapracuje změny.

### 4.7 Větve (Branches)

- **Nová větev:** Pravým klikem na commit → **New Branch…** → zadej název → **Create Branch**.
- **Přepnutí:** Dvojklik na větev v levém panelu (sekce **Branches**).
- **Merge:** Pravým klikem na větev → **Merge into current branch…**

### 4.8 Vizuální výhody Forku

- Přehledný **graf větví** – vidíš, kde se větve rozcházejí a spojují.
- Barevné zvýraznění změn v souborech (přidané řádky zeleně, smazané červeně).
- Snadné řešení konfliktů s vestavěným merge editorem.

---

## 5) Komentáře v kódu

**Co je komentář?** Text v kódu, který se **neprovede** – slouží pouze pro vysvětlení kódu lidem, kteří ho čtou.

### Proč komentáře používat?

- Vysvětlují, **co** kód dělá a **proč**.
- Pomáhají ostatním (i tobě za měsíc) pochopit logiku.
- Umožňují dočasně **deaktivovat** části kódu (kód se neprovede, ale nemusíš ho mazat).

### Typy komentářů v C\#

**Kód bez komentářů:**

```csharp
namespace PrvniCviceni
{
    internal class Program
    {
        static void Main(string[] args)
        {

        }
    }
}
```

**Kód s komentáři:**

```csharp
namespace PrvniCviceni
{
    internal class Program
    {
        // {} - Alt gr (pravý alt) + b / n
        // [] - Alt gr (pravý alt) + f / g
        // $ - levý alt + num36

        // Komentář - text, který není vykonán jako kód, slouží pro vysvětlení kódu
        /* Komentář - Pomocí těchto znaku můžete zakomentovat větší blok kódu */
        // Jednořádkový komentář - začíná dvěma lomítky //
        // Pomocí komentářů můžete deaktivovat části kódu (nebudou vykonány)

        static void Main(string[] args)
        {

        }
    }
}
```

### Shrnutí

| Typ | Syntaxe | Použití |
|---|---|---|
| Jednořádkový | `// text` | Krátké poznámky na jednom řádku |
| Víceřádkový (blokový) | `/* text */` | Delší vysvětlení nebo dočasné zakomentování většího bloku kódu |

> **Tip klávesové zkratky ve VS 2022:**
> - **Ctrl + K, Ctrl + C** – zakomentuje vybraný blok kódu
> - **Ctrl + K, Ctrl + U** – odkomentuje vybraný blok kódu

---

## 6) Metoda Main – vstupní bod aplikace

**Co je metoda Main?** Je to hlavní metoda programu – **první věc, která se spustí** při startu aplikace. Veškerý kód, který chceme vykonat, píšeme dovnitř jejích složených závorek `{ }`.

### Rozbor zápisu

**Kód bez komentářů:**

```csharp
static void Main(string[] args)
{

}
```

**Kód s komentáři:**

```csharp
// Hlavní metoda aplikace
// static - metoda je statická a patří ke třídě, ne k instanci třídy
// void - metoda nevrací žádnou hodnotu
// Main - název metody, hlavní metoda aplikace (při spuštění aplikace se spustí tato metoda)
// string[] args - parametr metody (pole řetězců), slouží pro předávání argumentů z příkazového řádku
static void Main(string[] args)
{
    // Sem píšeme kód, který se vykoná po spuštění programu
}
```

### Co znamenají jednotlivá klíčová slova?

| Slovo | Význam |
|---|---|
| `static` | Metoda patří přímo ke třídě – nemusíme vytvářet instanci (objekt), abychom ji mohli zavolat |
| `void` | Metoda nic nevrací (nemá návratovou hodnotu) |
| `Main` | Speciální název – C# ho rozpozná jako vstupní bod programu |
| `string[] args` | Pole textových parametrů z příkazového řádku (většinou ho nepoužíváme, ale musí tam být) |

---

## 7) Proměnné a datové typy

### Co je proměnná?

**Proměnná** je pojmenované místo v paměti, které uchovává určitou hodnotu. Představ si ji jako **krabičku s nálepkou** (název) a něčím uvnitř (hodnota).

### Syntaxe deklarace

```
DatovýTyp názevProměnné = hodnota;
```

### Datové typy v C\#

| Datový typ | Co uchovává | Příklad |
|---|---|---|
| `int` | Celé číslo | `5`, `-10`, `0` |
| `double` | Desetinné číslo (velmi přesné) | `3.14`, `-0.5` |
| `float` | Desetinné číslo (méně přesné než double, musíme psát f na konci) | `3.14f` |
| `string` | Text (řetězec znaků) | `"Ahoj"`, `"Honza"` |
| `bool` | Pravda / nepravda | `true`, `false` |
| `var` | Kompilátor sám odvodí typ podle přiřazené hodnoty | `var x = 5;` → bude `int` |

### Příklad z našeho programu

**Kód bez komentářů:**

```csharp
int a = 5;
int b = 2;
```

**Kód s komentáři:**

```csharp
int a = 5; // int - integer - celé číslo, proměnná "a" má hodnotu 5
int b = 2; // Proměnná má název "b" a hodnotu 2
```

### Co se stane v paměti?

1. Vytvoří se místo v paměti pojmenované `a` a uloží se tam číslo `5`.
2. Vytvoří se místo v paměti pojmenované `b` a uloží se tam číslo `2`.

> **Otestuj:** Po deklaraci proměnných zkus přidat `Console.WriteLine(a);` a spustit program – mělo by se vypsat `5`.

---

## 8) Práce s třídou Math a přetypování

### Třída Math

C# obsahuje vestavěnou třídu `Math`, která nabízí matematické metody a konstanty. Nemusíš ji importovat – je dostupná automaticky.

Metoda `Math.Pow(základ, exponent)` vypočítá mocninu.

### Co je přetypování?

**Přetypování** (type casting) nastává, když potřebuješ uložit hodnotu jednoho typu do proměnné jiného typu.

- `Math.Pow()` vrací vždy `double` (desetinné číslo), i když pracuješ s celými čísly.
- Pokud bychom chtěli uložit výsledek `Math.Pow(5, 2)` (= 25) do proměnné `int`, museli bychom přetypovat: `int vysledek = (int)Math.Pow(a, b);`
- V našem případě výsledek ukládáme do `double`, takže přetypování není potřeba.

### Implicitní vs. explicitní přetypování

| Typ | Popis | Příklad |
|---|---|---|
| **Implicitní** | Automatické – bez ztráty dat (menší typ → větší) | `int` → `double`: `double x = 5;` |
| **Explicitní** | Ruční – může dojít ke ztrátě dat (větší typ → menší) | `double` → `int`: `int x = (int)3.14;` → výsledek `3` |

### Příklad z našeho programu

**Kód bez komentářů:**

```csharp
int a = 5;
int b = 2;
double vysledek = Math.Pow(a, b);
```

**Kód s komentáři:**

```csharp
int a = 5; // základ mocniny
int b = 2; // exponent

// Výpočet mocniny pomocí metody Math.Pow
// Math - třída, která obsahuje matematické metody a konstanty
// Pow - metoda, která vypočítá mocninu (první parametr je základ, druhý je exponent)
// Do proměnné vysledek uložíme výsledek výpočtu
// Math.Pow vrací double → proměnná vysledek musí být typu double
// Zde dochází k implicitnímu přetypování: int a, int b se automaticky převedou na double
double vysledek = Math.Pow(a, b);
```

> **Otestuj:** Zkus přidat `Console.WriteLine(vysledek);` – mělo by se vypsat `25`.

---

## 9) Výpis do konzole a interpolace řetězců

### Console.WriteLine

`Console` je třída pro práci s konzolí (terminálový vstup/výstup). Metoda `WriteLine` vypíše text a přejde na nový řádek.

### Interpolace řetězců

**Interpolace** umožňuje vkládat hodnoty proměnných přímo do textu. Řetězec začíná znakem `$` a proměnné se píší do `{ }`.

### Příklad z našeho programu

**Kód bez komentářů:**

```csharp
Console.WriteLine("Aplikace pro mocnění");
Console.WriteLine($"Mocnina {a} na {b} = {vysledek}");
Console.WriteLine($"Mocnina {a} na {b} = {Math.Pow(a, b)}");
```

**Kód s komentáři:**

```csharp
// Výpis do konzole
// Console - třída, která obsahuje metody pro práci s konzolí
// WriteLine - metoda, která vypíše text do konzole a přejde na další řádek
// Do závorek píšeme výstup z aplikace, nezapomeňte na středník na konci řádku
Console.WriteLine("Aplikace pro mocnění");

// Různý výpis s použitím interpolace řetězců
// Interpolace řetězců - umožňuje vkládat hodnoty proměnných do textu pomocí {}
// Začínáme znakem $ před uvozovkami
// V {} píšeme název proměnné, jejíž hodnotu chceme vložit do textu nebo rovnou příkaz či operaci
Console.WriteLine($"Mocnina {a} na {b} = {vysledek}");

// Příklad s použitím metody Math.Pow přímo v interpolaci
// V {} můžeme psát i výrazy a volání metod – nejen názvy proměnných
Console.WriteLine($"Mocnina {a} na {b} = {Math.Pow(a, b)}");
```

### Způsoby spojování textu a proměnných

| Způsob | Příklad | Poznámka |
|---|---|---|
| Interpolace (`$""`) | `$"Výsledek: {a}"` | Nejčistší a nejčitelnější způsob |
| Spojování (`+`) | `"Výsledek: " + a` | Starší způsob, méně přehledné |
| `String.Format` | `String.Format("Výsledek: {0}", a)` | Formální, pozice v `{0}`, `{1}` atd. |

> **Otestuj:** Spusť program – na výstupu uvidíš:
> ```
> Aplikace pro mocnění
> Mocnina 5 na 2 = 25
> Mocnina 5 na 2 = 25
> ```

---

## 10) Typ string (řetězec)

### Co je string?

`string` je datový typ pro uložení textu (řetězce znaků). Text se vždy píše do **uvozovek** `" "`.

### Příklad z našeho programu

**Kód bez komentářů:**

```csharp
string jmeno = "Honza";
Console.WriteLine(jmeno);
```

**Kód s komentáři:**

```csharp
// Deklarace a použití proměnné typu string
// string - datový typ pro text
// jmeno - název proměnné
// "Honza" - hodnota (text musí být vždy v uvozovkách)
string jmeno = "Honza";
Console.WriteLine(jmeno); // Vypíše: Honza
```

> **Otestuj:** Změň hodnotu `"Honza"` na své jméno a spusť program.

---

## 11) Seznam (List) – dynamické pole

### Co je pole / seznam?

**Pole (Array)** a **Seznam (List)** slouží k uložení **více hodnot** do jedné proměnné. Rozdíl:

| Vlastnost | Pole (`array`) | Seznam (`List`) |
|---|---|---|
| Velikost | **Pevná** – určíš při vytvoření | **Dynamická** – můžeš přidávat/odebírat |
| Syntaxe | `string[] pole = new string[3];` | `List<string> list = new List<string>();` |
| Přidání prvku | Nelze (musíš vytvořit nové pole) | `list.Add("hodnota");` |

### Různé způsoby deklarace pole a seznamu

```csharp
// --- Klasické pole (Array) ---
string[] pole1 = new string[3];         // prázdné pole o velikosti 3
string[] pole2 = { "A", "B", "C" };    // pole s počátečními hodnotami
string[] pole3 = new string[] { "A", "B" }; // explicitní zápis

// --- Seznam (List) ---
List<string> list1 = new List<string>();                     // prázdný seznam
List<string> list2 = new List<string>() { "A", "B", "C" };  // seznam s hodnotami
var list3 = new List<string>() { "A", "B" };                 // s použitím var
```

### Příklad z našeho programu – vytvoření seznamu

**Kód bez komentářů:**

```csharp
var list = new List<string>() { "Pepa", "Karel", "Mirek", "Kryštof"};
Console.WriteLine($"Seznam jmen: {String.Join(",", list)}");
Console.WriteLine($"Jméno na pozici 1 = {list[1]}");
```

**Kód s komentáři:**

```csharp
// Deklarace proměnné pro List (seznam) jmen
/*                                0       1         2         3         */
var list = new List<string>() { "Pepa", "Karel", "Mirek", "Kryštof"};
// var - kompilátor sám určí datový typ proměnné (Dynamické typování)
// list - název proměnné
// List - třída, která reprezentuje seznam hodnot
// new List<string>() - vytvoření nové instance seznamu, který bude obsahovat hodnoty typu string
// { "Pepa", "Karel", "Mirek", "Kryštof"} - inicializace seznamu s počátečními hodnotami (oddělujeme čárkou)
// Přístup k jednotlivým hodnotám v seznamu pomocí indexu (pozice v seznamu, začíná od 0)
// Délka seznamu pomocí vlastnosti Count - počet hodnot v seznamu

// Výpis seznamu do konzole
// String.Join - metoda, která spojí hodnoty seznamu do jednoho řetězce, oddělené zadaným znakem (v tomto případě čárkou)
// Pokud bychom použili pouze list, vypíše se typ seznamu, ne jeho obsah
Console.WriteLine($"Seznam jmen: {String.Join(",", list)}");
Console.WriteLine($"Jméno na pozici 1 = {list[1]}");
```

### Indexování (přístup k prvkům)

Indexy začínají od **0** (nuly):

```
Index:    0        1        2         3
Hodnota: "Pepa"  "Karel"  "Mirek"  "Kryštof"
```

- `list[0]` → `"Pepa"`
- `list[1]` → `"Karel"`
- `list[3]` → `"Kryštof"`

### Operace se seznamem

**Kód bez komentářů:**

```csharp
list.Add("Jirka");
string jmena = $"Seznam jmen: {String.Join(",", list)}";
Console.WriteLine(jmena);

list.RemoveAt(0);
jmena = $"Seznam jmen: {String.Join(",", list)}";
Console.WriteLine(jmena);

list.Remove("Karel");
jmena = $"Seznam jmen: {String.Join(",", list)}";
Console.WriteLine(jmena);
```

**Kód s komentáři:**

```csharp
// list.Add() - metoda, která přidá novou hodnotu na konec seznamu
list.Add("Jirka");

// Uložení výpisu do proměnné a opětovný výpis do konzole
string jmena = $"Seznam jmen: {String.Join(",", list)}";
Console.WriteLine(jmena);

// list.RemoveAt() - metoda, která odstraní hodnotu na zadané pozici (indexu)
list.RemoveAt(0); // Odstraní "Pepa" (index 0)
jmena = $"Seznam jmen: {String.Join(",", list)}"; // Aktualizace proměnné s výpisem
Console.WriteLine(jmena);

// list.Remove() - metoda, která odstraní zadanou hodnotu podle názvu (první výskyt)
list.Remove("Karel"); // Odstraní "Karel"
jmena = $"Seznam jmen: {String.Join(",", list)}";
Console.WriteLine(jmena);
```

### Přehled metod seznamu (List)

| Metoda | Co dělá | Příklad |
|---|---|---|
| `Add(hodnota)` | Přidá prvek na konec seznamu | `list.Add("Jirka");` |
| `RemoveAt(index)` | Odstraní prvek na dané pozici | `list.RemoveAt(0);` |
| `Remove(hodnota)` | Odstraní první výskyt hodnoty | `list.Remove("Karel");` |
| `Count` | Vlastnost – vrátí počet prvků | `list.Count` → `4` |
| `Insert(index, hodnota)` | Vloží prvek na danou pozici | `list.Insert(0, "Adam");` |
| `Clear()` | Odstraní všechny prvky | `list.Clear();` |
| `Contains(hodnota)` | Zjistí, jestli seznam obsahuje hodnotu | `list.Contains("Pepa")` → `true`/`false` |

> **Otestuj:** Po každé operaci (`Add`, `RemoveAt`, `Remove`) se podívej na výpis v konzoli – seznam se pokaždé změní.

---

## 12) Třída (class) – co to je a proč ji vytvořit

### Co je třída?

**Třída (class)** je **šablona** (předpis) pro vytváření objektů. Definuje, jaké **vlastnosti** (data) a **metody** (chování) budou mít objekty vytvořené podle této třídy.

### Analogie

Představ si třídu jako **formulář** a objekt jako **vyplněný formulář**:
- Třída `Student` říká: „Každý student má jméno, příjmení a věk."
- Objekt (instance) `s1` je konkrétní student: „Jan Novák, 20 let."

### Kdy vytvořit třídu?

Třídu vytvoříme, když potřebujeme **sdružit více vlastností do jednoho celku**. Místo tří oddělených proměnných:

```csharp
// Špatně – nepřehledné pro víc studentů
string jmeno1 = "Jan";
string prijmeni1 = "Novák";
int vek1 = 20;

string jmeno2 = "Petr";
string prijmeni2 = "Svoboda";
int vek2 = 22;
```

Vytvoříme třídu a instance:

```csharp
// Dobře – přehledné a škálovatelné
var s1 = new Student("Jan", "Novák", 20);
var s2 = new Student("Petr", "Svoboda", 22);
```

### Příklad z našeho programu – definice třídy Student

**Kód bez komentářů:**

```csharp
public class Student
{
    public string jmeno;
    public string prijmeni;
    public int vek;

    public Student(string Jmeno, string Prijmeni, int Vek)
    {
        this.jmeno = Jmeno;
        this.prijmeni = Prijmeni;
        this.vek = Vek;
    }

    public string Popis()
    {
        return $"Student: {jmeno} {prijmeni}, věk: {vek}";
    }

    public string JinyZapisPopis() => $"Student: {jmeno} {prijmeni}, věk: {vek}";
}
```

**Kód s komentáři:**

```csharp
// Definice třídy Student
// class - klíčové slovo pro definici třídy
// Student - název třídy (konvence je psát názvy tříd s velkým počátečním písmenem)
// Třída je šablona pro vytváření objektů (instancí třídy)
public class Student
{
    // Vlastnosti třídy Student
    // public - vlastnost je veřejná a je přístupná z hlavní metody
    // string - datový typ vlastnosti (text)
    // int - datový typ vlastnosti (celé číslo)
    // jmeno, prijmeni, vek - názvy vlastností
    public string jmeno;
    public string prijmeni;
    public int vek;

    // Konstruktor třídy Student s parametry
    // Konstruktor je metoda, která se volá při vytvoření nové instance třídy a inicializuje její vlastnosti
    // Parametry konstruktoru jsou jméno, příjmení a věk studenta
    public Student(string Jmeno, string Prijmeni, int Vek)
    {
        // Inicializace vlastností třídy hodnotami z parametrů
        // this - odkaz na aktuální instanci třídy (objekt)
        // používáme jej k rozlišení mezi vlastností a parametrem, pokud mají stejný název
        this.jmeno = Jmeno;
        this.prijmeni = Prijmeni;
        this.vek = Vek;
    }

    // Metoda Popis - vrací řetězec s popisem studenta
    // public - metoda je veřejná a je přístupná z hlavní metody
    // string - datový typ návratové hodnoty metody (text)
    // Popis() - název metody, bez parametrů
    public string Popis()
    {
        // return - klíčové slovo, které vrací hodnotu z metody
        return $"Student: {jmeno} {prijmeni}, věk: {vek}";
    }

    // Alternativní zápis metody Popis pomocí výrazu lambda (=>)
    // Pokud metoda obsahuje pouze jeden příkaz, můžeme ji zapsat zkráceně
    public string JinyZapisPopis() => $"Student: {jmeno} {prijmeni}, věk: {vek}";
}
```

### Klíčová slova a modifikátory přístupu

| Slovo | Význam |
|---|---|
| `class` | Klíčové slovo pro definici třídy |
| `public` | Veřejné – přístupné odkudkoliv (z jiných tříd, z Main atd.) |
| `private` | Soukromé – přístupné pouze uvnitř třídy (výchozí, pokud neuvedeme nic) |
| `internal` | Přístupné v rámci stejného projektu (assembly) |

---

## 13) Konstruktor

### Co je konstruktor?

**Konstruktor** je speciální metoda třídy, která se **automaticky zavolá při vytvoření nové instance** (objektu). Slouží k nastavení počátečních hodnot vlastností.

### Pravidla konstruktoru

- Má **stejný název jako třída**.
- **Nemá návratový typ** (ani `void`).
- Může mít **parametry** (hodnoty, které předáme při vytváření objektu).
- Třída může mít **více konstruktorů** s různými parametry (přetížení).

### Konstruktor s parametry (náš příklad)

**Kód bez komentářů:**

```csharp
public Student(string Jmeno, string Prijmeni, int Vek)
{
    this.jmeno = Jmeno;
    this.prijmeni = Prijmeni;
    this.vek = Vek;
}
```

**Kód s komentáři:**

```csharp
// Konstruktor třídy Student s parametry
// Konstruktor je metoda, která se volá při vytvoření nové instance třídy a inicializuje její vlastnosti
// Parametry konstruktoru jsou jméno, příjmení a věk studenta
// Student(string Jmeno, string Prijmeni, int Vek) - definice konstruktoru s parametry a jejich datovými typy
public Student(string Jmeno, string Prijmeni, int Vek)
{
    // Inicializace vlastností třídy hodnotami z parametrů
    // this - odkaz na aktuální instanci třídy (objekt)
    // this.jmeno odkazuje na vlastnost třídy, Jmeno (s velkým J) je parametr konstruktoru
    this.jmeno = Jmeno;
    this.prijmeni = Prijmeni;
    this.vek = Vek;
}
```

### Klíčové slovo `this`

`this` odkazuje na **aktuální instanci** (objekt) třídy. Používáme ho k rozlišení mezi vlastností třídy a parametrem metody, pokud se jmenují podobně:

```csharp
this.jmeno = Jmeno;
//    ↑          ↑
// vlastnost   parametr konstruktoru
// třídy       (předaná hodnota)
```

### Prázdný konstruktor

Pokud bychom chtěli vytvořit instanci bez zadání parametrů, přidáme **prázdný konstruktor**:

```csharp
// Prázdný konstruktor – bez parametrů
public Student() { }
```

Pak bychom studenta vytvořili takto:

```csharp
var s5 = new Student();    // Vytvoření instance bez parametrů
s5.jmeno = "Lukáš";       // Ruční nastavení vlastností
s5.prijmeni = "Novotný";
s5.vek = 18;
```

> V našem programu prázdný konstruktor nemáme – používáme konstruktor s parametry, který vlastnosti nastaví ihned při vytvoření objektu.

---

## 14) Vytváření instancí (objektů)

### Co je instance?

**Instance** (objekt) je **konkrétní výskyt** třídy s vlastními hodnotami. Třídu jsme přirovnali k formuláři – instance je vyplněný formulář.

Klíčové slovo `new` říká: „Vytvoř nový objekt podle šablony (třídy) a zavolej konstruktor."

### Příklad z našeho programu

**Kód bez komentářů:**

```csharp
var s1 = new Student("Jan", "Novák", 20);
var s2 = new Student("Petr", "Svoboda", 22);
var s3 = new Student("Karel", "Černý", 19);
var s4 = new Student("Mirek", "Procházka", 21);
```

**Kód s komentáři:**

```csharp
// new Student() - vytvoření nové instance třídy Student
// Student - třída, která reprezentuje studenta (je vytvořená dále v kódu)
// s1, s2, s3, s4 - názvy proměnných, které budou obsahovat jednotlivé instance třídy Student (tkz. objekty)
// Konstruktor třídy Student - metoda, která se volá při vytvoření nové instance třídy a inicializuje její vlastnosti
// Parametry konstruktoru jsou jméno, příjmení a věk studenta (to je to, co píšeme do závorek)

var s1 = new Student("Jan", "Novák", 20);
var s2 = new Student("Petr", "Svoboda", 22);
var s3 = new Student("Karel", "Černý", 19);
var s4 = new Student("Mirek", "Procházka", 21);

// Každá proměnná (s1, s2, s3, s4) obsahuje jinou instanci třídy Student s vlastními hodnotami
```

### Co se stane v paměti?

| Proměnná | jmeno | prijmeni | vek |
|---|---|---|---|
| `s1` | "Jan" | "Novák" | 20 |
| `s2` | "Petr" | "Svoboda" | 22 |
| `s3` | "Karel" | "Černý" | 19 |
| `s4` | "Mirek" | "Procházka" | 21 |

> **Otestuj:** Zkus přidat `Console.WriteLine(s1.jmeno);` – vypíše `Jan`.

---

## 15) Přístup k vlastnostem objektu (tečková notace)

### Co je tečková notace?

K vlastnostem a metodám objektu přistupujeme pomocí **tečky** (`.`): `objekt.vlastnost` nebo `objekt.metoda()`.

### Příklad z našeho programu

**Kód bez komentářů:**

```csharp
Console.WriteLine(s1.jmeno);
Console.WriteLine(s2.jmeno);
Console.WriteLine(s1.prijmeni);
```

**Kód s komentáři:**

```csharp
// Přístup k vlastnostem objektu pomocí tečkové notace
// Vlastnosti jsou definované ve třídě Student (jmeno, prijmeni, vek)
// Vlastnosti jsou veřejné (public), takže k nim můžeme přistupovat z hlavní metody
// Našeptávač - po napsání tečky se zobrazí seznam dostupných vlastností a metod
Console.WriteLine(s1.jmeno);    // Vypíše: Jan
Console.WriteLine(s2.jmeno);    // Vypíše: Petr
Console.WriteLine(s1.prijmeni); // Vypíše: Novák
```

> **Tip pro VS 2022:** Po napsání `s1.` se zobrazí **IntelliSense** – automatické našeptávání, které ukáže všechny dostupné vlastnosti a metody objektu. Stačí vybrat a stisknout **Tab** nebo **Enter**.

---

## 16) Seznam instancí (List objektů)

### Proč seznam objektů?

Když máme víc objektů stejného typu, je praktické je uložit do seznamu. Pak s nimi můžeme pracovat hromadně (procházet, filtrovat, řadit apod.).

### Způsob 1: Vytvoření prázdného seznamu a postupné přidávání

**Kód bez komentářů:**

```csharp
var liststud = new List<Student>() { };

liststud.Add(s1);
liststud.Add(s2);
liststud.Add(s3);
liststud.Add(s4);
```

**Kód s komentáři:**

```csharp
// Vytvoření seznamu studentů a přidání jednotlivých studentů do seznamu
// new List<Student>() - vytvoření nové instance seznamu, který bude obsahovat hodnoty typu Student (objekty třídy Student)
var liststud = new List<Student>() { };

// Přidání jednotlivých studentů do seznamu pomocí metody Add
liststud.Add(s1);
liststud.Add(s2);
liststud.Add(s3);
liststud.Add(s4);
```

### Způsob 2: Vytvoření seznamu s okamžitou inicializací

**Kód bez komentářů:**

```csharp
var SeznamStudentu = new List<Student>()
{
    new Student("Mirek", "Procházka", 21),
    new Student("Karel", "Černý", 19),
    new Student("Petr", "Svoboda", 22),
    new Student("Jan", "Novák", 20),
    new Student("Anna", "Malá", 18),
    new Student("Eva", "Bílá", 23)
};

Console.WriteLine($"Počet studentů: {SeznamStudentu.Count}");
```

**Kód s komentáři:**

```csharp
// new List<Student>() s inicializací - vytvoření seznamu studentů přímo s hodnotami
var SeznamStudentu = new List<Student>()
{
    // new Student() - vytvoření nové instance třídy Student s parametry
    // Přidání jednotlivých studentů přímo do seznamu při jeho vytvoření
    // Každý objekt je oddělen čárkou a přidáváme je mezi {}. Nezapomeňte na středník na konci řádku
    new Student("Mirek", "Procházka", 21),
    new Student("Karel", "Černý", 19),
    new Student("Petr", "Svoboda", 22),
    new Student("Jan", "Novák", 20),
    new Student("Anna", "Malá", 18),
    new Student("Eva", "Bílá", 23)
}; // Zde je ten středník :)

// Výpis počtu studentů v seznamu pomocí vlastnosti Count (Vypíše délku listu)
Console.WriteLine($"Počet studentů: {SeznamStudentu.Count}");
```

### Porovnání obou způsobů

| Způsob | Kdy použít |
|---|---|
| Prázdný seznam + `Add()` | Když objekty přidáváš postupně (třeba v cyklu nebo na základě vstupu) |
| Seznam s inicializací | Když předem znáš všechny hodnoty |

---

## 17) Cyklus foreach

### Co je foreach?

Cyklus `foreach` prochází **všechny prvky** v kolekci (seznamu, poli) **od prvního do posledního**. Pro každý prvek vykoná blok kódu v `{ }`.

### Syntaxe

```csharp
foreach (DatovýTyp proměnná in kolekce)
{
    // kód, který se vykoná pro každý prvek
}
```

### Příklad z našeho programu

**Kód bez komentářů:**

```csharp
foreach (var student in liststud)
{
    Console.WriteLine($"Student: {student.jmeno} {student.prijmeni}, věk: {student.vek}");
}
```

**Kód s komentáři:**

```csharp
// Výpis seznamu studentů do konzole pomocí cyklu foreach
// foreach - cyklus, který prochází všechny hodnoty v seznamu (defaultně od začátku (od 0) do konce (do délky pole))
// student - název proměnné, která bude obsahovat aktuální hodnotu ze seznamu při každé iteraci cyklu
// Jednoduše řečeno - pro každý objekt (student) v seznamu (liststud) proveď následující blok kódu
// in liststud - určuje, ze seznamu liststud (který obsahuje objekty třídy Student) se budou brát hodnoty do proměnné student

// student sebere z první pozice (index 0) objekt s1, vykoná blok kódu, pak sebere z druhé pozice (index 1) objekt s2, vykoná blok kódu, atd. až do konce seznamu
foreach (var student in liststud)
{
    Console.WriteLine($"Student: {student.jmeno} {student.prijmeni}, věk: {student.vek}"); // Výpis vlastností aktuálního studenta
}
```

### Jak foreach funguje krok za krokem?

| Iterace | `student` obsahuje | Výstup |
|---|---|---|
| 1. | `s1` (Jan Novák, 20) | `Student: Jan Novák, věk: 20` |
| 2. | `s2` (Petr Svoboda, 22) | `Student: Petr Svoboda, věk: 22` |
| 3. | `s3` (Karel Černý, 19) | `Student: Karel Černý, věk: 19` |
| 4. | `s4` (Mirek Procházka, 21) | `Student: Mirek Procházka, věk: 21` |

> **Otestuj:** Zkus přidat dalšího studenta do `liststud` pomocí `liststud.Add(new Student("Nový", "Student", 25));` a sleduj, že foreach ho automaticky vypíše.

---

## 18) Metody ve třídě

### Co je metoda?

**Metoda** je blok kódu uvnitř třídy, který vykonává určitou akci. Může přijímat **parametry** (vstupní data) a **vracet hodnotu** (výstup).

### Struktura metody

```
modifikátor návratovýTyp Název(parametry)
{
    // tělo metody
    return hodnota; // pokud návratový typ není void
}
```

| Část | Příklad | Popis |
|---|---|---|
| Modifikátor | `public` | Kdo může metodu volat |
| Návratový typ | `string` | Jaký typ dat metoda vrací (`void` = nic nevrací) |
| Název | `Popis` | Jak se metoda jmenuje |
| Parametry | `()` | Co metoda přijímá na vstupu (prázdné = nic) |
| `return` | `return "text";` | Vrátí hodnotu z metody |

### Příklad z našeho programu – metoda Popis()

**Kód bez komentářů:**

```csharp
public string Popis()
{
    return $"Student: {jmeno} {prijmeni}, věk: {vek}";
}
```

**Kód s komentáři:**

```csharp
// Metoda Popis - vrací řetězec s popisem studenta
// public - metoda je veřejná a je přístupná z hlavní metody
// string - datový typ návratové hodnoty metody (text)
// Popis() - název metody, bez parametrů (v závorkách by byly parametry, pokud by nějaké byly)
public string Popis()
{
    // return - klíčové slovo, které vrací hodnotu z metody
    return $"Student: {jmeno} {prijmeni}, věk: {vek}";
}
```

### Alternativní zápis – lambda výraz (=>)

Pokud metoda obsahuje **pouze jeden příkaz**, můžeme ji zapsat zkráceně pomocí `=>`:

**Kód bez komentářů:**

```csharp
public string JinyZapisPopis() => $"Student: {jmeno} {prijmeni}, věk: {vek}";
```

**Kód s komentáři:**

```csharp
// Alternativní zápis metody Popis pomocí výrazu lambda (=>)
// Funguje stejně jako metoda Popis() výše – jen kratší zápis
// Hodí se, pokud metoda obsahuje pouze jeden příkaz (jeden řádek)
public string JinyZapisPopis() => $"Student: {jmeno} {prijmeni}, věk: {vek}";
```

### Volání metody v Main

**Kód bez komentářů:**

```csharp
Console.WriteLine(s1.Popis());
```

**Kód s komentáři:**

```csharp
// s1.Popis() - volání metody Popis() na objektu s1
// Metoda Popis() je definovaná ve třídě Student a vrací řetězec s popisem studenta
// Console.WriteLine pak tento řetězec vypíše do konzole
Console.WriteLine(s1.Popis()); // Vypíše: Student: Jan Novák, věk: 20
```

---

## 19) Rychlý tahák

### Git operace

| Operace | Co dělá | VS 2022 | Fork |
|---|---|---|---|
| **Commit** | Uloží změny lokálně | Git Changes → Commit All | Changes → Stage → Commit |
| **Push** | Odešle commity na GitHub | Git → Push | Tlačítko Push |
| **Fetch** | Zjistí nové změny (nestáhne) | Git → Fetch | Tlačítko Fetch |
| **Pull** | Stáhne a zapracuje změny | Git → Pull | Tlačítko Pull |
| **Branch** | Vytvoří novou větev | Git → New Branch | Pravý klik → New Branch |
| **Merge** | Sloučí větev | Git → Manage Branches → Merge | Pravý klik → Merge |

### C# pojmy

| Pojem | Vysvětlení |
|---|---|
| **Proměnná** | Pojmenované místo v paměti pro uložení hodnoty |
| **Datový typ** | Určuje, jakou hodnotu proměnná uchovává (`int`, `string`, `double`, `bool`) |
| **Přetypování** | Převod hodnoty z jednoho datového typu na jiný |
| **Interpolace** | Vkládání proměnných do textu: `$"Text {proměnná}"` |
| **List (seznam)** | Dynamická kolekce hodnot – lze přidávat/odebírat |
| **Třída (class)** | Šablona pro vytváření objektů s vlastnostmi a metodami |
| **Instance (objekt)** | Konkrétní výskyt třídy vytvořený pomocí `new` |
| **Konstruktor** | Metoda volaná při vytvoření instance – nastavuje počáteční hodnoty |
| **Metoda** | Blok kódu ve třídě, který vykonává akci |
| **foreach** | Cyklus procházející všechny prvky kolekce |
| **this** | Odkaz na aktuální instanci třídy |
| **return** | Vrátí hodnotu z metody |

### Klávesové zkratky ve VS 2022

| Zkratka | Akce |
|---|---|
| **Ctrl + F5** | Spustit bez debuggeru |
| **F5** | Spustit s debuggerem |
| **Ctrl + S** | Uložit soubor |
| **Ctrl + K, Ctrl + C** | Zakomentovat vybraný kód |
| **Ctrl + K, Ctrl + U** | Odkomentovat vybraný kód |
| **Ctrl + .** | Rychlé opravy a návrhy (Quick Actions) |
| **F12** | Přejít na definici |
| **Ctrl + Space** | Vyvolat IntelliSense (našeptávání) |

---

*Autor: učební materiál k předmětu – C# konzolová aplikace, Git/GitHub, VS 2022, .NET 9.*
