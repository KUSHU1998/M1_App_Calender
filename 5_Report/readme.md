CALENDAR SYSTEM USING C - By Kushla Devi

##### **Requirements:**

This project is to build a calendar system where we can find out the day at a particular date, view all the dates of a month, write a note.

## **Identify Features:**

- Find out the day
- View all the dates of a month
- Write a note

## State of art/Research:

Calendars have existed for thousands of years and have gone through several reforms until finally arriving at the currently widely used version, known as the Gregorian calendar. It is a solar calendar, meaning that it is based on the Earth&#39;s revolution around the Sun. Despite its seeming simplicity and ease-of-use, the rules which lay the foundation for the Gregorian calendar and its predecessors result in some complications. A year is not an exact integer of days, despite being presented as such. That is why certain years have a &quot;leap day&quot;, an additional day in the year, to compensate for the inaccuracy.

## **4-W&#39;s and 1-H:**

### **Why:**

The interface is user-friendly and simple to navigate.

### **Where:**

The Calendar System can be managed with in a system.

### **Who:**

It can be used by any person.

### **When:**

It can be used at anytime depending upon the person&#39;s preferences.

### **How:**

By entering certain commands you can view details and enter notes.

**SWOT Analysis:**

### **STRENGTH:**

- Simple and easy to operate.
- Multiple features
- Saves time and reduces overheads.
- No internet is needed.

### **WEAKNESS:**

- The interface is not as good.

### **OPPORTUNITIES:**

- Apart from those information that are mentioned above in the objectives, you can also use your ideas how to take this project to next level by adding more feature. The interface can be much better as well.

### **THREATS:**

- Inadequacy of infrastructure and hardware.

**Design &amp; Implementation**

**About Calendar in C:** Basically three operations can be done in this calendar application. To find out the day corresponding to a given date, the date, month and year are asked. You can list the days and dates of any month of any year. For example, entering 04 2014 (April 2014) will give you an output as shown in the screenshot in this post.

You can navigate the months using arrow keys, or press &#39;n&#39; and &#39;p&#39; keys to view the next and previous months respectively. The third feature of this C mini project on Calendar application utilizes file handling. With this feature, you can add important notes with corresponding dates.

- The system design of Calendar system will provide the design phase for this system.
- The main aim of the design phase is to provide the solution for the specified requirements and how the flow of the project is managed.
- It also displays how the features are implemented and can be used at every step.

# **High level Design:**

- Behavioral diagram(image given above)

The functions used in the source code are simple and easy to understand. The ones listed below have been used to produce background with color effects. They are described in the source code with comments.

- void SetColor(int ForgC)
- void ClearConsoleToColors(int ForgC, int BackC)
- void SetColorAndBackground(int ForgC, int BackC)

**void gotoxy (int x, int y)** – You need to understand this function as it is an important one used in this Calendar in C language. You can find this function used in many C projects. This function allows you to print text in any place of screen. Using this function in Code::Blocks requires coding, but it can be directly used in Turbo C. Here is a code for this function in Code::Blocks.

COORD coord = {0, 0}; // setting coordinates to (0,0) as global variables

void gotoxy (int x, int y)

{

coord.X = x; coord.Y = y; // X and Y are the coordinates

SetConsoleCursorPosition(GetStdHandle(STD\_OUTPUT\_HANDLE), coord);

}

**Source Code -**

#include\&lt;stdio.h\&gt;

#include\&lt;conio.h\&gt;

#include\&lt;windows.h\&gt;

struct Date{

int dd;

int mm;

int yy;

};

struct Date date;

struct Remainder{

int dd;

int mm;

char note[50];

};

struct Remainder R;

COORD xy = {0, 0};

void gotoxy (int x, int y)

{

xy.X = x; xy.Y = y; // X and Y coordinates

SetConsoleCursorPosition(GetStdHandle(STD\_OUTPUT\_HANDLE), xy);

}

//This will set the forground color for printing in a console window.

void SetColor(int ForgC)

