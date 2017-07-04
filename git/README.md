# Getting Started With Git

## Introduction
Git is a [version control system](https://www.atlassian.com/git/tutorials/what-is-version-control)

### Getting Started
You need to have git installed in your machine. I am going to use linux so skip this part if you've it installed. If not, Google it based on your linux distribution.

#### Step 1 : Creating a repository
Open a terminal and create a folder called `testing_git` on your machine. i.e.

```
> mkdir testing_git
> cd testing_git
> git init  #  initialize git repository
Initialized empty Git repository in /home/kaityln/testing_git/.git/
```

Now you have a repo -- `testing_git` that you are tracking.

#### Step 2 : Adding and committing a file

Open the `testing_git` repo with your favorite text editor. You probably have `gedit` but hey, there's other fancy ones like `Atom` and `Sublime Text` or go dark with `vim` :smiling_imp:

Add a new file `game.py` in your `testing_git` and save.

On the `testing_git` terminal do
```
> git status # Shows the files affected with a change
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	game.py

nothing added to commit but untracked files present (use "git add" to track)
```
This tells you that the file `game.py` is added but UNtracked.

To start tracking it we do
```
> git add game.py
```

Now we are tracking `game.py` :muscle:

So we need to commit that

```
> git commit -m "Add testing_python file."
[master (root-commit) 8b410ae] Add testing_python file.
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 game.py
> git status
On branch master
nothing to commit, working tree clean
```

#### Step 3 : making changes to file, adding new file
Lets write some python. in the file you created, type

```python
import sys
def playRockPaperScissors(player1, player2):
    """Rock, Paper, Scissors game."""
    if player1 == player2:
        return "Tie!"
    # You can even refactor this so that instead of if ... elif ... you
    # do a single statement like
    # if player2 == "p" or player2 == "s"
    # then return the single similar result
    elif player1 == "r":
        if player2 == "p":
            return "Player 1 wins"
        elif player2 == "s":
            return "Player 1 wins"
    elif player1 == "p":
        if player2 == "r":
            return "Player 2 wins"
        elif player2 == "s":
            return "Player 2 wins"
    elif player1 == "s":
        if player2 == "r":
            return "Player 2 wins"
        elif player2 == "p":
            return "Player 1 wins"

# How you run the game
if __name__ == '__main__':
    # something like python xxx r p
    player1 = sys.argv[1]
    player2 = sys.argv[2]  # or you can hook that random move you have implemented here :)
    print playRockPaperScissors(player1, player2)
```
Simple rock, paper, Scissors game.

Run the code.

```{r, engine='bash', code_block_name}
> python game.py r p
Player 1 wins
```
Good code is tested code so,
create  new file `test_game.py` and add the following ```

```python
"""TestCase for rps game."""
import unittest

from homework_2 import playRockPaperScissors


class RPSRelationCase(unittest.TestCase):
    """RPSRelationCase unittest."""

    def test_rock_paper_scissor_function(self):
        """Test the relations between options."""
        # Do the rest of the test cases
        # Remember to also test for invalid arguments depending on
        # how you will refactor your code to handle such situations
        self.assertTrue(playRockPaperScissors("r", "r"), "Tie!")
        self.assertEqual(playRockPaperScissors("r", "p"), "Player 1 wins")


if __name__ == '__main__':
    unittest.main()

```"""TestCase for rps game."""
import unittest

from homework_2 import playRockPaperScissors


class RPSRelationCase(unittest.TestCase):
    """RPSRelationCase unittest."""

    def test_rock_paper_scissor_function(self):
        """Test the relations between options."""
        # Do the rest of the test cases
        # Remember to also test for invalid arguments depending on
        # how you will refactor your code to handle such situations
        self.assertTrue(playRockPaperScissors("r", "r"), "Tie!")
        self.assertEqual(playRockPaperScissors("r", "p"), "Player 1 wins")


if __name__ == '__main__':
    unittest.main()
```

Run our tests
```
> python test
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```

Yay!!! :clap::clap::clap:

Okay.

Next check what changes we've made.

```
> git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:    game.py

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	game.py
	game.pyc
	test_game.py

no changes added to commit (use "git add" and/or "git commit -a")
```

Wow!

Okay so do the usual. Stage the modifications in the file `game.py`.

BUT WAIT!

We have a compiled version of the file, `game.pyc` in our project. We don't want that going out to the project!

Create a file in the directory `testing_git` and name it `.gitignore`. All the files we want ignored will go here.

Add all files that end with `.pyc` in the `.gitignore` file by editing the `.gitignore` file with `*.pyc`

```
> git status #  should not show game.pyc :)
```

Now stage and commit the `test_game.py` file.

We are almost done.

#### Step 4 : Configuring Git
Git needs some basic configuring so that later on when you're working on projects and using it, you don't have to specify obvious information all the time.

```
> git config --global user.email "your_email@example.com"
> git config --global user.name "Your Username"
```

#### Step 5 : Getting project on github

* Create github account
* Create a new repository and DON'T add Read Me.
* In your `testing_git` repository, enter

```
> git remote add origin <repository url>
> git push origin master # will FAIL
```

#### Step 6 : Creating SSH key and Adding it to github
SSH key allows us to connect to github (and any other server that is) securely.

Use [this guide to add SSH key into github](https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/)
 and the re-run `git push origin master`
