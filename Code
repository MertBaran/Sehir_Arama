#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

typedef struct sehirbilgileri
{
    int plaka;
    char bolge[5];
    char il[50];
    int komsusayisi;
    struct komsular *ileri;
    struct sehirbilgileri *on;
    struct sehirbilgileri *arka;
} SEHIR;

typedef struct komsular
{
    int komsuplaka;
    struct komsular *arka;
} KOMSU;

SEHIR *listebasi = NULL, *listesonu = NULL;

SEHIR *il_arama(char sehir[])
{
    SEHIR *p;
    p = listebasi;
    while(p != NULL)
    {
        if(strcmp(p -> il, sehir) == 0)
            return p;
        p = p -> arka;
    }
    return NULL;
}

void kriter_listele(int kriter1)
{
    SEHIR *p;
    p = listebasi;
    KOMSU *c;
    FILE *o;
    o = fopen("output.txt", "a");
    fprintf(o, "\n\n");
    while(p != NULL)
    {
        if(p -> komsusayisi > kriter1)
        {
            printf("\t%d\t%s\t%s\t%d\t", p -> plaka, p -> il, p -> bolge, p -> komsusayisi + 1);
            fprintf(o, "\t%d\t%s\t%s\t%d\t", p -> plaka, p -> il, p -> bolge, p -> komsusayisi + 1);
            c = p -> ileri;
            while(c != NULL)
            {
                fprintf(o, "%d\t", c -> komsuplaka);
                printf("%d\t", c -> komsuplaka);
                c = c -> arka;
            }
        printf("\n");
        fprintf(o, "\n");
        }
        p = p -> arka;
    }
    fprintf(o, "\n\n\n\n");
}

void bonus_ister(int kriter1, int kriter2)
{
    SEHIR *p;
    p = listebasi;
    KOMSU *c;

    while(p != NULL)
    {
        if(p -> komsusayisi + 1 > kriter1 && p -> komsusayisi + 1 < kriter2)
        {
            printf("\t%d\t%s\t%s\t%d\t", p -> plaka, p -> il, p -> bolge, p -> komsusayisi + 1);
            c = p -> ileri;
            while(c != NULL)
            {
                printf("%d\t", c -> komsuplaka);
                c = c -> arka;
            }
        printf("\n");
        }
        p = p->arka;
    }
}

void komsusayisi()
{
    SEHIR *p;
    p = listebasi;
    KOMSU *c;
    int i = 0;

    while(p != NULL)
    {
        c = p -> ileri;
        while(c -> arka != NULL)
        {
            i++;
            c = c -> arka;
        }
        p -> komsusayisi = i;
        i=0;
        p = p -> arka;
    }
}

int komsuplakadondur(char sehir[])
{
    SEHIR *p;
    p = listebasi;

    while(p != NULL)
    {
        if(strcmp(p -> il, sehir) == 0)
            return (p -> plaka);
        p = p -> arka;
    }
    return 0;
}

int komsu_ekleme(int plaka, SEHIR *p)
{
    KOMSU *node, *c;

    if(p -> ileri == NULL)
    {
        node = (struct komsular*)malloc(sizeof(KOMSU));
        node -> komsuplaka = plaka;
        node -> arka = NULL;
        p -> ileri = node;
        p->komsusayisi = p->komsusayisi + 1;
        return 0;
    }
    else
    {
        c = p -> ileri;
        while(c -> arka != NULL)
            c = c -> arka;

        node = (struct komsular*)malloc(sizeof(KOMSU));
        node -> komsuplaka = plaka;
        c -> arka = node;
        node -> arka = NULL;
        p->komsusayisi = p->komsusayisi + 1;
        return 0;
    }
    return 0;
}

void siraliEkle(SEHIR *p)
{
    if(listebasi != NULL)
    {
        listesonu -> arka = p;
        p -> on = listesonu;
        listesonu = p;
        listesonu -> arka = NULL;
        p -> ileri = NULL;
    }
    else
    {
        listebasi = p;
        listesonu = p;
        listebasi -> on = NULL;
        listebasi -> arka = NULL;
        p -> ileri = NULL;
    }
}

