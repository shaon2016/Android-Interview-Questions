# Android Interview Questions
Here you will find top interview questions I have faced during interviews. I have interviewed in many companies. 
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
