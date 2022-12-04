# programiranje
using System;
using System.Collections.Generic;
using System.Text;
using System.Text.RegularExpressions;

namespace ConsoleApp15
{
    class Program
    {
        static void unos (int n,int m,List<int> [] lista)
        {
            for (int i = 0; i < n; i++)
            {
                lista[i] = new List<int>();
            }
            for (int i = 0; i < m; i++)
            {
                Console.WriteLine("Uneti vezu");
                int a = int.Parse(Console.ReadLine());
                int b = int.Parse(Console.ReadLine());
                lista[a].Add(b);
            }
        }
        static void ispis(int n, List<int>[] lista)
        {
            for (int i = 0; i <n; i++)
            {
                Console.WriteLine("cvor " + i + " je u povezan sa sledecim cvorovima:");
                foreach (int x in lista[i])
                {
                    Console.WriteLine(x);
                }


            }
        }
        static bool udubinu(int r1, int r2, List<int>[] lista)
        {
            if (r1 == r2) return true;
            foreach (int p in lista[r1])
            { 
              if(  udubinu(p, r2, lista)) return true;
            }
            return false;


        }
        static bool udubinu2(int r1, int r2, List<int>[] lista, bool[] posecen)
        {
            if (r1 == r2) return true;
            if (posecen[r1]) return false;
            posecen[r1] = true;
            foreach (int p in lista[r1])
            {
                if (udubinu2(p, r2, lista, posecen)) return true;
            }
            return false;
        }
        static bool udubinustek(int r1, int r2, List<int>[] lista)
        {
            Stack<int> stek = new Stack<int>();
            bool[] posecen = new bool[lista.Length];
            bool postoji = false;
            stek.Push(r1);
            while (stek.Count > 0 && !postoji)
            {
                int p = stek.Pop();
                foreach (int i in lista[p])
                {
                    if (i == r2)
                    {
                        postoji = true;
                        break;
                    }
                    if (!posecen[i])
                    {
                        posecen[i] = true;
                        stek.Push(i);
                    }
                }
            }
            return postoji;
        }
        static bool usirinu(int r1, int r2, List<int>[] lista)
        {
            Queue<int> red = new Queue<int>();
            bool[] posecen = new bool[lista.Length];
            bool postoji = false;
            red.Enqueue(r1);
            while (red.Count > 0 && !postoji)
            {
                int p = red.Dequeue();
                foreach (int i in lista[p])
                {
                    if (i == r2)
                    {
                        postoji = true;
                        break;
                    }
                    if (!posecen[i])
                    {
                        posecen[i] = true;
                        red.Enqueue(i);
                    }
                }

            }
            return postoji;
        }
        static void unosmatrica( int m, bool[,] matrica)
        {
            for (int i = 0; i < m; i++)
            {
                Console.WriteLine("Unesite vezu");
                int a = int.Parse(Console.ReadLine());
                int b = int.Parse(Console.ReadLine());
                matrica[a, b] = true;
                matrica[b, a] = true;
            }
        }
        static void ispismatrica(int n, bool[,] matrica)
        {
            for (int i = 0; i < n; i++)
            {
             for (int j = 0; j < n; j++)
                {
                    Console.WriteLine(matrica[i, j]);
                }
            }
        }
        static int ntina_0(int a, int n)
        {
            return a & (~(1 << n));
        }
        static int ntina_1(int a, int n)
        {
            return a | (1 << n);
        }
        static int onvertujn(int a, int n)
        {
            return a ^ (1 << n);
        }
        static int isvaki3ci(int n)
        {
            int m = 1;
            while (n > m)
            {
                n = n ^ m;
                m = m << 3;
            }
            return n;
            
        }
        static int brojbitova(int n)
        {
            int br = 0;
            while (n > 0)
            {
                br++;
                n = n >> 1;
            }
            return br;
        }
        static int brojjedinica(int n)
        {
            int br = 0;
            while (n > 0)
            {
                if ((n & 1) == 1) br++;
                n = n >> 1;
            }
            return br;
        }
        static int zbirdvabroja(int x, int y)
        {
            while (y > 0)
            {
                int pom = x & y;
                x = x ^ y;
                y = pom << 1;
            }
            return x;
        }
        static int razlikadvabroja(int x, int y)
        {
            while (y > 0)
            {
                int pom = (~x) & y;
                x = x ^ y;
                y = pom << 1;
            }
            return x;
        }
        static int ostatakprideljenju(int x, int y)
        {
            int k = x & (y - 1);
            return k; 
        }
        static int provera(int i,int n)
        {
            n = n >> i;
            return n & 1;
        }
        static int razlikabrojakecevaizmedjuleveidesnestrane(int n,int a)
        {
            int x=0;
            int y= 0; ;
            for (int i = 0; i < a; i++)
            {
                if ((n & 1)==1 && (i < a / 2)) x++;
                if ((n & 1)==1 && (i > a / 2)) y++;
            }
            return (x - y);
        }
        static int invertovanjebitova(int n)
        {
            int m = 0;
            while (n > 0)
            {
                if ((n & 1) == 1) m = m | 1;
                m = m << 1;
                n = n >> 1;
            }
            return m >> 1;
        }
        static bool palindrom(string s1)
        {
            string s2 = "";
            s1.ToLower();
            s1.Replace(" ", "");
            int br = s1.Length;
            while(br>0)
            {
                s2 = s2 + s1[br];
                br--;
            }
            if (s1 == s2) return true;
            else return false;
        }
        static int proveradalisenekarecsadriziudrugojigde(string s1, string s2)
        {
            s1.ToLower();
            s2.ToLower();
            if (s1.Contains(s2)) return s1.IndexOf(s2);
            return -1;
        }
        static int kolikoseputasadrzirecudrugoj(string s1, string s2)
        {
            int br = 0;
            s1.ToLower();
            s2.ToLower();
            if (s1.Contains(s2))
            {
                s1 = s1.Remove(s1.IndexOf(s2), 1);
                br++;
            }
            return br;
        }
        static int domine(string s1, int n)
        {
            int br = 0;
            for (int i = 1; i <= s1.Length / 2; i++)
            {
                string a = s1.Substring(0, i);
                string b = s1.Substring(s1.Length - i, i);
                if (a.Equals(b)) br =i;
            }
            if (br == 0) return s1.Length * n;
            else return (s1.Length * n) - ((n - 1) * br);
            
        }
        static int ciklicni(string s1)
        {
            string n = s1;
            int br = n.Length;
            for (int i = 0; i < n.Length; i++)
            {
                char a = s1[0];
                s1 = s1.Remove(0, 1) + Convert.ToString(a);
                if (n.Equals(s1))br++ ;
            }
            return br;
        }
        static void periodicna(string s1)
        {
            string pom = "";
            for (int i = 1; i < (s1.Length-1)/2; i++)
            {
                string a = s1.Substring(0, i);
                string b = s1.Substring(i, i);
                if (a.Equals(b)) pom = a;   
            }
            if (pom != "") Console.WriteLine("jeste");
            else Console.WriteLine("nije");
        }
        
