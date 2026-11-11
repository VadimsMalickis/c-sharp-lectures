# C# OOP Pamati: Klases, Objekti, Static un Redzamības Modifikatori

## Mācību mērķis

Pēc šīs tēmas apguves students spēs:

- paskaidrot, kas ir klase un objekts;
- izveidot savas klases;
- izveidot objektus no klasēm;
- saprast atšķirību starp statiskiem un nestatiskiem laukiem;
- saprast atšķirību starp statiskām un nestatiskām metodēm;
- izmantot redzamības modifikatorus (`public`, `private`);
- izvēlēties piemērotu pieeju konkrētai situācijai.

---

# Kas ir klase?

Klase ir veidne (šablons), pēc kuras tiek veidoti objekti.

Piemēram:

```text
Klase -> Auto rasējums
Objekts -> Reāla automašīna
```

Programmēšanā klase apraksta:

- kādi dati tiks glabāti;
- kādas darbības būs iespējams veikt.

Piemērs:

```csharp
class Person
{
    public string Name;
    public int Age;
}
```

Šī klase apraksta personu.

Katram objektam būs:

- vārds (`Name`);
- vecums (`Age`).

---

# Kas ir objekts?

Objekts ir konkrēta klases instance.

Piemērs:

```csharp
Person person1 = new Person();
```

Šeit tiek izveidots objekts pēc klases `Person`.

Varam piešķirt datus:

```csharp
person1.Name = "Jānis";
person1.Age = 18;
```

Izvadām:

```csharp
Console.WriteLine(person1.Name);
Console.WriteLine(person1.Age);
```

Rezultāts:

```text
Jānis
18
```

---

# Vairāki objekti

No vienas klases var izveidot daudz objektu.

```csharp
Person p1 = new Person();
Person p2 = new Person();
```

Katrs objekts glabā savus datus.

```csharp
p1.Name = "Anna";
p2.Name = "Pēteris";
```

Rezultāts:

```text
Anna
Pēteris
```

---

# Nestatiski (parasti) lauki

Nestatiski lauki pieder katram objektam atsevišķi.

```csharp
class Student
{
    public string Name;
}
```

Izveidojam objektus:

```csharp
Student s1 = new Student();
Student s2 = new Student();
```

Piešķiram vērtības:

```csharp
s1.Name = "Anna";
s2.Name = "Jānis";
```

Katram objektam ir sava vērtība.

---

# Kas ir static?

Dažreiz dati nepieder konkrētam objektam.

Tie pieder visai klasei.

Tad izmanto:

```csharp
static
```

---

# Statisks lauks

Piemērs:

```csharp
class School
{
    public static string SchoolName;
}
```

Piekļuve:

```csharp
School.SchoolName = "Rīgas Valsts ģimnāzija";

Console.WriteLine(School.SchoolName);
```

Rezultāts:

```text
Rīgas Valsts ģimnāzija
```

---

# Kāpēc izmantot static?

Padomā par bibliotēku.

```text
Bibliotēkas nosaukums
```

ir viens visai sistēmai.

Nav vajadzīgi vairāki nosaukumi katram objektam.

Tāpēc:

```csharp
public static string LibraryName;
```

ir loģiska izvēle.

---

# Static lauka piemērs

```csharp
class Library
{
    public static int TotalBooks;
}
```

Piekļuve:

```csharp
Library.TotalBooks = 120;

Console.WriteLine(Library.TotalBooks);
```

Nav nepieciešams veidot objektu.

---

# Nestatisks lauks

```csharp
class Book
{
    public string Title;
}
```

Piekļuve:

```csharp
Book book = new Book();

book.Title = "C# Pamati";
```

Šeit objekts ir nepieciešams.

---

# Static metode

Statiska metode pieder klasei.

```csharp
class Calculator
{
    public static int Add(int a, int b)
    {
        return a + b;
    }
}
```

Izsaukums:

```csharp
int result = Calculator.Add(5, 3);

Console.WriteLine(result);
```

Rezultāts:

```text
8
```

---

# Nestatiska metode

Nestatiska metode pieder objektam.

```csharp
class Dog
{
    public void Bark()
    {
        Console.WriteLine("Vau!");
    }
}
```

Izsaukums:

```csharp
Dog dog = new Dog();

dog.Bark();
```

Rezultāts:

```text
Vau!
```

---

# Salīdzinājums

## Static

```csharp
Library.ShowStatistics();
```

Izsaukums caur klasi.

---

## Non-static

```csharp
Book book = new Book();

book.ShowInfo();
```

Izsaukums caur objektu.

---

# Kad izmantot static?

Izmanto, ja:

✅ Dati ir kopīgi visai sistēmai

✅ Metodei nav vajadzīgs objekta stāvoklis

✅ Aprēķini ir universāli

Piemēri:

```csharp
Math.Sqrt()
Math.Round()
Math.Abs()
```

Visas ir statiskas metodes.

---

# Kad izmantot objektus?

Izmanto, ja:

✅ Katram objektam ir savi dati

✅ Sistēmā eksistē vairāki neatkarīgi objekti

Piemēri:

```text
Grāmatas
Studenti
Automašīnas
Klienti
Pasūtījumi
```

---


Pareizi:

```csharp
Person person = new Person();

person.Name = "Anna";
```

---

## 2. Piekļuve private laukam

Nepareizi:

```csharp
person.age = 18;
```

Ja `age` ir `private`.

---

## 3. Statiska metode mēģina izmantot nestatisku lauku

Nepareizi:

```csharp
public static void Show()
{
    Console.WriteLine(Name);
}
```

Ja `Name` nav statisks.

---

# Kontroljautājumi

1. Kas ir klase?
2. Kas ir objekts?
3. Ko nozīmē `static`?
4. Kad izmantot statisku lauku?
5. Kad izmantot objektu laukus?
6. Ar ko atšķiras statiska un nestatiska metode?
7. Ko dara modifikators `public`?
8. Ko dara modifikators `private`?
9. Kāpēc bieži izmanto `private` laukus?
10. Vai statiskai metodei nepieciešams objekts?

---

# Kopsavilkums

✅ Klase ir objekta veidne.

✅ Objekts ir klases instance.

✅ Nestatiski lauki pieder katram objektam atsevišķi.

✅ Statiski lauki pieder visai klasei.

✅ Statiskas metodes izsauc caur klasi.

✅ Nestatiskas metodes izsauc caur objektu.

✅ `public` ļauj piekļūt no jebkuras vietas.

✅ `private` ļauj piekļūt tikai pašas klases iekšienē.

✅ `static` izmanto kopīgiem datiem un darbībām.

✅ Objektus izmanto, ja katram elementam nepieciešami savi dati.
