# Lekcija: C# Namespaces

## Mācību mērķis

Pēc šīs tēmas apguves students spēs:

- paskaidrot, kas ir `namespace`;
- saprast, kāpēc namespaces tika izveidoti;
- izmantot `using` direktīvas;
- organizēt projektu lielākās programmās;
- novērst klašu nosaukumu konfliktus;
- veidot savus namespaces.

---

# Kas ir Namespace?

Namespace ir mehānisms, kas ļauj grupēt saistītas klases, struktūras, interfeisus un citus programmas elementus.

Vienkāršāk sakot:

> Namespace ir mapes analogs programmēšanā.

Piemērs failu sistēmā:

```text
Documents
|
+-- School
|
+-- Photos
|
+-- Music
```

Līdzīgi C#:

```csharp
namespace School
{
    class Student
    {
    }
}
```

Šeit klase `Student` pieder namespace `School`.

---

# Kāpēc namespaces tika izgudroti?

Iedomāsimies, ka pasaulē ir daudz programmētāju.

Dažādi izstrādātāji var izveidot klasi ar vienādu nosaukumu:

```csharp
class Student
{
}
```

un

```csharp
class Student
{
}
```

Kompilators nezinātu, kuru klasi izmantot.

Namespaces atrisina šo problēmu.

---

# Nosaukumu konflikta piemērs

Bez namespaces:

```csharp
class Student
{
}

class Student
{
}
```

Rezultāts:

```text
Compilation Error
```

---

# Namespaces atrisina konfliktu

```csharp
namespace School
{
    class Student
    {
    }
}

namespace University
{
    class Student
    {
    }
}
```

Tagad abas klases var eksistēt vienlaicīgi.

---

# Pilns klases nosaukums

Patiesībā klase sastāv no:

```text
Namespace + Class
```

Piemērs:

```text
School.Student
```

un

```text
University.Student
```

Tās ir divas dažādas klases.

---

# Kā izmantot pilno nosaukumu?

```csharp
School.Student schoolStudent =
    new School.Student();

University.Student universityStudent =
    new University.Student();
```

---

# Namespace sintakse

```csharp
namespace LibrarySystem
{
    class Book
    {
    }
}
```

---

# Vairākas klases vienā namespace

```csharp
namespace LibrarySystem
{
    class Book
    {
    }

    class Author
    {
    }

    class Member
    {
    }
}
```

Tas palīdz sakārtot projektu.

---

# Kas ir using?

Ja katru reizi būtu jāraksta:

```csharp
LibrarySystem.Book book =
    new LibrarySystem.Book();
```

kods kļūtu pārāk garš.

Tāpēc izmanto:

```csharp
using LibrarySystem;
```

Pēc tam:

```csharp
Book book = new Book();
```

---

# Izmantošana praksē

```csharp
using LibrarySystem;

Book book = new Book();
```

Kompilators zina, ka `Book` atrodas namespace `LibrarySystem`.

---

# Populārākie .NET namespaces

Ikdienā programmētāji nepārtraukti izmanto namespaces.

---

## System

Pamata funkcijas.

```csharp
using System;
```

Ļauj izmantot:

```csharp
Console
Math
DateTime
Random
```

---

## System.Collections.Generic

Kolekcijas.

```csharp
using System.Collections.Generic;
```

Piemērs:

```csharp
List<string> names =
    new List<string>();
```

---

## System.IO

Darbs ar failiem.

```csharp
using System.IO;
```

Piemērs:

```csharp
File.WriteAllText(
    "test.txt",
    "Hello");
```

---

## System.Text

Darbs ar tekstiem un kodējumiem.

```csharp
using System.Text;
```

Piemērs:

```csharp
Encoding.UTF8
```

---

## System.Numerics

Vektori un matricas.

```csharp
using System.Numerics;
```

Piemērs:

```csharp
Vector2 position =
    new Vector2(10, 20);
```

---

# Kā darbojas using?

Šis kods:

```csharp
using System;

Console.WriteLine("Sveiki!");
```

ir tas pats kas:

```csharp
System.Console.WriteLine("Sveiki!");
```

`using` vienkārši saīsina rakstīšanu.

---

# Savu namespace izveide

Piemērs:

