# Fitness and Nutrition Buddy

I worked on this project with 3 other people in the Software Engineering II course at UIC.
The main goal was to create a prototypical Android app that would merge the features of standalone nutritional apps and standalone fitness apps, while incorporating realtime data.
The specifications were created by a previous 4 man group in the class, which can be viewed in totality in "Specifications.pdf."
My group's final report detailing our deliverables can be found in "Final Report.pdf."
Our app was coded completely in Java with Android Studio.

## What I worked on

### Home
I mainly worked under the "Home" subpackage, which is the fragment that creates the meal and workout logs in HomeFragment.java.
I created the meal log using a ViewPager2 with infinite scroll.
The ViewPager2 instantiates the same fragment class each time, with the corresponding date passed as a parameter to each fragment instance.
The date is calculated by taking the offset from the ViewPager2's start position.
In each date fragment there is a TabView for a meal fragment and a workouts fragment.
These have TextViews like "Breakfast" or "Cardio" and a ListView under each category to display the relevant meals or workouts.
If you click on a meal or workout, you will see a PopupMenu that I designed and coded show up that will allow you to edit the nutritional or workout info.

The meal log is also highly integrated with MealHistory.java, which contains a MaterialCalendarView.
The last date the user scrolled to in their meal log will influence the date that is first displayed in the MaterialCalendarView.
Likewise, the last date the user clicked in the MaterialCalendarView will be displayed in the meal log when the user clicks the back button.
Unfortunately, this was done by modifying "public static LocalDate lastScrolledToDay" - not in line with Android's guidelines.
This was done because Android's previous message passing architecture became deprecated, and I wanted to just get the prototype working rather than learning the new method.
On the plus side, switching between the calendar activity and the meal log still feels very responsive.

### Search
In the "Search" subpackage, I mainly worked in SearchFragment.java.
Searching for meals and workouts was done by querying the NutritionIX API.
I created one of the HTTP GET methods in SearchFragment.java, but my teammates eventually expanded on my work and improved the search.
Querying the NutritionIX database for food now returns detailed micronutrient info (I only retrieved results from NutritionIX's standard endpoint).
Querying the NutritionIX database for workouts is possible using natural language syntax (I did not work on this at all).
I also added autocomplete search suggestions to the search bar for common meals and workouts.
You can see these by clicking on the "Add X" buttons.

I also added inter-fragment communication from HomeFragment.java to SearchFragment.java.
If you click on the "Add X" buttons the "Search" bottom navigation menu will be clicked for the user and the search suggestions will be updated to whichever "X" the user clicked.
Again, this was done through the use of static variables to save time learning new inter-fragment communication Android features..

### Misc

I also added 5 Espresso tests to the project, mostly focused on clicking on the bottom navigation menu and verifying that the correct fragment was loaded.
I worked with Visual Enterprise to automatically-generate UML charts for our project - these can be seen in the final report.
I worked with querying Firebase and attempted to set up a realtime listener for when the user pushes changes to our database - but I could not get this working.
I was running into NPEs whenever I tried to update the meal or workout log by this method, and couldn't sucessfully debug why.
