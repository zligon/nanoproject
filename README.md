# memoryCardGame
The Match Game or Concentration is a game with an even number of tiles that tests the users focus and memory. The player turns over 2 tiles trying to find a match and those cards stay flipped if matched. If a match is not found, the tiles are turned back over in the same position. The game is complete when all tiles are matched. The player is ranked using a 3 star system. The rating changes to 2 stars after 20 moves and then to 1 star if there are 28 or more moves. There is a timer function that tracks how long it takes the player to complete the game. Once the game is completed, a popup is displayed that shows the player their star rating, time it took to complete and gives them the option to restart the game. Pressing the restart button essentially refreshes the main page setting everything back to it's default state.  To create the program, javascript or jquery was used to create the programming portion, html for website functionality/layout and css for styling.

Index.html

  This is the backbone of the user experience. There are two key components:
  A. Header Files:
  Links are made between the css stylesheet (app.css) and the javascript file (app.zlr) that detail the interaction between the user and the webpage.

  B. Body:
  In the body of the html file there are different containers
    1. Score panel that is at the top of the page, it shows the user the move count, timer, star rating and restart button.
    2. The popup class is the panel that is displayed once the user completes the game. It will give them the time it took,
        move count, star rating and gives them a chance to restart the game. Using the restart button sends the user back to the original webpage and it is refreshed.
  The app.zlr file will add the deck and shuffled cards to the designated container in HTML through it's function.

App.css

    App.css is the stylesheet for the styling of the html webpage. It adjusts the spacing, font and style for each element of the webpage. The background is pulled from a google search. It consists of:
        1. HTML styling adds the styling for what the user will see on the basic webpage.
        2. The styles for each card in the deck
        3. The popup when the user completes the game
        4. The score panel at the top of the webpage with the users performance rating

App.zlr

  This serves as the interaction with the html page. It consists of functions that set the parameters, like the following:

        1. The shuffle function randomizes the deck of cards each time the page is refreshed.
        2. deckHTML creates the html layout for the deck of cards
        3.  cardAssignment assigns the shuffled cards the html tags
        4. timeInterval formats the timer with hours, minutes, and seconds accordingly
        5. time function is what makes the timer work once the user makes their first click. It is formatted in
            hours, minutes and seconds layed out like 00:00:00. The function was found online at https://stackoverflow.com/questions/2604450/how-to-create-a-jquery-clock-timer
        6. runTimer calls the other functions and displays them
        7. popupDisplay displays the elements inside the endgame popup
        8. event function runs the game based on the clicks of the users
    There are also loops that run based on the conditions of the game
        1. Star ratings are based the number of moves by the user. 20 and under will give 3 stars, 21-27 2       stars, 28 and over will be 1 stars
        2. When the game is completed, cardDiplayCount and deckOfCards.length are the same. Once these conditions are met the popup is displayed. 


Dependencies

1. cardAssignment() needs the deckHTML() function to be called as its predecessor.
2. cardAssignment() uses the shuffle() function to randomize or shuffle the deckOfCards.
3. Timer() function only works if a boolean value registers as false and the variable timeElapsedSeconds is = to 0.
4. Timer() also uses the output of the timeElapsed() function.
5. timeElapsed() function uses the timeElapsedSeconds variable (suitably incremented) as input, to process it into the hours:minutes:seconds format
6. timeIntervalFormat() function pads the time interval input (either hours, minutes or seconds) with leading zeros as and when required.
7. popupDisplayParameters() clones the score panel elements i.e. timer, moves counter, star rating counter and adds these to the congratulations pop up. The z index is set to 1000 for the popup because the transformation in the css was causing the tiles to stay in front of the popup.
8. The restart function in the score panel and the popup, both reload the origianl html page.
