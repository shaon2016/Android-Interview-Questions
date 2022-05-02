# Android Interview Questions
Here you will find top interview questions. Some questions are very common and they are being asked frequently in every interview.
I will highlight some important topics into this thread. 

# Android Basics


* ***What is Context?***

Interface to global information about an application environment. This is an abstract class whose implementation is provided 
by the Android system. It allows access to application-specific resources and classes, as well as up-calls for application-level 
operations such as launching activities, broadcasting and receiving intents, etc.

Two types of context -> 
1) Application Context 
2) Activity Context.

[See this for more details](https://blog.mindorks.com/understanding-context-in-android-application-330913e32514)


* ***What is Intent? Explain in brief explicit and implicit intent.***

An intent is to perform an action. It is mostly used to start an activity, send broadcast receiver, start services.

1) Explicit Intent: In such a case, intent provides the external class to be invoked.
Explicit intents are used in the application itself wherein one activity can switch to other activity.
Example ```Intent intent = new Intent(this,Target.class);```

3) Implicit Intent: It doesn't specify the component. In such a case, intent provides information on available components provided 
4) by the system that is to be invoked.

Implicit Intents do not directly specify the Android components which should be called, 
it only specifies action to be performed. A Uri can be used with the implicit intent to specify the data type.

```Intent intent = new Intent(ACTION_VIEW,Uri.parse("http://www.google.com"));```

* ***What is content provider?***

Content providers can help an application manage access to data stored by itself, stored by other apps, and provide a way to share data with other apps. They encapsulate the data, and provide mechanisms for defining data security.

* ***The last callback in the lifecycle of an activity is onDestroy(). The system calls this method on your activity as the final signal that your activity instance is being completely removed from the system memory. Usually, the system will call onPause() and onStop() before calling onDestroy(). Describe a scenario, though, where onPause() and onStop() would not be invoked.***

onPause() and onStop() will not be invoked if finish() is called from within the onCreate() method. This might occur, for example, if you detect an error during onCreate() and call finish() as a result. In such a case, though, any cleanup you expected to be done in onPause() and onStop() will not be executed.
Although onDestroy() is the last callback in the lifecycle of an activity, it is worth mentioning that this callback may not always be called and should not be relied upon to destroy resources. It is better have the resources created in onStart() and onResume(), and have them destroyed in onStop() and onPause(), respectively.

* ***What is difference between Serializable and Parcelable ? Which is best approach in Android?***
 
Serializable is a standard Java interface. You simply mark a class Serializable by implementing the interface, and Java will automatically serialize it in certain situations.
Parcelable is an Android specific interface where you implement the serialization yourself. It was created to be far more efficient than Serializable, and to get around some problems with the default Java serialization scheme.

* ***What is the difference between Service and IntentService? How is each used?***

Service is the base class for Android services that can be extended to create any service. A class that directly extends Serviceruns on the main thread so it will block the UI (if there is one) and should therefore either be used only for short tasks or should make use of other threads for longer tasks.
IntentService is a subclass of Service that handles asynchronous requests (expressed as “Intents”) on demand. Clients send requests through startService(Intent) calls. The service is started as needed, handles each Intent in turn using a worker thread, and stops itself when it runs out of work. Writing an IntentService can be quite simple; just extend the IntentServiceclass and override the onHandleIntent(Intent intent) method where you can manage all incoming requests.

* ***What is broadcast receiver?***

A broadcast receiver (receiver) is an Android component which allows you to register for system or application events. All registered receivers for an event are notified by the Android runtime once this event happens.

We can use broadcast receiver to know -> check whether an internet connection is available, what the battery label should be, etc.


* ***Which method is called only once in a fragment life cycle?***

onAttached()

* ***Is it possible to create an activity in Android without a user interface?***

Yes, an activity can be created without any user interface. These activities are treated as abstract activities.

* ***Activity Lifecycle***

OnCreate → Creates the activity
OnStart → User can see the screen
OnResume → When user can interact the screen

onPause → when part of app is visible but in background
onStop → When app is not visible to user
OnDestroy → when activity is destroyed

* ***When should you use a Fragment rather than an Activity?***
        
1) When you have some UI components to be used across various activities
2) When multiple view can be displayed side by side just like viewPager