void komsu_kaydet_2(int line_count)
{
    FILE *file;
    SEHIR *p;
    p = listebasi;
    file = fopen("sehirler.txt", "r");
    int sayac, b = 0, j;
    int plk, plkgelen;
    char *virgul = ",";
    char *birkelime = NULL;
    char metin[100];
    char komsular[15];
    char *n = "\n";

    while(!feof(file) && b < line_count + 1 && p != NULL )
    {
        printf("\n");
        sayac = 0;
        fgets(metin, 100, file);
        birkelime = strtok(metin, virgul);

        while(birkelime != NULL)
        {
            sayac++;
            if(sayac > 3)
            {
                strcpy(komsular, birkelime);
                for(j = 0 ; j < strlen(komsular) ; j++ )
                {
                    if(komsular[j] == '\n')
                    {
                        komsular [j] = '\0';
                    }

                }
                plkgelen = komsuplakadondur(komsular);
                komsu_ekleme(plkgelen, p);
            }
            birkelime = strtok(NULL, virgul);
        }
        b++;
        p = p -> arka;
    }
}

void verileriOkuveEkle()
{
    SEHIR *p;
    int sayac, sayac2 = 0;
    int i;
    char eklemeyapilsin, metin[100];
    char *virgul = ",";
    char *birkelime = NULL;
    int plaka;
    char bolge[5];
    char il[50];

    FILE *dosya;
    dosya = fopen("sehirler.txt", "r");

    if(dosya == NULL)
        printf("Dosya Acilamadi!!\n");

    while(!feof(dosya))
    {
        sayac = 0;
        fgets(metin, 100, dosya);
        birkelime = strtok(metin, virgul);
        sayac2++;

        while(birkelime != NULL && sayac < 3 && sayac2 < 82)
        {
            sayac++;
            if(sayac == 1)
            {
                plaka = atoi(birkelime);
            }
            birkelime = strtok(NULL, virgul);
            sayac++;
            if(sayac == 2)
            {
                strcpy(il, birkelime);
            }
            birkelime = strtok(NULL, virgul);
            sayac++;
            if(sayac == 3)
            {
                strcpy(bolge, birkelime);
            }
            p = (char*)malloc(sizeof(SEHIR));
            p -> plaka = plaka;
            strcpy(p -> bolge, bolge);
            strcpy(p -> il, il);
            siraliEkle(p);
        }
    }
    komsu_kaydet_2(sayac2);
    fclose(dosya);
}

void listele()
{
    SEHIR *p;
    KOMSU *c;
    FILE *o;
    o = fopen("output.txt", "a");


    p = listebasi;
    if(p == NULL)
        printf("Bos Liste!!\n");

    while(p != NULL)
    {
        printf("\n%d   %s   %s   %d", p -> plaka, p -> il, p -> bolge, p -> komsusayisi + 1);
        fprintf(o, "\n%d  -> %s  -> %s  -> %d", p -> plaka, p -> il, p -> bolge, p -> komsusayisi + 1);
        c = p -> ileri;
        while(c != NULL)
        {
            fprintf(o, "  ->  %d  ", c -> komsuplaka);
            printf("   %d   ", c -> komsuplaka);
            c = c -> arka;
        }
        p = p -> arka;
    }
    printf("\n\n");
    fclose(o);

}

