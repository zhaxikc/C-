# C-

###### 1.this n *this.

# Date.h
#ifndef DATE_H
#define DATE_H
using namespace std;
class Date{
public:
	Date(int =2000, int =1, int =1);            //初始化变量
	Date& setyear(int);                         //返回变量的引用
	Date& setmonth(int);                        //返回变量的引用
	Date* setday(int);                           //返回变量的指针
	Date setDate(int,int,int);                     //临时变量的赋值
	void display();
private:
	int y，m，d;
};
#endif

# cpp
#include<iostream>
using namespace std;
#include"Date.h"
Date::Date(int newy,int newm,int newd)       //初始化变量的值
{
	y=newy;                          //this->y=newy
	m=newm;                          //this->m=newm
	d=newd;                          //this->d=newd
}
Date& Date::setyear(int year)             //返回对象的引用？
{
	y=year;
	return *this;                   //这里返回对象的引用，返回的是y的值，y原地址储存值是2000，这里把year值赋给y，this依旧指向y的地址。
}
Date& Date::setmonth(int month)
{
	m=month;                  
    return *this;
}
Date* Date::setday(int day)              //返回对象的指针？
{
	d=day;                         
	return this;
}
Date Date::setDate(int x,int y,int z)
{
	Date tmp;                          //定义的是临时变量
	tmp.y=x;                           //?????????
	tmp.m=y;
	tmp.d=z;                         
	return tmp;                       //这里return前面是到copy函数里进行备份
}
void Date::display()
{
	cout<<"address is:"<<this<<"\t"<<y<<":"<<m<<":"<<d<<endl; //这里的this是地址  
}

# Test 
#include<iostream>
using namespace std;
#include"Date.h"
int main()
{
	Date x1,x2;          //这里x1,x2是初始化变量里的值
	cout<<"x1";
	x1.display();       //跑出小黑屋的x1和x2的地址不同，这是肯定的！
	cout<<"x2";
	x2.display();

	x1.setyear(2007).setmonth(3).setday(30);       //x1这里
	cout<<"x1";
	x1.display();

	x1.setDate(2000,1,10).setday(30);                 //？？？？？？？？？？
	cout<<"x1";
	x1.display();
	
	x1.setDate(2000,1,10).setday(15);                 //？？？？？？？？？？
	cout<<"x1";
	x1.display();

	Date *p;                                         //   ?
	p=x1.setday(21);
	cout<<"p";
	p->display();                                 //    ?

	Date x3=x2.setyear(2006).setmonth(4);
	cout<<"x3";
	x3.display();
	getchar();

	return 0;
}
