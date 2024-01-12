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
                kok = yeniBlock(data);
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
            if (kok ==null)
            {
                return 0;
            }
            else
            {
                return 1 + elemanSayısı(kok.sol)  + elemanSayısı(kok.sag) ;   
            }
        }

        /*
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

        public int YaprakSayisi(Block kok) 
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
        */




        public int Yukseklik(Block kok)      // YÜKSEKLİK = KÖKE OLAN UZAKLIK 
        {
            if (kok ==null)
            {                
                return -1;
            }
            else
            {
                int l, r;
                l = Yukseklik(kok.sol); 
                r = Yukseklik(kok.sag);

                if (l>r)
                {
                    return l + 1; 
                }
                else
                {
                    return r + 1;
                }
            }
        }

        public void yerdegistir(Block kok)       // SAĞ DAL İLE SOL DALI "SWAP"  ETTİRECEĞİZ --- İNORDER İLE BÜYÜKTEN KÜÇÜĞE YAZDIRACAK
        {
            Block temp = null;
            if (kok !=null)
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

            if(kok == null ){ return null;}

            if (kok.data == silinecek)          // sileceğim düğüm budur 
            {
                if (kok.sol == kok.sag)    // silinecek düğümün altında dal yok demektir  // YAPRAK SİLİNECEK 
                {
                    kok = null;
                    return null;
                } 
                else if(kok.sol == null)    //  silinecek düğümün solu boş 
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

                    while (t1.sol!=null)
                    {
                        t1 = t1.sol;
                    }
                    t1.sol = kok.sol;   // yeni kök sağdaki oldu 
                    
                    return t2;
                }

            }
            else
            {
                if (silinecek<kok.data)     // silinecek eleman ağacın sol dallarındadır 
                {
                    kok.sol = agactansil(kok.sol,silinecek);
                }
                else                        // // silinecek eleman ağacın sağ dallarındadır 
                {
                    kok.sag = agactansil(kok.sag,silinecek);
                }
            }
            return kok;
        }


        // AĞAÇTA ARAMA METODU  
        public bool ARAMA(Block kok, int aranan) 
        {
            if (aranan>kok.data)   //  aranan eleman aktif blockdan büyüktür --> sağa gidecek 
            {
                if (kok.sag !=null)
                {
                    return ARAMA(kok.sag, aranan);
                }
                return false;
            }
            else if (aranan<kok.data)
            {
                if (kok.sol !=null)
                {
                    return ARAMA(kok.sol, aranan);
                }
                return false;
            }
            else   //   aranan == kok.data
            {

                return true;
            }
        } 
         
          
         
         

    }



    internal class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("main çalıştı");
            Agac bst = new Agac();
            


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

            bst.kok = bst.agacaEkle(bst.kok, 11);
            bst.kok = bst.agacaEkle(bst.kok, 5);
            bst.kok = bst.agacaEkle(bst.kok, 15);
            bst.kok = bst.agacaEkle(bst.kok, 20);
            bst.kok = bst.agacaEkle(bst.kok, 3);
            bst.kok = bst.agacaEkle(bst.kok, 12);
            bst.kok = bst.agacaEkle(bst.kok, 9);
           // bst.kok = bst.agacaEkle(bst.kok, 9);
            bst.kok = bst.agacaEkle(bst.kok, 8);
            bst.kok = bst.agacaEkle(bst.kok, 10);



            Console.WriteLine("preOrder:");
            bst.preOrder(bst.kok);
            Console.WriteLine("\ninOrder:");
            bst.inOrder(bst.kok);
            Console.WriteLine("\npostOrder:");
            bst.postOrder(bst.kok);


           


            // ELEMAN SAYISI 🔢
            Console.WriteLine("\ninOrdera göre ");
            bst.inOrder(bst.kok);
            Console.WriteLine("\n ELEMAN SAYISI :  " + bst.elemanSayısı(bst.kok));

            // YAPRAK SAYISI
            bst.inOrder(bst.kok);           
            Console.WriteLine("\n YAPRAK SAYISI:" + bst.YaprakSayisi(bst.kok));


            // YÜKSEKLİK BULMA 
            Console.WriteLine("\n YÜKSEKLİK : " + bst.Yukseklik(bst.kok));

            // yer değiştirme
            //Console.WriteLine("\nDalların yeri değiştiriliyor...");
            //bst.yerdegistir(bst.kok);
            //Console.WriteLine("inOrdera göre ");
            //bst.inOrder(bst.kok);


            // silme işlemi 
            Console.WriteLine("\nsilme işleminden önce");

            bst.preOrder(bst.kok);

            bst.kok = bst.agactansil(bst.kok,3);
            
            bst.kok = bst.agactansil(bst.kok, 5);
            bst.kok = bst.agactansil(bst.kok, 15);
            
            Console.WriteLine("\nsilindikten sonra PREORDER ");
            bst.preOrder(bst.kok);

            bool arama = bst.ARAMA(bst.kok, 3); Console.WriteLine("\n 3 "+ arama);
            bool arama1 = bst.ARAMA(bst.kok, 20); Console.WriteLine("20 "+arama1);
            bool arama2 = bst.ARAMA(bst.kok, 33); Console.WriteLine("33 "+arama2); 

            Console.ReadLine();
        }
    }
}
