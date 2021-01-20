# Quickstart & Cheatsheets

This is a quickstart & cheatsheet guide for `git` and `python3`

# GIT

## Preliminary setup - SSH keys

### MacOS & Linux

---
**For MacOS users:**

* be sure to have the developer-tools installed: `xcode-select --install`
* the [brew](https://brew.sh/) package manager can always come in handy. Install it by running
```shell
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```
* use it to install missing MacOS packages. E.g., `openssl` is highly reccommended. Install it by running `brew install openssl`

----

First let's configure ssh keys to interact with git without the need to authenticate ourselves each time.
Open up a terminal window and run

```shell
ssh-keygen -t rsa
```

You'll get the following output. You can leave everything as default and also omit the passphrase for convenience:

```shell
Enter file in which to save the key (/Users/tony/.ssh/id_rsa):
Created directory '/Users/tony/.ssh'.
Enter passphrase (empty for no passphrase):
Enter same passphrase again:
Your identification has been saved in /Users/tony/.ssh/id_rsa.
Your public key has been saved in /Users/tony/.ssh/id_rsa.pub.
```

Now your public key is saved in `~/.ssh/id_rsa.pub`. You need to copy the content of that file. To do so, run:

```shell
pbcopy < ~/.ssh/id_rsa.pub
```

Now your public key is copied to your clipboard. Go to your [GitHub Key settings page](https://github.com/settings/keys)
or [GitLab Key settings page](https://gitlab.com/-/profile/keys) and add your newly created public key.

You can now interact with remote repositories with ssh without the need to authenticate each time.
Be sure to use ssh addresses for the repos:

* **https**: `https://github.com/Develawpers/name-of-the-repo.git` <-- NO
* **ssh**: `git@github.com:Develawpers/name-of-the-repo.git` <-- YES

### Winzoz (coming soon)

## Preliminary stup - Default user & editor

First of all, to avoid being trapped in `VIM`, set `nano` as a default text editor:

```shell
git config --global core.editor "nano"
```

If you don't run the following commands, at the first interaction with the remote repo you'll be asked to 
edit the configuration file:

```shell
git config --global user.name “[firstname lastname]”
```

and

```shell
git config --global user.email “[valid-email]”
```

## (Very) basic usage

---

When creating a repo via the web interface, be sure to include a README.md file
so you can clone the repo and start working on it right away, without worring about initializing it yourself.

Most of the following was blatanlty stolen from [here](https://education.github.com/git-cheat-sheet-education.pdf)

For the time being, you can focus on the basic commands.

* clone the repo: `git clone git@github.com:Develawpers/name-of-the-repo.git`

* (Then, be sure to get into the repo's directory: `cd name-of-the-repo`)

---

### README and .gitignore

* `README.md` is a file such as this one, where a description and basic instruction are provided.
  It's the first thing a user reads and a rendered version of it is the first thing displayed by GitHub, GitLab or BitBucket
  
* `.gitignore` is a file that tells `git` which files or directories to ignore.
  GitHub offers some templates [here](https://github.com/github/gitignore) but also offers you to select one when creating a repo

### Stage and snapshot

* `git status`: show modified files in working directory, staged for your next commit
  
* `git add [file]`: add a file as it looks now to your next commit (stage)

* `git reset [file]`: unstage a file while retaining the changes in working directory

* `git diff`: diff of what is changed but not staged

* `git diff --staged`: diff of what is staged but not yet commited

* `git commit -m “[descriptive message]”`: commit your staged content as a new commit snapshot

### Share and update

* `git push [alias] [branch]`: Transmit local branch commits to the remote repository branch

* `git pull`: fetch and merge any commits from the tracking remote branch

### Branch and merge

* `git branch`: list your branches. a * will appear next to the currently active branch

* `git branch [branch-name]`: create a new branch at the current commit

* `git checkout`: switch to another branch and check it out into your working directory

* `git merge [branch]` merge the specified branch’s history into the current one

* `git log`: show all commits in the current branch’s history

pro-tip: use `git checkout -b [branch name]` to create a new branch at the current commit and switch to it

# Python

Blatantly stolen from [here](https://github.com/biagiodistefano/python-cheatsheet)

A simple cheatsheet for python beginners.

Be sure to download python **at least** version 3.6 from [here](https://www.python.org/downloads/)

## Virtual environment

First things first. It is good practice to work in a virtual environment.
This way, you can work on multiple projects with different dependencies
without causing a mess.

Create the environment:

`python3 -m venv venv`

Load the environment:

`source venv/bin/activate`


## Style matters

Readability counts. Your coding style should be PEP-8 compliant,
unless you absolutely need to do something different, e.g. when using
some libraries that require so.

A few examples:

```python
def my_cool_function():  # very_good
    pass


def myCoolFunction():  # veryBad
    pass
    
```

**There are two empty lines between the functions in the main code**

Same goes for variables:

```python
my_variable = 10  # very_good
myVariable = 10  # veryBad

```

For classes, it is quite the opposite. UpperCamelCase should be used.

```python
class MyCoolClass:  # VeryGood
    pass


class my_cool_class:  # very_bad
    pass
    
```

**There are two empty lines between the classes in the main code**


Use uppercase for "constants" (Python doesnt really have costants)

```python
MY_COSTANT = 10  # VERY_NICE
my_costant = 10  # very_bad

```

**To add comment next to a line of code, let `#` be preceded by _two_ spaces**


## Use __main__

To have a clean code that runs like `python myscript.py`, dont just put code
into the file, organize it neatly

```python
def first_function():
    pass
    

def second_function():
    pass
    

if __name__ == '__main__':
    first_function()
    second_function()

```

Always end a script with a new line

## Do not shadow names

Python has some builtin variables and functions. DO NOT SHADOW THEM.

e.g.:

```python
file = "my/file.txt"  # very, very bad

def open(path):  # I think I might die for this
    pass

```

Shadowing can also be a matter of scope:

```python
def add(a, b):
    c = 2  # shadows 'c' from outer scope
    return a + b + c
    
if __name__ == "__main__":
    c = 10
    print(add(1, 2))

```


## Beware of objects' reference behavior

```python
my_list = [1, 2, 3]
my_new_list = my_list

my_new_list.append(4)

print(my_list)
# >>> [1, 2, 3, 4]

```

**Same goes for `dict`, `classes` and in general any other object**

So, to actually copy:

```python
my_list = [1, 2, 3]
my_other_list = my_list.copy()
# or
my_other_list = my_list[:]

```

But beware, if inside the list are contained other objects, this wont work:

```python
my_dict = dict(a=1, b=2)
my_list = [1, 2, my_dict]
my_other_list = my_list.copy()
my_dict["b"] = 5

print(my_other_list)
# >>> [1, 2, {'a': 1, 'b': 5}]

```

To avoid this problem, use deepcopy from the copy library

```python
import copy

my_dict = dict(a=1, b=2)
my_list = [1, 2, my_dict]
my_other_list = copy.deepcopy(my_list)
my_dict["b"] = 5

print(my_other_list)
# >>> [1, 2, {'a': 1, 'b': 3}]

```

## Some neat tricks

### enumerate
Sometimes you may want to get the index and the value in a list

```python
my_list = ["a", "b", "c"]
for i, c in enumerate(my_list):
    print(i, c)

# >>> 0, 'a'
# >>> 1, 'b'
# >>> 2, 'c'
```

### zip

Sometimes you may want to iterate two lists at once
```python
first_list = [1, 2, 3]
second_list = ["a", "b", "c"]

for x, y in zip(first_list, second_list):
    print(x, y)

# >>> 1, 'a'
# >>> 2, 'b'
# >>> 3, 'c'
```


### dicts

#### Use get

Sometimes you are not sure if a dictionary has a certain key

```python
my_dict = dict(a=1, b=2, c=3)

# DONT:
if "a" in my_dict.keys():
    v = my_dict["a"]
    
# DO:
v = my_dict.get("a")

v = my_dict.get("z")  # returns None

v = my_dict.get("x", 10)  # the second value will be returned if the given key is not present

```

#### use items()

Sometimes you may need to iterate over keys and values

```python
my_dict = dict(a=1, b=2, c=3)
for key, value in my_dict.items():
    print(key, value)

```

### Collections

[Please explore the library here](https://docs.python.org/3.7/library/collections.html)

#### use defaultdict

Sometimes you may need to dynamically build a complex dict

DONT:
```python
d = dict()
d["a"] = []
d["a"].append(1)

```

DO:
```python
from collections import defaultdict

d = defaultdict(list)
d["a"].append(1)

```

If you REALLY, REALLY need a complex dict dynamically built, you
can use nested defaultdicts with lambda functions

```python
from collections import defaultdict

my_ddict = defaultdict(lambda : defaultdict(list))
my_ddict["a"]["x"].append(1)

```

#### use Counter
```python
from collections import Counter

def count_stuff(my_string):
    alph = Counter()
    for char in my_string:
        alph[char] += 1
    return alph
    
# or EVEN BETTER:

def count_stuff(my_string):
    return Counter(my_string)
    
```

### for-else

You can use `else` to close a for loop. The `else` is triggered if the `for` loop finishes without `break`ing.

```python
for c in ['a', 'b', 'c', 'd']:
    if c == 'c':
        break
else:
    print('loop finished without breaking')  # <-- does not get triggered
```
In the case above the loop breaks when `c == 'c'`, so `else` is not triggered.
```python
for c in ['a', 'b', 'c', 'd']:
    if c == 'e':
        break
else:
    print('loop finished without breaking')  # <-- does not get triggered
```
In the case above the `else` gets triggered, because `c` is never equal to `'e'`

## Write classes like a pro

### Coming soon