{

WORD wColor;

//We will need this handle to get the current background attribute

HANDLE hStdOut = GetStdHandle(STD\_OUTPUT\_HANDLE);

CONSOLE\_SCREEN\_BUFFER\_INFO csbi;

//We use csbi for the wAttributes word.

if(GetConsoleScreenBufferInfo(hStdOut, &amp;csbi))

{

//Mask out all but the background attribute, and add in the forgournd color

wColor = (csbi.wAttributes &amp; 0xF0) + (ForgC &amp; 0x0F);

SetConsoleTextAttribute(hStdOut, wColor);

}

return;

}

void ClearColor(){

SetColor(15);

}

void ClearConsoleToColors(int ForgC, int BackC)

{

WORD wColor = ((BackC &amp; 0x0F) \&lt;\&lt; 4) + (ForgC &amp; 0x0F);

//Get the handle to the current output buffer...

HANDLE hStdOut = GetStdHandle(STD\_OUTPUT\_HANDLE);

//This is used to reset the carat/cursor to the top left.

COORD coord = {0, 0};

//A return value... indicating how many chars were written

// not used but we need to capture this since it will be

// written anyway (passing NULL causes an access violation).

DWORD count;

//This is a structure containing all of the console info

// it is used here to find the size of the console.

CONSOLE\_SCREEN\_BUFFER\_INFO csbi;

//Here we will set the current color

SetConsoleTextAttribute(hStdOut, wColor);

if(GetConsoleScreenBufferInfo(hStdOut, &amp;csbi))

{

//This fills the buffer with a given character (in this case 32=space).

FillConsoleOutputCharacter(hStdOut, (TCHAR) 32, csbi.dwSize.X \* csbi.dwSize.Y, coord, &amp;count);

FillConsoleOutputAttribute(hStdOut, csbi.wAttributes, csbi.dwSize.X \* csbi.dwSize.Y, coord, &amp;count );

//This will set our cursor position for the next print statement.

SetConsoleCursorPosition(hStdOut, coord);

}

return;

}

void SetColorAndBackground(int ForgC, int BackC)

{

WORD wColor = ((BackC &amp; 0x0F) \&lt;\&lt; 4) + (ForgC &amp; 0x0F);;

SetConsoleTextAttribute(GetStdHandle(STD\_OUTPUT\_HANDLE), wColor);

return;

}

int check\_leapYear(int year){ //checks whether the year passed is leap year or not

if(year % 400 == 0 || (year % 100!=0 &amp;&amp; year % 4 ==0))

return 1;

return 0;

}

void increase\_month(int \*mm, int \*yy){ //increase the month by one

++\*mm;

if(\*mm \&gt; 12){

++\*yy;

\*mm = \*mm - 12;

}

}

void decrease\_month(int \*mm, int \*yy){ //decrease the month by one

--\*mm;

if(\*mm \&lt; 1){

--\*yy;

if(\*yy\&lt;1600){

printf(&quot;No record available&quot;);

return;

}

\*mm = \*mm + 12;

}

}

int getNumberOfDays(int month,int year){ //returns the number of days in given month

switch(month){ //and year

case 1 : return(31);

case 2 : if(check\_leapYear(year)==1)

return(29);

else

return(28);

case 3 : return(31);

case 4 : return(30);

case 5 : return(31);

case 6 : return(30);

case 7 : return(31);

case 8 : return(31);

case 9 : return(30);

case 10: return(31);

case 11: return(30);

case 12: return(31);

default: return(-1);

}

}

char \*getName(int day){ //returns the name of the day

switch(day){

case 0 :return(&quot;Sunday&quot;);

case 1 :return(&quot;Monday&quot;);

case 2 :return(&quot;Tuesday&quot;);

case 3 :return(&quot;Wednesday&quot;);

case 4 :return(&quot;Thursday&quot;);

case 5 :return(&quot;Friday&quot;);

case 6 :return(&quot;Saturday&quot;);

default:return(&quot;Error in getName() module.Invalid argument passed&quot;);

}

}

