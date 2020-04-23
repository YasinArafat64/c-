
It's a restaurant management system in c++
#include<iostream>
#include<fstream>
#include <string>
#include<string.h>
#include<conio.h>
#include<cstdio>
#include<stdlib.h>
#include<windows.h>
using namespace std;
class table // table is create
{
    protected:
struct ru{
    char tab[100];
    int key;
    float code;
}ru;
};
class make : public table //interite table class to make class
{
protected:
    void create_table()
{
    char a;
    int k;
    fstream obj;
    start:
    do {
        obj.open("table.txt",ios::in|ios::binary);
        cout<<"Enter the table key:";
        cin>>k;
         while(obj.read((char*)&ru,sizeof(ru)))
            {
                if(ru.key==k)
                {
                    cout<<"Key is already exist"<<endl;
                    obj.close();
                goto start;
                }
            }
        obj.close();
        obj.open("table.txt",ios::app|ios::binary);
        ru.key=k;
        cin.ignore();
        cout<<"ENTER THE TABLE NAME:";
        gets(ru.tab);
        cout<<"ENTER THE TABLE CODE:";
        cin>>ru.code;
        obj.write((char*)&ru,sizeof(ru));
        cout<<"Do you want to add an other ? [y/n]:";
        cin>>a;
        obj.close();
    }
    while(a!='n');
}

};
class admin // create admin class
{
    protected:
struct r{
    char dish[100];
    int key;
    float price;
}r;
};
class Resturant : public admin ,public make //inherite admin and make class to resturant
{
protected:
    void update();
    void delet();
    void admin();

void create()
{
    char a;
    int k;
    fstream obj;
    start:
    do {
        obj.open("resturant.txt",ios::in|ios::binary);
        cout<<"Enter the dish key:";
        cin>>k;
         while(obj.read((char*)&r,sizeof(r)))
            {
                if(r.key==k)
                {
                    cout<<"Key is already exist"<<endl;
                    obj.close();
                goto start;
                }
            }
        obj.close();
        obj.open("resturant.txt",ios::app|ios::binary);
        r.key=k;
        cin.ignore();
        cout<<"ENTER THE DISH NAME:";
        gets(r.dish);
        cout<<"ENTER THE DISH PRICE:";
        cin>>r.price;
        obj.write((char*)&r,sizeof(r));
        cout<<"Do you want to add an other ? [y/n]:";
        cin>>a;
        obj.close();
    }
    while(a!='n');
}
void display()
{
      int c=0;
     fstream obj;
     obj.open("resturant.txt",ios::in|ios::binary);
     cout<<"\tKey\t\tDISH NAME\t\tPRICE"<<endl;
     while(obj.read((char*)&r,sizeof(r)))
    {
            cout<<"\t"<<r.key<<"\t\t"<<r.dish<<"\t\t\t"<<r.price<<endl;
            c++;
    }
    if(c==0)
    {
        cout<<"List is empty"<<endl;
    }
    obj.close();
}
void query()
{
     int a,c=0;
     fstream obj;
     obj.open("resturant.txt",ios::in);
    cout<<"Enter the dish key:";
    cin>>a;
    while(obj.read((char*)&r,sizeof(r)))
    {
           if(r.key==a)
           {
            cout<<"\t"<<r.key<<"\t\t"<<r.dish<<"\t\t\t"<<r.price<<endl;
            c++;
           }
    }
    if(c==0)
    {
        cout<<"Not found"<<endl;
    }
    obj.close();
}

};