* ***What is the difference between adding/replacing fragment in backstack?***

The important difference is:
replace removes the existing fragment and adds a new fragment..
but add retains the existing fragments and adds a new fragment that means existing fragment will be active and they wont be in 'paused' state hence when a back button is pressed onCreateView() is not called for the existing fragment(the fragment which was there before new fragment was added).

* ***What is the purpose of addToBackStack() while commiting fragment transaction?

By calling addToBackStack(), the replace transaction is saved to the back stack so the user can reverse the transaction and bring back the previous fragment by pressing the Back button. 
   

# Advance Android

* ***What is ANR in Android? What are the measures you can take to avoid ANR?***

ANR(Application is Not Responding) is a dialog box that appears when the application is not responding. This ANR dialogue is displayed whenever the main thread within an application has been unresponsive for a long time under the following conditions:
1) When there is no response to an input event even after 5 seconds.
2) When a broadcast receiver has not completed its execution within 10 seconds.

Following measures can be taken to avoid ANR:
    • An application should perform lengthy database or networking operations in separate threads to avoid ANR.
    • For background task-intensive applications, you can lessen pressure from the UI thread by using the IntentService.

* ***What are the troubleshooting techniques you can follow if an application is crashing frequently?***

If an Android application is crashing frequently, you can follow the below-given techniques:
Compatibility Check:
It is not possible to test an application for all kinds of devices and operating systems. There might be a possibility that an application is not compatible with your OS.
Memory Management:
    • Some apps run perfectly on one mobile device but might crash on other devices. This is where processing power, memory management, and CPU speed are considered.
    • As there is a limited amount of memory space on mobile devices, you can free up memory space for the application to function properly.
    • If an application is frequently crashing, you can delete the application’s data, which will clear its cache memory and allow some free space on your device and might boost the app’s performance.

* ***What is the function of an intent filter?***

Because every component needs to indicate which intents they can respond to, intent filters are used to filter out intents that these components are willing to receive. One or more intent filters are possible, depending on the services and activities that is going to make use of it.

* ***When should we use serHasFixedSize(true) in Recyclerview?***

If we have a RecyclerView with match_parent as height/width, we should add setHasFixedSize(true) since the size of the RecyclerView itself does not change inserting or deleting items into it.
setHasFixedSize should be false if we have a RecyclerView with wrap_content as height/width because each element inserted by the adapter could change the size of the RecyclerView depending on the items inserted/deleted, so, the size of the RecyclerView will be different each time we add/delete items.
To be more clear, if we use a fixed width/height

```
    <android.support.v7.widget.RecyclerView
    android:id="@+id/my_recycler_view"
    android:layout_width="match_parent"
    android:layout_height="match_parent"/>
```
    
We can use my_recycler_view.setHasFixedSize(true)

Then if we do not use a fixed width/height

```<android.support.v7.widget.RecyclerView
        android:id="@+id/my_recycler_view"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"/> 
```

We should use my_recycler_view.setHasFixedSize(false) since wrap_content for widthor height can change the size of our RecyclerView.
When we talk about RecyclerView setHasFixedSize we are not talking about the quantity of elements inside of it but instead the the size of the View itself.


# Design Pattern

* ***What is MVVM?***

Model-View-ViewModel (MVVM) is a software design pattern that is structured to separate program logic and user interface controls.
The separation of the code in MVVM is divided into View, ViewModel and Model.

1) View is the collection of visible elements, which also receives user input. This includes user interfaces (UI), animations and text. The content of View is not interacted with directly to change what is presented.
2) ViewModel is located between the View and Model layers. This is where the controls for interacting with View are housed, while binding is used to connect the UI elements in View to the controls in ViewModel.
3) Model houses the logic for the program, which is retrieved by the ViewModel upon its own receipt of input from the user through View.

* ***Why you are using MVVM?***

we’re going with MVVM over MVP because Android Architecture Components already has a built-in ViewModel class—no MVVM framework necessary.

1) it separates the logic and view related code. It is more readable and understandable.
2) Improves testability. As view and logic are separate. It is easy to test view and logic
3) Logic and view parts are separate. So we know which part goes where.
4) Collaborative work. As view and logic parts are separate. Team can work each part separately. 