void bolgeyegorelistele(char bolgeler[])
{
    SEHIR *p;
    p = listebasi;
    FILE *o;
    o = fopen("output.txt", "a");


    while(p != NULL)
    {
        if(strcmp(bolgeler, "AK") == 0)
        {
            if(strcmp(p -> bolge, "AK")==0)
            {
                printf("%d      %s    %s\n", p -> plaka, p -> il, p -> bolge);
                fprintf(o, "%d      %s      %s\n", p -> plaka, p -> il, p -> bolge);
            }
                p = p -> arka;
        }
        else if(strcmp(bolgeler, "DA") == 0)
        {
            if(strcmp(p -> bolge, "DA") == 0)
                {
                    printf("%d      %s    %s\n", p -> plaka, p -> il, p -> bolge);
                    fprintf(o, "%d      %s      %s\n", p -> plaka, p -> il, p -> bolge);
                }
                p = p -> arka;
        }
        else if(strcmp(bolgeler, "EG") == 0)
        {
            if(strcmp(p -> bolge, "EG") == 0)
                {
                    printf("%d      %s    %s\n", p -> plaka, p -> il, p -> bolge);
                    fprintf(o, "%d      %s      %s\n", p -> plaka, p -> il, p -> bolge);
                }
                p = p -> arka;
        }
        else  if(strcmp(bolgeler, "GA") == 0)
        {
            if(strcmp(p -> bolge, "GA")==0)
                {
                printf("%d      %s    %s\n", p -> plaka, p -> il, p -> bolge);
                fprintf(o, "%d      %s      %s\n", p -> plaka, p -> il, p -> bolge);
                }
            p = p -> arka;
        }
        else  if(strcmp(bolgeler, "IA") == 0)
        {
            if(strcmp(p -> bolge, "IA") == 0)
                {
                printf("%d      %s    %s\n", p -> plaka, p -> il, p -> bolge);
                fprintf(o, "%d      %s      %s\n", p -> plaka, p -> il, p -> bolge);
                }
                p = p -> arka;
        }
        else  if(strcmp(bolgeler, "MA") == 0)
        {
            if(strcmp(p -> bolge, "MA")==0)
                {
                printf("%d      %s    %s\n", p -> plaka, p -> il, p -> bolge);
                fprintf(o, "%d      %s      %s\n", p -> plaka, p -> il, p -> bolge);
                }
                p = p -> arka;
        }
        else
        {
            if(strcmp(p -> bolge, "KA") == 0)
               {
                printf("%d      %s    %s\n", p -> plaka, p -> il, p -> bolge);
                fprintf(o, "%d      %s      %s\n", p -> plaka, p -> il, p -> bolge);
                }
                p = p -> arka;
        }
    }
    fprintf(o, "\n\n\n\n");
    fseek(o,SEEK_END,SEEK_END);
}

SEHIR *aranan(int aranan)
{

    SEHIR *p;
    p = listebasi;
    while(p != NULL)
    {
        if(aranan == p -> plaka)
        {
            return p;
        }
        p = p -> arka;
    }
    return NULL;
}

KOMSU *komsusehirarama(int plaka)
{
    SEHIR *p;
    KOMSU *c;
    p = listebasi;
    c = p -> ileri;

    while(c != NULL){
        if(c -> komsuplaka == plaka)
            return c;
            c = c -> arka;
    }
}
void  klavyedenSehirOku(int plkoku)
{
    SEHIR *p;
    SEHIR *bul;
    bul = aranan(plkoku);
    if(bul == NULL)
    {
        p = (char*)malloc(sizeof(SEHIR));
        printf("Lutfen eklenecek sehir ismini girin: \n");
        scanf("%s", p -> il);
        printf("Bolge ismini girin: \n");
        scanf("%s", p -> bolge);
        p -> plaka = plkoku;
        siraliEkle(p);
        printf("Ekleme islemi yapilmistir\n");
    }
    else
    {
        printf("Bu plaka numarasina ait bir sehir listede bulunmaktadir!!! Ekleme yapamazsiniz\n");
    }
}

void klavyedenSehirOku2(char ekle[])
{
    SEHIR *p, *bul;
    bul = il_arama(ekle);
    if(bul == NULL)
    {
        p = (char*)malloc(sizeof(SEHIR));
        printf("Lutfen eklenecek sehrin plaka kodunu girin: \n");
        scanf("%d", &(p -> plaka));
        strcpy(p -> il, ekle);
        printf("Bolge ismini girin: \n");
        scanf("%s", p -> bolge);
        siraliEkle(p);
        printf("Ekleme islemi yapilmistir\n");
    }
}

