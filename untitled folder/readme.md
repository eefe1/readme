

MVC

MVC is a part of architectural patterns, which has an important place in Software Engineering. The MVC pattern consists of 3 layers and the layers work independently (without affecting each other). For this reason, it is mostly preferred in large-scale projects to ensure the management and control of the projects more easily. In projects developed with MVC, many people can easily work simultaneously according to the details of the project.

Model
The model is the section where the business logic of the project is created in MVC. Along with business logic, validation and data access operations are also performed in this section.

View
The view is the section where the interfaces of the project are created in MVC. In this section, there are HTML files of the project that will be presented to the users. File extensions can also change according to the software languages in which the project is developed. Another point to be considered according to the size of the projects is the folder.

Controller
The controller is the part in MVC that controls the internal processes of the project. In this section, the connection between View and Model is established. Requests from users are evaluated in Controllers, which actions will be taken according to the details of the request and which View will be returned to the user (response).

Life Cycle of MVC 

 
MVP

The MVP pattern instead considers the View to be both the XML and Activity combined and the View component can be either the Activity class itself or a separate component that interacts with the UI elements in said activity, and should strictly be used for this purpose with minimal logic.
The logic is thus handled in a new component known as the Presenter which acts as a bridge between the View and the Model. The Presenter also decides what happens when a user interacts with the view, such as clicking a button, and thus, would have a method to handle each possible case.
The Model acts as a provider of data and is responsible for communicating with both the network and the local database.

This architecture has it so the Presenter knows of both the View and the Model but those components don’t know of any other component in the architecture, thus the Presenter handles all of the communication between the components.

 

MVP has a problem though, and that is the Presenter’s life is coupled to the Activity’s. This creates an opportunity for the activity to get leaked when the Presenter performs long-running tasks that get interrupted when the activity gets destroyed, like through configuration changes (e.g. screen rotation) or the system’s natural processes.

And while the performance overhead brought about by this isn’t so bad in most cases, it also does create an opportunity for crashing your app as the View will try to interact with an activity that no longer exists. While there are solutions to this problem, it carries the trouble of 1) being aware of this problem and 2) additional boilerplate.

MVC VS MVP

Each of these architectures offers plenty in the domain of separation of concerns, testability, and modularity, but each of them has advantages and disadvantages that they individually offer.
MVP is simple but involves a heavy lifecycle problem and doesn’t offer much that the architectures don’t, apart from its simplicity.
The lifecycle problem of MVP can be overwhelming. This creates easy opportunities for memory leaks, bugs, and crashes. 
MVP is simple well-known architecture even outside of programming and thus, has an easier learning curve for most.
MVP is easy to implement with DI.
MVP has an additional boilerplate and constant awareness of the above problem is required to fix it.
MVP Doesn’t offer much that the other architectures don’t.
MVC supports rapid and parallel development. 
MVC Model, you can create multiple views for a model.
MVC pattern returns data without applying any formatting. Hence, the same components can be used and called for use with any interface. 
MVC pattern increases the code testability and makes it easier to implement new features as it highly supports the separation of concerns.
MVC Unit testing of Model and Controller is possible as they do not extend or use any Android class.
MVC Code layers depend on each other even if MVC is applied correctly.
MVC has No parameter to handle UI logic i.e., how to display the data.




4- MVC for the project

In spite of applying MVC schema to give a modular design to the application, code layers do depend on each other. In this pattern, View and Controller both depend upon the Model. Multiple approaches are possible to apply the MVC pattern in the project:
Approach 1: Activities and fragments can perform the role of Controller and are responsible for updating the View.
Approach 2: Use activity or fragments as views and controller while Model will be a separate class that does not extend any Android class.

In MVC architecture, application data is updated by the controller and View gets the data. Since the Model component is separated, it could be tested independently of the UI. Further, if the View layer respects the single responsibility principle then their role is just to update the Controller for every user event and just display data from the Model, without implementing any business logic. In this case, UI tests should be enough to cover the functionalities of the View.
Controller and View will be handled by the Activity. Whenever the user clicks the buttons, activity directs the Model to handle further operations. The activity will act as an observer.
The Model will be a separate class that contains the data to be displayed. The operations on the data will be performed by functions of this class and after updating the values of the data this Observable class notifies the Observer(Activity) about the change.
Step 1: Create a new project
1.	Click on File, then New => New Project.
2.	Choose Empty activity
3.	Select language as Java/Kotlin
4.	Select the minimum SDK as per your need.

Step 2: Modify String.xml file
All the strings which are used in the activity are listed in this file.


XML
Step 3: Working with the activity_main.xml file
Open the activity_main.xml file and add 3 Buttons to it which will display the count values as per the number of times the user clicks it. Below is the code for designing a proper activity layout.

<?xml version="1.0" encoding="utf-8"?>
	<androidx.coordinatorlayout.widget.CoordinatorLayout xmlns:android="http://schemas.android.com/apk/res/android"
	    xmlns:app="http://schemas.android.com/apk/res-auto"
	    xmlns:tools="http://schemas.android.com/tools"
	    android:layout_width="match_parent"
	    android:layout_height="match_parent"
	    android:fitsSystemWindows="true"
	    app:statusBarBackground="@color/colorPrimaryDark"
	    tools:context=".ui.movieslist.MoviesActivity">
	

	    <com.google.android.material.appbar.AppBarLayout
	        android:id="@+id/appbar"
	        android:layout_width="match_parent"
	        android:layout_height="?attr/actionBarSize"
	        android:theme="@style/ThemeOverlay.AppCompat.Dark.ActionBar">
	

	        <include layout="@layout/toolbar" />
	

	    </com.google.android.material.appbar.AppBarLayout>
	

	    <FrameLayout
	        android:id="@+id/fragment_container"
	        android:layout_width="match_parent"
	        android:layout_height="match_parent"
	        android:layout_marginBottom="?attr/actionBarSize"
	        android:clipToPadding="false"
	        app:layout_behavior="@string/appbar_scrolling_view_behavior" >
	

	

	

	    </FrameLayout>
	

	    <FrameLayout
	        android:layout_width="match_parent"
	        android:layout_height="wrap_content"
	        android:layout_gravity="bottom">
	

	        <com.google.android.material.bottomnavigation.BottomNavigationView
	            android:id="@+id/bottom_navigation"
	            android:layout_width="match_parent"
	            android:layout_height="?attr/actionBarSize"
	            android:layout_gravity="bottom"
	            android:background="@color/colorPrimary"
	            app:elevation="4dp"
	            app:itemIconTint="@color/bottom_nav_item_colors"
	            app:itemTextColor="@color/bottom_nav_item_colors"
	            app:menu="@menu/bottom_navigation" />
	

	        <!--This border vector was inspired by Chris Banes's tivi app-->
	        <ImageView
	            android:layout_width="match_parent"
	            android:layout_height="6dp"
	            android:layout_marginBottom="?attr/actionBarSize"
	            android:contentDescription="@string/bottom_navigation_border"
	            android:scaleType="fitXY"
	            app:srcCompat="@drawable/bottom_nav_border" />
	    </FrameLayout>
	

	</androidx.coordinatorlayout.widget.CoordinatorLayout>

Step 4: Creating the Model class
Create a new class named Model to separate all data and its operations. This class will not know the existence of View Class.



Step 5: Define functionalities of View and Controller in the MainActivity file
This class will establish the relationship between View and Model. The data provided by the Model will be used by View and the appropriate changes will be made in the activity.
 
 





