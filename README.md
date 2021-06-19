# Cpp-snippets-Design-patterns
In this Repository, there are design patterns and explanation when to use the patterns.

### Skip Guard Plan
We needs to skip over a section of code when certain conditions arise. For example, you may need to skip over a computation when it would result in an attempt to divide by zero:
```C++
if (Count > 0)
   {
   Average = Total / Count;
   cout << "Average: " << Average << endl;
   }
else
   cout << "No data.  The average cannot be computed." << endl;
```
### Count-Controlled Loop Plan
This is used to read in and process a sequence of data items when you know in advance the number of items to be read. The outline looks like the following. Of course, in a real program one would add messages to the user, code for the Process function, etc.

```C++
int k;
Get the Count of how many data items should be processed;
for (k = 0; k < Count; k++)
   {
   Read one data item into Item;
   Process(Item);
   }
```
### Input Checking Plan
This plan forces the user to enter an acceptable data item. For instance, the acceptable items might be Y, y, N, and n. The Unacceptable function shown below might, of course, be replaced by a simple condition. There is no need to write a function here unless the algorithm for determining unacceptable items is fairly complex.

```C++
cout << "Enter an item: ";
cin >> Item;
while (Unacceptable(Item))
   {
   cout << "Re-enter: ";
   cin >> Item;
   }
```
### Sentinel-Controlled Loop Plan
Here the idea is to enter a special item (the sentinel) to indicate end of the sequence of data items to be processed. The sentinel itself is not one of the data items. One might, for example, have data consisting of a string of positive integers and use 0 to signal the end of the data. Or, one might tell the user to press CTRL z to indicate the end of the data. (In Linux one uses CTRL d to end data input, as CTRL z is used to suspend the current process.) This pattern uses EOF (end of file) as a sentinel. The outline is as follows:

```C++
cin >> Item;
while (Item != Sentinel)
   {
   Process(Item);
   cin >> Item;
   }
   ```
As an example, let's write out more detail of how to use EOF as a sentinel. Suppose we want to enter and process a sequence of integers, with CTRL z used to indicate the end of data entry. Then we would use something like this:

```C++
int Item;
cin >> Item;
while (! cin.fail())
   {
   Process(Item);
   cin >> Item;
   }
   ```
The fail function returns true whenever the previous stream operation failed to input an acceptable value. The usual reasons for such failure are that the user pressed CTRL z or that the user entered something (such as abcd) that could not be interpreted as an integer. Although the code shown above reads data from the keyboard, it could easily be adapted to read the data from a file.




### Do a Problem Until the User Wants to Quit
Often you want to allow the user to do some task repeatedly. A simple way to allow this is to ask the user whether or not to do another of whatever the task at hand might be.

```C++
char Reply;
do
   {
   OneProblem();
   cout << "Do another (y/n)? ";
   cin >> Reply;
   }
while (Reply == 'y');
```
### Menu-Driven Plan
This is similar to the previous plan, but adds a menu that is printed to show the user possible commands, here assumed to be the letters a, b, c, and q. The letter q is used as the signal that the user wants to quit. Of course, you can use integers or whatever is convenient. After getting the user's choice the plan picks out the proper task to execute. Then, as long as the choice is not to quit, loop around and present the menu again, etc.

```C++
do
   {
   PrintMenu();
   cin >> Choice;
   if (Choice == 'a')
      DoA();
   else if (Choice == 'b')
      DoB();
   else if (Choice == 'c')
      DoC();
   else if (Choice != 'q')
      cout << "Invalid choice" << endl;
   }
while (Choice != 'q');
```
### Adding a Counter to a Sentinel-Controlled While Loop
We have already seen how to create a sentinel-controlled while loop. This type of loop is used to read in data until the sentinel is reached. Often we want to count the number of data items read in (not including the sentinel itself). All you need is an integer Count variable that is initialized to zero and incremented each time a new data item is obtained. Here is how this is done:

```C++
int Count;
Count = 0;
cin >> Item;
while (Item != Sentinel)
   {
   Count++;
   Process(Item);
   cin >> Item;
   }
```
### Adding a Running Total to a Sentinel-Controlled While Loop
We can also add a running total to a sentinel-controlled while loop. The following example finds the total of all of the data items entered. Of course, the data items must be of a type that can be added, perhaps integers or floats, and the variable Total must have the same type. This example assumes that finding the total is the only processing that is needed on the data items.

```C++
Total = 0;
cin >> Item;
while (Item != Sentinel)
   {
   Total = Total + Item;
   cin >> Item;
   }
```
### Finding an Average in a Sentinel-Controlled While Loop
Since we know how to total and count the data items read in by a sentinel-controlled while loop, we can now easily find the average of these data items.

```C++
int Count;
Count = 0;
Total = 0;
cin >> Item;
while (Item != Sentinel)
   {
   Count++;
   Total = Total + Item;
   cin >> Item;
   }

if (Count > 0)
   {                                                                           
   Average = Total / Count;                                                    
   cout << "Average: " << Average << endl;                   
   }                                                                           
else                                                                           
   cout << "No data.  The average cannot be computed." << endl;    
```
