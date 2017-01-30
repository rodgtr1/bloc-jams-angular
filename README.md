#Bloc Jams Angular
Bloc Jams is a digital music player like Spotify that we originally created using HTML/CSS, and JavaScript (vanilla and jQuery).

In this project we revisited our original BlocJams project and undertook an almost complete recreation of it using AngularJs.

<br />

![BlocJams Landing](assets/images/BlocJams Landing.png)

##Project Summary
To setup, we installed four Grunt plugins from the outset (Watch, Copy, Clean, and Hapi). We declared an Angular module (angular.module(‘blocJams’, []);) and bootstrapped the application using the ng-app directive in the root element (<html>).  We set index.html as our global file, with our templates being landing.html, album.html, and collection.html. Much of the data in these templates were copied over from our prior Bloc Jams project. In order to display these templates in the view, we used UI-Router to set our URL routes. We injected the UI-Router Module into our module in app.js (angular.module(‘blocJams’, [‘ui.router’]);. We then configured our module with two providers, $stateProvider and $locationProvider. We set the $locationProvider to html5Mode so that the user will see clean URL’s without the hasbang (i.e. /#i/album). We configured the stateProvider in order to configure our template “states,” and changed our href anchor tags to ui-sref=“(state name), so that it will trigger a change in state and not reload entire pages when we click on them. 

Next, in the song rows we had to set the different states for the number/play/pause button. When it was not playing and the mouse was off hover, we set it to show the song number. When the song is not playing and the mouse is on hover, we set it to the play button. When the song is playing, we had it display the pause button. We then used ng-include to display our player bar. 

We set up our controllers for the three states: Landing, Collection and Album in app.js, used ng-repeat to populate out album collection, and replaced the static song info and data using the corresponding scope properties and {{ }} markup. 

Next up we created a service with Fixtures.js , moved our album info that we used before into it, and injected it into our AlbumCtrl and CollectionCtrl. We created a SongPlayer service and injected it into our AlbumController as that is the view we will play music from. We then wrote and play and pause method, with the help of the Buzz library, so that our songs will functionally play and pause.  

Now that our songs play in album view, we wanted to get our player bar in sync with the songs playing and set its associated controls (next, previous, play and pause). Since the scope of our PlayerBar controller is different than our Album Controller, it did not have access to the song object, therefore we had to take our private attribute, currentSong and make it public, SongPlayer.currentSong and updated all  instance of currentSong and our play/pause methods. We then set up our previous and next methods on the player bar.

##Preview
Check out my [Netlify deploy](http://bloc-jams-travis-rodgers.netlify.com/) to see it in action.

##More Screenshots
![BlocJams Landing](assets/images/BlocJams Collection.png)

<br />

![BlocJams Landing](assets/images/BlocJams Album.png) 

We created a custom directive for our seekbar and used the logic from our foundational Bloc Jams project to configure our seekbar functionality as well as the thumb (circle) on the seekbar using a click event and mousedown/mouseup.  Next we used an $observe attribute to tell Angular to observe the object and added an attribute named onChange and a function that would continually update the value with the new value. 

Finally, in order to update the song’s playback progress from anywhere we accessed the $rootScope service. We then set up the volume bar to make it functional similar to the method used for the seekbar.  And to finish things up, we created a timecode filter to convert our seconds to minutes. 