* ***What is the difference between MVVM and MVP?***

The one-to-one relationship exists between the Presenter and the View. Multiple View can be mapped with single ViewModel. The Presenter has knowledge about the View. ViewModel has no reference to the View.


* ***Do you have a problem working with MVVM?***

No I don’t. I have been working on Android development using MVVM pattern almost 5 years. So many support and sample project from google team. I actually love it. 

* ***What is SOLID?***

The SOLID Principles are five principles of Object-Oriented class design. They are a set of rules and best practices to follow while designing a class structure. 
they are:

1) The Single Responsibility Principle 
   A class should do one thing and therefore it should have only a single reason to change.
      
2) The Open-Closed Principle
   Classes should be open for extension and closed to modification.
   Modification means changing the code of an existing class, and extension means adding new functionality.
      
3) The Liskov Substitution Principle
   Subclasses should be substitutable for their base classes.
	 This means that, given that class B is a subclass of class A, we should be able to pass an object of class B to any 
   method that expects an object of class A and the method should not give any weird output in that case.
              
4) The Interface Segregation Principle
   Segregation means keeping things separated, and the Interface Segregation Principle is about separating the interfaces. 
	 The principle states that many client-specific interfaces are better than one 	general-purpose interface. 
   Clients should not be forced to implement a function they do no need.
      
5) The Dependency Inversion Principle
      Our classes should depend upon interfaces or abstract classes instead of concrete classes and functions.

[More details](https://www.freecodecamp.org/news/solid-principles-explained-in-plain-english/)


* ***What does clean code mean to you?***

Clean code means that your code is easy to read, easy to understand, and easy to change. It's as simple as having descriptively named variables, functions, and classes so that as you read, you know what each contains or does without guesswork.

In a nutshell, to create understandable, readable, and testable code that many developers can collaboratively work on.


* ***What is Clean Architecture?***

Clean architecture is a software design philosophy that separates the elements of a design into ring levels. An important goal of clean architecture is to provide developers with a way to organize code in such a way that it encapsulates the business logic but keeps it separate from the delivery mechanism. 

It consists of UI Independence, Data independence, Framework independence, Testable.


# Threading

* ***What is multithreading***

Multithreading is a model of program execution that allows for multiple threads to be created within a process, executing independently but concurrently sharing process resources. Depending on the hardware, threads can run fully parallel if they are distributed to their own CPU core.

* ***What Is Multithreading Used For?***

The main reason for incorporating threads into an application is to improve its performance. Performance can be expressed in multiple ways:
1) A web server will utilize multiple threads to simultaneous process requests for data at the same time.
2) An image analysis algorithm will spawn multiple threads at a time and segment an image into quadrants to apply filtering to the image.
3) A ray-tracing application will launch multiple threads to compute the visual effects while the main GUI thread draws the final results.


# Reactive Programming (RxJava 2)

* ***What is Reactive Programming***

Reactive programming is programming with asynchronous data streams.

* ***Difference between concatMap and flatMap?***

Flatmap converts stream(s) into a single streams without maintaining a order where as concatmap does the same along with maintaining the order

Flatmap example -[[1,2,3],[4,5,6],[7,8,9]] -> [1,4,7,2,5,8,3,6,9]

Concatmap example -[[1,2,3],[4,5,6],[7,8,9]] -> [1,2,3,4,5,6,7,8,9]

* ***When does Observable Start to Emit Items?***

In Observable, there are two types: Cold and Hot Observables. Cold Observables will perform work and subsequently emit items only once is someone has subscribed, whereas Hot Observables will perform work and emit items regardless of observers or not.

* ***How many times can onNext(), onError() and onComplete() be called?***

onNext() can be called from zero to an infinite number of times, onError() can be called at maximum once per stream; similarly onComplete() is called at maximum once per stream.

* ***Define Observable chain***

List of operations or transformations performed in between the source and end subscriber. One of the examples, it to emit User objects, filtering out the admin users and checking for authentication of users, and finally map full name.

* ***What is backpressure?***
Backpressure is the inability of a Subscriber to handle all incoming events in time. In other words Backpressure can occur when the Producer of events is faster than the Consumer. If not handled correctly it can error out a stream.

* ***How to deal with backpressure issues?***