void *sehirsil(int silinecek)
{
    SEHIR *p;
    p = aranan(silinecek);

    if(p == NULL)
        return NULL;

    if(listebasi == p)
    {
        if(listebasi -> arka != NULL)
        {
            listebasi = p -> arka;
            listebasi -> on = NULL;
        }
        else
        {
            listebasi = NULL;
            listesonu = NULL;
        }
    }
    else
    {
        p -> on -> arka = p -> arka;
        if(listesonu == p)
        {
            listesonu = listesonu -> on;
        }
        else
            p -> arka -> on = p -> on;
    }
    free(p);
    return p;
}

 void komsuluk_silme()
{
    int hedef_sehir_plaka, i = 1;
    SEHIR *p;
    KOMSU *c,  *bironceki = NULL;

    printf("Hangi ilin komsusunu silmek istiyorsunuz? (plaka giriniz)\n");
    scanf("%d", &hedef_sehir_plaka);
    p = aranan(hedef_sehir_plaka);

    c = p -> ileri;

     while (c != NULL)
        {
            int hedef_komsu_plaka = c -> komsuplaka;
            SEHIR *hedef_komsu = aranan(hedef_komsu_plaka);
            printf("\t%d. %s (%d)\n", i, hedef_komsu->il, hedef_komsu->plaka);
            c = c->arka;
            i++;
        }
    c = p -> ileri;

    printf("\n%s sehrinden hangi komsuyu silmek istiyorsunuz? (plaka giriniz)\n", p -> il);
    scanf("%d", &hedef_sehir_plaka);

    while (c != NULL)
    {
        if(hedef_sehir_plaka == c->komsuplaka)
        {
            if(bironceki == NULL)
            {
                if(p -> ileri -> arka != NULL)
                    p -> ileri = c -> arka;
                else
                    p -> ileri = NULL;
            }
            else if(c -> arka == NULL)
                bironceki -> arka = NULL;
            else
                bironceki -> arka = c -> arka;
            free(c);
            p ->komsusayisi = p ->komsusayisi - 1;
        }
        bironceki = c;
        c = c -> arka;
    }
    return;
}

