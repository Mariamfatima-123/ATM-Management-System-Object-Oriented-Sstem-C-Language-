# ATM-Management-System-Object-Oriented-Sstem-C++ language
#include<iostream>
#include<string>
#include<fstream>
using namespace std;
class ACCOUNT
{
private:
string name;
int account_no;
int pin;
string account_type;
protected:
int sav_balance;
int c_balance;
int deposit;
int withdraw;
public:
int pn()
{
int PIN=12;
cout<<"PLEASE ENTER YOUR P.I.N"<<endl;
for (int i=0; i<3; i++)
{
cin>>pin;
if(pin==PIN)
{
cout << "\n
*******************WELCOME*******************\n\n";
return 0;
}
else
{
cout<<"WRONG PIN"<<endl;
}
}
exit(0);
}
void get_AccountDetails()
{
system("cls");
fstream atm;
atm.open("D:Customers detail.txt",ios::app);
cout<<"\nEnter Customer Name : ";
cin>>name;
cout<<"Enter Account Number : ";
cin>>account_no;
cout<<"Enter Account Type : ";
cin>>account_type;
if(atm.is_open())
{
atm<<"Customer name: "<<name<<endl;
atm<<"Account no: "<<account_no<<endl;
atm<<"Account type: "<<account_type<<endl;
}
atm.close();
}
void display_alldetail()
{
fstream atm;
atm.open("D:Customers detail.txt",ios::in);
if(atm.is_open())
{
string ch;
while(!atm.eof())
{
getline(atm,ch);
cout<<"\t"<<ch<<endl;
}
cout<<endl;
}
atm.close();
}
void display_Details()
{
system("cls");
cout<<"\n\nCustomer Name : "<<name;
cout<<"\nAccount Number : "<<account_no;
cout<<"\nAccount Type : "<<account_type;
}
};
class CURRENT_ACCOUNT : public ACCOUNT
{
public:
CURRENT_ACCOUNT(int c)
{
c_balance=c;
}
void c_display()
{
cout<<"\nCurrent Balance :"<<c_balance;
}
void c_deposit()
{
system("cls");
fstream atm;
atm.open("D:Customers detail.txt",ios::app);
cout<<"\nEnter amount to Deposit:";
cin>>deposit;
if(atm.is_open())
{
atm<<"Deposit : "<<deposit<<endl;
}
atm.close();
c_balance = c_balance + deposit;
cout<<"Amount after deposit "<<c_balance;
cout<<"\n";
cout<<"\n\t\tThank you...!\n";
cout<<"\tFor using"<<endl;
cout<<"\t\tOur ATM Service"<<endl;
}
void c_withdraw()
{
system("cls");
fstream atm;
atm.open("D:Customers detail.txt",ios::app);
cout<<"\n\nBalance : "<<c_balance;
cout<<"\nEnter amount to be withdraw in a multiple of 500:";
cin>>withdraw;
if(atm.is_open())
{
atm<<"Withdraw: "<<withdraw<<endl;
}
atm.close();
if(withdraw %500==0)
{
c_balance=c_balance-withdraw;
cout<<"\nBalance Amount After Withdraw:"<<c_balance;
cout<<"\n";
cout<<"\n\t\tThank you...!\n";
cout<<"\tFor using"<<endl;
cout<<"\t\tOur ATM Service"<<endl;
}
else if(withdraw%500!=0)
{
cout<<"you can't withdraw"<<endl;
char ch;
cout<<"\nDo you want to do an other transaction "<<endl;
cin>>ch;
if(ch=='y')
{
c_withdraw();
}
else if(ch=='n')
{
exit(0);
}
}
}
void transfer_money()
{
system("cls");
fstream atm;
atm.open("D:Customers detail.txt",ios::app);
float transfer_balc;
int acc_n;
float new_account_balanse=0;
cout<<"Enter account number in which you want to transfer money"<<endl;
cin>>acc_n;
cout<<"Please enter the amount you want to transfer"<<endl;
cin>>transfer_balc;
if(atm.is_open())
{
atm<<"Transfer amount "<<transfer_balc<<endl;
}
atm.close();
if(transfer_balc>c_balance)
{
cout<<"Inufficient account balance"<<endl;
}
else
{
c_balance-=transfer_balc;
cout<<transfer_balc<<" Amount transferred"<<endl;
cout<<"The operation is successful,your remaining balance is: "<<c_balance<<endl;
new_account_balanse+=transfer_balc;
cout<<"Now,amount in new account is "<<new_account_balanse<<endl;
}
}
};
class SAVING_ACCOUNT : public ACCOUNT
{
public:
SAVING_ACCOUNT(int s)
{
sav_balance=s;
}
void s_display()
{
cout<<"\nSaving Balance :"<<sav_balance;
}
void s_deposit()
{
system("cls");
fstream atm;
atm.open("D:Customers detail.txt",ios::app);
cout<<"\nEnter amount to Deposit : ";
cin>>deposit;
if(atm.is_open())
{
atm<<"Deposit : "<<deposit<<endl;
}
atm.close();
sav_balance = sav_balance + deposit;
cout<<"Amount after deposit "<<sav_balance;
cout<<"\n";
cout<<"\n\t\tThank you...!\n";
cout<<"\tFor using"<<endl;
cout<<"\t\tOur ATM Service"<<endl;
}
void s_withdraw()
{
system("cls");
fstream atm;
int months;
float interest;
atm.open("D:Customers detail.txt",ios::app);
cout<<"\nBalance :- "<<sav_balance;
cout<<"\nEnter amount to be withdraw in a multiple of 500: ";
cin>>withdraw;
if(atm.is_open())
{
atm<<"Withdraw : "<<withdraw<<endl;
}
atm.close();
if(withdraw %500==0)
{
sav_balance=sav_balance-withdraw;
cout<<"\nBalance Amount After Withdraw: "<<sav_balance<<endl;
cout<<"\n";
cout<<"\n\t\tThank you...!\n";
cout<<"\tFor using"<<endl;
cout<<"\t\tOur ATM Service"<<endl;
}
else if(withdraw%500!=0)
{
cout<<"You can't withdraw"<<endl;
char ch;
cout<<"\nDo you want to do an other transaction "<<endl;
cin>>ch;
if(ch=='y')
{
s_withdraw();
}
}
cout<<"\nYour interest in saving account "<<endl;
cout<<"Enter months"<<endl;
cin>>months;
if(months>=5)
{
interest=(sav_balance*months)/100;
cout<<"Interest"<<interest<<endl;
sav_balance+=interest;
cout<<"Your saving balance after adding interest: "<<sav_balance<<endl;
atm.open("D:Customers detail.txt",ios::app);
if(atm.is_open())
{
atm<<"Interest: "<<interest<<endl;
atm<<"Your saving balance after adding interest: "<<sav_balance<<endl;
}
atm.close();
}
}
void transfer_moneysaving()
{
system("cls");
fstream atm;
atm.open("D:Customers detail.txt",ios::app);
float transfer_bals;
int acc_no;
float new_account_balance=0;
cout<<"Enter account number in which you want to transfer money"<<endl;
cin>>acc_no;
cout<<"Please enter the amount you want to transfer"<<endl;
cin>>transfer_bals;
if(atm.is_open())
{
atm<<"Transfer amount "<<transfer_bals<<endl;
}
atm.close();
if(transfer_bals>sav_balance)
{
cout<<"Inufficient account balance"<<endl;
}
else
{
sav_balance-=transfer_bals;
cout<<transfer_bals<<" Amount transferred"<<endl;
cout<<"The operation is successful,your remaining balance is: "<<sav_balance<<endl;;
new_account_balance+=transfer_bals;
cout<<"Now,amount in new account is "<<new_account_balance<<endl;
}
}
};
int main()
{
account a1;
CURRENT_ACCOUNT c1(2000);
SAVING_ACCOUNT s1(3000);
char type;
cout << "\n *****************************ATM MACHINE
SOFTWARE***************************\n\n";
cout<<"ENTER YOUR ATM CARD "<<endl;
a1.pn();
cout<<"Select account type"<<endl;
cout<<"\t\t\t 1.saving"<<endl;
cout<<"\t\t\t 2.current"<<endl;
cout<<"\nEnter S for saving customer and C for current account customer : ";
cin>>type;
int choice;
if(type=='s' || type=='S')
{
s1.get_AccountDetails();
system("cls");
while(1)
{
cout<<"\n\t\t\t\t*********************************";
cout<<"\n\t\t\t Choose Your Choice"<<endl;
cout<<"\t\t\t\t1) Deposit"<<endl;
cout<<"\t\t\t\t2) Withdraw"<<endl;
cout<<"\t\t\t\t3) Display Balance"<<endl;
cout<<"\t\t\t\t4) Transfer Money"<<endl;
cout<<"\t\t\t\t5) Display Detail of customer"<<endl;
cout<<"\t\t\t\t6) Display Details of all customer"<<endl;
cout<<"\t\t\t\t7) Exit"<<endl;
cout<<"\t\t\t\t*********************************"<<endl;
cout<<"Enter Your choice: ";
cin>>choice;
switch(choice)
{
case 1 :
s1.s_deposit();
break;
case 2 :
s1.s_withdraw();
break;
case 3 :
s1.s_display();
break;
case 4 :
s1.transfer_moneysaving();
break;
case 5 :
s1.display_Details();
s1.s_display();
break;
case 6:
s1.display_alldetail();
break;
case 7:
exit(0);
}
}
}
else if(type=='c' || type=='C')
{
c1.get_AccountDetails();
system("cls");
while(1)
{
cout<<"\n\t\t\t\t*********************************";
cout<<"\n\t\t\t Choose Your Choice"<<endl;
cout<<"\t\t\t\t1) Deposit"<<endl;
cout<<"\t\t\t\t2) Withdraw"<<endl;
cout<<"\t\t\t\t3) Display Balance"<<endl;
cout<<"\t\t\t\t4) transfer money"<<endl;
cout<<"\t\t\t\t5) Display Details of customer"<<endl;
cout<<"\t\t\t\t6) Display Details of all customer"<<endl;
cout<<"\t\t\t\t7) Exit"<<endl;
cout<<"\t\t\t\t*********************************"<<endl;
cout<<"Enter Your choice: ";
cin>>choice;
switch(choice)
{
case 1 :
c1.c_deposit();
break;
case 2 :
c1.c_withdraw();
break;
case 3 :
c1.c_display();
break;
case 4 :
c1.transfer_money();
break;
case 5 :
c1.display_Details();
c1.c_display();
break;
case 6:
c1.display_alldetail();
break;
case 7:
exit(0);
}
}
}
return 0;
}
