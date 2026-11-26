# The Bakery: objects working together

**Week 2 · Python workshop** · Classes, instances and delegation

So far you've written classes that work on their own. Real programs are made of
several classes whose objects work together: they pass objects to each other and
ask each other to do jobs. In this workshop you'll read a small bakery program
built from a `Cake` and a `Baker`, and then use objects to fill customer orders.

---

## Learning objectives

By the end of this session you can:

1. **Create objects from a class.** Make several objects from one class and
   explain why each one keeps its own data.
2. **Read a class.** Describe what its objects *know* (attributes) and what
   they can *do* (methods).
3. **Make objects work together.** Pass an object into another object's
   method so two classes can cooperate.
4. **Explain delegation.** One object asks another to do a job instead of
   doing it itself, so each class stays in charge of its own data.
5. *Stretch:* **Describe a method precisely.** Name its parameters, what it
   returns and what side effects it has.

---

## How the session runs

| Step | What happens | Who |
|---|---|---|
| **1. Objectives** | We go through the learning objectives above. | Together |
| **2. Read the code** | We read `Cake` and `Baker` in `exercise_1.py` and talk it through. | Together |
| **3. Practise** | Do **Exercise 2: Fill the orders**. If it feels too hard, do the **Exercise 1 tasks** instead. | Solo or in pairs |

---

## Part 1: Read together: `Cake` and `Baker`

Open `exercise_1.py`. There are two classes in it.

| | `Cake` | `Baker` |
|---|---|---|
| **Knows** (attributes) | `flavour`: starts empty<br>`size`: starts at 100 (percent) | `stomach_space_remaining`: starts at 100<br>`cakes_sampled`: a list, starts empty |
| **Can do** (methods) | `set_flavour(flavour)`<br>`take_slice(slice)` | `eat_cake(cake, slice)`<br>`check_space()`<br>`cakes()`<br>`choose_favourite()` |

### Delegation in one method

```python
def eat_cake(self, cake, slice):
    cake.take_slice(slice)          # the Baker asks the Cake to shrink itself
    if cake in self.cakes_sampled:
        print("You've tried this one already!")
    else:
        self.cakes_sampled.append(cake)
        self.stomach_space_remaining -= slice
```

The `Baker` never writes `cake.size -= slice` itself. It **delegates** that job
to the cake by calling `cake.take_slice(slice)`. Only the `Cake` changes its own
size. The `Baker` only changes the `Baker`'s data.

### Talk it through

- Where does the `cake` passed into `eat_cake` come from? Who has to create it first?
- What does `self` mean inside `take_slice`? And inside `eat_cake`?
- What's stored in `cakes_sampled`: flavour words, or whole cake objects? How does `cakes()` get the flavours back out?
- If we make two cakes and slice one, what happens to the other? Why?
- Eat the same cake twice. What happens to the cake? What happens to the baker's stomach? Is that fair?

---

## Part 2: Exercise 2: Fill the orders

Customers are placing orders. Each order wants a cake of a particular
**flavour** and **size**. Make a cake that matches and hand it over. Keep going
until the shop opens.

**Run it:**

```bash
python3 -i exercise_2.py
```

(Or `ipython -i exercise_2.py` if you use IPython.) The `-i` keeps Python open
after the file runs, so you can type commands and play.

**Where to start.** Work through these questions in order:

1. An order is already waiting in a variable called `order`. What does it want?
   Try `order.flavour` and `order.size`.
2. Which class in the file lets you make a cake? How do you create one?
3. How do you give your cake the right flavour?
4. A new cake is always size 100. How big a slice do you need to take so that
   what's left matches the order?
5. Which method on `Order` takes a cake? Give your cake to it.
6. When an order is satisfied, a new one replaces it in `order`. Check it again
   and repeat.

**Watch out:**

- Match the flavour exactly, capitals included: `"Chocolate"`, not `"chocolate"`.
- Every cake starts at 100. Make a new cake for each order.
- The game pauses for a few seconds after each correct answer. Be patient.

### Stuck? Do the Exercise 1 tasks instead

Run `python3 -i exercise_1.py` and try these in order:

1. Make two cakes. Give them different flavours. Check each one's `flavour`.
2. Take a slice from one cake. Check the `size` of both cakes.
3. Make a `Baker`. Have them eat a slice of each cake. Look at
   `baker.cakes_sampled` and `baker.stomach_space_remaining`.
4. Make the baker eat the same cake twice. What changed, and what didn't?
5. Bake a few more cakes with new flavours and have the baker eat them. Then
   call `baker.choose_favourite()`.
6. Call `baker.check_space()`. Careful: when the shop opens or the baker
   passes out, the program ends and closes Python.

---

## Stretch: Complete the function signature template

In `exercise_1.py`, the `Cake` methods have an empty template above them. Fill
it in, then add one above every `Baker` method too. Here is one done for you:

```python
# Parameters:
#  - flavour: a string, e.g. "Lemon"
# Returns:
#  - nothing
# Side effect:
#  - sets this cake's flavour attribute
def set_flavour(self, flavour):
    self.flavour = flavour
```

A **side effect** is anything a method changes or does besides returning a
value, for example changing an attribute or printing to the screen.

---

## Words to know

| Word | Meaning |
|---|---|
| **Class** | The recipe. It describes what its objects know and can do. `Cake` is a class. |
| **Object / instance** | A thing made from the class. `my_cake = Cake()` makes one. |
| **Instantiate** | To make an object from a class by calling it: `Cake()`. |
| **Attribute** | Data an object keeps, like `my_cake.flavour`. |
| **Method** | A function that belongs to a class, like `my_cake.take_slice(20)`. |
| **`self`** | Inside a method, the object the method was called on. |
| **Delegation** | Asking another object to do a job instead of doing it yourself. |
