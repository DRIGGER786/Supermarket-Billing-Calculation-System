# Supermarket-Billing-Calculation-System
#include<iostream>
#include<fstream>
using namespace std;
class head
{
    char Iname[50][50];
    public:
    int totalitems;
    float Qty[5];
    float price[5];
    int vatprice[5];
    int tprice[5];
    void input();
    void output();
};
class vat:public head
{
    float vats;
    public:
    void vatcal();
    void outputs();
    void sum();
};

//******************************************************************
//      INPUT FUNCTION
//******************************************************************

void head::input()
{
    system("CLS");
    cout<<"\nEnter number of items= ";
    cin>>totalitems;

    for(int i=0; i<totalitems; i++)
    {
        cout<<"\nEnter name of item "<<": ";
        cin>>Iname[i];
        cout<<"\nEnter quantity: ";
        cin>>Qty[i];
        cout<<"\nEnter price of item "<<": ";
        cin>>price[i];
        tprice[i]=Qty[i]*price[i];
    }
}
//* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
//     OUTPUT FUNCTION
//* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
void head::output()
{
    int a;

    ifstream infile("SAMPLE.TXT");
    infile>>a;

    ofstream outfile("SAMPLE.TXT");
    a+=1;
    outfile<<a;
    outfile.close();

    {ofstream outfile("FILE1.TXT", ios::app);
    outfile<<endl<<"Bill No.: "<<a<<endl;
    outfile<<"------------------------------------------------------------------------"<<endl;
    cout<<"\n";
    cout<<"Name of Item   Quantity  Price  Total Price\n";
    for(int i=0;i<totalitems;i++)
    {
        outfile<<"Name: "<<Iname[i]<<" Qty: "<<Qty[i]<<" Price: "<<tprice[i]<<endl;
        cout<<Iname[i]<<"\t\t"<<Qty[i]<<"\t "<<price[i]<<"\t "<<tprice[i]<<'\n';
    }

    outfile<<"------------------------------------------------------------------------"<<endl;
    outfile.close();
    }
}
//* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
//     VAT CALCULATION
//* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
void vat::vatcal()
{
    input();
    for(int i=0;i<totalitems;i++)
    {
        if(price[i]<=100)
        {
            vatprice[i]=tprice[i];
        }
        else
        {
            vatprice[i]=tprice[i];
        }
    }
}
// * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
//      VAT OUTPUTS
//*  * * * * * * * * * * * * * * * * * * * * ** * * * * * * * * * * * * * * * * * * * * * * * * *
void vat::outputs()
{
    output();

    float cash=0,sum=0,qty=0,sumt=0;

    for(int i=0;i<totalitems;i++)
    {
           sumt+=tprice[i];
           sum+=vatprice[i];
           qty+=Qty[i];
    }
    cout<<"\nTotal:";
    cout<<"\n------------------------------------------------------------------------------";
    cout<<"\n\tQuantity= "<<qty<<"\t\t Sum= "<<sum<<"\tWith Vat:"<<sum;
    cout<<"\n------------------------------------------------------------------------------";

pay:

    cout<<"\n\n\t\t\t * * * * PAYMENT SUMMARY * * * * \n";
    cout<<"\n\t\t\tTotal cash given: ";
    cin>>cash;

    if(cash>=sum)
        cout<<"\n\t\t\tTotal cash repaid: "<<cash-sum<<'\n';

    else
    {   cout<<"\n\t\t\tCash given is less than total amount!!!";

    goto pay;
    }
}
//* * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *
//      PROTECTION PASSWORD
//* * * * * * * * * * * *  * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * * *

int passwords()
{

    char p1,p2,p3;

    cout<<"ENTER THE PASSWORD: ";

    cin>>p1;
    cout<<"*";
    cin>>p2;
    cout<<"*";
    cin>>p3;
    cout<<"*";

    if ((p1=='s'||p1=='S')&&(p2=='i'||p2=='I')&&(p3=='d'||p3=='D'))

        return 1;

    else
        return 0;
}
// END of Password.

//****************************************************************
//      THE MAIN FUNCTION OF PROGRAM
//****************************************************************


int main()
{
    vat obj;
    char opt, ch;
    int a=1;
    ifstream fin;

    a==passwords();
    if(!a)
    {
        for(int i=0;i<2;i++)
        {
            cout<<"\nWrong password try once more\n";
            if(passwords())
            {
                goto last;
            }
            else
            {
                cout<<"\n\n\t\t\t all attempts failed.....";
                cout<<"\n\n\n\t\t\t see you.................. ";
                exit(0);
            }

        }
        cout<<"\t\t\t sorry all attempts failed............. \n \t\t\tinactive";
             }
    else{
last:;
     do{
start:
    system("PAUSE");
    system("CLS");
    cout<<"\n\n\t\t\t------------------------------";
    cout<<"\n\t\t\tSupermarket Billing Management System";
    cout<<"\n\t\t\t------------------------------";
     cout<<"\n\n\t\t\tWhat you want to do?";
     cout<<"\n\t\t\t1.\tTo enter new entry\n\t\t\t2.\tTo view previous entries\n\t\t\t3.\tExit\n";
     cout<<"\n\nEnter your option: ";
     cin>>opt;
     switch(opt)
     {
     case'1':
         obj.vatcal();

         obj.outputs();
         goto start;
     case'2':

         fin.open("FILE1.TXT", ios::in);
         while(fin.get(ch))
         {
             cout<<ch;
         }
         fin.close();

         goto start;
     case'3':
         exit(0);
     default:
         cout<<"\a";
     }

     }while(opt!=3);
    }
    return 0;
}
