#include<iostream>
#include<string.h>
#include<fstream>
#include<stdio.h>
#include<conio.h>
#include<iomanip>
#include<windows.h>
using namespace std;
class Canteen{
    char itemname[20];
    int price;
    int code;
    int stock;
    int qtysold;
    public:
    Canteen()
    {
        qtysold=0;
    }
    void putstock(int s)
    {
        stock=s;
    }
    int takeorder()
    {
        int qty;
        cout<<"\tEnter Quantity :";
        cin>>qty;
        if(qty>stock)
           {
               cout<<" \nsorry !! ITEM NOt available!";
               return 0;
           } 
        else
            stock-=qty;
            qtysold+=qty;
            return qty*price;
    }
    bool owner_loginpage();
    void user_loginpage();
    friend class customer;
    void add();
    void update();
    void showdetails();
    void deleterecord(char*);
    char *getname()
    {
        return itemname;
    }
    void menu()
    {
        cout<<"\n\t\t"<<code<<"\t\t"<<itemname<<"\t\t"<<price;
    }
   friend  int order();
    friend  void totalsales();
    // edititems();

};
class employee
{
    char ename[20];
    int age;
    char address[30];
    char phonenumber[10];
    int salary;
    int salarypaid;
    char date[12];
    public:
        employee()
        {
            salarypaid=0;
        }
        void addemployee();
        void delete_employee(char*);
        void show_e_record();
        void modifyrecord();
        void paysalary();
};
void employee::modifyrecord()
{
    char name[20];
    int flag=0;
    cout<<"Enter employee name : ";
    cin.ignore();
    cin.get(name,20);
    fstream file("employee.dat",ios::binary|ios::in|ios::out);
    file.seekg(0,ios::beg);
    int index=0;
    while(file.eof()!=true);
    {
       
        file.read((char*)this,sizeof(employee));
        index++;
        if(!strcmp(name,ename))
        {
            int location=(index-1)*sizeof(employee);
            file.seekp(location);
            cout<<"\nEnter Employee Name : ";
            cin.ignore();
            cin.get(ename,30);
            cout<<"\nEnter employee Age :";
            cin>>age;
            cout<<"\nEnter Phone number :";
            cin>>phonenumber;
            cout<<"\nEnter Employee Addresss :";
            cin.ignore();
            cin.get(address,20);
            file.write((char*)this,sizeof(employee));
            flag=1;
        }
    }
    file.clear();
    file.close();
    if(flag==0)
        cout<<"\n NO RECORD FOUND!!";
    else 
        cout<<" \nRECORD UPDATED";
 }
 void employee::paysalary()
 {
 char name[20];
    int flag=0;
    cin.ignore();
    cout<<"Enter employee name : ";
    cin.get(name,20);
    fstream file("employee.dat",ios::in|ios::out|ios::binary);
    file.seekg(0,ios::beg);
    while(file.read((char*)this,sizeof(employee)));
    {
        if(!strcmp(name,ename))
        {
            Canteen c;
            // if(c.owner_loginpage())
            // {
                salary=0;
                file.write((char*)this,sizeof(employee));
                flag=1;
           // }
        }
    }
    file.close();
    if(flag==0)
        cout<<"\nNO RECORD FOUND!!!";
    else
        cout<<"\nSALARY PAID SUCCESFULLY!";
 }
