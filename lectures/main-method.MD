# Lekcija: C# `Main()` metode

## Mācību mērķis

Pēc šīs lekcijas skolēns spēs:

- izskaidrot, kas ir `Main()` metode;
- saprast, kāpēc programma sāk darboties tieši no `Main()`;
- uzrakstīt vairākus `Main()` metodes variantus;
- izmantot komandrindas argumentus;
- saprast atgriežamo vērtību (`return`) nozīmi.

---

# Kas ir `Main()` metode?

`Main()` ir **programmas sākuma punkts** (*Entry Point*).

Kad operētājsistēma palaiž programmu, .NET izpildvide meklē metodi:

```csharp
Main()
```

un sāk izpildīt kodu no tās.

Vienkāršāk sakot:

> `Main()` ir pirmā metode, ko izpilda programma.

---

# Vienkāršākais piemērs

```csharp
class Program
{
    static void Main()
    {
        Console.WriteLine("Sveika pasaule!");
    }
}
```

Rezultāts:

```text
Sveika pasaule!
```

Programmas darbības secība:

1. Tiek atrasta `Main()` metode.
2. Izpildās `Console.WriteLine()`.
3. Programma beidzas.

---

# Kāpēc nepieciešams `static`?

Parasti metodes pieder objektiem.

Tomēr programmas sākumā vēl nav neviena objekta.

Tāpēc `Main()` jābūt:

```csharp
static
```

Piemērs:

```csharp
static void Main()
{
}
```

Tas ļauj izsaukt metodi bez objekta izveides.

---

# Kāpēc tiek izmantots `void`?

`void` nozīmē:

> metode neko neatgriež.

```csharp
static void Main()
{
    Console.WriteLine("Programma darbojas");
}
```

Šeit programma vienkārši izpilda darbības un beidzas.

---

# Programmas izpildes plūsma

Apskatīsim piemēru:

```csharp
class Program
{
    static void Main()
    {
        Console.WriteLine("1");

        SayHello();

        Console.WriteLine("3");
    }

    static void SayHello()
    {
        Console.WriteLine("2");
    }
}
```

Rezultāts:

```text
1
2
3
```

Izpildes secība:

```text
Main()
 ↓
Console.WriteLine("1")
 ↓
SayHello()
 ↓
Console.WriteLine("2")
 ↓
atgriežas uz Main()
 ↓
Console.WriteLine("3")
```

---

# Main ar parametriem

Programma var saņemt informāciju no komandrindas.

```csharp
static void Main(string[] args)
{
    Console.WriteLine(args[0]);
}
```

Palaižot:

```text
Program.exe Jānis
```

Rezultāts:

```text
Jānis
```

---

# Kas ir `args`?

`args` ir komandrindas argumentu masīvs.

Piemērs:

```csharp
static void Main(string[] args)
{
    foreach (string item in args)
    {
        Console.WriteLine(item);
    }
}
```

Palaišana:

```text
Program.exe Anna 18 Rīga
```

Rezultāts:

```text
Anna
18
Rīga
```

---

# Main ar atgriežamo vērtību

Dažreiz programmai jāpasaka operētājsistēmai, vai viss izdevās.

Tad izmanto:

```csharp
static int Main()
{
    return 0;
}
```

---

# Ko nozīmē Return Code?

Parasti:

```text
0 = veiksme
```

```text
1 = kļūda
```

Piemērs:

```csharp
static int Main()
{
    Console.WriteLine("Viss izdevās");

    return 0;
}
```

---

## Kļūdas gadījums

```csharp
static int Main()
{
    Console.WriteLine("Kļūda");

    return 1;
}
```

---

# Mūsdienu C# pieeja

Sākot no C# 9, iespējams rakstīt kodu bez redzamas `Main()` metodes.

Piemērs:

```csharp
Console.WriteLine("Sveika pasaule!");
```

Kompilators pats ģenerē:

```csharp
class Program
{
    static void Main()
    {
        Console.WriteLine("Sveika pasaule!");
    }
}
```

To sauc par:

```text
Top-level statements
```

---

# Kad izmantot klasisko Main?

Mācību nolūkos:

```csharp
class Program
{
    static void Main()
    {
    }
}
```

jo tas palīdz saprast programmas struktūru.

---

# Biežākās kļūdas

## 1. Aizmirsts `static`

Nepareizi:

```csharp
void Main()
{
}
```

Pareizi:

```csharp
static void Main()
{
}
```

---

## 2. Metode ārpus klases

Nepareizi:

```csharp
static void Main()
{
}
```

(atrodas ārpus klases)

Pareizi:

```csharp
class Program
{
    static void Main()
    {
    }
}
```

---

## 3. Nepareizs argumenta tips

Nepareizi:

```csharp
static void Main(string args)
{
}
```

Pareizi:

```csharp
static void Main(string[] args)
{
}
```

---

# Praktiskais uzdevums

Izveido programmu, kas:

1. Sagaida lietotāja vārdu.
2. Izvada sveicienu.
3. Aprēķina lietotāja vecumu pēc 5 gadiem.

Paraugs:

```text
Ievadi vārdu: Jānis
Ievadi vecumu: 17

Sveiks Jāni!
Pēc 5 gadiem tev būs 22 gadi.
```

Programmai obligāti jāsākas no:

```csharp
static void Main()
{
}
```

---

# Kontroljautājumi

1. Kas ir `Main()` metode?
2. Kāpēc `Main()` metodei jābūt `static`?
3. Ko nozīmē `void`?
4. Kāda ir atšķirība starp `void Main()` un `int Main()`?
5. Kam paredzēts parametrs `string[] args`?
6. Ko nozīmē atgrieztā vērtība `0`?
7. Kas ir *Top-level statements*?

---

# Kopsavilkums

Svarīgākie fakti:

✅ `Main()` ir programmas sākuma punkts.

✅ Programma sāk izpildi no `Main()`.

✅ `static` ļauj metodi izsaukt bez objekta.

✅ `void` nozīmē, ka metode neko neatgriež.

✅ `string[] args` ļauj saņemt komandrindas argumentus.

✅ `int Main()` var atgriezt programmas izpildes kodu.

✅ Jaunajās C# versijās var izmantot *Top-level statements*, bet aizkulisēs joprojām eksistē `Main()` metode.

> Galvenais, ko atcerēties:
>
> Katrā C# konsoles lietotnē ir viens sākuma punkts, un tas ir `Main()` metodes izsaukums.