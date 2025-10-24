
# Klasser eksempel
```C#
namespace Oblig1;

public class Punkt2D
{
	// Datamedlemmer
	private double x, y;
	
	// Tilgangsmedlemmer
    public double X
    {
        get { return x; }
        set {
	        if (value < 0) lengde = 0;
	        else x = value; }
    }
    
    public double Y
    {
        get { return y; }
        set { y = value; }
    }

    // Konstruktører
    public Punkt2D() : this(0,0)
    {
        //X = 0;
        //Y = 0;
    }

    public Punkt2D(double nyX, double nyY) {
        this.X = nyX;
        this.Y = nyY;
    }
}
```

```C#
namespace N02_O5
{
    class KomplekstTall
    {
        // datamedlemmer lages av kompilator
        public double Re
        {
            get;
            set; 
        }
        public double Im 
        {
            get;
            set; 
        }

        public KomplekstTall(double iR, double iI)
        {
            this.Re = iR;
            this.Im = iI;
        }
        public KomplekstTall() : this(0,0)
        {
        }

        public double Abs()
        {
            return Math.Sqrt(Re*Re + Im*Im);
        }

        public KomplekstTall LeggTil(KomplekstTall denAndre)
        {
            KomplekstTall svar = new KomplekstTall();
            svar.Re = this.Re + denAndre.Re;
            svar.Im = this.Im + denAndre.Im;
            return svar;
            // return new KomplekstTall(this.Re + denAndre.Re, this.Im + denAndre.Im);
        }

        public KomplekstTall MultipliserMed(KomplekstTall denAndre)
        {
            KomplekstTall svar = new KomplekstTall();
            svar.Re = this.Re * denAndre.Re - this.Im * denAndre.Im;
            svar.Im = this.Im * denAndre.Re + this.Re * denAndre.Im;
            return svar;
        }

        public string UtskriftKartesisk()
        {
            // kan trimmes mer for å håndtere 0-verdier og negative Im
            return string.Format($"{Re} + {Im}i");
        }

        public KomplekstTall KomleksKonjugert()
        {
            return new KomplekstTall(this.Re, -this.Im);
        }
        public string UtskriftPolar()
        {
            double r = this.Abs();
            double theta = Math.Atan2(this.Im, this.Re);

            return string.Format($"{r} * e^({theta}i)");
        }



    }
}
```

```C#
namespace N01_O1_Start
{
    class Rektangel
    {
        private double lengde;
        private double bredde;

        public Rektangel(): this(0,0)
        {
            // Lengde = 0;
            // Bredde = 0;
        }

        public Rektangel(int iL, int iB)
        {
            Lengde = iL;
            Bredde = iB;    
        }

        public double Lengde
        {
            get { return lengde; }
            set 
            {
                if (value < 0) lengde = 0;
                else lengde = value; 
            }
        }

        public double Bredde
        {
            get { return bredde; }
            set 
            {
                if (value < 0) bredde = 0;
                else bredde = value;
            }
        }

        public double Areal()
        {
            return Lengde * Bredde;
        }

        public void Tegn(char tegn)
        {
            int rader = Convert.ToInt32(Math.Round(Lengde));
            int kolonner = Convert.ToInt32(Math.Round(Bredde));

            for (int i = 0; i < rader; i++)
            {
                for (int j = 0; j < kolonner; j++)
                {
                    Console.Write(tegn);
                }
                Console.WriteLine();
            }
        }

        public void LesDimensjoner()
        {
            Console.WriteLine("Oppgi bredde:");
            Bredde = LesEtTall();
            Console.WriteLine("Oppgi lengde:");
            Lengde = LesEtTall();
        }

        private double LesEtTall()
        {
            double svar = 0;

            bool ferdig = false;
            while (!ferdig)
            {
                try
                {
                    Console.Write("Oppgi et desimaltall: ");
                    svar = Convert.ToDouble(Console.ReadLine());

                    if (svar < 0)
                    {
                        // throw new Exception();
                        Console.WriteLine("Feil: Verdien må være et desimaltall større enn 0. " +
                       "\n Prøv på nytt ");
                    }
                    else
                    {
                        ferdig = true;
                    }
                }
                catch (Exception)
                {
                    Console.WriteLine("Feil: Verdien må være et desimaltall større enn 0. " +
                        "\n Prøv på nytt ");
                }

            }
            return svar;
        }

        public bool ErStørreEnn(Rektangel r)
        {
            bool svar = false;

            // if (this.Areal() > r.Areal())
            if (Areal() > r.Areal())
            {
                svar = true;
            }

            return svar;
        }

        public void SkrivData()
        {
            // Console.WriteLine("Rektangel ({0},{1}) med areal {2} er størst.", l, b, Areal(l, b));
            Console.WriteLine($"Rektangel ({Bredde},{Lengde}) med areal {Areal()} er størst.");
        }

        //public void Foo() 
        //{
        //    Console.WriteLine(Areal());
        //}
    }
}
```


