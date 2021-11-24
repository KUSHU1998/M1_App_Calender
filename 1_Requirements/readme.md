CALENDAR SYSTEM USING C - By Kushla Devi

**Requirements**

- VS Code
- Laptop with Windows
- C compiler

**Calendars**** -**Calendars have existed for thousands of years and have gone through several reforms until finally arriving at the currently widely used version, known as the Gregorian calendar. It is a solar calendar, meaning that it is based on the Earth&#39;s revolution around the Sun. Despite its seeming simplicity and ease-of-use, the rules which lay the foundation for the Gregorian calendar and its predecessors result in some complications. A year is not an exact integer of days, despite being presented as such. That is why certain years have a &quot;leap day&quot;, an additional day in the year, to compensate for the inaccuracy.

**About Calendar in C:** Basically three operations can be done in this calendar application. To find out the day corresponding to a given date, the date, month and year are asked. You can list the days and dates of any month of any year. For example, entering 04 2014 (April 2014) will give you an output as shown in the screenshot in this post.

You can navigate the months using arrow keys, or press &#39;n&#39; and &#39;p&#39; keys to view the next and previous months respectively. The third feature of this C mini project on Calendar application utilizes file handling. With this feature, you can add important notes with corresponding dates.

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

**Output:**

[![](RackMultipart20211123-4-12a0514_html_3dec203d787e038c.png)](https://www.codewithc.com/wp-content/uploads/2014/04/printf-all-days-and-dates-of-a-month.png)
