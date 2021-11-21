## Introduction to OOPS  

### Principles of Object Oriented Programming

1. Abstraction
2. Encapsulation (Data hiding)
3. Inheritance
4. Polymorphism

<pre>
- <strong>Abstraction</strong> is hiding the implementation details of a class. When we dont know the internal details. 
   for example -> take a TV, we don't want to know how it works, we just want to know that it is a TV. There are buttons(functions) present in the TV. We just press that button and it works.
   Without knowing how the cout function is working, we just use it i.e a clear example of Abstraction. 

- <strong>Encapsulation</strong> is the bundling of data so that users can't access raw data just operate on functions to avoid mishandling(not security). 
   for example -> You went through bank, you will take a withdrawal slip(function) not directly go to the locker and take your cash. 
   We don't want to modify the value thats why we bundle the data. 

- <strong>Inheritance</strong> is the process of creating a new class that inherits all the properties and methods from another class.
   for example -> BMW is a car, TATA is a car, Toyota is a car, Honda is a car.

- <strong>Polymorphism</strong> is the ability of an object to take on many forms.
   for example -> I am driving a car, (no matter which brand) I can drive any car if i know the basic principles.
                  a man at the same time is a father, a husband, an employee. So the same person posses different behavior in different situations.
   With the help of inheritance, we achieve polymorphism.
</pre>

********************************************************************************************************************************************************************

####  What is a Class? (User-defined data type)
- A class is a blueprint for creating objects. A class is a collection of properties and methods.

   Suppose in a college there a students belong to varioous departments like Computer Science, Electronics, Mechanical, etc.
   Here each departments represents a class. On the broader side every student is human being which again belong to a class. 

   Therefore student is an object and human being is a class.

####  What is a Object?
- An object is a real world entity. An object is an instance of a class.


********************************************************************************************************************************************************************

 For accessing the members of a class we use dot operator. 

  Below is the small example 

```cpp
   class Rectangle{
      public: 
       int length;
       int breadth;

       int area(){
              return length*breadth;
       }

       int perimeter(){
              return 2 * (length + breadth);
       } 
   };

   int main()
   {
       Rectangle a, b;   // memory allocated in stack 

       a.length = 10;
       a.breadth = 12;   //dot operators or accessing the members of a class

       Rectangle *p = &a;  //memory allocated in heap
       
       return 0;
   }
```


###  What is constructor? 
- A constructor is a special type of member function of a class which initializes objects of a class. Constructor is automatically called when object create. 
   It is special member function of the class because it does not have any return type.

    #### Types of constructors:

    1. Default constructor -> It is a constructor which does not have any parameter. It is also a default constructor.

    2. Parameterized constructor -> It is a constructor which has parameters. 
       ```cpp
        Rectangle(int l, int b)   //if the class members name and parameters name are same then you can access the class member by this
        {
             length = l;
             breadth = b;
        }  //we can also use default values for the parameters.
       ```

    3. Copy constructor -> It is a constructor which takes another object as a parameter.
       ```cpp
         Rectangle(Rectangle &r)
         {
              length = r.length;
              breadth = r.breadth;
         } 
       ```  

        The advantage of user defined copy constructor over default copy constructor is that default copy constructor creates a shallow copy i.e both the objects 
        point to the same memory location. to make a deep copy we need to use our copy constructor. In this both variables are pointing to different memory location
        but the value are same.
        Careful with arrays or anything you are creating by pointers.
<pre>
- <strong>Mutators</strong> are functions which change the value of a class member.  (set length, setbreadth)   //modifying
   <strong>Accessors</strong> are functions which return the value of a class member. (get length, get breadth)  //reading
   <strong>Facilitators</strong> are functions which perform some operation on the class member. (int area(), int perimeter())
   <strong>Enquiry</strong> are functions which basically tells us it is true or false. (isEmpty(), isFull(), isSquare())
   <strong>Destructors</strong> are functions which destroy the object. (delete, delete[] )
</pre>

- <strong>Scope resolution operator</strong> : the scope of the function is within a class. For example you declare a function perimeter inside a class but you didn't write its body.
   So if you want to write the body or define it outside the class, you need to use scope resolution operator.

   for example: 
 ```cpp
   class Rectangle{
      public: 
       int length;
       int breadth;

       int area(){
              return length*breadth;
       }

       //all the constructors 

       int perimeter();
   };
 
   int Rectangle::perimeter(){                //format -> data type class name :: function name (:: == scope resolution operator)
              return 2 * (length + breadth);
   }
   ```
   
   There is seperate machine code executed for scope resolution operator and the function body. Otherwise all the machine code will be in the main body.
   But in case of scope resolution operator, the machine code is seperate. return hoga main me wo code wha se execute hoke. 
<pre>
-  <strong>Inline functions</strong>: The functions which expand in the same line where they are called i.e there is no seperate block. If we defined a function within a class, it is automatically inlined function. For another we can write inline in front of fnction name to make it inline. Then the machine code will be in the main function.
</pre>

