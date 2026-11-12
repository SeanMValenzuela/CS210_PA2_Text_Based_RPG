# Reflection Questions
### 1. For every function you wrote (TODO 1 to 19), explain in your own words what it does and give its time complexity in terms of n, the number of scenes. One short paragraph each.
#### TODO 1 (Scene): 
Scene is a constructor, which constructs a scene through two parameters; data and numChoices. Each scene is assigned
its respective data and empty slots are created based on the number of choices outlined previously for its children
and assigned to nullptr. Scene runs in O(1) time, which comes from looping through the choice slots but keeping in mind
the fact that the maximum number of choices is 3.
#### TODO 2 (~Scene):
Unlike the constructor Scene, ~Scene is the destructor, which frees everything that a Scene holds (data_ and choices_). It 
deletes every child scene by looping through each one, and then deletes the choices_ array itself and then finally data_. 
~Scene also runs in O(n) time, as it loops through every child scene as aforementioned.
#### TODO 3 (isEnding):
isEnding is a function that returns true or false on whether or not a Scene is an ending. This is determined by checking if
a Scene's numChoices is equal to zero, as that means that it has no child scenes, meaning it is a leaf and therefore an ending.
Else, it is not a leaf and therefore not an ending, so false is returned. isEnding runs in O(1) time, as the check whether or not
numChoices is equal to zero is in constant time.
#### TODO 4 (getChoice):
getChoice is essentially responsible for retrieving the child scene of a Scene at a given index, taken from the choices_ array.
However, if the given index is invalid, which is if it is less than zero, greater than or equal to numChoices, or the child scene
at a given index does not exist (nullptr), nullptr is returned. getChoice runs in O(1) time, as accessing an array through an index
runs in constant time.
#### TODO 5 (setChoice):
setChoice is simply the setter complement to the getter in getChoice, and is responsible for assigning a child scene at a given index.
Similar to how getChoice operates, if the given index is invalid, which is if it less than zero or greater than or equal to numChoices, 
the function returns early without modifying the array. setChoice runs in O(1) time, as assigning a value at a given index in an array 
runs in constant time.
#### TODO 6 (countScenes):
countScenes takes in a Scene as a parameter, which is made the root of a subtree. The function then uses recursion to count the starting Scene and the number of descendants
of the root Scene in the subtree and returns that value. The base case is when the current Scene is nullptr, while the recursive case is calling the function
with a child of the current Scene. countScenes runs in O(n) time, as it traverses through every single scene in the subtree to count each and every one of them.
#### TODO 7 (countEndings):
countEndings runs in a similar fashion to countScenes by using recursion on a Scene parameter as well. Through recursion, it traces every possible path starting
from the Scene given as the parameter, with two base cases being the current Scene being nullptr returning 0 and if the current Scene being an ending returning 1. After the unwinding
phase is completed, the function returns a value representing the number of endings starting from the original Scene parameter. countEndings runs in O(n) time, as it traverses through
every path and therefore, also every single scene starting from the original Scene to find the number of endings.
#### TODO 8 (height):
height is another function that uses recursion, similar to the previous two functions in StoryTree.h. However, height is responsible for finding the longest path a player can
take starting from a given Scene parameter and returns the number of choices encountered along the path, which makes up the height of the tree, hence the name of the function.
It has two base cases: one for when the current Scene is nullptr and one for when the current Scene is an ending. Its recursive case is tracing through every possible path starting from 
the Scene given as the parameter and finding which is the longest, whose number of choices represents the value returned in the end. height runs in O(n) time, as it traverses through
every path and therefore, also every single scene starting from the original Scene to find the maximum number of choices in any path.
#### TODO 9 (clear):
clear does not use recursion like the other functions in StoryTree.h, and is rather quite simple in comparison. It simply frees every scene in the story by deleting the root and simultaneously
setting it to nullptr, which essentially deletes all of the data in the StoryTree object but it still remains valid, just now empty. clear runs in O(n) time as deleting the root invokes the ~Scene
destructor, which itself runs in O(n) time.
#### TODO 10 (load):
load is responsible for opening the given story file and using it to build the actual tree. If something fails, such as the file not being able to read or the starting scene being nullptr, the
function will return false. However, if everything succeeds and the function can run properly, the player's HP level will be set to the starting HP outlined in the given story file and the tree
is built by setting the tree's root to the given starting scene. load runs in O(n) time, as the call back to readScene happens each time a Scene has to be read and
built exactly once.
#### TODO 11 (readScene):
readScene reads a specific scene in the tree and identifies all of its characteristics, which includes: its description, HP change, loot change, item change, and how many choices there are.
If something goes wrong, such as a line not being able to be read or the numChoices being invalid, nullptr will be returned. However, if everything goes right, a Scene object and its children scenes
are created using the given scene's characteristics. readScene runs in O(n) time, as the recursion reads each scene in the file exactly once.
#### TODO 12 (askChoice):
askChoice asks the player what choice they want to go with while playing the game by selecting a corresponding number. If a line cannot be read, the function will return zero.
If the player fails to give a valid input, such as a number less than 1 or greater than the number of choices indicated, they will be prompted to re-enter a different number, but if the input is
valid, their number of choice will be returned. askChoice runs in O(1), as asking for a user input and returning that same input runs in constant time.
#### TODO 13 (play):
play is responsible for a good chunk of the gameplay of the story, starting from the root Scene. It is responsible for carrying out many tasks and printing their respective outputs
such as: HP changes, loot changes, bag additions, deciding when the player died, deciding when the player reached an ending, and asking the player for their choice (using call to askChoice).
play runs in O(n^2) time, as it will run through every scene in a given path the player decides to take, but also searches through the inventory at any given scene, which
potentially contains up to n items.
#### TODO 14 (printStats):
printStats helps print the stats of a given story tree, specifically its number of scenes, endings, and longest possible playthrough (height). printStats runs in O(n) time as it calls
back to the functions countScenes, countEndings, and height, which all run in O(n) time.
#### TODO 15 (printSpoilers):
printSpoilers is the function that prints every ending in a given story tree. It first gets the root of the tree and then calls to another function called printEndings, which is
responsible for printing every single ending below a given Scene. printSpoilers therefore runs in O(n) time, as it calls back to printEndings, which runs in O(n) time due to its
nature of traversing through every path and therefore every Scene below the given original Scene. 
#### TODO 16 (printEndings):
printEndings is implemented to print every single ending below a given Scene (a parameter) and its path to get there. If the original given Scene is already a leaf, and
therefore an ending, the function will simply print "Path (start):" and the text of the Scene. On the other hand, if a certain path has to be taken to achieve a certain ending,
both the path and the text will be printed. As aforementioned, printEndings runs in O(n) time due to its nature of traversing through every possible path starting from a given 
Scene and therefore also every Scene below the given original Scene.
#### TODO 17 (greedyRun):
greedyRun finds the path a player will have to take if all they prioritize is choosing the choice at a given scene that results in the most amount of loot each time.
This is done by starting from the root of a given story tree and then identifying the choice at each scene that gives the most loot, while ignoring everything else. At the end, 
it will print out the specific path, its amount of loot collected on the run, and the result of the ending (died or simply reached an ending). greedyRun runs in O(n) time as it 
will have to traverse through every single Scene in the greediest path a player can take.
#### TODO 18 (bestLoot):
bestLoot is tasked with finding the  path a player can take when playing out a story that results in the most amount of loot possible by going through the entire tree 
starting from the root and tracing through every possible path one can take. The path that results in an ending with the greatest amount of loot possible is considered 
that path. If every possible path results in the player's death, -1 is returned. bestLoot runs in O(n) time as it will have to traverse through every part of a given 
story tree and therefore all of its Scenes as well in order to find the path that gives the most loot.
#### TODO 19 (optimalRun):
optimalRun uses bestLoot to first find the path that gives the greatest amount of loot in a given tree, and then uses the best path provided as the parameter
and loot value that bestLoot returns to print those statistics. optimalRun runs in O(n) time as it calls back to bestLoot, which runs in O(n) time as it 
traverse through every part of a story tree and therefore all of its Scenes as well in order to find the path that gives the most loot.