class Resturant_A: public Resturant
{
    public:
        void update()
{
 int a,p,c=0;
     fstream obj;
     obj.open("resturant.txt",ios::in|ios::out|ios::binary);
    cout<<"enter the dish key:";
    cin>>a;
    obj.seekg(0);
    while(obj.read((char*)&r,sizeof(r)))
    {
        if(r.key==a)
        {
            cout<<"Destinatio record:"<<endl;
            cout<<"\t"<<r.key<<"\t\t"<<r.dish<<"\t\t\t"<<r.price<<endl;
            p=obj.tellg()-(sizeof(r));
            obj.seekp(p);
            cout<<"Enter the dish key:";
            cin>>r.key;
            cin.ignore();
            cout<<"ENTER THE DISH NAME:";
             gets(r.dish);
            cout<<"ENTER THE DISH PRICE:";
            cin>>r.price;
            obj.write((char*)&r,sizeof(r));
            c++;
           }

        }
        if(c==0)
        {
            cout<<"Not found"<<endl;
        }

    obj.close();
}
    void delet()
{
     int a,c;
     fstream obj,obj1;
     obj.open("resturant.txt",ios::in|ios::binary);
     obj1.open("temp.txt",ios::app|ios::binary);
    cout<<"Enter the dish key:";
    cin>>a;
    while(obj.read((char*)&r,sizeof(r)))
    {
        if(r.key==a)
        {
            c++;
            cout<<"\t"<<r.key<<"\t\t"<<r.dish<<"\t\t\t"<<r.price<<endl;
            cout<<"Destination record is deleted"<<endl;
        }
        if(r.key!=a)
        {
            obj1.write((char*)&r,sizeof(r));
           }
    }
    obj.close();
    obj1.close();
    if(c==0)
       {
         cout<<"Not found"<<endl;
       }
    remove("resturant.txt");
    rename("temp.txt","resturant.txt");
}
 int login()
 {
   string pass ="";
   char ch;
   cout <<"\n\n\n\n\t\t\t\t\tNFC Billing System";
   cout <<"\n\n\n\n\n\t\t\t\t\tEnter Your Password :";
   ch = _getch();
   while(ch != 13)
   {
      pass.push_back(ch);
      cout << '*';
      ch = _getch();
   }
   if(pass == "pass"){
    cout<<"\n\n\n\t\t\t\t\tLOADING \n\t\t\t\t\t";
    for(int a=1;a<10;a++)
    {
       Sleep(500);
       cout << "...";
    }
      cout << "\n\n\n\t\t\t\t\tAccess Granted!! \n\n\n";

      system("pause");
      system("cls");
   }else{
      cout << "\nAccess Aborted...\n";
      login();
   }
}
 void admin()
{

char a;
    do{
            cout<<"\n\t\t\t\t\t Welcome to our digital resturant service  "<<endl;
            cout<<"\n\t\t\t\t\t\t|||||||||||||||||||||||||"<<endl;
            cout<<"\t\t\t\t\t\t|                       |"<<endl;
            cout<<"\t\t\t\t\t\t|  1) ADD DISH          |"<<endl;
            cout<<"\t\t\t\t\t\t|  2) Display           |"<<endl;
            cout<<"\t\t\t\t\t\t|  3) QUERY             |"<<endl;
            cout<<"\t\t\t\t\t\t|  4) UPDATE            |"<<endl;
            cout<<"\t\t\t\t\t\t|  5) DELETE            |"<<endl;
            cout<<"\t\t\t\t\t\t|  6) TABLE             |"<<endl;
            cout<<"\t\t\t\t\t\t|  0) EXIT TO MAIN MANU |"<<endl;
            cout<<"\t\t\t\t\t\t|                       |"<<endl;
            cout<<"\t\t\t\t\t\t|||||||||||||||||||||||||"<<endl;
            cout<<"\t\t\t\t\t\t Select the key : ";
            cin>>a;
            switch(a)
            {
            case '0':
                break;
            case '1':
                system("CLS");
               create();
                break;
            case '2':
                system("CLS");
               display();
                break;
            case '3':
                system("CLS");
               query();
                break;
            case '4':
                system("CLS");
               update();
                break;
            case '5':
                system("CLS");
             delet();
                break;
            case '6':
                system("CLS");
             create_table();
                break;
            }
    }
    while(a!='0');
}
};
class customer //class for customer
{
    protected:
 struct {
char d[50];
float p,amount;
int qty;
}rd;
};