void print\_date(int mm, int yy){ //prints the name of month and year

printf(&quot;---------------------------\n&quot;);

gotoxy(25,6);

switch(mm){

case 1: printf(&quot;January&quot;); break;

case 2: printf(&quot;February&quot;); break;

case 3: printf(&quot;March&quot;); break;

case 4: printf(&quot;April&quot;); break;

case 5: printf(&quot;May&quot;); break;

case 6: printf(&quot;June&quot;); break;

case 7: printf(&quot;July&quot;); break;

case 8: printf(&quot;August&quot;); break;

case 9: printf(&quot;September&quot;); break;

case 10: printf(&quot;October&quot;); break;

case 11: printf(&quot;November&quot;); break;

case 12: printf(&quot;December&quot;); break;

}

printf(&quot; , %d&quot;, yy);

gotoxy(20,7);

printf(&quot;---------------------------&quot;);

}

int getDayNumber(int day,int mon,int year){ //retuns the day number

int res = 0, t1, t2, y = year;

year = year - 1600;

while(year \&gt;= 100){

res = res + 5;

year = year - 100;

}

res = (res % 7);

t1 = ((year - 1) / 4);

t2 = (year-1)-t1;

t1 = (t1\*2)+t2;

t1 = (t1%7);

res = res + t1;

res = res%7;

t2 = 0;

for(t1 = 1;t1 \&lt; mon; t1++){

t2 += getNumberOfDays(t1,y);

}

t2 = t2 + day;

t2 = t2 % 7;

res = res + t2;

res = res % 7;

if(y \&gt; 2000)

res = res + 1;

res = res % 7;

return res;

}

char \*getDay(int dd,int mm,int yy){

int day;

if(!(mm\&gt;=1 &amp;&amp; mm\&lt;=12)){

return(&quot;Invalid month value&quot;);

}

if(!(dd\&gt;=1 &amp;&amp; dd\&lt;=getNumberOfDays(mm,yy))){

return(&quot;Invalid date&quot;);

}

if(yy\&gt;=1600){

day = getDayNumber(dd,mm,yy);

day = day%7;

return(getName(day));

}else{

return(&quot;Please give year more than 1600&quot;);

}

}

int checkNote(int dd, int mm){

FILE \*fp;

fp = fopen(&quot;note.dat&quot;,&quot;rb&quot;);

if(fp == NULL){

printf(&quot;Error in Opening the file&quot;);

}

while(fread(&amp;R,sizeof(R),1,fp) == 1){

if(R.dd == dd &amp;&amp; R.mm == mm){

fclose(fp);

return 1;

}

}

fclose(fp);

return 0;

}

