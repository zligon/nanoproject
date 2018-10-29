$(document).ready(function() {
  //Variable deckOfCards populates the "fa or Font Awesome" cards for the game
  var deckOfCards = [
    "fa fa-diamond",
    "fa fa-paper-plane-o",
    "fa fa-anchor",
    "fa fa-bolt",
    "fa fa-cube",
    "fa fa-anchor",
    "fa fa-leaf",
    "fa fa-bicycle",
    "fa fa-diamond",
    "fa fa-bomb",
    "fa fa-leaf",
    "fa fa-bomb",
    "fa fa-bolt",
    "fa fa-bicycle",
    "fa fa-paper-plane-o",
    "fa fa-cube"

  ];
  // VARIABLE DEFINITION:
  // cardDisplay: List used to store the attributes of the 2 user selected
  //     cards from the deck.
  //  cardPosition: List used to store the position of the card in the deck.
  // cardsFlipped: Variable used to keep count of the number of cards turned
  //     over at any one time.
  // moveCount: Variable used to indicate number of moves made while playing
  //     the game.
  // cardDisplayCount: Variable used to indicate the number of cards displayed.
  // Pre-definition of the secondsFormatted, minutesFormatted and
  //     hoursFormatted variables used to store related formatted quantities.
  //  timeElapsedSeconds: Variable used to store number of seconds elapsed.
  // timer: Variable used to store intervalID from the setInterval function
  //     in the runTimer() function.
  var cardDisplay = [];//
  var cardPosition = [];//
  var cardsFlipped = 0;//
  var moveCount = 0;
  var cardDiplayCount = 0;
  var secondsFormatted,
    minutesFormatted,
    hoursFormatted = 0;
  var seconds,
    minutes,
    hours = 0;
  var timeElapsedSeconds = 0;
  var timer;

// Shuffle function from http://stackoverflow.com/a/2450976. Provided in example from udacity
  function shuffle(array) {
    var currentIndex = array.length,
      temporaryValue,
      randomIndex;
    while (currentIndex !== 0) {
      randomIndex = Math.floor(Math.random() * currentIndex);
      currentIndex -= 1;
      temporaryValue = array[currentIndex];
      array[currentIndex] = array[randomIndex];
      array[randomIndex] = temporaryValue;
    }
    return array;
  }

//deckHTML creates the HTML element for the deck of cards
  function deckHTML() {
    $(".container").append('<ul class="deck"></ul>');
    for (var i = 0; i < deckOfCards.length; i++) {
      $(".deck").prepend('<li class="card"><i></i></li>');
      $.each($(".deck .card"), function(i, item) {
        $(item).attr("data-cardDeckPosition", i);
      });
    }
  }

//cardAssignment assigns each shuffled card to one of the spaces provided in the HTML
//tags
  function cardAssignment() {
    var shuffledCards = [];
    shuffledCards = shuffle(deckOfCards);
    for (var i = 0; i < deckOfCards.length; i++) {
      $(".deck .card")
        .children()
        .eq(i)
        .addClass(shuffledCards[i]);
    }
  }

//timeInterval function formats the zeros in the score panel
  function timeInterval(timeInterval) {
    return (timeInterval < 10 ? "0" : "") + timeInterval;
  }

//time function starts when the user makes their first click. It is formatted in
// hours:minutes:seconds or 00:00:00.
//Function utilized from: https://stackoverflow.com/questions/2604450/how-to-create-a-jquery-clock-timer
  function time(timeElapsedSeconds) {
    hours = Math.floor(timeElapsedSeconds / 3600);
    timeElapsedSeconds %= 3600;
    minutes = Math.floor(timeElapsedSeconds / 60);
    timeElapsedSeconds %= 60;
    seconds = Math.floor(timeElapsedSeconds);
    var hoursFormatted = timeInterval(hours);
    var minutesFormatted = timeInterval(minutes);
    var secondsFormatted = timeInterval(seconds);
    var currentTimeString =
    hoursFormatted + ":" + minutesFormatted + ":" + secondsFormatted;
    return currentTimeString;
  }

//runtimer function calls the setInterval method and calls the function timeElapsed
//and the incremented by 1 variable timeElapsedSeconds. It also outputs the time in the score Panel
//reference: https://stackoverflow.com/questions/109086/stop-setinterval-call-in-javascript
  function runTimer() {
    timer = setInterval(function() {
        timeElapsedSeconds++;
        $(".score-panel .timer").text(time(timeElapsedSeconds));
  }, 1000);
}

// popupDisplay function that is used to display the star rating,
// number of moves to complete, time it took to complete and restart
  function popupDisplay() {
    $(".score-panel .stars")
      .clone()
      .appendTo($(".popup-star-display-element"));
    $(".moves")
      .clone()
      .appendTo($(".popup-move-counter-element"));
    $(".timer")
      .clone()
      .appendTo($(".popup-timer-element"));
  }
  deckHTML();
  cardAssignment();
  var booleanValue = 0;
  $(".card").click(function(event) {
    if (timeElapsedSeconds === 0 && !booleanValue) {
      booleanValue = 1;
      runTimer();
    }
    if (
      //conditional statement that does not allow more than 2 cards opened at Once
      cardsFlipped < 2 &&
      !$(this)
        .children()
        .hasClass("open")
    ) {
      $(this).toggleClass("open");
      //toggleClass will toggle the selected card to open
      cardsFlipped++;
      if (cardsFlipped === 1) {
        cardPosition.push($(this).attr("data-cardDeckPosition"));
        cardDisplay.push(
          $(this)
            .children()
            .attr("class")
        );
      } else {
        cardPosition.push($(this).attr("data-cardDeckPosition"));
        cardDisplay.push(
          $(this)
            .children()
            .attr("class")
        );
        //The following ensures that the cards from the deck match and same position is
        //not selected twice causing a false match
        //Once matching conditions are met, the card stays flipped over.
        //If cards do not match, both cards are flipped back over (reverted to original css state)
        if (
          cardDisplay[0] === cardDisplay[1] &&
          cardPosition[0] !== cardPosition[1]
        ) {
          $(".card")
            .filter(".open")
            .removeClass()
            .addClass("card match");
          cardDisplay = [];
          cardDiplayCount += 2;
          cardPosition = [];
          moveCount += 1;
          cardsFlipped = 0;
          $(".moves").text(moveCount);
        } else if (cardPosition[0] !== cardPosition[1]) {
          setTimeout(function() {
            $(".card")
              .filter(".open")
              .removeClass()
              .addClass("card");
            cardDisplay = [];
            cardPosition = [];
            moveCount += 1;
            cardsFlipped = 0;
            $(".moves").text(moveCount);
          }, 1000);
        } else {
          setTimeout(function() {
            $(".card")
              .filter(".open")
              .removeClass()
              .addClass("card");
            cardDisplay = [];
            cardPosition = [];
            cardsFlipped = 0;
            $(".moves").text(moveCount);
          }, 1000);
        }
      }
      //the following adjusts the star rating in the score panel and the final popup
      //If numberOfMoves is between 21 and 27 user gets a 2 star rating.
      //If numberOfMoves is 28 or over uset gets a 1 star rating
      if (moveCount > 20 && moveCount < 28) {
        var thirdStar = $(".stars")
          .find("li")
          .eq(2);
        thirdStar.css("color", "black");
      }
      if (moveCount > 28) {
        var secondStar = $(".stars")
          .find("li")
          .eq(1);
        secondStar.css("color", "black");
      }
    }
    //Once all cards are matched, this calls a popup with numberOfMoves, timer and a restart option
    //updates the css to force it into the foreground by using block and changing the z index to 1000
    if (cardDiplayCount === deckOfCards.length) {
      clearInterval(timer);
      $(".popup").css("display", "block");
      $(".popup").css("z-index", "1000");
      popupDisplay();
    }
  });
});