If you thing Backpressure might occur, then Flowable with a correct BackpressureStrategy is the safest choice.


* ***Difference between FlatMap and Map***

1) Map
Map transforms the items emitted by an Observable by applying a function to each item.
2) FlatMap
FlatMap transforms the items emitted by an Observable into Observables.
In your case you need map, since there is only 1 input and 1 output. 
map - Supplied function simply accepts an item and returns an item which will be emitted further (only once) down.
flatMap - Supplied function accepts an item then returns an "Observable", meaning each item of the new "Observable" will be emitted separately further down. 
May be code will clear things up for you:

```
    Observable.just("item1").map(str -> {
        System.out.println("inside the map " + str);
        return str;
    }).subscribe(System.out::println);

    Observable.just("item2").flatMap(str -> {
        System.out.println("inside the flatMap " + str);
        return Observable.just(str + "+", str + "++", str + "+++");
    }).subscribe(System.out::println);

Output:
inside the map item1
item1
inside the flatMap item2
item2+
item2++
item2+++
```

* ***ZIP Operator***

Zip combine the emissions of multiple Observables together via a specified function and emit single items for each combination based on the results of this function.
Zip operator allows us to get the results from multiple observables at a time.

```
Observable.zip(
        getCricketFansObservable(),
        getFootballFansObservable(),
        BiFunction<List<User>, List<User>, List<User>> { cricketFans, footballFans ->
            return@BiFunction filterUserWhoLovesBoth(
                cricketFans,
                footballFans
            )
        }).subscribeOn(Schedulers.io()).observeOn(AndroidSchedulers.mainThread())
        .subscribe(getObserver())
```


# OOP

* ***What is Object Oriented Programming?***

Object-Oriented Programming(OOPs) is a type of programming that is based on objects rather than just functions and procedures. Individual objects are grouped into classes. OOPs implements real-world entities like inheritance, polymorphism, hiding, etc into programming. It also allows binding data and code together.

* ***Why use OOPs?***

1) OOPs allows clarity in programming thereby allowing simplicity in solving complex problems
2) Code can be reused through inheritance thereby reducing redundancy
3) Data and code are bound together by encapsulation
4) OOPs allows data hiding, therefore, private data is kept confidential
5) Problems can be divided into different parts making it simple to solve
6) The concept of polymorphism gives flexibility to the program by allowing the entities to have multiple forms

if you stick to the rules, it makes complex code easier to develop, more relieable, more maintainable, and generally better.

Because OOP insists that you think about what you expose to the outside world, it lets you change the implementation of an object without affecting any other code. (Encapsulation)
Because it allows you to have many different functions, all with the same name, all doing the same job, but on different data. (Polymorphism)
Because it lets you write generic code: which will work with a range of data, so you don't have to write basic stuff over, and over again. (Generics)

There are four major benefits to object-oriented programming:

1) Encapsulation: in OOP, you bundle code into a single unit where you can determine the scope of each piece of data.
2) Abstraction: 
      Abstraction is a process of providing functionality to the users by hiding its implementation details from them. In other words, the user will have just the knowledge of what an entity is doing instead of its internal working.
      Data abstraction is the process of hiding certain details and showing only essential information to the user.
Abstraction can be achieved with either abstract classes or interfaces
      We can achieve 100% abstraction using interfaces.
3) Inheritance: because a class can inherit attributes and behaviors from another class, you are able to reuse more code.
4) Polymorphism: one class can be used to create many objects, all from the same flexible piece of code.
The word polymorphism means having many forms.
Real-life Illustration: Polymorphism
A person at the same time can have different characteristics. Like a man at the same time is a father, a husband, an employee. So the same person possesses different behavior in different situations. This is called polymorphism. 
Method Overloading: When there are multiple functions with the same name but different parameters then these functions are said to be overloaded.

Method Overriding: When derived class has a definition for a method of the base class.

* ***When to use abstract classes and abstract methods with an example***