void employee::show_e_record()
{
    fstream file("employee.dat",ios::binary|ios::in);
    file.seekg(0,ios::beg);
    cout<<"\n*************************************************************EMPLOYEE RECORD**************************************************************";
    cout<<"\n\t NAME"<<"    AGE"<<" "<<"ADDRESS"<<"       PHONE NO   "<<"  SALARY    "<<"  SALARY PAID  "<<"  DATE OF JOINING ";
    while (file.read((char*)this,sizeof(employee)))
    {
    cout<<"\n\t"<<ename<<"    "<<age<<" "<<address<<"      "<<phonenumber<<"  "<<salary<<"  "<<salarypaid<<"    "<<date;
    }
     cout<<"\n*************************************************************EMPLOYEE RECORD**************************************************************";
    file.close();
    
}
void employee::addemployee()
{
    fstream file("employee.dat",ios::binary|ios::out|ios::app);
    cout<<"\nEnter Employee Name : ";
    cin.ignore();
    cin.get(ename,20);
    cout<<"\nEnter employee Age :";
    cin>>age;
    cout<<"\nEnter Phone number :";
    cin>>phonenumber;
    cout<<"\nEnter Employee Addresss :";
    cin.ignore();
    cin.get(address,30);
    cout<<"\nEnter Salary :";
    cin>>salary;
    cout<<"\nEnter joining date :";
    cin.ignore();
    cin.get(date,11);
    file.write((char*)this,sizeof(employee));
    file.close();
}
void employee::delete_employee(char*name)
{
   fstream oldfile("employee.dat",ios::binary|ios::in);
   fstream nfile("temp.dat",ios::binary | ios::out|ios::app);
   oldfile.seekg(0,ios::beg);
   int flag=0;
   while(!oldfile.eof())
    {
        // if(oldfile.eof()==true)
            
        //     { break;
        //     }
        oldfile.read((char*)this,sizeof(employee));
        if(oldfile)
        {
            cout<<ename;
            cout<<name;
            if(!strcmp(name,ename))
            {
                cout<<"\nRecord is to be deleted is :";
                cout<<"\tNAME "<<"\tAGE\t"<<" SALARY \t"<<"\tJOINING DATE";
                cout<<"\n\t"<<name<<"\t"<<age<<"\t"<<salary<<" \t\t   "<<date;
                flag=1;
            }
            else
            {
                nfile.write((char*)this,sizeof(employee));
            }
        }
    }
    oldfile.clear();
    oldfile.close();
    nfile.close();
    remove("employee.dat");
    rename("temp.dat","employee.dat");
    if(flag==0)
        cout<<"\nNO record found!! ";

}

int order()
{
    Canteen c;
    int code;//code for taking order
    cout<<"\n\t\t CODE"<<"\t\tITEMS "<<"\t\tPRICE";
     fstream file("stocks.dat",ios::binary | ios::out |ios::in);
    file.seekg(0,ios::beg);
    while(file.read((char*)&c,sizeof(c)))
    {
        c.menu();

    }
    file.clear();
    cout<<"\nEnter code of item you want : ";
    cin>>code;
    //c.takeorder();
     int serialno=0, flag=0;//flag for checking item exists or not
    file.seekg(0,ios::beg);
    int bill;
    while(!file.eof())
    {
        file.read((char*)&c,sizeof(c));
        serialno++;
        if(code==c.code)
        {
            int location=(serialno-1)*sizeof(c);
            file.clear();
            file.seekp(location);
            bill=c.takeorder();
            file.write((char*)&c,sizeof(c));
            file.clear();
            file.close();
            flag=1;
            return bill;
        }
    }
    if(flag==0)
        {
            cout<<"Invalid code!";
            return 0;
        }
    return 0;
}
void totalsales()
{
    Canteen c;
    int sales_in_rupees;
    fstream file("stocks.dat",ios::binary | ios::out |ios::in);
    file.seekg(0,ios::beg);
    cout<<"\n\t\tITEM "<<"\t\tTOTAL SALES (pieces)"<<"\t\tTOTAL SALES (RUPEES)";
    while(file.read((char*)&c,sizeof(c)))
    {
        cout<<"\n\t\t"<<c.itemname<<"\t\t"<<c.qtysold<<"\t\t"<<c.qtysold*c.price;
    }


}
void Canteen:: add()
{
    cout<<"\nEnter Item Name : ";
    cin.ignore();
    cin.get(itemname,20);
    cout<<"\nEnter Item price : ";
    cin>>price;
    cout<<"\nENter item code : ";
    cin>>code;
    cout<<"\nEnter item Quantity : ";
    cin>>stock;
}
void Canteen::update()
{
    cout<<"\nEnter Item new Name : ";
    cin>>itemname;
    cout<<"\nEnter Item price : ";
    cin>>price;
    cout<<"\nENter item code : ";
    cin>>code;
    cout<<"\nEnter item Quantity : ";
    cin>>stock;
}
void Canteen::showdetails()
{
    cout<<"\n\t\t\t"<<code<<"\t\t"<<itemname<<"\t\t"<<price<<" \t\t\t "<<stock;
}
void Canteen::deleterecord(char *name)
{
    fstream oldfile("stocks.dat",ios::binary | ios::in);
    fstream nfile("temp.dat",ios::binary|ios::out);
    oldfile.seekg(0,ios::beg);
    int flag=0;
    while(!oldfile.eof())
    {
         oldfile.read((char*)this,sizeof(Canteen));
        if(oldfile)
        {
        if(!strcmp(name,itemname))
        {
            char ch;
             cout<<"\nRecord deleted is :";
            cout<<"\n\t\t " <<setw(14)<<" ITEM  "<<"\t\t"<<" CODE "<<"\t\tPRICE"<<"\tSTOCK";
              cout<<"\n\t\t "<<setw(14)<<itemname<<"\t\t"<<code<<"\t\t "<<price<<" \t  "<<stock;
              flag=1;
        }
        else
        {
            nfile.write((char*)this,sizeof(Canteen));   
        }
        }
    }
  oldfile.close();
  nfile.close();
  remove("stocks.dat");
  rename("temp.dat","stocks.dat");
  if(flag==0)
      cout<<"\nNO record found !!";
    else
        cout<<"\nRecord deleted succesfully!";
}
bool Canteen::owner_loginpage(){
    char pass[4];
    int i;
    cout<<"\nENTER OWNER PASSWORD : ";
    
   for( i=0;i<4;i++)
   {
       pass[i]=getch();
       cout<<"*";
   }
   pass[i]='\0';
   char pas[5]={'p','a','s','s'};
    bool flag=false;
    if(!strcmp(pass,pas))
    {
        char any_key;
        cout<<endl<<"	\nOWNER ACCESS GRANTED"<<endl;
        cout<<endl<<"	PRESS ANY KEY TO CONTINUE"<<endl;
        cout<<"	";
        cin>>any_key;
      return true;
    }
    else
    {
        cout<<endl<<"\n	INVALIDPASSWORD"<<endl;
        return false;
    }
    //return flag;
}
class customer
{
    char cid[6];
    char custname[20];
    char custaddre[40];
    char phnumber[12];
    int Mcharges;
    public:
    customer()
    {
         Mcharges=3000;
    }

