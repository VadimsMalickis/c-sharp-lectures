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

# Redzamības modifikatori

Redzamības modifikatori nosaka, kur objektiem un metodēm drīkst piekļūt.

---

# Public

Pieejams visur.

```csharp
public string Name;
```

Piemērs:

```csharp
Person person = new Person();

person.Name = "Anna";
```

Tas strādā, jo lauks ir `public`.

---

# Private

Pieejams tikai pašas klases iekšienē.

```csharp
private int age;
```

Piemērs:

```csharp
class Person
{
    private int age;
}
```

Šāds kods radīs kļūdu:

```csharp
Person p = new Person();

p.age = 18;
```

Kļūda:

```text