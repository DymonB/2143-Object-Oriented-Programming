 H01 - Commenting Code
Je Vonte Browne
Description:
This program implements a list data structure that links together nodes of integers. 

### Files

|   #   | File     | Description                      |
| :---: | -------- | -------------------------------- |
|   1   | main.cpp | Main driver of my list program . |


// Author:        Je Vonte Dymon Browne
// Email:         Dymon.browne@hotmail.com
// Label:         01-H01
// Title:         Linked List Class
// Course:        CMPS 2134
// Semester:      Fall 2020

// Description:
//       This program implements a class that allows a linked list to be used just like 
//       an array. It overloads the "[]" (square brackets) to simulate accessing seperate 
//       array elements, but really it traverses the list to find the specified node using
//       an index value. It also overloads the "+" and "-" signs allowing a user to "add"
//       or "push" items onto the end of the list, as well as "pop" items off the end of our 
//       array. This class is not meant to replace the STL vector library, its simply a project
//       to introduce the beginnings of creating complex / abstract data types. 
//       
// Usage: 
//      - $ ./main filename
//      - This will read in a file containing whatever values to be read into our list/array. 
//      
// Files:            
//      main.cpp    : driver program 
//      list.h      : header file with list defintion
//      list.cpp    : list implementation


#include <iostream>

using namespace std;

int A[100];                         //Size of the Array 100 integers

struct Node                         // Data Variable for node
{
    int x;                         // initialize x as an integer
    Node *next;                    // next address
    Node()
    {
        x = -1;
        next = NULL;
    }
    Node(int n)
    {
        x = n;                    
        next = NULL;
    }
};

/**
 * Class Name List
 * 
 * Description:
 *      This program implements a class that allows a linked list to be used just like an array
 * 
 * Public Methods:
 *     void 
 * 
 * Private Methods:
 *      int : Size
 *      
 */
class List                          // Class name
{                                    
  private:                          // A list of Private methods
    Node *Head;                     // pointer variable named Head
    Node *Tail;                     // pointer variable named Tail
    int Size;                       // initializied size as integer

  public:                           // A list of public methods
                                    // with return types
    List()
    {
        Head = Tail = NULL;
        Size = 0;                  // Set size to 0
    }
      /**
     * Public : Push
     * 
     * Description:
     *      allocate new memory and init node in list
     * 
     * Returns:
     *      nothing
     */
    void Push(int val)            
    {
        // allocate new memory and init node
        Node *Temp = new Node(val);

        if (!Head && !Tail)
        {
            Head = Tail = Temp;
        }
        else
        {
            Tail->next = Temp;
            Tail = Temp;
        }
        Size++;
    }
      /**
     * Public : Insert
     * 
     * Description:
     *     allocate new memory and figure out where it goes in list
     * 
     * Params:
     *      int*    :  array of integers
     *    
     * 
     * Returns:
     *      nothing
     */
    void Insert(int val)
    {
        // allocate new memory and init node
        Node *Temp = new Node(val);

        // figure out where it goes in the list

        Temp->next = Head;
        Head = Temp;
        if (!Tail)
        {
            Tail = Head;
        }
        Size++;
    }
         /**
     * Public : PrintTail
     * 
     * Description:
     *      Prints Tail list.
     * 
     * Params:
     *    void  prints tail
     * 
     * Returns:
     *      List*   : tail
     */
    void PrintTail()
    {
        cout << Tail->x << endl;
    }
         /**
     * Public : Print
     * 
     * Description:
     *      prints all the values in list.
     * 
     * Params:
     *      string    :  list of integers
     *   
     * 
     * Returns:
     *      List*   : a pointer to a linked list of integers.
     */
    string Print()
    {
        Node *Temp = Head;
        string list;

        while (Temp != NULL)
        {
            list += to_string(Temp->x) + "->";
            Temp = Temp->next;
        }

        return list;
    }
         /**
     * Public : Pop
     * 
     * Description:
     *      remove from list.
     * 
     * Params:
     *      int*    :  array of integers
     *      
     * Returns:
     *      List*   : remaining linked list of integers.
     */
    // not implemented 
    int Pop()
    {
        Size--;
        return 0; 
    }

    List operator+(const List &Rhs)
    {
        // Create a new list that will contain both when done
        List NewList;

        // Get a reference to beginning of local list
        Node *Temp = Head;

        // Loop through local list and Push values onto new list
        while (Temp != NULL)
        {
            NewList.Push(Temp->x);
            Temp = Temp->next;
        }

        // Get a reference to head of Rhs
        Temp = Rhs.Head;

        // Same as above, loop and push
        while (Temp != NULL)
        {
            NewList.Push(Temp->x);
            Temp = Temp->next;
        }

        // Return new concatenated version of lists
        return NewList;
    }

    // Implementation of [] operator.  This function returns an
    // int value as if the list were an array.
    int operator[](int index)
    {
        Node *Temp = Head;

        if (index >= Size)
        {
            cout << "Index out of bounds, exiting";
            exit(0);
        }
        else
        {

            for (int i = 0; i < index; i++)
            {
                Temp = Temp->next;
            }
            return Temp->x;
        }
    }

    friend ostream &operator<<(ostream &os, List L)
    {
        os << L.Print();
        return os;
    }
};

int main(int argc, char **argv)       // Main Driver 
{
    List L1;
    List L2;

    for (int i = 0; i < 25; i++)
    {
        L1.Push(i);
    }

    for (int i = 50; i < 100; i++)
    {
        L2.Push(i);
    }

    //cout << L1 << endl;
    L1.PrintTail();                 // Print tail in L1
    L2.PrintTail();                 // Print in L2

    List L3 = L1 + L2;              // Add L1 and L2, store in L3
    cout << L3 << endl;             // Print L3

    cout << L3[5] << endl;
    return 0;
}