        char *getid()
        {
            return cid;
        }
         string getname()
        {
            return custname;
        }
         string getaddress()
        {
            return custaddre;
        }
        char *getnumber()
        {
            return phnumber;
        }
        void getcustdetails();
        void showallcustdetails();
        friend char* show_one_custdetails();
        void modifydetails();
        void deleterecord(char* );
        friend void paybill();
        friend class Canteen;
};
void customer::deleterecord(char *name)
{
    fstream oldfile("custdetails.txt",ios::binary | ios::in);
    fstream nfile("temp.txt",ios::binary|ios::out);
    oldfile.seekg(0,ios::beg);
    int flag=0;
    while(!oldfile.eof())
    {
         oldfile.read((char*)this,sizeof(customer));
          cout<<custname;
        if(oldfile)
        {
        if(!strcmp(name,custname))
        {
    
            char ch;
            cout<<"\nremaining bill of "<<custname<<" is rupees "<<Mcharges<<"\n you need pay remaining bill to delete record ??";
            cin>>ch;
            if(ch=='y' || ch=='Y')
            {
                cout<<"BIll paid succesfully!!";
                Mcharges=0;
             cout<<"\nRecord deleted is :";
            cout<<"\n\t\t " <<setw(14)<<" NAME "<<"\t\t"<<" ADDRESS "<<setw(10)<<" \t\t\t\tPH.NUMBER"<<"\t\tRemaining bill";
              cout<<"\n\t\t "<<setw(14)<<custname<<"\t\t"<<custaddre<<"\t\t\t\t"<<setw(10)<<phnumber<<"\t\t\t"<<Mcharges;
              flag=1;
             }
             else   
                return;
        }
        else
        {

            nfile.write((char*)this,sizeof(customer));   
        }
        }
    }
  oldfile.close();
  nfile.close();
  remove("custdetails.txt");
  rename("temp.txt","custdetails.txt");
  if(flag==0)
      cout<<"\nNO record found !!";
    else
        cout<<"\nRecord deleted succesfully!";
}
void customer::getcustdetails()
{      
        cout<<"\nEnter customer Name :";
            //fgets(custname,30,stdin);
            cin.ignore();
           // getline(cin,custname);
           cin.get(custname,20);
       // cout<<"\nENter last four digits of Aadhar customer :  ";
        //cin>>cid;
        cin.ignore();
        cout<<"\nEnter address: ";
        cin.get(custaddre,40);
        cout<<"\nEnter phone number : ";
       cin>>phnumber;
}

