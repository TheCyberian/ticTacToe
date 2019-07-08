# ticTacToe


7 added winning positions to the game scripts
8 added comparison to winning position and game state and the active player at the time
9 added a reset function and button to reset the game
packaged and ready


Creating a simple Tic Tac Toe android game application using Java

### Step 1:
First, I have created images to be used for the application using GNU Image Manipulation Program, popularly known as GIMP. The game board, X's and 0's were created as part of these images. If you're doing the same, make sure the images are created as '.png' or '.jpg' format only. Otherwise, you may download copyright free images from the internet, which ever way works for you.

### Step2:
After creating the necessary images, I launched the Android Studio and opened a new project with an empty activity. Once the gradle build finishes, I continued with setting up the layout of the application. An empty project by default has a TextView set up within a Constraint Layout. So, I went forward and deleted the Text View and pulled in a grid view on top of the existing constraint layout. For the grid, I added the rowCount and columnCount attributes of layout, as 3 and 3 respectively. I moved forward by setting up the tic tac toe board, on the grid layout, by placing the background attribute of the layout, as the board image created in the first step.

### Step3:
By the beginning of step3, your application would be looking something like this.
<Image tag goes here>
Now for each of the cell, to contain the image or X or 0, we need to add 9 ImageViews. One for each cell of the grid. So, go ahead and start placing ImageViews for each of the cells. You can place any of the image (either X or 0) for now, as we'll be removing them after the view is created and be placing them back in place programmatically. 

### Step4:
After the ImageViews are in place, we'll need to add an onClick function for all the image views. This function will do the task of animating the X or O falling into the Grid cell which is being tapped by the user. This will be done by a simple piece of code, being added to MainActivity.java file, in app/main/java:
<code>
  public void dropIn(View view){

    ImageView counter = (ImageView) view;
    counter.setTranslationY(-1500);
    counter.setImageResource(R.drawable.X);
    counter.animate().translationYBy(1500).rotation(3600).setDuration(500);

  }
</code>
The above piece of code, takes care of the animated movement for the symbol X, but doesn't do anything close to, what is required for the game to work like we want it to, yet. 


### Step5:
To make it work like the tic tac toe game, one of fundamental things is to be able to alternate between the symbols being used. We'll handle it by creating two players and assigning them each one of the symbols. The above code snippet changes to:

<code>
  int activePlayer = 0;

  public void dropIn(View view){

    ImageView counter = (ImageView) view;

    counter.setTranslationY(-1500);

    if(activePlayer == 1 ){
                  counter.setImageResource(R.drawable.x);
                  activePlayer = 0;
              }
              else{
                  counter.setImageResource(R.drawable.o);
                  activePlayer = 1;
              }

    counter.animate().translationYBy(1500).rotation(3600).setDuration(500);

  }
</code>

The above piece of code allows the user to alternate between X's(activePlayer=1) and O's(activePlayer=0) being placed on the grid.


### Step6:
Now the difficult part, how do we keep track of the game's current state? Since, it's one of the easy games, we needn't look much further then using arrays. We are 

going to use a 1-D int array and tag attribute of the ImageView to achieve this. Assign each of the Imageview value of tag; begin with 0, at the top left corner; all the way to 8, at the bottom right corner. The tags values may look like below:
|0|1|2|
|3|4|5|
|6|7|8|

After this we can start with the coding, we add a gameState array, initialized with value 2 in all places(Since, we are using 0, 1, to identify the player, we can use 

2 as neutral value) and a int variable to capture which of the cells were tapped by user, by checking the activePlayer variable.
So, now our code looks like below:

<code>
int activePlayer = 0;
int[] gameState = {2, 2, 2, 2, 2, 2, 2, 2, 2};

public void dropIn(View view){

	ImageView counter = (ImageView) view;
	int tappedCounter = Integer.parseInt(counter.getTag().toString());

	if(gameState[tappedCounter] == 2){	
		
		gameState[tappedCounter] = activePlayer;	
		counter.setTranslationY(-1500);
	
		if(activePlayer == 1 ){
                	counter.setImageResource(R.drawable.x);
	                activePlayer = 0;
        	    }
	            else{
        	        counter.setImageResource(R.drawable.o);
                	activePlayer = 1;
	            }

	counter.animate().translationYBy(1500).rotation(3600).setDuration(500);

	}
}
</code>
The above code, places Zeros and ones in the gameState integer array. It does so, by getting tag value of the tapped image view and replacing that index(tag value) in gameState array with activePlayer value.

Now we have a somewhat functioning appliaction. We now need to add function to check for a winner when someone gets three in a row and to reset the game when someone has won.