## Interface
Program
```C#
namespace O3;

class Program
{
    static void Main(string[] args)
    {
        List<ISensor> Liste = new List<ISensor>(1000);
        for (int i = 0; i < 5; i++)
        {
            Liste.Add(new Temperaturmåler(i + 1));
            Liste[i].PosisjonX = 1;
            Liste[i].PosisjonY = i + 1;
        }
        for (int i = 0; i < 5; i++)
        {
            Liste.Add(new Trykkmåler(i + 6));
            Liste[i + 5].PosisjonX = i * 2 + 1;
            Liste[i + 5].PosisjonY = 1;
        }

        foreach (ISensor obj in Liste)
        {
            obj.Maal();
            if (obj is Temperaturmåler tempmåler)
            {
                Console.WriteLine($"ID: {tempmåler.Id}, TEMPERATUR: {tempmåler.Temperatur:f2}");
            }
            else if (obj is Trykkmåler trykkmåler)
            {
                Console.WriteLine($"ID: {trykkmåler.Id}, TEMPERATUR: {trykkmåler.Trykk:f2}");
            }

            Console.WriteLine($"{obj.ToString()}");

        }
        
    }
}
```
Interface
```C#
namespace O3;

interface ISensor 
{ 
    double PosisjonX 
    { 
      get; 
      set; 
    } 
    double PosisjonY 
    { 
      get; 
      set; 
    } 
    int Id 
    { 
      get; 
    } 

    void Maal(); 
    string ToString(); 
} 

```
Klasse 1
```C#
namespace O3;

public class Temperaturmåler : ISensor
{
    // Konstruktør
    public Temperaturmåler() : this(0) {}
    public Temperaturmåler(int Id) {
        PosisjonX = 0;
        PosisjonY = 0;
        this.id = Id;
    }


    private double x, y;
    private int id;
    private double temperatur;


    public double PosisjonX {
        get { return x; }
        set {
            if ((value < -180) || (value > 179)) x = 0;
            else x = value;
        }
    }

    public double PosisjonY {
        get { return y; }
        set {
            if ((value < -90) || (value > 90)) y = 0;
            else y = value;
        }
    }

    public int Id{get { return id; }}
    
    public double Temperatur {
        get { return temperatur; }
        set { temperatur = value; }
    }

    public void Maal() {
        Random R = new Random();
        Temperatur = R.NextDouble() * 1273.1;
    }
    public override string ToString() {
        return $"c-({this.PosisjonX},{this.PosisjonY})";
    }


}
```


