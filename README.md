# android_arch_comp

This simple Android app showcases how you might use a ViewModel 
and LiveData in your apps. You can get the article that accompanies
this project on [medium](https://proandroiddev.com/introduction-to-android-architecture-components-cab33baa65f6) 
or [developerlife.com](https://developerlife.com/2017/12/07/introduction-to-android-architecture-components/).

The sample just has 1 Java file — MainActivity.java. 
This Activity loads its state from a StateViewModel, which 
contains two pieces of data.

*Data # 1* - There’s a UUID String that is generate the first 
time this StateViewModel is created and this is displayed 
in the UI. This String does not change for the lifetime of 
the Activity. It is stable across configuration changes. 
So as you rotate the screen, and the Activity is destroyed 
and then recreated (but not finished), the same UUID 
String will be displayed in the UI. When you finish the Activity 
by pressing the back button, or by going to the task 
switcher and swiping the Activity away, then the 
ViewModel will be destroyed and onCleared() will be called.

*Data # 2* - The ViewModel also creates a ScheduledExecutor that 
runs a simple task every second. This task simply updates a 
counter, and it generates a log message (“tick”, or “tock”). 
This Executor also sets the value of this counter in 
a CounterLiveData object. The UI actually subscribes to 
this LiveData object and when it changes the UI gets updated with 
the current count. This too is stable across 
configuration changes. When the Activity is finally 
finished, the onCleared() method actually shuts the 
executor down. Also, you have to be mindful of which thread 
the CounterLiveData’s value is set.