There are situations in which we will want to define a superclass that declares the structure of a given abstraction without providing a complete implementation of every method. That is, sometimes we will want to create a superclass that only defines a generalization form that will be shared by all of its subclasses, leaving it to each subclass to fill in the details.
Consider a classic “shape” example, perhaps used in a computer-aided design system or game simulation. The base type is “shape” and each shape has a color, size, and so on. From this, specific types of shapes are derived(inherited)-circle, square, triangle, and so on — each of which may have additional characteristics and behaviors. For example, certain shapes can be flipped. Some behaviors may be different, such as when you want to calculate the area of a shape. The type hierarchy embodies both the similarities and differences between the shapes.
 

* ***Difference between Structs and Classes***

1) Struct are value types whereas Classes are reference types.
2) Structs are stored on the stack whereas Classes are stored on the heap.
3) Value types hold their value in memory where they are declared, but a reference type holds a reference to an object in memory.
4) Value types are destroyed immediately after the scope is lost whereas reference type only destroys the variable after the scope is lost. The object is later destroyed by the garbage collector.
5) When you copy a struct into another struct, a new copy of that struct gets created. The modified struct won't affect the value of the other struct.
6) When you copy a class into another class, it only copies the reference variable.
7) Both reference variables point to the same object on the heap. Changes done to one variable will affect the other reference variable.
8) Structs can not have destructors, but classes can have destructors.
  
* ***Can you call the base class method without creating an instance?***

Yes, you can call the base class without instantiating it if:
1) It is a static method
2) The base class is inherited by some other subclass
    
* ***What are the limitations of inheritance?***

1) Increases the time and effort required to execute a program as it requires jumping back and forth between different classes
2) The parent class and the child class get tightly coupled
3) Any modifications to the program would require changes both in the parent as well as the child class
5) Can not do multiple inheritance using class

* ***What is polymorphism?***

Polymorphism refers to the ability to exist in multiple forms. Multiple definitions can be given to a single interface. For example, if you have a class named Vehicle, it can have a method named speed but you cannot define it because different vehicles have different speed. This method will be defined in the subclasses with different definitions for different vehicles.

* ***What is static polymorphism?***

Static polymorphism (static binding) is a kind of polymorphism that occurs at compile time. An example of compile-time polymorphism is method overloading.

* ***What is dynamic polymorphism?***

Runtime polymorphism or dynamic polymorphism (dynamic binding) is a type of polymorphism which is resolved during runtime. An example of runtime polymorphism is method overriding.

* ***What is method overloading?***

Method overloading is a feature of OOPs which makes it possible to give the same name to more than one methods within a class if the arguments passed differ.

* ***What is method overriding?***

Method overriding is a feature of OOPs by which the child class or the subclass can redefine methods present in the base class or parent class. Here, the method that is overridden has the same name as well as the signature meaning the arguments passed and the return type.

* ***What is data abstraction?***

Data abstraction is a very important feature of OOPs that allows displaying only the important information and hiding the implementation details. For example, while riding a bike, you know that if you raise the accelerator, the speed will increase, but you don’t know how it actually happens. This is data abstraction as the implementation details are hidden from the rider.

* ***What is Garbage Collection(GC)?***

GC is an implementation of automatic memory management. The Garbage collector frees up space occupied by objects that are no longer in existence.


# Kotlin

* ***What are advantages of Kotlin over Java***

1) one of the biggest conveniences with using Kotlin is that it's compatible with Java!
With all its tools and frameworks, you can just add these to your Kotlin projects — nice and easy —with no need to change the entire project in Java.
2) More readable and need to write less code than java

3) Kotlin is null-safe by default. It does not allow variables to be assigned with a null value. But in Java, we can assign null values to variables and, it may lead to null pointer exception that may crash the application.

* ***Why did you choose a specific coding language, certain framework or technology?***

1) One of the biggest conveniences with using Kotlin is that it's compatible with Java!
With all its tools and frameworks, you can just add these to your Kotlin projects — nice and easy —with no need to change the entire project in Java.
2) More readable and need to write less code than java
3) Kotlin is null-safe by default. It does not allow variables to be assigned with a null value. But in Java, we can assign null values to variables and, it may lead to null pointer exception that may crash the application.


# Data Structure

* ***Hash functions***

Hashing is the process of converting an input of any length into a fixed size string of text using a mathematical function. Any text can be converted into an array of numbers and letters through an algorithm. The message to be hashed is called input, the algorithm is to do so is called hash function and the output is called hash value.