# Første faget
#### Eksempel 1 out og med returverdi
 ```C#
 namespace O3
 {
     internal class Program
     {
         static void Main(string[] args)
         {
             double radius = 0;
             double hoyde = 0;
             double volum = 0;
 
             Introduksjon();
 
             LesSylinderDimensjoner(out radius, out hoyde);
 
             volum = SylinderVolum(radius, hoyde);
 
             Utskrift(radius, hoyde, volum);
 
             Console.ReadKey(true);
         }
 
         static void Introduksjon()
         {
             Console.Write("En sylinders volum er gitt ved formel 'V = PI * r^2 * h'\n");
             Console.Write("Der 'r' er radius og 'h' er høyde. \n");
         }
 
         static void LesSylinderDimensjoner(out double radius, out double hoyde)
         {
             Console.Write("Skriv inn radius: ");
             radius = double.Parse(Console.ReadLine());
             Console.Write("Skriv inn høyde: ");
             hoyde = double.Parse(Console.ReadLine());
         }
 
         static double SylinderVolum(double radius, double hoyde)
         {
             return Math.PI * Math.Pow(radius, 2) * hoyde;
         }
 
         static void Utskrift(double radius, double hoyde, double volum)
         {
             Console.Write("Volum til en sylinder med radus " + radius.ToString());
             Console.Write(" og høyde " + hoyde.ToString() + " er lik ");
             Console.WriteLine(volum.ToString());
         }
     }
 }
 
 ```

#### Eksempel 2 out
```C#
namespace O4
{
    internal class Program
    {
        static void Main(string[] args)
        {
            
            KompMult(1, 2, 3, -4, out string C);
            Console.WriteLine(C);
        }
        static void KompMult(float Ar, float Aj, float Br, float Bj, out string C)
        {
            float Cr = Ar * Br - Aj * Bj;
            float Cj = Ar * Bj + Aj * Br;
            if (Cj < 0)
            {
                C = $"{Cr} - {Math.Abs(Cj)}j";
            } else
            {
                C = $"{Cr} + {Cj}j";
            }
        }
    }
}
```


# Eksamen Vår 2023
## Oppgave 1
```C#
// a
{
 string a = "Charlie";
 int b = -29;
 double c = 2.72;
 char d = 'D';
 string[] e = {"Dette", "går", "bra"};
 char f = '#';
 Boolean g = true;
 Console.WriteLine(a);
 Console.WriteLine(b);
 Console.WriteLine(c);
 Console.WriteLine(d);
 Console.WriteLine(e);
 Console.WriteLine(f);
}

// b
{
    Random r = new Random();
    int tall = r.Next(25,36);
    Console.WriteLine(tall);
}

// c 
{
    for (int i = 1001; i <= 1999; i=i+2) {
        Console.WriteLine(i);
    }
}

// d
{
    int [] tabell = new int[100];
    for (int i = 0; i < 100; i++) {
        tabell[i] = i+1;
}}

// e
{
    for (int i = 1; i <= 100; i++) {
        if (i%9 == 0) {
            Console.WriteLine(i);
        }
}}

// f
{
    int a = 1, b = 2, c = 3, d = 4;
    double svar;
    int suma = a + 3*b;
    double sumb = Math.Pow(c,3) / Math.Sqrt(d);

    if (suma > sumb) {
        svar = suma;
    } else {
        svar = sumb;
    }
}

// g
{
    Console.WriteLine("Skriv inn ett ord");
    string input = Console.ReadLine();
    Console.WriteLine(input.Length);
}

// h
{
    for (int p = 10; p < 20; p++) {
        Console.WriteLine(p);
    }
}

// i
{
    void Utskrift(int tall) {
        Console.WriteLine(tall);
    }

    Utskrift(3);
}

// j
{
    float x = 3, y = 4;
    Midtpunkt(x, y, out float svars);
    
    static void Midtpunkt(float x, float y, out float svar) {
        svar = (x + y) / 2;
    }
}

```

## Oppgave 3