int main()
{
    system("color a");
    int arama, secim, plkgelen, eklemesecimi, blg, plaka_ara, kmsplk;
    int aramasecimi, silmesecimi;
    int plaka, silinecek, pl;
    int komsuplaka, plaka1, plaka2, plaka3;
    char istenen_sehir1[20];
    char istenen_sehir2[20];
    char bolgeler[10];
    char sehirarama[20];
    char ekle[2];
    char ekle1[]="E", ekle2[]="H";
    KOMSU *x;
    SEHIR *p;
    SEHIR *silme;
    SEHIR *ar;
    SEHIR *komsuekleme;
    verileriOkuveEkle();
    komsusayisi();

    do
    {
        printf("        1-) Sehir veya Komsuluk Ekleme\n");
        printf("        2-) Arama\n");
        printf("        3-) Kayit Silme\n");
        printf("        4-) Bolgeye gore listeleme\n");
        printf("        5-) Komsu sayisi kriterine gore listeleme\n");
        printf("        6-) Bonus ister\n");
        printf("        7-) Komsu silme\n");
        printf("        8-) Illeri Listele\n");
        printf("        9-) Cikis\n");
        scanf("%d", &secim);

        switch(secim)
        {

        case 1:
            printf("    1-)Sehir Ekleme\n");
            printf("    2-)Komsuluk Ekleme\n");
            printf("Lutfen secim yapiniz:\n");

            scanf("%d", &eklemesecimi);

            if(eklemesecimi == 1)
            {
                printf("\tEklemek istedginiz sehrin plaka kodunu girin: ");
                scanf("%d", &plaka_ara);
                klavyedenSehirOku(plaka_ara);
            }
            else
            {
                printf("\tKomsu eklemek istediginiz sehrin plaka kodunu giriniz: \n");
                scanf("%d", &kmsplk);
                komsuekleme = aranan(kmsplk);
                if(komsuekleme != NULL)
                {
                    printf("\tEklemek istediginiz komsu sehrin plakasini giriniz: \n");
                    scanf("%d", &komsuplaka);
                    x = komsusehirarama(komsuplaka);
                    if(x == NULL)
                    {
                        kmsplk = komsu_ekleme(komsuplaka,komsuekleme);
                            if(kmsplk == 0)
                                printf("Komsuluk eklenmistir...\n");
                    }
                    else
                        printf("Bu komsu sehir zaten listede vardir.Ekleme yapamazsiniz!!...\n");
                }
                else
                    printf("Bu sehir  listede yoktur.Ekleme yapamazsiniz!!...\n");
            }
            break;

        case 2:
            printf("\t1-)Aramayi plakaya gore yapmak\n\t2-)Aramayi sehir ismine gore yapmak\nLutfen secim yapin: \n");
            scanf("%d", &aramasecimi);
            if(aramasecimi == 1)
            {
                printf("\tLutfen plaka kodunu giriniz: \n");
                scanf("%d", &plaka);
                ar = aranan(plaka);
                if(ar != NULL)
                {
                    x = ar -> ileri;
                    printf("%d   %s   %s  %d\t", ar -> plaka, ar -> il, ar -> bolge, ar -> komsusayisi + 1);
                        while(x != NULL)
                        {
                            printf("\t%d\t", x -> komsuplaka);
                            x = x -> arka;
                        }
                    printf("\n");
                }
                else
                {
                    printf("Aranan plaka listede yoktur!!\nEkleme yapmak ister misiniz(E/H): ?\n");
                    scanf("%s", ekle);

                    if(strcmp(ekle, ekle1) == 0)
                        klavyedenSehirOku(plaka);
                        break;
                }
            }
            else if(aramasecimi == 2)
            {
                printf("\tLutfen sehir ismini giriniz: \n");
                scanf("%s", sehirarama);
                ar = il_arama(sehirarama);
                if(ar != NULL)
                {
                    x = ar -> ileri;
                    printf("%d   %s   %s  %d\t", ar -> plaka, ar -> il, ar -> bolge, ar -> komsusayisi + 1);
                    while(x != NULL)
                    {
                        printf("\t%d\t", x -> komsuplaka);
                        x = x -> arka;
                    }
                    printf("\n");
                }
                else
                {
                    printf("Aranan sehir listede yoktur!!\nEkleme yapmak ister misiniz(E/H): ?\n");
                    scanf("%s", &ekle);
                    if(strcmp(ekle, ekle1) == 0)
                        klavyedenSehirOku2(sehirarama);
                        break;
                }
            }
            break;

        case 3:
            printf("\t1-)Sehir Silme\n");
            scanf("%d", &silmesecimi);

            if(silmesecimi == 1)
            {
                printf("\tSilmek istediginiz plakayi girin:\n");
                scanf("%d", &silinecek);
                silme = sehirsil(silinecek);
                if(silme == NULL)
                    printf("Silinmek istenen listede yoktur!!\n");
                else
                    printf("Silindi...\n");
                break;
            }

        case 4:
            printf("\nListelenmesini istediginiz bolgeyi yazin:\n");
            scanf("%s", bolgeler);

            bolgeyegorelistele(bolgeler);
            break;

        case 5:
            printf("\tKac taneden fazla komsu sayisina sahip illeri listelememi istersiniz: ?\n");
            scanf("%d", &plaka1);
            kriter_listele(plaka1);
            break;

        case 6:
            printf("   Komsu sayisinin listelenmesini istediginiz araligi girin:\n");
            scanf("%d", &plaka2);
            scanf("%d", &plaka3);

            bonus_ister(plaka2, plaka3);
            break;
         case 7:
            komsuluk_silme();
            break;

        case 8:
            listele();
            break;

        default:
            printf("Cikis yapiliyor...");
            break;
        }
    }
    while(secim > 0 && secim < 9);
}
