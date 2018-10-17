# JSON-and-AJAX-youtube-tutorial
//https://www.youtube.com/watch?v=rJesac0_Ftw&amp;t=1298s

//https://www.youtube.com/watch?v=rJesac0_Ftw&t=1298s
//New variable that equals 1 and increment that value each time it gets clicked 
var pageCounter = 1;

//Variable that points to an empty <div> to display all the information to
var animalContainer = document.getElementById("animal-info");

//We only want to download our new data if and when someone clicks on the button 
var btn = document.getElementById("btn");
//set up the event listener for when the button gets clicked 
btn.addEventListener("click", function() {
  var ourRequest = new XMLHttpRequest();
  ourRequest.open('GET', 'https://learnwebcode.github.io/json-example/animals-' + pageCounter + '.json');
  //A method that says what happens once the data is loaded 
  ourRequest.onload = function() {

    //Save the data to a variable
    var ourData = JSON.parse(ourRequest.responseText);
    //Call the renderHTML() function created below
    renderHTML(ourData);
  };
  //we've defined the request so next we have to send the request 
  ourRequest.send();
  pageCounter++;
  if (pageCounter > 3) {
    btn.classList.add("hide-me");
  }
});

//As a way of staying organised, create a function whose sole purpose is to add HTML elements 
function renderHTML(data) {
  //Initialise an empty vairable
  let htmlString = "";
  //Loop through the pet array
  for (i = 0; i < data.length; i++) {
    htmlString += "<p>" + data[i].name + " is a" + data[i].species + " that likes to eat ";
    //loop through the likes array to display their likes 
    for (ii = 0; ii < data[i].foods.likes.length; ii++) {
      if (ii == 0) {
        htmlString += data[i].foods.likes[ii];
      } else {
        htmlString += " and " + data[i].foods.dislikes[ii];
        for (ii = 0; ii < data[i].foods.dislikes.length; ii++) {
          if (ii == 0) {
            htmlString += data[i].foods.dislikes[ii];
          } else {
            htmlString += " and " + data[i].foods.dislikes[ii];
          }
        }
      }
    }
    //Add the closing tag 
    htmlString += ' and dislikes ';
    htmlString += '.</p>';
  }
  //Target the empty div using the variable animalContainer defined at the top 
  animalContainer.insertAdjacentHTML('beforeend', htmlString)
}