- Difference between Struct and Class:
   1. In Struct, everyhting is public by default.
   2. In Class, we need to specify whether public or private. (only this much difference)
   3. In C, you can't write functions inside Struct but you can write in cpp.

********************************************************************************************************************************************************************

### Operator Overloading

   CPP has the ability to provide the operators with a special meaning for a data type, this ability is known as operator overloading.
   For our own data types, we can overload the operators. 

   for example: we need to add two complex numbers i.e their real and imaginary part. 
   ```cpp
   class Complex{
      private: 
         int real;
         int imag;

      public:
        Complex(int real = 0, int imag = 0)
        {
               this->real = real;
               this->imag = imag;
        }
        
        Complex add(Complex x)
        {
            Complex temp;

            temp.real = this->real + x.real;
            temp.imag = this->imag + x.imag;

            return temp;
        }
   };

   int main()
   {
        Complex a(10, 20);
        Complex b(30, 40);

        Complex c = a.add(b);
        
        return 0;
   }
   ```

   Now how to make this function overloading (add one) we  can change the function name of add() to operator+. 
   Then in the main body we can write a.operator+(b) and it will work. or we can simple write

   ``` Complex c = a + b; //this is  called as operator overloading. ```
        
### <strong>Friend Operator Overloading</strong> 
   In this a third person will add values of two person, In above we are addding c2 to c1 or c1 to c2. But here, we can pass both as parameters and return the value in c3. We can use private members of a class in friend function.
   ```cpp
   class Complex{
    public: 
       int real;
       int imag;

       Complex(int real = 0, int imag = 0)
       {
            this->real = real;
            this->imag = imag;
       }

       friend Complex operator+(Complex c1, Complex c2);
   };

   Complex operator+(Complex c1, Complex c2)
   {
      Complex c3;

      c3.real = c1.real + c2.real;
      c3.imag = c1.imag + c2.imag;

      return c3;
   }

   int main()
   {
      Complex c1(7,3);
      Complex c2(3,4);

      Complex c3 = c1 + c2;         // or operator+(c1, c2)
      
      cout << c3.real << " + " << c3.imag << "i" << endl;

      return 0;
   }
   ```

#### In this case no scope resolution operator is needed. 

### Insertion Operation Overloading
   ```cpp
   class Complex{
      private: 
         int real;
         int imag;

      public:
         Complex(int real = 0, int imag = 0)
         {
                this->real = real;
                this->imag = imag;
         }
   
         friend ostream& operator<<(ostream &out, Complex c);
   };

   ostream& operator<<(ostream &out, Complex c)
   {
      out << c.real << " + " << c.imag << "i";

      return out;
   }

   int main()
   {
      Complex c1(7,3);

      cout << c1 << endl;   //operator<<(cout, c1)

      return 0;
   }
   ```

<pre>
   Note: if we use void instead of ostream&(line no 246 and line no 249) then cout << c1; will work. 
         cout << c1 << endl; will not work. 

         As in case of ostream in cout << c1 << endl; operator<<(cout, c1) will return another cout which will interact with endl.
         but in case of void function it will return nothing. Therefore an error will come. That's why it is healthier to use ostream type instead of void type.
</pre>
*******************************************************************************************************************************************************************

## Inheritance 
   The process of creating a new class that inherits all the properties and methods from another class. So that we dont have to write the same code again and again. It can be reused.

   ```cpp
   class Base{
       public: 
         int x;

        public:
         void display(){
            cout << x << endl;
         }
   };

   class Derived: public Base{
      private: 
         int y;

      public:
        void show(){
           cout << y << x << endl;
        }
   };
   ```
<pre>
- Here Derived class inherits all the properties and methods of Base class. So we can use the properties and methods of Base class in Derived class.
- We can't access the private members of Base class in Derived class. We need to use mutators. 

- If we make constructors in Base and Derived class, and then make the object of Derived class, then the object of Derived class will call the defualt constructor(always) of 
   Base class and then its constructor. Calling and executing are different things.
 </pre>

   ```cpp
   class Base{
       public:
         Base(){
            cout << "Base constructor called" << endl;
         }

         Base(int x){
            cout << x << endl;
         }
   };

   class Derived: public Base{
      public:
         Derived(){
            cout << "Derived constructor called" << endl;
         }

         Derived(int a){
            cout << a << endl;
         }
   };

   int main()
   {
      Derived d;      // Output will give Base constructor called 
                             //           Derived constructor called.

      Derived d1(10);  // First it will call default constructor of Base class and then it will call parameterised constructor of Derived class.
      return 0;
   }
   ```

- Then how to call parameterised constructor of Base class. There is a special constructor called conversion constructor. 

   ```cpp
   Derived(int a, int x): Base(x){
      cout << a << endl;
   }

   Derived d1(10, 20);   // Output will be 20 and 10.
   ```