class custmer: public Resturant_A , public customer //inherite resturant_a and customer class to custmer
{
public:

void bill()
{
     int a,c=0;
     char ch;
     float total=0;
    fstream obj,obj1;
    dish_menu();
    obj1.open("bill.txt",ios::out|ios::binary);
     do{
    obj.open("resturant.txt",ios::in|ios::binary);
    cout<<"Enter the dish key:";
    cin>>a;
    while(obj.read((char*)&r,sizeof(r)))
    {
           if(r.key==a)
           {
            c++;
            cout<<"Enter the quantity:";
            cin>>rd.qty;
            rd.amount=rd.qty*r.price;
            cout<<"\t"<<r.dish<<"\t\t"<<r.price<<"*"<<rd.qty<<"\t\t"<<rd.amount<<endl;
            strcpy(rd.d,r.dish);
            rd.p=r.price;
            obj1.write((char*)&rd,sizeof(rd));
            total=total+rd.amount;
           }
        }
        if(c==0)
     {
        cout<<"Not found"<<endl;
     }

    cout<<"Do you want to order more [y/n]";
    cin>>ch;
    obj.close();
     }
     while(ch!='n');
    obj1.close();
    cout<<"||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||"<<endl;
    cout<<"|||||||||||||||||||||||||||||||||||||||||||||||| BILL  |||||||||||||||||||||||||||||||||||||||||||||||||||||||"<<endl;
     cout<<"||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||"<<endl;
    showbill();
    cout<<"||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||"<<endl;
    cout<<"|||\t\t\t\t\t\t\t   TOTAL="<<total<<"\t\t\t\t\t   |||"<<endl;
    cout<<"||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||||"<<endl;
}
 void showbill(){
    fstream obj;
    obj.open("bill.txt",ios::in|ios::binary);
    cout<<"\tDISH NAME\t\tPRICE\t\tQTY\t\tAMOUNT"<<endl;
    while(obj.read((char*)&rd,sizeof(rd)))
    {

            cout<<"\t"<<rd.d<<"\t\t\t"<<rd.p<<"\t\t"<<rd.qty<<"\t\t"<<rd.amount<<endl;


    }
    obj.close();
 }
 void dish_menu()
 {
      fstream obj;
     obj.open("resturant.txt",ios::in|ios::binary);
    while(obj.read((char*)&r,sizeof(r)))
    {


            cout<<"\t\t"<<r.key<<") "<<r.dish<<"------- TAKA  "<<r.price<<endl;
    }
    obj.close();
 }
 void info()
 {
     cout<<"-----------------------------------------------------------"<<endl;
     cout<<"Resturant Service Project"<<endl;
     cout<<"-----------------------------------------------------------"<<endl;
     cout<<"Idea Credit: -> KAZI TANVIR"<<endl;
     cout<<"-----------------------------------------------------------"<<endl;
     cout<<"Helping and guideline credit: -> DIPTA JUSTIN GOMES"<<endl;
     cout<<"-----------------------------------------------------------"<<endl;
     cout<<"Coding and Developing Credit: -> YASIN ARAFAT"<<endl;
     cout<<"-----------------------------------------------------------"<<endl;
     cout<<"Main feature of this project is : "<<endl;
     cout<<"                                 1.Admin system.(For resturant owner.)"<<endl;
     cout<<"                                 2.Customer system.(For ordering resturant customer.)"<<endl;
     cout<<"                                 3.Transaction .(For seeing the last bill.)"<<endl;
     cout<<"-----------------------------------------------------------"<<endl;
     cout<<"Admin features of this project : "<<endl;
     cout<<"                                 1. Admin can add dish by his willing. "<<endl;
     cout<<"                                 2. Admin can see the adding dish in Display. "<<endl;
     cout<<"                                 3. Admin can update added dish. "<<endl;
     cout<<"                                 4. Admin can also delete added dish. "<<endl;
     cout<<"                                 5. Admin can Quarey. "<<endl;
     cout<<"-----------------------------------------------------------"<<endl;
     cout<<"Customer features of this project : "<<endl;
     cout<<"                                   1. Customer can see offering dish by his willing. "<<endl;
     cout<<"                                   2. Customer when stop ordering then bill will be print on the screen. "<<endl;
     cout<<"-----------------------------------------------------------"<<endl;

 }
};
int main()
{
    char a;
    custmer obj;
    do
    {
        cout<<"\n\t\t\t\t\t Welcome to our digital resturant service  "<<endl;
        cout<<"\n\t\t\t\t\t\t||||||||||||||||||||"<<endl;
        cout<<"\t\t\t\t\t\t|                  |"<<endl;
        cout<<"\t\t\t\t\t\t|    1)Admin       |"<<endl;
        cout<<"\t\t\t\t\t\t|    2)Customer    |"<<endl;
        cout<<"\t\t\t\t\t\t|    3)Transaction |"<<endl;
        cout<<"\t\t\t\t\t\t|    4)About       |"<<endl;
        cout<<"\t\t\t\t\t\t|    0)Exit        |"<<endl;
        cout<<"\t\t\t\t\t\t|                  |"<<endl;
        cout<<"\t\t\t\t\t\t||||||||||||||||||||"<<endl;
        cout<<"\t\t\t\t\t\tSelect the menu : ";
        cin>>a;
        switch(a)
        {
        case '0':
            break;
        case '1':
             system("CLS");
             obj.login();
            obj.admin();
            break;
        case '2':
             system("CLS");
            obj.bill();
            break;
             case '3':
             system("CLS");
            obj.showbill();
            break;
            case '4':
             system("CLS");
            obj.info();
            break;
        }
    }
    while(a!='0');
}
