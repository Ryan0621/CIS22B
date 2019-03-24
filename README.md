# CIS22B
Final Study Guide

# Chapter 7 - Vectors and 2-D Arrays
- Do you know how to define a vector, insert and remove elements from a vector?
- Can you declare a two-dimensional array and pass it to a function? How does it look like in the function header?
- Do you know how to access/update a specific element in a two-dimensional array?
```
#include <iostream>
#include <vector>
using namespace std;


void populate(int array[][3]) {
	for (int i=0; i<3; i++) {
		for (int j=0; j<3; j++) {
			array[i][j] = i+j+1;
		}
	}
}
void modify(int array[][3]) {
	for (int i=0; i<3; i++) {
		for (int j=0; j<3; j++) {
			array[i][j] += 1;
		}
	}
}

int main() {
	// your code goes here
	int array [3][3];
	populate(array);
	modify(array);
	for (int i=0; i<3; i++) {
		for (int j=0; j<3; j++) {
			cout << array[i][j] << " ";
		}
	}
	return 0;
}
```

# Chapter 9 - Pointers
- Do you know how to dynamically allocate and release memory?
```
    char *c = nullptr;
	c = new char;
	*c = 'z';
	cout << c << endl;
	
	int *d = nullptr;
	d = new int;
	*d = 1.1;
	cout << *d;
	return 0;
```

- Do you know how to access a value using a pointer variable?
- Do you know how to pass pointers to functions and return them from functions?

```
int* popu(int *a) {
	for (int i=0; i<5; i++)
		a[i] = i+1;
	int *value;
	value = new int;
	*value = 5;
	return value;
}

int main() {
	// your code goes here
	int *a;
	a = new int[5];
	int *b;
	b = new int;
	b = popu(a);
	
	for (int i=0; i<5; i++)
		cout << *(a+i) << " ";	
	cout << *b;
	return 0;
}
```

- Do you understand how pointers relate to arrays?

# Chapter 10 - C-Strings and String Objects
- How are they similar? 
    > They are a sequence of characters stored in adjacent locations
    > Can access different position of a character using syntax [ ] 

- How are they different?
    > C-str: Has fixed size of an array, Does not track their own size, Terminated by their NULL character
    > String: Flexible size, Able to track size, Enclosed in “_”

- The character testing functions (isdigit, isalpha, islower, isupper, isspace, etc)
- The character conversion functions (tolower, toupper)
- c-string library functions and string object methods

# Chapter 11 - Structures
- How to define a structure
- How to access a structure variable's members
```
struct Student {
int id;
string name;
double gpa;
};

Student oneStudent;
oneStudent.id = 123;
oneStudent.name = "John";
oneStudent.gpa = 3.8;
```
- How to define an array or vector of structures.
```
Student classroom[10];
vector<Student> s(10);
```
# Chapter 13 - Object-oriented programming
- What members are accessible within the class implementation only and which ones are accessible by the objects of that class?
    > implementation: public, protected, private
    > object: public
- How to define a class and its members
```
#include <iostream>
#include <vector>
using namespace std;

class Student {
private:
	int id;
	double gpa;
public:
	string name;
	Student(string s, int n, double d) {
		name = s; 
		id = n;
		gpa = d;
	} 
};

int main() {
	Student student("Ryan", 20361855, 4.0);
	cout << student.name;
	return 0;
}
```
- What is the difference between private, protected and public members of a class in terms of accessibility?
    > public: Can be accessed by functions outside of the class
    > protected / private: Can only be called by or accessed by functions that are members of the class
- inline method definition vs defining methods outside the class specification
    > regular functions – when called, compiler stores return address of call, allocates memory for local variables, etc.
    > inline function – larger executable program, but no function call overhead, hence faster execution
- What is the difference between a class and an object?
    > class : a blueprint consisting of attributes and behavior
    > object : actual instantiation of the blueprint
- Can you implement a class from a UML diagram?
    > UML consists of everything that a class implementation: class name, attributes & their data types, member functions w/ parameter & return data type, constructors, destructors, data-hiding (public, private) https://deanza.instructure.com/courses/7448/files/1411978/download?download_frd=1

# Chapter 14 - Static Member variables and Copy Constructors
- Do you know the difference between a static and a non-static variable of a class?
    > static: one variable shared among all objects of a class
    > non-static: each object of a class keeps a copy of the variable
- Do you know the difference between a static and a non-static member function of a class?
    > static: can be used to access static member variable; can be called before any objects are defined
    > non-static: used to access non-static variable, only can be called after object is defined
```
#include <iostream>
#include <vector>
using namespace std;

class Student {
private:
	int id;
	string name;
	double gpa;
	static int count;
	static void incrCount() {
		count ++;
	}
public:
	Student(string s, int n, double d) {
		name = s; 
		id = n;
		gpa = d;
		incrCount();
		cout << "A new student is created. Current student count is: " << count << endl;
	} 
};
int Student::count = 0;

int main() {
	Student student1("Ryan", 20361855, 4.0);
	Student student2("Bryan", 20362855, 2.0);
	return 0;
}
```
- Do you understand the difference between a copy constructor, a default constructor and other constructors?
    > Copy: Special constructor used when a newly created object is initialized to the data of another object of same class
    > Default: Constructor without parameter / All parameters with default value
```
class X { 
public:   
    X();                       // Default constructor with no arguments   
    X(int = 0);                // Default constructor with one default argument   
    X(int, int , int = 0);     // Constructor 
};
```

# Chapter 15 - Inheritance
- How to define a derived class
```
class Student       // base class
{
    . . .
};

class UnderGrad : public student 
{
    // derived class
    . . .
};
```
- How accessible are the parent's private, protected and public members to the child class
    > Child class can access the parent's protected and public member
- What is an abstract class and how does it relates to creating objects?
    > Abstract class is a class that is specifically designed to be used as a base class and  have no objects. It serves as a basis for derived classes that will have objects
- What is a pure virtual function and what does it mean to a class?
    > A virtual member function that must be overridden in a derived class that has objects
# Chapter 17 - Linked Lists
- Do you understand the purpose of linked list?
    > Can grow and shrink as needed, unlike arrays, which have a fixed size
- Do you understand how to insert a node between two nodes on a linked list?
    > While traversing the linked list, one pointer (nodeptr) to locate the node with data value greater than that of node to be inserted, another pointer (previousNode) to 'trail behind' one node, to point to node before point of insertion
    > After traversing, if it's not the end or beginning of the list, `newNode->next = nodeptr; previousNode->next = newNode;`
- Do you understand how and why you should cleanup memory that you allocated for the list?
    > Prevent memory leak


