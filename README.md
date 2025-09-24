# Week04 Quiz1:

## 1. Requirements:

This program is a system that manages bank account information for three people. Each account contains account number, username, date of birth, and balance information. The account information of three people is stored in the array, and write a code to perform the task by entering your name, deposit and withdrawal selection, and the amount to be deposited and withdrawn.

- Writing code using c++
- Use `BankAccount class` and `Date class` to complete your code. 
- Changing the provided class is not allowed. You can `only use the provided class and the functions defined within it`.
- Use the provided account data as the initial data.
- You need to store the `two given class definitions` in the `BankAccount.h` and `Date.h` files respectively. Store the `function definitions and the main function` in the `main.cpp` file.   
  `(Please submit the above three documents, and if you do not name the main file "main.cpp", the test will not pass and you will receive zero points)`
- Please confirm the containment relationship between classes and ensure reasonable calls between header files.
<br/>

### Account Data:  
```
{1001, Kim, 3/7/2000, 5000}  
{1002, Lee, 5/17/2002, 8000}  
{1003, Park, 20/50/2008, 15000}
```

<br/>

### BankAccount class:
- Complete and use the following class:
```C++
class BankAccount
{
  private:
  	int accountNumber;
  	string userName;
  	Date* BirthDate;
  	int balance;
  
  public:
  	explicit BankAccount(int = 0, string = "", int = 1, int = 1, int = 1900, int = 0);
      // constructure, The provided data is raw data in the format of "account number, user name, month of birth, day of birth, year of birth, and deposit balance"

  	void deposit(int money); // add the value of its parameters to the balance

  	void withdraw(int money); // reduce the value of its parameters from the balance

  	int Check();  // return the value of balance

  	void printAll();  // outputs all information inside

  	string getUserName(); // return userName

  	~BankAccount(); // destructure
};
```
- If the balance is insufficient when withdrawal, handle the error and print out the `"Error: Not enough balance"` message, and then output corresponding account information.
- printAll() will print all information in the format of ` accountNumber, userName, month/day/year, balance `.  
  e.g. `1002, Lee, 5/17/2002, 7500`

<br/>

### Date class
- Complete and use the following class:
```C++
class Date
{
  private:
  	unsigned int month;
  	unsigned int day;
  	unsigned int year;
  
  	unsigned int checkDay(int) const; // verify that if the  input day is correct

  public:
  	static const unsigned int monthsPerYear = 12;

  	explicit Date(int = 1, int = 1, int = 1900);
      // constructure, The provided data is raw data in the format of "month, day, and year".

  	void print() const; // print in the format of `month/day/year`

  	~Date();
};
```
- When the constructor is called, output `"Date object constructor for date " along with the corresponding date`.  
  e.g. `Date object constructor for date 3/7/2000`
- When the destructor is called, output `"Date object destructor for date " along with the corresponding date`.  
  e.g. `Date object destructor for date 3/7/2000`
- If an error occurs while creating a Date class, output the error message and use the default value of `January 1, 1900`.  
   ( When the day is less than 1 or exceeds the maximum number of days in the month, output `"Error: Invalid day for current month and year"`, When the month is less than 1 or more than 12, output `"Error: Month must be 1-12"`. )
- `checkDay(int day)` function is used to verify that if the  input day is correct, return the input day when correct, and throw an exception when incorrect.  
   ( `static const int daysPerMonth[13] = { 0, 31, 28, 31, 30, 31, 30, 31, 31, 30, 31, 30, 31 }`，In a leap year, February has 29 days. )
- Leap year: Years that can be divided by 4 but not by 100, or years that can be divided by 400.
  ```C++
  bool leap;
  if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0))
  leap = true;
  else
  leap = false;
  ```
- `print()`function is used to output data in the format of `month/day/year`.e.g. `5/17/2002`   

<br/>

### Input
- The first line contains a number (int type) representing the number of accounts that are about to be entered.
- Starting from the second line, input the corresponding number of query commands based on the numbers entered in the first line. Format as `Name(string/char[] Type) orderWord(int Type) money(int Type)`, separated by spaces. Each command is followed by a new line until all inputs are complete. Order word `1` for deposit and `2` for withdraw.  
  e.g. `Kim 1 5000`. 

<br/>

### Output  

- The first three lines output the date data generation information corresponding to the three users' accounts.
- Afterwards, output the processed account information based on the previously entered instructions. When an error occurs, output error handling information.
- The last three lines output the corresponding date data deletion information when the data is deleted.

<br/>

### Error handling

- When the day is less than 1 or exceeds the maximum number of days in the month, output `"Error: Invalid day for current month and year"`.
- When the month is less than 1 or more than 12, output `"Error: Month must be 1-12"`.
- When both of the above two problems exist, output error message in order.
- When the input name is not in the list, output `"Error: No such people."`.
- When the order word is not 1 or 2, output `"Error: Invalid keyword". message, and then output corresponding account information`.
- If the balance is insufficient when withdrawal, handle the error and print out the `"Error: Not enough balance" message, and then output corresponding account information`.

<br/>

### Other tips
- When reading part of the input through `cin` and wanting to skip the subsequent part, the cache can be cleared using `cin.ignore(std::numeric_limits< streamsize >::max(), '\n');`.
- If your compiler version does not support the use of `std::numeric_limits`, you can replace it with a sufficiently large number, such as 1024.

<br/>

## 2. Scoring Criteria (5 points in total):

- Uploaded `BankAccount.h`, `Date.h` and `main.cpp` three files with no compilation errors: 1 point
- The cpp file calls two header files and declares the given functions: 2 point
- The result is correct: 2 point

<br/>

## 3 Example(Red font for input, blue font for output):
![image](https://github.com/chyh001228/images/blob/main/w4q1.png)

**Input:**

```
5
Kim 1 5000
Lee 2 500
Park 2 20000
Lee 3 1000
Boob 1 10000
```

**Output:**

```
Date object constructor for date 3/7/2000
Date object constructor for date 5/17/2002
Error: Month must be 1-12
Error: Invalid day for current month and year
Date object constructor for date 1/1/1900
1001, Kim, 3/7/2000, 10000
1002, Lee, 5/17/2002, 7500
Error: Not enough balance
1003, Park, 1/1/1900, 15000
Error: Invalid keyword
1002, Lee, 5/17/2002, 7500
Error: No such people.
Date object destructor for date 1/1/1900
Date object destructor for date 5/17/2002
Date object destructor for date 3/7/2000
```

**Actual results:**  
![image](https://github.com/chyh001228/images/blob/main/w4q1_c.png)

(The deadline is 00:00a.m. on September 28, 2025)

<img src="https://cdn.imweb.me/upload/S201906178853c3e170808/c5d876d707352.jpg" width=30% align=center />