void printMonth(int mon,int year,int x,int y){ //prints the month with all days

int nod, day, cnt, d = 1, x1 = x, y1 = y, isNote = 0;

if(!(mon\&gt;=1 &amp;&amp; mon\&lt;=12)){

printf(&quot;INVALID MONTH&quot;);

getch();

return;

}

if(!(year\&gt;=1600)){

printf(&quot;INVALID YEAR&quot;);

getch();

return;

}

gotoxy(20,y);

print\_date(mon,year);

y += 3;

gotoxy(x,y);

printf(&quot;S M T W T F S &quot;);

y++;

nod = getNumberOfDays(mon,year);

day = getDayNumber(d,mon,year);

switch(day){ //locates the starting day in calender

case 0 :

x=x;

cnt=1;

break;

case 1 :

x=x+4;

cnt=2;

break;

case 2 :

x=x+8;

cnt=3;

break;

case 3 :

x=x+12;

cnt=4;

break;

case 4 :

x=x+16;

cnt=5;

break;

case 5 :

x=x+20;

cnt=6;

break;

case 6 :

x=x+24;

cnt=7;

break;

default :

printf(&quot;INVALID DATA FROM THE getOddNumber()MODULE&quot;);

return;

}

gotoxy(x,y);

if(cnt == 1){

SetColor(12);

}

if(checkNote(d,mon)==1){

SetColorAndBackground(15,12);

}

printf(&quot;%02d&quot;,d);

SetColorAndBackground(15,1);

for(d=2;d\&lt;=nod;d++){

if(cnt%7==0){

y++;

cnt=0;

x=x1-4;

}

x = x+4;

cnt++;

gotoxy(x,y);

if(cnt==1){

SetColor(12);

}else{

ClearColor();

}

if(checkNote(d,mon)==1){

SetColorAndBackground(15,12);

}

printf(&quot;%02d&quot;,d);

SetColorAndBackground(15,1);

}

gotoxy(8, y+2);

SetColor(14);

printf(&quot;Press &#39;n&#39; to Next, Press &#39;p&#39; to Previous and &#39;q&#39; to Quit&quot;);

gotoxy(8,y+3);

printf(&quot;Red Background indicates the NOTE, Press &#39;s&#39; to see note: &quot;);

ClearColor();

}

void AddNote(){

FILE \*fp;

fp = fopen(&quot;note.dat&quot;,&quot;ab+&quot;);

system(&quot;cls&quot;);

gotoxy(5,7);

printf(&quot;Enter the date(DD/MM): &quot;);

scanf(&quot;%d%d&quot;,&amp;R.dd, &amp;R.mm);

gotoxy(5,8);

printf(&quot;Enter the Note(50 character max): &quot;);

fflush(stdin);

scanf(&quot;%[^\n]&quot;,R.note);

if(fwrite(&amp;R,sizeof(R),1,fp)){

gotoxy(5,12);

puts(&quot;Note is saved sucessfully&quot;);

fclose(fp);

}else{

gotoxy(5,12);

SetColor(12);

puts(&quot;\aFail to save!!\a&quot;);

ClearColor();

}

gotoxy(5,15);

printf(&quot;Press any key............&quot;);

getch();

fclose(fp);

}

void showNote(int mm){

FILE \*fp;

int i = 0, isFound = 0;

system(&quot;cls&quot;);

fp = fopen(&quot;note.dat&quot;,&quot;rb&quot;);

if(fp == NULL){

printf(&quot;Error in opening the file&quot;);

}

while(fread(&amp;R,sizeof(R),1,fp) == 1){

if(R.mm == mm){

gotoxy(10,5+i);

printf(&quot;Note %d Day = %d: %s&quot;, i+1, R.dd, R.note);

isFound = 1;

i++;

}

}

if(isFound == 0){

gotoxy(10,5);

printf(&quot;This Month contains no note&quot;);

}

gotoxy(10,7+i);

printf(&quot;Press any key to back.......&quot;);

getch();

}

int main(){

ClearConsoleToColors(15, 1);

SetConsoleTitle(&quot;Calender Project - Programming-technique.blogspot.com&quot;);

int choice;

char ch = &#39;a&#39;;

while(1){

system(&quot;cls&quot;);

printf(&quot;1. Find Out the Day\n&quot;);

printf(&quot;2. Print all the day of month\n&quot;);

printf(&quot;3. Add Note\n&quot;);

printf(&quot;4. EXIT\n&quot;);

printf(&quot;ENTER YOUR CHOICE : &quot;);

scanf(&quot;%d&quot;,&amp;choice);

system(&quot;cls&quot;);

switch(choice){

case 1:

printf(&quot;Enter date (DD MM YYYY) : &quot;);

scanf(&quot;%d %d %d&quot;,&amp;date.dd,&amp;date.mm,&amp;date.yy);

printf(&quot;Day is : %s&quot;,getDay(date.dd,date.mm,date.yy));

printf(&quot;\nPress any key to continue......&quot;);

getch();

break;

case 2 :

printf(&quot;Enter month and year (MM YYYY) : &quot;);

scanf(&quot;%d %d&quot;,&amp;date.mm,&amp;date.yy);

system(&quot;cls&quot;);

while(ch!=&#39;q&#39;){

printMonth(date.mm,date.yy,20,5);

ch = getch();

if(ch == &#39;n&#39;){

increase\_month(&amp;date.mm,&amp;date.yy);

system(&quot;cls&quot;);

printMonth(date.mm,date.yy,20,5);

}else if(ch == &#39;p&#39;){

decrease\_month(&amp;date.mm,&amp;date.yy);

system(&quot;cls&quot;);

printMonth(date.mm,date.yy,20,5);

}else if(ch == &#39;s&#39;){

showNote(date.mm);

system(&quot;cls&quot;);

}

}

break;

case 3:

AddNote();

break;

case 4 :

exit(0);

}

}

return 0;

}

**Output:**

[![](RackMultipart20211125-4-qexw1m_html_3dec203d787e038c.png)](https://www.codewithc.com/wp-content/uploads/2014/04/printf-all-days-and-dates-of-a-month.png)
