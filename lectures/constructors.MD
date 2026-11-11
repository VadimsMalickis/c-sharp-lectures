# Lekcija: C# Konstruktori, Getter un Setter

## Mācību mērķis

Pēc šīs tēmas apguves students spēs:

- paskaidrot, kas ir konstruktors;
- izveidot konstruktorus ar un bez parametriem;
- saprast konstruktoru pielietojumu;
- izveidot īpašības (*Properties*) ar `get` un `set`;
- paskaidrot datu enkapsulācijas (Encapsulation) nozīmi;
- izmantot getterus un setterus datu validācijai.

---

# Kas ir konstruktors?

Konstruktors ir īpaša metode, kas tiek izsaukta automātiski objekta izveides brīdī.

Piemērs:

```csharp
Student s = new Student();
```

Kad izpildās:

```csharp
new Student();
```

automātiski tiek izsaukts konstruktors.

---

# Kāpēc nepieciešami konstruktori?

Pieņemsim, ka katram studentam jāpiešķir sākotnējās vērtības.

Bez konstruktora:

```csharp
Student s = new Student();

s.Name = "Anna";
s.Age = 18;
```

Ar konstruktoru:

```csharp
Student s =
    new Student("Anna", 18);
```

Kods kļūst īsāks un drošāks.

---

# Vienkāršākais konstruktors

```csharp
class Student
{
    public Student()
    {
        Console.WriteLine("Objekts izveidots!");
    }
}
```

Izmantošana:

```csharp
Student s = new Student();
```

Rezultāts:

```text
Objekts izveidots!
```

---

# Konstruktora pazīmes

Konstruktors:

✅ Sakrīt ar klases nosaukumu

✅ Tam nav atgriežamā tipa

✅ Tiek izsaukts automātiski

---

# Nepareizs piemērs

```csharp
public void Student()
{
}
```

Šī nav konstruktora definīcija.

Tā ir parasta metode.

---

# Pareizs piemērs

```csharp
public Student()
{
}
```

---

# Konstruktors bez parametriem

To sauc par noklusējuma konstruktoru.

```csharp
class Student
{
    public string Name;

    public Student()
    {
        Name = "Nezināms";
    }
}
```

Izmantošana:

```csharp
Student s = new Student();

Console.WriteLine(s.Name);
```

Rezultāts:

```text
Nezināms
```

---

# Konstruktors ar parametriem

Ļauj nodot datus objekta izveides laikā.

```csharp
class Student
{
    public string Name;

    public Student(string name)
    {
        Name = name;
    }
}
```

Izmantošana:

```csharp
Student s = new Student("Jānis");

Console.WriteLine(s.Name);
```

Rezultāts:

```text
Jānis
```

---

# Vairāki parametri

```csharp
class Student
{
    public string Name;
    public int Age;

    public Student(string name, int age)
    {
        Name = name;
        Age = age;
    }
}
```

Izmantošana:

```csharp
Student s =
    new Student("Anna", 17);
```

---

# Konstruktora galvenā ideja

Objekts tiek uzreiz izveidots korektā stāvoklī.

```csharp
Student s =
    new Student("Anna", 17);
```

nav jāatceras vēlāk piešķirt visas vērtības.

---

# Vairāki konstruktori (Overloading)

Vienai klasei var būt vairāki konstruktori.

```csharp
class Book
{
    public string Title;

    public Book()
    {
        Title = "Nezināma grāmata";
    }

    public Book(string title)
    {
        Title = title;
    }
}
```

Izmantošana:

```csharp
Book b1 = new Book();

Book b2 =
    new Book("C# Pamati");
```

---

# Konstruktori reālajā dzīvē

Bibliotēkas sistēma:

```csharp
Book book =
    new Book(
        "C# Pamati",
        "Jānis Ozols",
        2025);
```

Students:

```csharp
Student student =
    new Student(
        "Anna",
        18,
        "IT-21");
```

Bankas konts:

```csharp
BankAccount account =
    new BankAccount(
        "LV01BANK123");
```

---

# Kas ir Properties?

Līdz šim izmantojām publiskus laukus.

```csharp
public int Age;
```

Tas nav ideāls risinājums.

Jebkurš var ierakstīt:

```csharp
student.Age = -50;
```

Kas nav korekti.

---

# Getter un Setter

Properties ļauj kontrolēt datu piekļuvi.

```csharp
public int Age
{
    get;
    set;
}
```

---

# Kas ir get?

Getter atgriež vērtību.

```csharp
Console.WriteLine(
    student.Age);
```

Tiek izmantots:

```csharp
get
```

---

# Kas ir set?

Setter piešķir vērtību.

```csharp
student.Age = 18;
```

Tiek izmantots:

```csharp
set
```

---

# Auto-implemented Property

Visizplatītākais variants.

```csharp
public string Name
{
    get;
    set;
}
```