```csharp
namespace SchoolManagement
{
    class Student
    {
        public string Name;
    }
}
```

Izmantošana:

```csharp
using SchoolManagement;

Student student =
    new Student();
```

---

# Namespace vairākos failos

Fails:

```text
Student.cs
```

```csharp
namespace SchoolManagement
{
    class Student
    {
    }
}
```

Fails:

```text
Teacher.cs
```

```csharp
namespace SchoolManagement
{
    class Teacher
    {
    }
}
```

Abas klases atrodas vienā namespace.

---

# Hierarhiski namespaces

Namespaces var veidot vairākos līmeņos.

```csharp
namespace Company.Project.Database
{
}
```

---

# Piemērs

```csharp
namespace School.Library.Books
{
    class Book
    {
    }
}
```

Pilns nosaukums:

```text
School.Library.Books.Book
```

---

# Faila-scoped namespace (C# 10+)

Mūsdienu C# bieži izmanto:

```csharp
namespace LibrarySystem;

class Book
{
}
```

Tas ir tas pats kas:

```csharp
namespace LibrarySystem
{
    class Book
    {
    }
}
```

Vienkārši īsāk.

---

# Reāls projekts

```text
LibrarySystem
|
+-- Models
|   |
|   +-- Book.cs
|   +-- Author.cs
|
+-- Services
|   |
|   +-- BookService.cs
|
+-- Data
|   |
|   +-- Database.cs
```

Namespaces:

```csharp
namespace LibrarySystem.Models;
```

```csharp
namespace LibrarySystem.Services;
```

```csharp
namespace LibrarySystem.Data;
```

Tas palīdz uzturēt kārtību lielos projektos.

---

# Kad namespaces ir īpaši svarīgi?

Mazās programmās:

```csharp
100 - 200 rindas
```

atšķirība nav ļoti jūtama.

Lielos projektos:

```csharp
50+
klases

100+
faili

vairāki programmētāji
```

bez namespaces projekts kļūtu grūti uzturams.

---

# Tipiskākās kļūdas

## Aizmirsts using

```csharp
List<string> names =
    new List<string>();
```

Kļūda:

```text
The type or namespace name 'List'
could not be found
```

Risinājums:

```csharp
using System.Collections.Generic;
```

---

## Namespace konflikts

```csharp
School.Student
```

un

```csharp
University.Student
```

Tad jānorāda pilnais nosaukums.

---

## Nepareizs namespace

Fails:

```csharp
namespace Library
{
}
```

bet mēģinām izmantot:

```csharp
using Books;
```

Rezultāts:

```text
Compiler Error
```

---

# Praktiskais uzdevums

Izveido namespace:

```csharp
SchoolManagement
```

Tajā izveido klases:

```csharp
Student
Teacher
Course
```

Katram objektam pievieno vismaz vienu lauku.

Pēc tam:

1. Pievieno `using SchoolManagement;`
2. Izveido pa vienam objektam no katras klases.
3. Izvada datus konsolē.

---

# Kontroljautājumi

1. Kas ir namespace?
2. Kāpēc namespaces tika izveidoti?
3. Kādu problēmu tie atrisina?
4. Ko dara `using`?
5. Vai vienā namespace var atrasties vairākas klases?
6. Vai viena klase var atrasties vairākos namespaces?
7. Kas ir faila-scoped namespace?
8. Kāds ir namespace galvenais ieguvums lielos projektos?

---

# Kopsavilkums

✅ Namespace ir klašu organizēšanas mehānisms.

✅ Namespace palīdz izvairīties no nosaukumu konfliktiem.

✅ `using` ļauj izmantot namespace elementus īsākā formā.

✅ Vienā namespace var atrasties daudzas klases.

✅ Namespaces ir īpaši svarīgi lielos projektos.

✅ .NET bibliotēkās plaši izmanto namespaces, piemēram:

```csharp
System
System.IO
System.Text
System.Collections.Generic
System.Numerics
```

✅ Pašu veidotos projektos ieteicams veidot savus namespaces, lai kods būtu sakārtots un viegli uzturams.

> Namespaces programmēšanā ir tas pats, kas mapes failu sistēmā - tās palīdz uzturēt kārtību un novērst neskaidrības lielos projektos.