void customer::showallcustdetails()
{
         fstream fin("custdetails.txt",ios::in);
        fin.seekg(0,ios::beg);
        int i=1;
        //fin.read((char*)&cs,sizeof(cs));
        cout<<"\t**************************************************************Customer details**************************************************************";
        cout<<"Sr no"<<setw(10)<<"\n\t\t\tCustomer Name\t\t"<<"\tAddress\t\t\t\t" <<"Phone Number"<<" \t\tBill";
        while(fin.read((char*)this,sizeof(customer)))
        { 
            cout<<"\n------------------------------------------------------------------------------------------------------------------------------------------------";
            cout<<"\n\t\t\t  "<<setw(14)<<custname<<"\t\t"<<custaddre<<"\t\t\t\t"<<setw(10)<<phnumber<<"\t\t"<<Mcharges;
            cout<<"\n------------------------------------------------------------------------------------------------------------------------------------------------";
        }
        fin.clear();
        fin.close();
}
void customer::modifydetails()
{
    char ch;
    int bill,flag=0;
    char name[20];
    int totalcustomers=0;
    cout<<"Enter customer name :";
    cin.ignore();
    cin.get(name,20);
    fstream file("custdetails.txt",ios::out | ios::in |ios::binary);
    int serialno=0;
    file.seekg(0,ios::beg);
    while(file.read((char*)this,sizeof(customer)))
    {  serialno++;
        if(!strcmp(name,custname))
        {
        int location=(serialno-1)*sizeof(customer);
        file.seekp(location);
        cin.ignore();
        cout<<"\nEnter new name : ";
        cin.get(custname,20);
        cin.ignore();
        cout<<"\nEnter new Address : ";
        cin.get(custaddre,40);
        cout<<"\nEnter new numbeR : ";
        cin>>phnumber;
     cout<<"\nEnter  bill amount  you want to pay : ";
    cin>>bill;
    Mcharges-=bill;
    file.write((char*)this,sizeof(customer));
     flag=1;
    file.close();
    }
    }
    if(flag==0)
    {
        cout<<"\ncustomer not found!!";
    }
}
void Canteen::user_loginpage(){
    string pass;
    string user_name;
    cout<<"ENTER USER NAME : ";
    cin>>user_name;
    cout<<"\nENTER PASSWORD : ";
    cin>>pass;
    //add file to check for details...
    if(pass=="x" && user_name=="yyy"){
        cout<<"USER ACCESS GRANTED .....";
        
    }
    else if(pass!="x"){
        cout<<"INVALID PASSWORD...";
    }
    else if(user_name!="yyy"){
        cout<<"INVALID USER NAME >>>";
    }
}
void employeerecord()
{
    int ch;
    employee e;
    do{
    cout<<"\n1:ADD NEW EMPLOYEE \n2:DELETE EMPLOYEE RECORD \n3:EDIT EMPLOYEE \n4:PAY EMPLOYEE SALARY \n5:SHOW ALL EMPLOYEE RECORD \n6:BACK";
    cout<<"\nENTER YOUR CHOICE :";
    cin>>ch;
    switch (ch)
    {
    case 1:
        e.addemployee();
        break;
    case 2:
        char name[20];
        cout<<"ENTER EMPLOYEE NAME :";
        cin.ignore();
        cin.get(name,20);
        cout<<"2233";
        e.delete_employee(name);
        break;
    case 3:
        e.modifyrecord();
        break;
    case 4:
        e.paysalary();
        break;
    case 5:
     e.show_e_record();
     break;
    default:
        break;
    }
    } while (ch!=6);
    
}
void invetorymanagement()
{
    int ch1;//for switch case
do{
    
    cout<<"\n1:Add Item \n2:Edit Items \n3:View Stocks\n4:Total sales\n5:Delete An item "; 
    cout<<"\nENter your choice : ";
    cin>>ch1;
    switch(ch1)
    { 
        case 1:
            {
            Canteen can;
                fstream file("stocks.dat",ios::binary | ios::app);
                can.add();
                file.write((char*)&can,sizeof(Canteen));
                file.close();
                cout<<"\nItem addes succesfully";
            }
        break;
        case 2:
        {
            Canteen can;
            char name[20];
            cout<<"Enter item name : ";
            cin>>name;
            int serialno=0, flag=0;//flag for checking item exists or not
            fstream file("stocks.dat",ios::binary | ios::out |ios::in);
            file.seekg(0,ios::beg);
            while(file.read((char*)&can,sizeof(can)))
            {
                serialno++;
                if(!strcmp(name,can.getname()))
                {
                    int location=(serialno-1)*sizeof(can);
                    file.seekp(location);
                    file.clear();
                    cout<<"\nEnter new values :\n ";
                    can.update();
                    file.write((char*)&can,sizeof(can));
                    flag=1;
                    //file.clear();
                    file.close();
                    cout<<"\nITEM UPDATED!!!";
                }
            }
            if(flag==0)
                cout<<"\nItem does not exists";
        }
        break;
        case 3:
        {
            Canteen can;
            fstream file("stocks.dat",ios::binary | ios::in);
            file.seekg(0,ios::beg);
            cout<<"\n\t\t\tCode"<<"\t\tITEM"<<"\t\tPRICE"<<"\t\tQUANTITY";
            while(file.read((char*)&can,sizeof(Canteen)))
            {
                can.showdetails();
            }
                file.clear();
                file.close();
        }
        break;
        case 4:
        {
            totalsales();
            break;
        }
        case 5:
            {
            Canteen c;
            char item[20];
            cout<<"\n Enter Name of Item You Wants To Delete : ";
            cin.ignore();
            cin.get(item,20);
            c.deleterecord(item);
            }
            break;
        case 6:
            break;
        default:
            cout<<"Incorrect choice";
            break;
    }
    }while(ch1!=6);
}
int main(){
    Canteen cn;
    customer cs;
    int choice;
    char id[5];
    
    do{
        cout<<"\n \n WELCOME TO SCOE CANTEEN\n\n";
        cout<<"\n1.MANAGER LOGIN\n2. Exit";
        cout<<"\nEnter your choice : ";
        cin>>choice;
        //ofstream fout;
        switch(choice)
        {
            case 1: 
                if(cn.owner_loginpage())
                {
                    int ch;
                    do{
                    cout<<"\n1:Add New Customer\n2:Show All customer Details\n3:Modify A record\n4:Delete a  cust record\n5:Manage inventory";
                    cout<<"\n6:ORDER\n7:Employee's Record\n8:Back to main menu";
                    cout<<"\n\1Enter Your choice\2";
                    cin>>ch;
                    switch(ch)  
                            {
                            case 1:\
                             {
                                ofstream fout ;
                                //fout.seekp(0,ios::beg);
                                fout.open("custdetails.txt",ios::binary|ios::app );
                                cs.getcustdetails();
                                fout.write((char*) &cs,sizeof(customer));
                                cout<<"\nDetails Addes succesfully";
                                fout.close();
                            }
                                break;
                            case 2:
                            {
                                customer cs;
                                cs.showallcustdetails();
                                }
                                break;
                                case 3:
                                {
                                    customer cs;
                                    cs.modifydetails();
                                    break;
                                }
                                case 4:
                                {
                                    customer cs;
                                    char name[20];
                                    cin.ignore();
                                    cout<<"\nEnter  customer Name to delete a record ";
                                    cin.get(name,20);
                                    cs.deleterecord(name);
                                    break;
                                }
                                case 5:
                                {
                                    invetorymanagement();
                                }
                                break;          
                                case 6:{
                                            char ch;
                                            int bill=0;
                                        st1: bill+= order();
                                        cout<<"\nWant toorder anything more (y if yes) : ";
                                        cin>>ch;
                                        if(ch=='y'||ch=='Y')
                                                goto st1;
                                            else
                                            { 
                                                cout<<"\nTotal bill is : "<<bill;
                                                break;
                                            }
                                        }
                                case 7:
                                employeerecord();
                                    break;
                                default:
                                cout<<"INVALID CHOICE!!";
                                break;
                    }
            }while(ch!=8);
            }
             break;
            case 2: 
            {
            cn.user_loginpage();
            break;
            }
            case 4:
                break;
            }
    }while(choice!=4);
    return 0;
}