Saīsināta forma.

Kompilators pats izveido slēpto lauku.

---

# Pilns variants

```csharp
private string name;

public string Name
{
    get
    {
        return name;
    }

    set
    {
        name = value;
    }
}
```

Tas dara tieši to pašu.

---

# Kāpēc izmantot Properties?

Lai validētu datus.

---

# Piemērs

```csharp
private int age;

public int Age
{
    get
    {
        return age;
    }

    set
    {
        if (value >= 0)
        {
            age = value;
        }
    }
}
```

---

# Kas ir value?

Setterī rezervētais mainīgais:

```csharp
student.Age = 18;
```

Šeit:

```csharp
value = 18
```

---

# Validācijas piemērs

```csharp
Student student =
    new Student();

student.Age = -5;
```

Vecums netiks saglabāts.

Jo:

```csharp
if (value >= 0)
```

nosacījums nav izpildīts.

---

# Tikai lasāma īpašība

```csharp
public string University
{
    get;
}
```

Vērtību var lasīt:

```csharp
Console.WriteLine(student.University);
```

Bet nevar mainīt:

```csharp
student.University = "RTU";
```

Kļūda.

---

# Tikai rakstāma īpašība

Retāk sastopama.

```csharp
private string password;

public string Password
{
    set
    {
        password = value;
    }
}
```

---

# Privāts Setter

Ļoti populārs risinājums.

```csharp
public string StudentId
{
    get;
    private set;
}
```

Lasīt drīkst visi.

Mainīt drīkst tikai pati klase.

---

# Properties un konstruktors kopā

```csharp
class Student
{
    public string Name
    {
        get;
        set;
    }

    public int Age
    {
        get;
        set;
    }

    public Student(
        string name,
        int age)
    {
        Name = name;
        Age = age;
    }
}
```

Izmantošana:

```csharp
Student student =
    new Student(
        "Anna",
        18);
```

---

# Reāls piemērs

```csharp
class Book
{
    public string Title
    {
        get;
        set;
    }

    public int Year
    {
        get;
        set;
    }

    public Book(
        string title,
        int year)
    {
        Title = title;
        Year = year;
    }
}
```

Objekta veidošana:

```csharp
Book book =
    new Book(
        "C# Pamati",
        2025);
```

---

# Enkapsulācija

Getter un setter ir daļa no OOP principa:

```text
Encapsulation
```

jeb datu paslēpšana.

Ideja:

```text
Neļauj lietotājiem piekļūt datiem tieši.
```

Tā vietā:

```text
Kontrolē piekļuvi caur Properties.
```

---

# Tipiskākās kļūdas

## Public lauki visur

```csharp
public int Age;
```

Labāk:

```csharp
public int Age
{
    get;
    set;
}
```

---

## Konstruktors ar nepareizu nosaukumu

Nepareizi:

```csharp
public void Student()
{
}
```

Pareizi:

```csharp
public Student()
{
}
```

---

## Getter bez return

Nepareizi:

```csharp
get
{
}
```

Pareizi:

```csharp
get
{
    return age;
}
```

---

# Praktiskais uzdevums

Izveido klasi:

```csharp
Car
```

Īpašības:

```csharp
Brand
Year
Mileage
```

Prasības:

- izmantot Properties;
- izveidot konstruktoru;
- nepieļaut negatīvu nobraukumu;
- izvadīt informāciju par automašīnu.

Piemērs:

```csharp
Car car =
    new Car(
        "Audi",
        2022,
        15000);
```

---

# Kontroljautājumi

1. Kas ir konstruktors?
2. Kad tiek izsaukts konstruktors?
3. Vai konstruktoram ir atgriežamais tips?
4. Kāpēc izmanto konstruktorus?
5. Kas ir getter?
6. Kas ir setter?
7. Kas ir `value` setterī?
8. Kāpēc izmantot Properties lauku vietā?
9. Kas ir enkapsulācija?
10. Kā ierobežot datu mainīšanu no ārpuses?

---

# Kopsavilkums

✅ Konstruktors ir īpaša metode objekta inicializēšanai.

✅ Konstruktors tiek izsaukts automātiski, izmantojot `new`.

✅ Vienai klasei var būt vairāki konstruktori.

✅ Getter (`get`) lasa vērtību.

✅ Setter (`set`) piešķir vērtību.

✅ Properties ļauj kontrolēt piekļuvi datiem.

✅ Properties palīdz validēt lietotāja ievadītos datus.

✅ Getter un setter ir svarīga enkapsulācijas daļa.

✅ Reālos projektos Properties tiek izmantotas daudz biežāk nekā publiski lauki.

> Labs OOP kods neļauj nekontrolēti mainīt objektu datus. Konstruktori nodrošina korektu objekta izveidi, bet Properties kontrolē piekļuvi šiem datiem visā programmas darbības laikā.