### 2. Why does each scene allocate exactly numChoices slots instead of declaring Scene<T>* choices[3]? What does an ending hold in choices_, and why?
Each scene allocates exactly numChoices slots instead of declaring Scene<T>* choices[3] because not every Scene has three choices, therefore there is no
need to allocate space for three slots in the choices array. An ending holds a nullptr in choices_, because since it is an ending, it is a leaf and there
are no choices (numChoices is zero) that follow for the player to choose from.

### 3. Walk through your Scene destructor. What gets deleted, and in what order? What would go wrong if choices_ were deleted first?
The Scene destructor first goes through the choices array belonging to the given Scene, where it deletes each child Scene. 
It then deletes the array itself and then the data of the given Scene. If choices_ (the choices array) was deleted first, 
then the destructor would lose access to the child Scene pointers and therefore could no longer delete them, leading to a memory leak.

### 4. Show the path greedy took and the path optimal took on your story, with the loot for each. Explain why greedy lost. If greedy did not lose, change your story until it does, and explain what you changed.
The path greedy took in my garage band story (1-2-1) was deciding to play loud punk, crashing a bigger band's gig as the band's first gig,
and then continuing to play despite security noticing, which results in a total loot of 13. The path optimal took in my story (3-1-1-1-1-1) was deciding to
play moody indie, playing at the local dive bar as the band's first gig, talking to fans after the show, opening the mysterious envelope, 
having coffee with the booker, and then accepting the festival slot, which results in a total loot of 20. Being greedy lost because those 
choices that led to that ending were driven by a desire to get famous and attention quickly, which ultimately led to chaos and being kicked out
of their own band.

### 5. bestLoot tries every path, yet it runs in O(n) time. Explain why it is not exponential, using what you know about paths and leaves in a tree.
bestLoot tries every possible path, but does not run in exponential time because all the paths share scenes within the same tree. Instead of separately
traversing the tree for every possible path, bestLoot uses recursion to visit each Scene and its children to explore all possible outcomes.
Since each Scene is visited only once and there are n total Scenes, it runs in O(n) time.

### 6. Which List methods does your game use, and why? What does one search cost as the bag grows?
My game uses the List methods search, addFront, size, and print, specifically in the play function in Adventure.cpp when dealing with the player's bag/inventory. 
play uses search as it will look to see if an item that is to be added from encountering a scene already exists in the player's bag, addFront is used to add 
an item to the player's bag if it does not already exist, size checks for the number of items in the player's bag, and print prints all the items in the player's bag.
One search costs O(n) as the bag grows, where n represents the number of items currently in the bag. As more and more items are added to the bag, search gets slower.