# Eksamen Vår 2022
## Oppgave 1
```C#
/* Skriv C#-programkode som oppretter et tilfeldig desimaltall, og skriver det ut med 5 siffer bak komma.
Programmet skal generere et nytt tilfeldig tall for hver programutføring. */
{
    Random r = new Random();
    float tall = (float)r.NextDouble();
    Console.WriteLine($"{tall:F5}");
}

/* Skriv C#-programkode som skriver ut alle tall i den lille multiplikasjonstabellen for 7, dvs. 7, 14, 21, ... 70.
Programmet skal bruke løkke. */
{
    for (int i = 1; i <= 10; i++) Console.WriteLine(7*i);
}

/* Skriv C#-programkode som ber brukeren taste inn en 4-siffret kode (heltall) og som skriver ut teksten
"Koden er korrekt. Det er åpent!" dersom koden er lik en kode du har lagret i programmet (en kode du har
valgt selv mens du programmerer).
Dersom brukeren taster feil kode skal programmet skrive ut "Koden er feil. Prøv igjen!" og be om ny
inntasting.
Programmet skal be om ny input hver gang det tastes feil (tall som ikke er 4-sifret eller annet ugyldig input).
Programmet skal avslutte når det tastes 0 (null).
Merk: Programmet må ikke krasje (gi kjøretidsfeil) dersom brukeren taster ugyldig input. */
{
    bool loop = true;
    while(loop) {
        try {
            Console.WriteLine("Skriv inn PIN: ");
            string PIN = Console.ReadLine();
            switch (PIN) {
                case "1234":
                    Console.WriteLine("Riktig kode!");
                    loop = false; break;
                case "0":
                    Console.WriteLine("Avbryter.");
                    loop = false; break;
                default:
                    Console.WriteLine("Ikke riktig PIN");
                    break;
            }
        } catch {
            Console.WriteLine("Feil input. Forsøk igjen.");
        }
    }
}

/* Lag et C#-program som spør brukeren etter et ord med lengde maks 15 tegn.
Skriv deretter ut ordet på skjermen, baklengs. Om ordet er lengre enn 15 tegn skal det i stedet gis en
feilmelding. */
{
    try {
        Console.WriteLine("SKriv inn et ord med lengde maks 15 tegn:");
        string ord = Console.ReadLine();
        if (ord.Length > 15) 
            Console.WriteLine("For langt ord! " + ord.Length);
        else {
            Console.WriteLine("Baklengs:");
            for (int i = ord.Length; i >= 1; i--){
                Console.Write(ord[i-1]);
            }
        }
    } catch {
        Console.WriteLine("feil input");
    }
}

/* Oppgi C# kode som skriver ut en tilfeldig, liten, bokstav (‘a’-‘z’) på skjermen. Programmet skal generere
en ny tilfeldig bokstav for hver programutføring. */
{
    while(true) {
        string alfabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
        
        Random r = new Random();
        int index = r.Next(1,alfabet.Length);
        Console.WriteLine(alfabet[index]);
        Console.ReadLine();
    }
}


/* Lag et C#-program som oppretter en liste av tekststrenger. Listen skal ha ti elementer. La programmet
legge inn teksten "a" som første element, "aa" som andre element, "aaaa" som tredje og så videre, dvs. at
antall ‘a’ dobles for hvert element i lista. */
{
    List<string> list = new List<string>();
    for (int i = 0; i < 10; i++) {
        string temp = "";
        for (int j = 1; j <= Math.Pow(2,i); j++) {
            temp = temp + "a";
        }
        list.Add(temp);
        Console.WriteLine(list[i]);
    }
}

/* h) Lag en C#-metode (metoden skal ha navnet Fakultet) som tar imot et heltall N (fra for eksempel
hovedprogrammet) og beregner svaret 1*2*3* ... *N. Metoden skal returnere resultatet (skal ikke være
"void"). */
{
    long Fakultet(long tall) {
        for (long i = tall-1; i > 0; i--) tall = tall *i;
        return tall;
    }
    Console.WriteLine(Fakultet(10));
}

/* i) Lag en C#-metode (kall den Fakultet2) som tar imot en et heltall N (fra for eksempel
hovedprogrammet) og beregner svaret 1*2*3* ... *N. Metoden skal ha "void" som returdatatype, men
likevel kunne levere resultatet til kallende program. Metoden skal ikke bruke globale variabler eller
tilsvarende. */
{
     void Fakultet(long tall, out long svar) {
        for (long i = tall-1; i > 0; i--) tall = tall *i;
        svar = tall;
    }
    long svar;
    Fakultet(4, out svar);
    Console.WriteLine(svar);
}

```
## Oppgave 2