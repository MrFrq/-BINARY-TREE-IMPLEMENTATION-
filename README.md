# -BINARY-TREE-IMPLEMENTATION-
BINARY TREE IMPLEMENTATION  C# 



using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace treeler
{


    class Block
    {
        public int data;
        public Block sol;
        public Block sag;

        public Block(int data)
        {
            this.data = data;
            sol =null;
            sag = null;
        }


    }
    /*
     public class TreeNode 
    {
      public int val;
      public TreeNode left;
      public TreeNode right;
      public TreeNode(int val=0, TreeNode left=null, TreeNode right=null) 
      {
          this.val = val;
          this.left = left;
          this.right = right;
      }
     }
     */
    class Agac
    {
        public Block kok;

        public Agac()
        {

            kok = null;

        }

        public Block yeniBlock(int data)
        {
            kok = new Block(data);
            Console.WriteLine(data + " agaca eklendi");
            return kok;

        }

        // AĞACA EKLEME TEKRARSIZ 
        #region AĞACA EKLEME TEKRARSIZ   
        /*  
        public Block agacaEkle(Block kok, int data)                      // O(n)  =  logN   // 2 tabbanında log    //  WORST CASE =  N 
        {


            if (kok != null)
            {
                if (data < kok.data)
                {
                    kok.sol = agacaEkle(kok.sol, data);
                }
                else if (data > kok.data)
                {
                    kok.sag = agacaEkle(kok.sag, data);
                }
                else  // eklenmeye çalışan değer ağaçta vardır
                    return null;
            }

            else
            {
                //kok = yeniBlock(data);
                kok = new Block(data);
                Console.WriteLine(data + " agaca eklendi");
                return kok; // 

            }
            return kok;

        }
        */
        #endregion

        public Block agacaEkle(Block kok, int data)                      // O(n)  =  logN   // 2 tabbanında log    //  WORST CASE =  N 
        {


            if (kok != null)
            {
                if (data < kok.data)
                {
                    kok.sol = agacaEkle(kok.sol, data);
                }
                else
                {
                    kok.sag = agacaEkle(kok.sag, data);             // TEKRAR EDEN ELEMAN OLURSA SAĞA EKLENSİN
                }

            }

            else
            {
                //kok = yeniBlock(data);
                kok = new Block(data);
                Console.WriteLine(data + " agaca eklendi");
                return kok; // 

            }
            return kok;

        }




        //public int calisma = 0;
        public void preOrder(Block kok)             //   KÖK - SOL - SAĞ 
        {

            //Console.Write(calisma==0 ? "KÖK-> " : "");
            //calisma++;

            if (kok != null)
            {
                Console.Write(kok.data + "  ");
                preOrder(kok.sol);
                preOrder(kok.sag);
            }

        }

        public void inOrder(Block kok)             //   SOL- KÖK - SAĞ 
        {

            if (kok != null)
            {
                inOrder(kok.sol);
                Console.Write(kok.data + "  ");
                inOrder(kok.sag);
            }
        }

        public void postOrder(Block kok)             //   SOL - SAĞ  - KÖK 
        {

            if (kok != null)
            {
                postOrder(kok.sol);
                postOrder(kok.sag);
                Console.Write(kok.data + "  ");
            }

        }

        public int elemanSayısı(Block kok)
        {
            if (kok == null) return 0;
            return 1 + elemanSayısı(kok.sol) + elemanSayısı(kok.sag);
        }

        /*  AMELASYON  düğüm sayısı 
        public int DugumSayisi(Block dugum) 
        {
            int count = 0;
            if (dugum !=null)
            {
                count = 1;
                count += DugumSayisi(dugum.sol);
                count += DugumSayisi(dugum.sag);
            }
            return count;
        }
        */

        #region YAPRAK İŞLEMLERİ 
        public int YaprakSayisi(Block kok)
        {
            if (kok == null) return 0;
            if (kok.sol == null && kok.sag == null) return 1;
            return YaprakSayisi(kok.sol) + YaprakSayisi(kok.sag);
        }
        public int YaprakSayisi1(Block kok)
        {
            return (kok == null) ? 0 : (kok.sol == null && kok.sag == null) ? 1 : YaprakSayisi1(kok.sol) + YaprakSayisi1(kok.sag);
        }
        public int YaprakToplami(Block kok)
        {
            //int toplam = 0;
            if (kok == null) return 0;
            if (kok.sol == null && kok.sag == null) return kok.data; //return toplam += kok.data;
            return YaprakToplami(kok.sol) + YaprakToplami(kok.sag);
        }
        public int YaprakToplami1(Block kok)
        {
            return (kok == null) ? 0 : (kok.sol == null && kok.sag == null) ?
                kok.data : YaprakToplami1(kok.sol) + YaprakToplami1(kok.sag);
        }

        // DÜĞÜMLERİN TOPLAMI 
        public int DüğümlerToplamı(Block kok)
        {
            if (kok == null) return 0;
            int soltoplam = DüğümlerToplamı(kok.sol);
            int sagtoplam = DüğümlerToplamı(kok.sag);
            Console.WriteLine(kok.data + " için: " + (soltoplam + sagtoplam));
            return kok.data + soltoplam + sagtoplam;
        }

        /*
        public int YaprakSayisi1(Block kok) 
        {
            
            if (kok !=null)
            {
                if (kok.sol == null && kok.sag == null)
                {
                    return 1;
                }
                else
                    return  YaprakSayisi(kok.sol) + YaprakSayisi(kok.sag);
            }
            return 0;
        }
        */ // yaprak sayısı 2

        /*
        public int YaprakSayisi2(Block kok)
        {
            int count = 0;
            if (kok != null)
            {
                if (kok.sol == null && kok.sag == null)
                {
                    count = 1 ;
                }
                else
                    count = count + YaprakSayisi2(kok.sol) + YaprakSayisi2(kok.sag);
            }

            return count;
        }
        */  // yaprak sayısı 3 
        #endregion


        public int Yukseklik(Block kok)      // AĞAÇ  YÜKSEKLİK'i = KÖK YÜKSEKLİĞİ 
        {
            if (kok == null) return -1;
            int l, r;
            l = Yukseklik(kok.sol);
            r = Yukseklik(kok.sag);
            if (l > r) return l +1;
            return r+1 ;


        } 
        
        public int maxderinlik(Block kök, int derinlik = 0)
        {
            if (kök == null) return 0;
            int lm = maxderinlik(kök.sol,derinlik+1) ; 
            int  rm = maxderinlik(kök.sag, derinlik + 1);

            if (lm == 0 && rm == 0) return derinlik;
            if (lm >= rm) return lm;
            return rm;
        
        }

        public void yerdegistir(Block kok)       // SAĞ DAL İLE SOL DALI "SWAP"  ETTİRECEĞİZ --- İNORDER İLE BÜYÜKTEN KÜÇÜĞE YAZDIRACAK
        {
            Block temp = null;
            if (kok != null)
            {
                yerdegistir(kok.sol);
                yerdegistir(kok.sag);

                temp = kok.sol;

                kok.sol = kok.sag;
                kok.sag = temp;
            }
        }

        //  AĞAÇTAN  ELEMAN SİLME  
        public Block agactansil(Block kok, int silinecek)
        {
            Block t1, t2;

            if (kok == null) { return null; }

            if (kok.data == silinecek)          // sileceğim düğüm budur 
            {
                if (kok.sol == kok.sag)    // silinecek düğümün altında dal yok demektir  // YAPRAK SİLİNECEK 
                {
                    kok = null;
                    return null;
                }
                else if (kok.sol == null)    //  silinecek düğümün solu boş 
                {
                    t1 = kok.sag;
                    return t1;
                }
                else if (kok.sag == null)    //  silinecek düğümün sağı boş
                {
                    t1 = kok.sol;
                    return t1;
                }
                else    // silinecek düğümün solu da sağı da dolu demektir 
                {
                    t1 = t2 = kok.sag;

                    while (t1.sol != null)
                    {
                        t1 = t1.sol;
                    }
                    t1.sol = kok.sol;   // yeni kök sağdaki oldu 

                    return t2;
                }

            }
            else
            {
                if (silinecek < kok.data)     // silinecek eleman ağacın sol dallarındadır 
                {
                    kok.sol = agactansil(kok.sol, silinecek);
                }
                else                        // // silinecek eleman ağacın sağ dallarındadır 
                {
                    kok.sag = agactansil(kok.sag, silinecek);
                }
            }
            return kok;
        }


        // AĞAÇTA ARAMA METODU   AMELASYON 
        //public bool ARAMA(Block kok, int aranan) 
        //{
        //    if (kok!=null)
        //    {
        //        if (aranan > kok.data)   //  aranan eleman aktif blockdan büyüktür --> sağa gidecek 
        //        {
        //            if (kok.sag != null)
        //            {
        //                return ARAMA(kok.sag, aranan);
        //            }
        //            return false;
        //        }
        //        else if (aranan < kok.data)
        //        {
        //            if (kok.sol != null)
        //            {
        //                return ARAMA(kok.sol, aranan);
        //            }
        //            return false;
        //        }
        //        else   //   aranan == kok.data
        //        {

        //            return true;
        //        }
        //    }
        //    return false;

        //} 

        public bool ARAMA(Block kok, int aranan)
        {
            if (kok == null) return false;
            if (kok.data == aranan) return true;
            if (ARAMA(kok.sol, aranan)) return true;
            if (ARAMA(kok.sag, aranan)) return true;
            return false;
        }
        //public bool ARAMA(Block kok, int aranan)
        //{
        //    if (kok == null) return false;
        //    if (kok.data == aranan) return true;
        //    if (kok.data > aranan) return ARAMA(kok.sol, aranan);
        //    return ARAMA(kok.sag, aranan);

        //}

        // TEKRAR EDEN ELEMAN SAYISI
        public int AraSay(Block kok, int aranan)
        {
            return kok == null ?
                0 : kok.data == aranan ?
                1 + AraSay(kok.sol, aranan) + AraSay(kok.sag, aranan) : AraSay(kok.sol, aranan) + AraSay(kok.sag, aranan);
        }
        // TEKRAR EDEN ELEMAN SAYISI  BEDO
        public int tekrar(Block kok, int aranan, int sayac = 0)
        {
            if (kok != null)
            {
                sayac = tekrar(kok.sol, aranan, sayac);
                sayac = tekrar(kok.sag, aranan, sayac);
                if (aranan == kok.data) sayac++;
            }
            return sayac;
        }

        // İKİ TREE EŞİT Mİ KONTROL 
        public bool EsitMi(Block kok1, Block kok2)
        {
            if ((kok1 == null) != (kok2 == null)) return false;  // biri boş biri doluysa false döndürür
            if (kok1 == null && kok2 == null) return true; // ikisi de boşsa  null=null dan TRUE döndürür
            if (kok1.data != kok2.data) return false;   // dataları eşit değilse false döndürür
            return EsitMi(kok1.sol, kok2.sol) && EsitMi(kok1.sag, kok2.sag);
        }

        public int istenenkatmandakielemansayısı(Block kok, int aranankatman, int mevcutkatman = 0)
        {
            return kok == null ? 0 : aranankatman == mevcutkatman ? 1
           : (istenenkatmandakielemansayısı(kok.sol, aranankatman, mevcutkatman + 1)
           + istenenkatmandakielemansayısı(kok.sag, aranankatman, mevcutkatman + 1));
        }
        public int istenenkatmandakielemanlartoplamı(Block kok, int aranankatman, int mevcutkatman = 0)
        {
            return kok == null ? 0 : aranankatman == mevcutkatman ? kok.data
           : (istenenkatmandakielemanlartoplamı(kok.sol, aranankatman, mevcutkatman + 1)
           + istenenkatmandakielemanlartoplamı(kok.sag, aranankatman, mevcutkatman + 1));
        }



        #region FİNAL ÇIKMIŞ 
        // FİNAL SORULARI		
       
        
        public int AltAgacToplami(Block kok)     
        {        
            if (kok == null) return 0;
            int soltoplam = AltAgacToplami(kok.sol);
            int sagtoplam = AltAgacToplami(kok.sag);
            Console.WriteLine(kok.data + " için: " + (soltoplam + sagtoplam));
            return kok.data + soltoplam + sagtoplam; 
        }
        #endregion

        public int alttoplam(Block kok) 
        {
            if (kok == null) return 0;
            int toplam = 0;
            if(kok.sag==null  && kok.sol == null) toplam += kok.data;
            if(kok.sag==null  && kok.sol != null) toplam += kok.sol.data + alttoplam(kok.sol);
            if(kok.sol==null  && kok.sag != null) toplam += kok.sag.data + alttoplam(kok.sag);
            if(kok.sol!=null  && kok.sag != null) toplam +=  kok.data+   alttoplam(kok.sag)+ alttoplam(kok.sol);



            return toplam;
        }

        public int AltAgacToplamiRec(Block kok, bool iskok = true)
        {
            if (kok == null) return 0;
            int toplam = 0;
            if (!iskok) toplam += kok.data;
            toplam += AltAgacToplamiRec(kok.sol,false);
            toplam += AltAgacToplamiRec(kok.sag,false );

            return toplam;
        }

    }




    internal class Program
    {
        

        static void Main(string[] args)
        {
            Console.WriteLine("main çalıştı");
            Agac bst = new Agac();
            Agac bst2 = new Agac();
            Agac bst3 = new Agac();



            /*
            bst.kok = bst.agacaEkle(bst.kok, 010);
            bst.kok = bst.agacaEkle(bst.kok, 0015);
            bst.kok = bst.agacaEkle(bst.kok, 005);
            bst.kok = bst.agacaEkle(bst.kok, 003);
            bst.kok = bst.agacaEkle(bst.kok, 006);

            Console.WriteLine("kök: " + bst.kok.data);
            Console.WriteLine("kök.sag: " + bst.kok.sag.data);
            Console.WriteLine("kök.sol: " + bst.kok.sol.data);
            Console.WriteLine("kök.sol.sol: " + bst.kok.sol.sol.data);
            Console.WriteLine("kök.sol.sag: " + bst.kok.sol.sag.data);

            */

            bst.kok = bst.agacaEkle(bst.kok, 13);
            bst.kok = bst.agacaEkle(bst.kok, 5);
            bst.kok = bst.agacaEkle(bst.kok, 15);
            bst.kok = bst.agacaEkle(bst.kok, 19);
            bst.kok = bst.agacaEkle(bst.kok, 3);
            bst.kok = bst.agacaEkle(bst.kok, 14);
            bst.kok = bst.agacaEkle(bst.kok, 10);
            // bst.kok = bst.agacaEkle(bst.kok, 9);
            bst.kok = bst.agacaEkle(bst.kok, 9);
            bst.kok = bst.agacaEkle(bst.kok, 16);
            bst.kok = bst.agacaEkle(bst.kok, 11);
            bst.kok = bst.agacaEkle(bst.kok, 20);
            bst.kok = bst.agacaEkle(bst.kok, 20);
            bst.kok = bst.agacaEkle(bst.kok, 20);
            bst.kok = bst.agacaEkle(bst.kok, 18);





            bst2.kok = bst2.agacaEkle(bst2.kok, 13);
            bst2.kok = bst2.agacaEkle(bst2.kok, 5);
            bst2.kok = bst2.agacaEkle(bst2.kok, 15);
            bst2.kok = bst2.agacaEkle(bst2.kok, 19);
            bst2.kok = bst2.agacaEkle(bst2.kok, 3);
            bst2.kok = bst2.agacaEkle(bst2.kok, 14);
            bst2.kok = bst2.agacaEkle(bst2.kok, 10);
            // bst2.kok = bst2.agacaEkle(bst2.kok, 9);
            //bst2.kok = bst2.agacaEkle(bst2.kok, 9);
            //bst2.kok = bst2.agacaEkle(bst2.kok, 16);
            //bst2.kok = bst2.agacaEkle(bst2.kok, 11);
            //bst2.kok = bst2.agacaEkle(bst2.kok, 20);
            //bst2.kok = bst2.agacaEkle(bst2.kok, 18);


            Console.WriteLine("\nPREOrder:");
            bst.preOrder(bst.kok);

            Console.WriteLine("\npostOrder:");
            bst.postOrder(bst.kok);

            Console.WriteLine("\ninOrder:");
            bst.inOrder(bst.kok);



            // ELEMAN SAYISI 🔢                      
            Console.WriteLine("\n ELEMAN SAYISI :  " + bst.elemanSayısı(bst.kok));

            // YAPRAK SAYISI                    
            Console.WriteLine("\n YAPRAK SAYISI:" + bst.YaprakSayisi(bst.kok));
            Console.WriteLine("\n YAPRAKLAR TOPLAMI :" + bst.YaprakToplami(bst.kok));
            Console.WriteLine("\n YAPRAKLAR TOPLAMI 1 :" + bst.YaprakToplami1(bst.kok));

            // YÜKSEKLİK BULMA 
            Console.WriteLine("\n YÜKSEKLİK : " + bst.Yukseklik(bst.kok));
            
            // MAX DERİNLİK 
            Console.WriteLine(" MAX DERİNLİK: " + bst.maxderinlik(bst.kok));

            // yer değiştirme
            //Console.WriteLine("\nDalların yeri değiştiriliyor...");
            //bst.yerdegistir(bst.kok);
            //Console.WriteLine("inOrdera göre ");
            //bst.inOrder(bst.kok);


            // SİLME İŞLEMİ 
            Console.WriteLine("\nsilme işleminden önce");

            bst.preOrder(bst.kok);

            bst.kok = bst.agactansil(bst.kok,3);
            
            bst.kok = bst.agactansil(bst.kok, 5);
            bst.kok = bst.agactansil(bst.kok, 15);

            Console.WriteLine("\nsilindikten sonra PREORDER ");
            bst.preOrder(bst.kok);
            Console.WriteLine();

            Console.WriteLine(bst.ARAMA(bst.kok,3) ? "VAR":"YOK");
            Console.WriteLine(bst.ARAMA(bst.kok,20) ? "VAR":"YOK");
            Console.WriteLine(bst.ARAMA(bst.kok, 19) ? "VAR":"YOK");
            Console.WriteLine(bst.ARAMA(bst.kok, 1) ? "VAR":"YOK");
            Console.WriteLine(bst.ARAMA(bst.kok, 1) ? "VAR":"YOK");
            Console.WriteLine(bst.ARAMA(bst.kok, 20) ? "VAR" : "YOK");
            Console.WriteLine(bst.ARAMA(bst.kok, 2) ? "VAR":"YOK");
            Console.WriteLine(bst.ARAMA(bst.kok, 18) ? "VAR":"YOK");
            Console.WriteLine(bst.ARAMA(bst.kok, 14) ? "VAR" : "YOK");
            Console.WriteLine(bst.ARAMA(bst.kok, 16) ? "VAR":"YOK");
            Console.WriteLine(bst.ARAMA(bst.kok, 9) ? "VAR":"YOK");
            

            // TEKRAR EDEN ELEMAN SAYISI
            int tekrar = bst.tekrar(bst.kok, 20, 0);
            int tekrar2 = bst.AraSay(bst.kok, 20);
            Console.WriteLine(tekrar);
            Console.WriteLine(tekrar2);

            //  İKİ TREE EŞİT Mİ KONTROL 
            Console.WriteLine(bst.EsitMi(bst.kok, bst2.kok) ? "AĞAÇLAR EŞİT" : "AĞAÇLAR EŞİT DEĞİL");

            bst.preOrder(bst.kok);
            Console.WriteLine(  );
            bst2.preOrder(bst2.kok);

            Console.WriteLine("\n 0.katmandaki eleman sayısı , toplamı : " + bst.istenenkatmandakielemansayısı(bst.kok,0) + " - " + bst.istenenkatmandakielemanlartoplamı(bst.kok,0));
            Console.WriteLine("\n 1.katmandaki eleman sayısı , toplamı : " + bst.istenenkatmandakielemansayısı(bst.kok,1) + " - " + bst.istenenkatmandakielemanlartoplamı(bst.kok,1));
            Console.WriteLine("\n 2.katmandaki eleman sayısı , toplamı : " + bst.istenenkatmandakielemansayısı(bst.kok,2) + " - " + bst.istenenkatmandakielemanlartoplamı(bst.kok,2));
            Console.WriteLine("\n 3.katmandaki eleman sayısı , toplamı : " + bst.istenenkatmandakielemansayısı(bst.kok,3) + " - " + bst.istenenkatmandakielemanlartoplamı(bst.kok,3));
            Console.WriteLine("\n 4.katmandaki eleman sayısı , toplamı : " + bst.istenenkatmandakielemansayısı(bst.kok,4) + " - " + bst.istenenkatmandakielemanlartoplamı(bst.kok,4));



            Console.WriteLine("-----------------------------FİNAL--------------------------");
            bst3.kok = bst3.agacaEkle(bst3.kok, 13);
            bst3.kok = bst3.agacaEkle(bst3.kok, 4);
            bst3.kok = bst3.agacaEkle(bst3.kok, 15);
            bst3.kok = bst3.agacaEkle(bst3.kok, 3);
            bst3.kok = bst3.agacaEkle(bst3.kok, 20);
            bst3.kok = bst3.agacaEkle(bst3.kok, 6);
            bst3.kok = bst3.agacaEkle(bst3.kok, 14);

            bst3.preOrder(bst3.kok);

            Console.WriteLine("kök:" + bst3.kok.data);

            Console.WriteLine(" \nalttoplam:" + bst3.alttoplam(bst3.kok));

            Console.WriteLine("\n" + bst3.AltAgacToplami(bst3.kok));

            Console.WriteLine("\nonatello:" + bst3.AltAgacToplamiRec(bst3.kok));

            Console.ReadLine();
        }
    }
}