        static void Main(string[] args)
        {

            Console.WriteLine("unesite broj cvorova i froj veza");
            int n = int.Parse(Console.ReadLine());
            int m = int.Parse(Console.ReadLine());
            List<int>[] lista = new List<int>[n];
            bool[,] matrica = new bool[n, n];
            unosmatrica(m, matrica);
            ispismatrica(n, matrica);
            unos(n, m, lista);
            ispis(n, lista);
            Console.WriteLine("unsite dva cvora za proveru povezanosti");
            int r1 = int.Parse(Console.ReadLine());
            int r2 = int.Parse(Console.ReadLine());
            if (udubinu(r1, r2, lista)) Console.WriteLine("povezani su");
            else Console.WriteLine("nisu povezani");


            StringBuilder s1 = new StringBuilder(Console.ReadLine());
            StringBuilder s3 = new StringBuilder(Console.ReadLine());
            StringBuilder s2 = new StringBuilder(s1.Length);
            int brojac = s1.Length;
            while (brojac > 0)
            {
                s2.Append(s1[brojac - 1]);
            }
            if (s1.Equals(s2)) Console.WriteLine("palindrom je ");


            string sablon = @"\b[m..M]\w+";
            string sablon2 = @"\w+[m..M]\b";
            string sablon3 = @"\s+";
            Regex rg = new Regex(sablon);
            Regex rg2 = new Regex(sablon2);
            string tekst = Console.ReadLine();
            MatchCollection pok = rg.Matches(tekst);
            foreach (var x in pok)
            {
                Console.WriteLine(x);
            }
            Console.ReadKey();
        }

    }
}