### isA or hasA 
   
   ```cpp
   class Rectangle{};

   class Square: public Rectangle{}; // Square is a Rectangle.

   class Table{
      public:
       Rectangle a;  // Table has a Rectangle.
   };
   ```

### Access Specifiers --- (public, private and protected).
<pre>
   You can not access members of private and protected in main function. But in case of child class, you can access members of public as well as protected. 

   Take an example of Car(JC). Suppose you(MyCar) inherited the design from JC, So JC gives you the design of MyCar, you can add features to it, modify it but you can 
   modify to an extent only as JC has told you not to change some parts of the design. So you have acccess of public and protected members of JC. 
   If you sell MyCar to a customer, then he can modify it but to a certain extent as he/she has the permission of public parts of MyCar or JC.
</pre>
###  Type of Inheritance
<pre>
1. Simple/Single Level inheritance

   Rectangle <- Cuboid

2. Hierachical Inheritance

         <- Car1
    Car  <- Car2
         <- Car3

3. Multi Level Inheritance

    point <- circle <- Cylinder

4. Multiple Inheritance   (not possible in Java)
   
   Camera       

   Phone          <- Smartphone

   Media player

5. Hierachical Multiple Inheritance

   Camera       

   Phone          <- Smartphone  <- Tablet

   Media player

   Note: Tablet has all the features of Camera Phone and Media Player. This means it can access its parent's parent's class. This is also called multipath inheritance.

   To remove multipath inheritance we can use virtual base classes.

   class A{};

   class B : virtual public A{};
   class C : virtual public A{};

   class D : public B, public C{};

   You can't access members and methods of A in D class i.e we have remove ambiguity. 
</pre>

### Ways of Inheritance

   ```cpp
   class A { 
      public: 
         Something;

      private:
         Something;
      
      protected: 
         Something;
   };

   class B: public/private/protected A{};
   ```
<pre>
   Suppose you inherit B from a class A publically then all its members will remain same i.e 
                   public A = public B 
                   private A = private B
                   protected A = protected B

   But when you inherit from class A protectedly then nothing will be public in the class B i.e 
                  public A = protected B
                  private A = private B
                  protected A = protected B

   if you inherit privately then 
                  public A = private B
                  private A = private B
                  protected A = private B
   </pre>
         
   This is a very special feature given in cpp which is not presented in Java. As suppose you inherit Class C from class B (private from class A)
   then you can't access members of class B as all the members are private. 

   ### Generalisation Vs Specialisation 
<pre>
       Rectangle <- Cuboid // Basically Cuboid is a Specialisation of Rectangle. Both exist in real world. 
       Innova <- Fortuner // Fortuner is a specialisation of Innova with more added features. Both exist in real world.    

       But in case of Shapes 

              <- circle
              <- Cylinder
       Shape  <- Rectangle
              <- Square
              <- Triangle

              Here Circle, Cylinder, Rectangle, Square and Triangle are inherited from Shape. But does Shape really exist? Or it is a virtual term. 
              It is a general term. It is not a real term. So this is called generalisation. We have generalised all the shapes into one Shape class.(to bring
              them into a particular platform) 
              But we have not done any specialisation. 

      Another example of generalisation

            <- Toyota
            <- Honda
            <- Maruti
       Car  <- Hyundai
            <- Ford
            <- Honda     

      Notice in generalisation, all the derived classes are existing in real world, but we have just given them common terms and give them a common class i.e Bottom to 
      Up approach.
      In case of specialisation, there is first parent class(Innova) and then we add features make it specialised to a different class(fortuner). Top-Down approach.
</pre>
- <strong>The purpose of generalisation is to achieve polymorphism. (Generalised term -> Car but there are different brands, different design etc.)</strong>
- <strong>The purpose of specialisation is to achieve share its features to its child classes i.e inheritance.</strong>
                                 
### Base Class pointer Derived Class Object

   <strong>In Cpp it is possible we can assign a pointer of a base class to the derived class object i.e </strong>
    
   ```cpp
    class Base{
        public:
          somethingofBaseClass();
    };

    class Derived{
         public:
           somethingofDerivedClass();
    };

    int main()
    {
        Base* b = new Derived();      

        b->somethingofBaseClass();   //This is valid
        b->somethingofDerivedClass(); //This is not valid
        return 0;

        // or you can also write 
        Derived a;
        Base* b = &a; 

        b->somethingofBaseClass();   //This is valid
        b->somethingofDerivedClass(); //This is not valid

        return 0;
    }  
   ``` 
   
  
-  Yes it is possible but we can only access to the member and functions of base class only. You can have a base class pointer and have derived class object But
   you can't call the derived class functions. 
   Suppose you derive an advanced car from basic car and then 
<pre>

                                       BasicCar* Car = new AdvancedCar(); 
</pre>

-  So is the advanced Car a basic car? Yes it is. As it has inherited but can you call the advanced car functions as well? No. You can't. 

-  But what if you take a derived class pointer and point it towards the base class object?
   No you can't. As the basic car can't performs the advanced car functions. 
