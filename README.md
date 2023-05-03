Download Link: https://assignmentchef.com/product/solved-cs1027-assignment4
<br>
To gain experience with

<ul>

 <li>Working with linked data structures</li>

 <li>Recursive approaches to problem solving</li>

 <li>Putting together many concepts into one project</li>

 <li>Algorithm design</li>

</ul>

<h1>Introduction</h1>

Minesweeper is a solitaire computer game in which there are bombs hidden in a grid of cells, and the objective is to clear out all the non-bomb cells without hitting a bomb. If a bomb is clicked, the game is over in failure.

To help the player determine where the bombs are located, the other cells contain a number that indicates the number of bombs in the eight adjacent (both orthogonal and diagonal) cells. The number on a cell is revealed when that cell is clicked. Additionally, when a cell that has no adjacent bombs (let’s call this a 0-cell) is clicked, it triggers a “region clear” which means that a region beginning with the clicked cell and expanding outward will be revealed at once. The region will include all 0-cells connected to the clicked cell, and numbered cells connected to those 0-cells. Figure 1 shows examples of 3 cleared regions. For each of these regions, one of the inner 0-cells was clicked, and the surrounding region was consequently cleared.




Figure 1. A screenshot of a completed (lost) game in which a bomb cell was clicked after revealing 3 regions throughout the board. Cells with a number indicate how many bombs cell are neighbouring (orthogonally or diagonally adjacent).




<h1>Provided files</h1>




The following is a list of files provided to you for this assignment. Please do not alter these files in any way.

<ul>

 <li>java – provides a method for randomly placing bombs</li>

 <li>java – provides the visual GUI for the program</li>

 <li>java – represents each cell in the game board</li>

 <li>java – represents a node for a singly-linked list</li>

 <li>java – a simple exception class</li>

 <li>java – provides several tests to check that LinkedGrid is working</li>

 <li>java – provides several tests to check that the Game methods are working</li>

</ul>




<h1>Classes to implement</h1>




For this assignment, you must implement 2 Java classes: <em>LinkedGrid</em> and <em>Game</em>. Follow the guidelines for each one below.

In both of these classes, you can implement more private (helper) methods, if you want to, but you may<strong> not</strong> implement more public methods. You may<strong> not</strong> add instance variables other than the ones specified below. Penalties will be applied if you break these rules.




<h2>LinkedGrid.java</h2>




This class represents a 2D grid (matrix) that is created as an array of singly linked lists. This class must work for any generic type T and must be created using the descriptions explained here. The array, which must be the width of the grid, will contain the front (or top) nodes of each of the linked lists. The height of the grid is represented by the number of nodes in each of the linked lists. The example below shows a 5 by 4 grid (remember the front node of each list is contained in the array so there are 4, not 3, nodes in each list).




Figure 2. A diagram depicting the LinkedGrid structure as an array of linked lists.

The class must have the following <em>private</em> variables:

<ul>

 <li>width (int)</li>

 <li>height (int)</li>

 <li>grid (LinearNode&lt;T&gt; array)</li>

</ul>

The class must have the following <em>public</em> methods:

<ul>

 <li>LinkedGrid (constructor) – takes in 2 parameters for width and height and assigns their values into the corresponding instance variables. The grid must be initialized properly by creating the LinearNode objects and connecting them as singly linked lists. The first node of each list must be stored in the corresponding array cell in the grid parameter.</li>

 <li>setElement – takes in 3 parameters: int col, int row, T data. If the col or row is outside the bounds of the grid, throw a LinkedListException. Otherwise, find the cell in the grid at the given col, row pair and set the element of that node to the given value, data.</li>

 <li>getElement – takes in 2 parameters: int col, int row. If the col or row is outside the bounds of the grid, throw a LinkedListException. Otherwise, find the cell in the grid at the given col, row pair and return the element contained in that node.</li>

 <li>getWidth – returns the width</li>

 <li>getHeight – returns the height</li>

 <li>toString – builds a string that represents the entire grid of elements. Include 2 spaces between each of the elements and use a newline character at the end of a row to continue the string on the next line. Return the completed string.</li>

</ul>




<h2>Game.java</h2>




This class contains the Minesweeper-related code. It is used to initialize the game board, determine the numbers for each cell (which indicate how many bombs are in neighbouring cells), the recursive “region clearing”, etc.

The class must have the following <em>private</em> (unless stated otherwise) variables:

<ul>

 <li>board (LinkedGrid&lt;Character&gt;)</li>

 <li>cells (LinkedGrid&lt;GUICell&gt;)</li>

 <li>width (int) – must be public static</li>

 <li>height (int) – must be public static</li>

 <li>gui (GUI)</li>

</ul>

The class must have the following methods:

<ul>

 <li>Game (constructor #1) – takes in int width, int height, boolean fixedRandom, boolean showGUI. Set the width and height class variables and then initialize the board grid with an ‘_’ (underscore) character in every cell. Then initialize the cells grid of GUICell elements (NOTE: even if the GUI is not being shown, we still use the GUICell class for these cells). Use the BombRandomizer’s placeBombs method (sending in the board and fixedRandom parameter) to randomly place bombs throughout the game board. Call the determineNumbers method (see description below) to get the number for each cell which indicates how many bomb cells are neighbouring each cell. Lastly, if showGUI is true, then initialize the GUI object.

  <ul>

   <li>NOTE: the fixedRandom variable is used to determine if you want to use the same random seed each time you run it for testing purposes. If fixedRandom is true, then it uses a fixed seed so the board will be the same every time you run it (assuming the size is not changed). Otherwise set fixedRandom to false if you want to run the game with a different, actually random board each time.</li>

  </ul></li>

 <li>Game (constructor #2) – takes in LinkedGrid&lt;Character&gt; board, boolean showGUI. This constructor is almost the same as the 1<sup>st</sup> one above. The only differences are that the board is already set so you do not need to follow the same board initialization and random bomb placement. Instead, simply assign the board parameter to the corresponding instance variable. The rest of the method is identical.</li>

 <li>getWidth – returns the width</li>

 <li>getHeight – returns the height</li>

 <li>getCells – returns the LinkedGrid cells</li>

 <li>determineNumbers – go through every single node in the board and calculate how many bombs are in surrounding cells, and insert that number into the corresponding node in the cells grid. Cells that contain bombs must have a number of -1 (even if they are adjacent to other bombs), but all other cells must have a number (from 0 to 8) that indicates the number of bombs around that cell.</li>

 <li>processClick – this method processes a cell being clicked OR a simulated click and returns an int value representing how many cells are being revealed or -1 if a bomb is revealed. It takes in two integers for col and row, and gets the GUICell from that position in the grid.

  <ul>

   <li>If the given cell contains -1 (bomb) then set the background of this cell to red (use cell.setBackground(Color.red)) and reveal the cell (look at the GUICell methods to see how to do this).</li>

   <li>If the cell contains a 0, begin the recursive “region clearing” from this cell and return the result that is returned from the recursive method.</li>

   <li>If the cell contains any other number (1 through 8), then check if it was previously revealed. Return 0 if previously revealed. If it wasn’t previously revealed, make sure to reveal it and set it to white and then return 1.</li>

  </ul></li>

 <li>recClear [private, and name is not important] – takes in two integers for col and row and returns an int representing the number of cells being revealed from this method call. This is the recursive helper method invoked from the processClick method. Read the description of “Region clearing” and the pseudocode for recClear below.</li>

</ul>




<h1>Region clearing</h1>




One of the terms used in this assignment is “region clearing”. This occurs when a 0-cell (a cell that does not have a bomb nor is adjacent to a bomb) is clicked. The cell itself is revealed but it also triggers its region to become revealed immediately. The region is defined as the contiguous (connected) 0-cells and even up to numbered cells along the perimeter of the region but no further than the numbered cells. This form of clearing can be done very elegantly with recursion.

Examine the following illustrations that demonstrate “region clearing” in a sample 5 by 5 game grid with 7 bombs. Figure 3 shows the original game board before clicking any cells, and it shows the bombs’ locations just for demonstrative purposes (bombs are not shown in the actual game!) Figures 4-6 illustrate each recursive step in the algorithm from clicking the middle cell.




Figure 3. A sample 5 by 5 game grid with 7 bombs (visible for demonstration purposes)




Figure 4. The sample game board after clicking the middle cell, which is a 0-cell. Red arrows indicate which cells will be revealed in the first recursive step of the region clearing.







Figure 5. After one recursive step, the cells surrounding the clicked (middle) cell are revealed. The next step will reveal the cells surrounding the 0-cells at the top of the existing region.

Numbered cells indicate the region’s perimeter, so the clearing doesn’t go beyond those cells.







Figure 6. The clearing has completed since Figure 4. The cells just revealed are either numbered or are along the edge of the board itself, so there are no more recursive calls. This is the finished “region clearing” from clicking that middle cell (NOTE: the region would have been the exact same from clicking on <strong>any</strong> of the 0-cells in the top-left corner of this region).













<h2>Pseudocode</h2>




function recClear (int c, int r)

<strong>Input</strong>: column c and row r of cell being clicked

<strong>Output</strong>: int value representing how many cells were revealed         if c or r is outside bounds of game board, return 0    if cells(c, r) is already revealed, return 0           if cells(c, r) is a bomb (-1), return 0    else if cells(c, r) is a numbered cell (&gt; 0)

reveal cells(c, r)

set cells(c, r) colour to white in gui (if gui != null)

return 1           else

reveal cells(c, r)

set cells(c, r) colour to white in gui (if gui != null)

result = 1;

result += recClear(c-1, r)

… (all other recursive calls)   return result


