
#include<stdio.h>
#include<stdlib.h>

char* month_str[]= {"January","February","March","April","May","June","July","August","September","October","November","December"};
char* week[]= {"Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"};


int IsLeapYear(int year) /*find out the year is leap year or not*/
{
    if((year%4==0&&year%100!=0)||(year%400==0)) //这里是判断是否是闰年的
        return 1; //如果是闰年就返回值1
    else
        return 0;//不是的话返回0

}
int month_day(int year,int month) //这个函数用来判断这年的月分有多少天的
{
    int mon_day[]= {31,28,31,30,31,30,31,31,30,31,30,31};
    if(IsLeapYear(year)&&month==2) /*判断是判断是否是闰年，如果是闰年而且这个月是2月那这个月有29天*/
        return 29;
    else
        return(mon_day[month-1]);

}
int DaySearch(int year,int month,int day) /*这个函数是计算输入的日期对应的星期*/
{
    int c=0;
    float s;
    int m;
    for(m=1; m<month; m++)
        c=c+month_day(year,m); //这是计算输入的月分的累计天数
    c=c+day; //计算日期在这一年中是第几天
    s=year-1+(int)(year-1)/4+(int )(year-1)/100+(int)(year-1)/400-40+c; /*这是计算日期对应的星期公式，这个公式可在网上查到*/
    return ((int)s%7); //与上语句同属计算日期对应的星期
}

int PrintAllYear(int year)/*这个函数是用来输出全年的日历*/
{
    int temp;
    int i,j;
    printf("\n\n%d Calander\n",year);
    for(i=1; i<=12; i++)
    {
        printf("\n\n%s(%d)\n",month_str[i-1],i); //输出月分名称
        printf("0 1 2 3 4 5 6 \n");
        printf("S M T W T F S \n\n");
        temp=DaySearch(year,i,1);
        for(j=1; j<=month_day(year,i)+temp; j++)
        {
            if(j-temp<=0)
                printf(" ");
            else if(j-temp<10)
                printf("%d ",j-temp);
            else
                printf("%d ",j-temp);

            if(j%7==0)
                printf("\n");
        }
    }
    return 0;
}

int main()
{
    int option,da;
    char ch;
    int year,month,day;
    printf("Copyright @ 2005 TianQian All rights reserved!:):):)");
    printf("\n\nWelcome to use the WanNianLi system!\n");

    while(1)
    {
        printf("\nPlease select the service you need:\n"); //用来提示选择执行功能
        printf("\n1 Search what day the day is"); //选择1时，用来计算这一天是星期几
        printf("\n2 Search whether the year is leap year or not"); //计算是否这年是闰年
        printf("\n3 Print the calander of the whole year"); //输入全年的日历
        printf("\n4 Exit\n"); //选择退出程序
        scanf("%d",&option);


        switch(option) //用来选择执行
        {
        case 1:
            while(1)
            {
                printf("\nPlease input the year,month and day(XXXX,XX,XX):"); //提示输入
                scanf("%d,%d,%d,%c",&year,&month,&day); //读入数据
                da=DaySearch(year,month,day); //调用DaySearch()函数来计算是星期几
                printf("\n%d-%d-%d is %s,do you want to continue?(Y/N)",year,month,day,week[da]);
                fflush(stdin); //刷新输入缓冲区
                scanf("%c",&ch);
                if(ch=='N'||ch=='n')
                    break;
            }
            break;
        case 2: /*当为2时，进行相应运算*/
            while(1)
            {
                printf("\nPlease input the year which needs searched?(XXXX)");
                scanf("%d",&year);
                if(IsLeapYear(year))
                    printf("\n%d is Leap year,do you want to continue?(Y/N)",year);
                else
                    printf("\n%d is not Leap year,do you want to continue(Y/N)?",year);
                fflush(stdin);
                scanf("%c",&ch);
                if(ch=='N'||ch=='n')
                    break;
            }
            break;
        case 3: /*当为3时运行相应的运算*/
            while(1)
            {
                printf("\nPlease input the year which needs printed(XXXX)");
                scanf("%d",&year);
                PrintAllYear(year);
                printf("\nDo you want to continue to print(Y/N)?");
                fflush(stdin);
                scanf("%c",&ch);
                if(ch=='N'||ch=='n')
                    break;
            }
            break;
        case 4:
            fflush(stdin);
            printf("Are you sure?(Y/N)");
            scanf("%c",&ch);
            if(ch=='Y'||ch=='y')
                exit(1);
            break;
        default:
            printf("\nError:Sorry,there is no this service now!\n");
            break;
        }

    }

    return 0;
}
