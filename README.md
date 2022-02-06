// Here is file handling program of part of library 
// you can enter book detail ,search book,view all books record,delete book

#include<iostream>
#include<conio.h>
#include<string.h>
#include<fstream>
#include<windows.h>
using namespace std;
class book{
int id;
char bname[20];
float price;
public:
    book(){
    id=0;
    strcpy(bname,"no title");
    price=0.0;
    }
    void input(){
    cout<<endl<<"Enter id,book name,Price\n";
    cin>>id;
    cin.ignore();
    cin.getline(bname,19);
    cin>>price;
    }
    void display();
    int ifile();
    int view();
    void search();
   void de();

};

void book::de(){
    char ch[20];
cout<<endl<<"Enter the title U want to delete";
cout<<endl;
cin.ignore();
cin.getline(ch,19);
ifstream fin;
ofstream tout;
tout.open("temp.dat",ios::out|ios::binary);
fin.open("bookfile.dat",ios::in|ios::binary);
fin.read((char*)this,sizeof(*this));
while(!fin.eof()){

     if(strcmp(this->bname,ch))
    tout.write((char*)this,sizeof(*this));
    fin.read((char*)this,sizeof(*this));

}
fin.close();
tout.close();
remove("bookfile.dat");
rename("temp.dat","bookfile.dat");


}

void book::search(){
char ch[20];
cout<<endl<<"Enter the title U want to search";
cout<<endl;
cin.ignore();
cin.getline(ch,19);
ifstream fin;
fin.open("bookfile.dat",ios::in|ios::binary);
fin.read((char*)this,sizeof(*this));
while(!fin.eof()){

     if(!strcmp(this->bname,ch))
    display();
    fin.read((char*)this,sizeof(*this));

}
fin.close();




}
int book::view(){
ifstream fin;
fin.open("bookfile.dat",ios::in|ios::binary);
fin.read((char*)this,sizeof(*this));
while(!fin.eof()){

    display();
    fin.read((char*)this,sizeof(*this));

}
fin.close();
return 0;

}
int book::ifile(){
ofstream fout;
if(id==0||price==0.0){
    cout<<"Values not initialized";
    return 0;
}
fout.open("bookfile.dat",ios::app);

fout.write((char*)this,sizeof(*this));
fout.close();
return 0;
}
void book::display(){
cout<<endl;
cout<<"|Book id="<<id;
cout<<" |Book name ="<<"\""<<bname<<"\"";
cout<<"|book Price="<<price<<"|";

}
int main(){
book b1;
char ch;

while(1){
        system("cls");
    system("color 3f");
    cout<<"Enter your choice:\n1.Enter record\n2.search record\n3.Delete record\n4.View record\n5.exit";
cin>>ch;
 switch(ch){
 case'1':system("cls");
 system("color f3");
 b1.input();
 b1.ifile();
 break;
 case'2':
     system("cls");
     system("color 8e");
     b1.search();

     getch();
 break;
 case'3':
     system("cls");
     system("color af");
     b1.de();

     break;
 case'4':
     system("cls");
     system("color 6");
     b1.view();
     getch();
     break;
 case'5':
    return 0;
    break;
    default: cout<<"enter correct choice";

 }




}
getch();
return 0;


}
