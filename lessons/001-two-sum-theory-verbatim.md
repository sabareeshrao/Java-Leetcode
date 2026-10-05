# 🐼 Lesson 1 — Your First LeetCode Problem: Learning How to Think

**JAVA LEETCODE INTERVIEW WORLD · LESSON 001**

**Today's interview problem:** LeetCode 1 — Two Sum  
**Current level:** New graduate · Java basics · Zero LeetCode experience

**Characters:**  
🐯 **Mentor** — experienced Java developer and coding-interview mentor  
🐼 **Student** — recent graduate who knows basic Java but has no LeetCode practice

---

## 🐯 Step 1 — Before we touch LeetCode

**Mentor:** Before I give you a problem, tell me what happens when you normally see a coding interview question.

**Student:** Usually I read it and don't know where to start.

Then if I see the solution, it makes sense.

But I don't think I could discover that solution myself.

**Mentor:** Good. That's the exact problem we're going to work on.

For now, I don't care how many LeetCode problems you complete.

Someone can memorize 200 solutions and still struggle when an interviewer changes the question slightly.

I want you to develop this ability:

```text id="faqzkw"
Unknown Problem
      ↓
Understand it
      ↓
Find a simple solution
      ↓
Notice what's inefficient
      ↓
Improve that specific weakness
      ↓
Explain the final solution
```

**Student:** So we're not starting by memorizing patterns?

**Mentor:** Correct.

Patterns will come.

But first you need to understand **why a pattern becomes useful**.

Today we'll use one of the most famous interview problems to learn that process.

---

# 🦊 Step 2 — The interviewer gives us Two Sum

**Mentor:** Imagine you're in an interview.

The interviewer says:

> Given an integer array `nums` and an integer `target`, return the indices of two numbers whose values add up to `target`.

You cannot use the same element twice.

You can assume exactly one valid answer exists.

Example:

```text id="exkty8"
nums   = [2, 7, 11, 15]
target = 9
```

Expected output:

```text id="fjmvus"
[0, 1]
```

**Student:** I've heard of Two Sum.

I think we're supposed to use a HashMap.

**Mentor:** Forget that for a moment.

Pretend you've never seen this problem.

Let's understand what the interviewer actually wants.

---

# 🐨 Step 3 — Understand the input before solving anything

**Mentor:** Here's our array:

```text id="v3062f"
Index:    0   1    2    3
          ↓   ↓    ↓    ↓
nums =   [2,  7,  11,  15]
```

And:

```text id="2c61xn"
target = 9
```

What are we trying to find?

**Student:** Two numbers whose sum is `9`.

**Mentor:** Correct.

Which two?

**Student:**

```text id="1wnhuk"
2 + 7 = 9
```

So `2` and `7`.

**Mentor:** What should we return?

**Student:** `[2, 7]`?

**Mentor:** Look at the requirement again.

It doesn't ask for the **values**.

It asks for the **indices**.

```text id="hy9ulh"
Value:    2    7
Index:    0    1
```

Therefore:

```text id="kmmj03"
return [0, 1]
```

**Student:** Okay. That's an important distinction.

**Mentor:** Very important.

Your first habit for every LeetCode problem should be:

```text id="s3yr5l"
What am I GIVEN?
      ↓
What am I trying to FIND?
      ↓
What exactly must I RETURN?
```

For Two Sum:

```text id="zjfb76"
GIVEN
nums + target

      ↓

FIND
two different elements
whose values add to target

      ↓

RETURN
their indices
```

Don't write code until that is clear.

---

# 🐯 Step 4 — Solve it like a human first

**Mentor:** Now forget optimization.

Suppose I physically wrote these numbers on paper:

```text id="m63q7e"
[2, 7, 11, 15]
```

How could you find two numbers that make `9`?

**Student:** I'd start with `2`.

Then try adding it to the other numbers.

**Mentor:** Do it.

**Student:**

```text id="45dhsg"
2 + 7 = 9
```

Found it.

**Mentor:** Excellent.

Let's make the example slightly harder.

```text id="j9um4e"
nums   = [3, 2, 4]
target = 6
```

Start with `3`.

**Student:**

```text id="v7tpc5"
3 + 2 = 5 ❌

3 + 4 = 7 ❌
```

Neither works.

Then I move to `2`.

```text id="jowlxk"
2 + 4 = 6 ✅
```

So the answer is:

```text id="tpg5es"
[1, 2]
```

**Mentor:** Perfect.

Notice something important.

You just created an algorithm without knowing any LeetCode trick.

Your algorithm is basically:

```text id="8lpl3f"
Take first number
      ↓
Try it with every number after it

Take second number
      ↓
Try it with every number after it

Continue until target is found
```

That's our **brute-force solution**.

---

# 🐼 Step 5 — Convert your human solution into Java

**Student:** Since I need to compare pairs, I'm guessing we need two loops.

**Mentor:** Exactly.

Let's write only what we understand.

```java id="uzcf4p"
for (int i = 0; i < nums.length; i++) {

    for (int j = i + 1; j < nums.length; j++) {

        if (nums[i] + nums[j] == target) {
            return new int[]{i, j};
        }
    }
}
```

**Student:** I understand `i`, but why does `j` start at:

```java id="hfz5ie"
i + 1
```

?

**Mentor:** Let's visualize it.

Suppose:

```text id="x5n3k0"
i = 0
```

Then:

```text id="hz8jbo"
nums[i] = nums[0] = 3
```

If `j` also started at `0`, our first comparison would be:

```text id="qa6bp9"
nums[0] + nums[0]

3 + 3
```

We're using the **same element twice**.

But the problem doesn't allow that.

So when:

```text id="v46wm2"
i = 0
```

we start:

```text id="mp72i3"
j = 1
```

When:

```text id="s6nl53"
i = 1
```

we start:

```text id="zlgdg6"
j = 2
```

Visually:

```text id="pdpehz"
[3, 2, 4]
 ↑  ↑
 i  j
```

Then:

```text id="xiy9zc"
[3, 2, 4]
 ↑     ↑
 i     j
```

Then:

```text id="6k52tu"
[3, 2, 4]
    ↑  ↑
    i  j
```

Every useful pair gets checked.

---

# 🦊 Step 6 — Dry-run the brute-force solution

Let's use:

```text id="pkakj9"
nums   = [3, 2, 4]
target = 6
```

First:

```text id="u5doee"
i = 0
j = 1

nums[i] = 3
nums[j] = 2

3 + 2 = 5
```

Not `6`.

Move `j`:

```text id="9doczb"
i = 0
j = 2

3 + 4 = 7
```

Still not `6`.

Now `i` moves:

```text id="7q9zig"
i = 1
j = 2

2 + 4 = 6
```

Found it.

Therefore:

```java id="om2535"
return new int[]{1, 2};
```

**Student:** So technically we've already solved Two Sum.

**Mentor:** Yes.

That's important.

Your brute-force solution is not "wrong."

It is:

**correct but inefficient.**

Interview optimization becomes much easier when you first have a correct solution.

---

# 🐯 Step 7 — Why is brute force considered slow?

**Student:** Is it because we're using nested loops?

**Mentor:** That's what many people memorize.

I want you to understand what's actually happening.

Imagine the array contains many numbers.

For the first number, we potentially search almost the entire remaining array.

```text id="71rt05"
Number 1
   ↓
check many numbers
```

Then for the second:

```text id="zj3xk8"
Number 2
   ↓
check many numbers
```

Then again:

```text id="nmwpqt"
Number 3
   ↓
check many numbers
```

We're repeatedly searching.

For `n` elements, the number of comparisons grows roughly like:

```text id="4l882o"
n × n
```

So we describe the time complexity as:

```text id="sd1ybn"
O(n²)
```

**Student:** So I shouldn't just memorize:

> nested loop = O(n²)

**Mentor:** Correct.

You should understand:

> For many elements, I'm repeatedly comparing one element against many other elements.

That's the expensive work.

Now we have something useful to optimize.

---

# 🐨 Step 8 — Ask a better question

**Mentor:** Go back to:

```text id="dm9m5d"
nums   = [2, 7, 11, 15]
target = 9
```

Suppose our current number is:

```text id="uzsb9z"
2
```

Instead of asking:

> "Which number should I pair with 2?"

we can calculate exactly what we're looking for.

We know:

```text id="l57jbj"
2 + ? = 9
```

What is `?`?

**Student:** `7`.

**Mentor:** How did you calculate it?

**Student:**

```text id="01qpdo"
9 - 2 = 7
```

**Mentor:** Exactly.

So:

```text id="d7tfxb"
target - currentNumber = numberNeeded
```

We usually call the number we need the **complement**.

In Java:

```java id="99jeyr"
int complement = target - nums[i];
```

If:

```text id="uhu5wq"
target = 9
nums[i] = 2
```

then:

```text id="hgam1i"
complement = 9 - 2
           = 7
```

Our question has changed.

Before:

```text id="unv5l1"
Try current number against many other numbers.
```

Now:

```text id="eeiedj"
I know EXACTLY which number I need.
```

That's a major improvement in our thinking.

---

# 🐯 Step 9 — But we still have a problem

**Student:** Okay.

If I know I need `7`, can't I search the array for `7`?

**Mentor:** You could.

But what happens for the next number?

**Student:** I'd search again.

**Mentor:** Exactly.

Then again.

And again.

We haven't really eliminated repeated searching.

So now ask:

> Can we remember numbers we've already seen in a structure that lets us check them quickly?

**Student:** Is this where the HashMap comes in?

**Mentor:** Exactly.

Now you have a **reason** for using it.

---

# 🦊 Step 10 — Imagine the HashMap as a notebook

**Mentor:** Imagine you're walking through the array carrying a notebook.

Whenever you see a number, write:

```text id="u2e8pv"
number → index
```

Suppose you first see:

```text id="ygsmzy"
2
```

at index:

```text id="hm0za6"
0
```

Write:

```text id="7jn8mc"
2 → 0
```

Now you reach:

```text id="k5d2kn"
7
```

at index:

```text id="nb1tfg"
1
```

Before writing it down, calculate:

```text id="z3f9tg"
target - current

9 - 7 = 2
```

Then ask your notebook:

> Have I already seen `2`?

Your notebook contains:

```text id="hnicrv"
2 → 0
```

Yes.

So:

```text id="ruq7f3"
previous number index = 0
current number index  = 1
```

Return:

```text id="baff2p"
[0, 1]
```

**Student:** So the HashMap isn't some special Two Sum trick.

We need it because we want to remember previous values and find them quickly.

**Mentor:** Exactly.

That's the important lesson.

---

# 🐼 Step 11 — What goes inside the HashMap?

We create:

```java id="vs0cy0"
Map<Integer, Integer> map = new HashMap<>();
```

**Student:** Both sides say `Integer`.

How do I know what each one represents?

**Mentor:** For this problem:

```text id="qry5mx"
KEY     → VALUE

number  → index
```

Example:

```text id="q1wd9v"
2 → 0
7 → 1
```

Therefore:

```java id="y25coh"
map.put(nums[i], i);
```

means:

> Store the current number as the key and its index as the value.

If:

```text id="knwjph"
i = 0
nums[i] = 2
```

then:

```java id="s8f6p2"
map.put(2, 0);
```

and conceptually our map becomes:

```text id="pcqt65"
{2=0}
```

---

# 🐯 Step 12 — Build the optimized solution one piece at a time

First create our memory:

```java id="qo6eh5"
Map<Integer, Integer> map = new HashMap<>();
```

Then visit each number:

```java id="e7d0es"
for (int i = 0; i < nums.length; i++) {
```

Calculate what we need:

```java id="p6h6xc"
int complement = target - nums[i];
```

Ask whether we've already seen it:

```java id="ykef5m"
if (map.containsKey(complement)) {
```

If yes, return its index and our current index:

```java id="kxrgim"
return new int[]{map.get(complement), i};
```

Otherwise remember the current number:

```java id="fmkso6"
map.put(nums[i], i);
```

Put everything together:

```java id="hd7mn1"
import java.util.HashMap;
import java.util.Map;

class Solution {

    public int[] twoSum(int[] nums, int target) {

        Map<Integer, Integer> map = new HashMap<>();

        for (int i = 0; i < nums.length; i++) {

            int complement = target - nums[i];

            if (map.containsKey(complement)) {
                return new int[]{map.get(complement), i};
            }

            map.put(nums[i], i);
        }

        return new int[]{};
    }
}
```

**Student:** This looks much easier now than if you had shown me the code at the beginning.

**Mentor:** That's exactly how I want you to learn algorithms.

The code should be the **result of our reasoning**, not the starting point.

---

# 🦊 Step 13 — Dry-run the HashMap solution

Let's trace:

```text id="mdf9be"
nums   = [2, 7, 11, 15]
target = 9
```

Initially:

```text id="nbul44"
map = {}
```

### First iteration

```text id="n8aroh"
i = 0
nums[i] = 2
```

Calculate:

```text id="qsduqz"
complement = 9 - 2
           = 7
```

Ask:

```text id="ni7zuv"
Does map contain 7?
```

Current map:

```text id="5x4tn6"
{}
```

No.

So store:

```text id="ox4ar5"
2 → 0
```

Now:

```text id="49ltcl"
map = {2=0}
```

---

### Second iteration

Now:

```text id="lpff7k"
i = 1
nums[i] = 7
```

Calculate:

```text id="z7k36e"
complement = 9 - 7
           = 2
```

Ask:

```text id="ze8cdd"
Does map contain 2?
```

Our map:

```text id="lmy58c"
{2=0}
```

Yes.

Get its index:

```text id="ev20k8"
map.get(2)
     ↓
     0
```

Current index:

```text id="hvehf5"
i = 1
```

Therefore:

```text id="igug72"
return [0, 1]
```

Done.

---

# 🐨 Step 14 — Let's deliberately try to break it

**Mentor:** Consider this:

```text id="szerg6"
nums   = [3, 3]
target = 6
```

Some beginners get nervous because the values are identical.

Can our solution handle it?

**Student:** Let's trace it.

Initially:

```text id="xj9mfx"
map = {}
```

First number:

```text id="p0sxxh"
i = 0
nums[i] = 3
```

Complement:

```text id="hdkvcz"
6 - 3 = 3
```

Does the map contain `3`?

No.

Store:

```text id="6unnt9"
3 → 0
```

Now:

```text id="8km5rz"
map = {3=0}
```

Second number:

```text id="7ceovo"
i = 1
nums[i] = 3
```

Complement:

```text id="wbmq8g"
6 - 3 = 3
```

Now the map contains `3`.

Its stored index is `0`.

Current index is `1`.

So:

```text id="jxdt9s"
return [0, 1]
```

**Mentor:** Perfect.

---

# 🐯 Step 15 — There's a subtle reason our code works

Look carefully at this order:

```java id="mxl1ro"
if (map.containsKey(complement)) {
    return new int[]{map.get(complement), i};
}

map.put(nums[i], i);
```

We:

```text id="jabjms"
CHECK
  ↓
STORE
```

Why don't we do:

```text id="zouq7v"
STORE
  ↓
CHECK
```

?

Consider:

```text id="ng3j59"
nums   = [3, 3]
target = 6
```

At index `0`:

```text id="9ig2xd"
current = 3
complement = 3
```

If we stored first:

```text id="yovhqu"
3 → 0
```

and immediately asked:

```text id="xccghi"
Does the map contain 3?
```

Yes!

But that's the exact same element we just inserted.

We could accidentally try to use:

```text id="ij6jug"
index 0 + index 0
```

The problem explicitly says:

> You cannot use the same element twice.

That's why our algorithm naturally follows:

```text id="0ed7ji"
Calculate complement
        ↓
Check previous values
        ↓
If not found
        ↓
Store current value
```

---

# 🦊 Step 16 — Time complexity

**Student:** Our first solution was:

```text id="zdgkho"
O(n²)
```

What about this one?

**Mentor:** We walk through the array once:

```text id="6ga36j"
for each element
```

For each element we perform HashMap operations such as:

```java id="32bfxs"
map.containsKey(...)
map.get(...)
map.put(...)
```

HashMap lookup/insertion is **O(1) on average**.

So for `n` elements:

```text id="u307c6"
Time Complexity

O(n)
```

**Student:** But we're storing numbers now.

**Mentor:** Exactly.

In the worst case, our map can contain roughly `n` entries.

Therefore:

```text id="k6v6uv"
Space Complexity

O(n)
```

Compare them:

| Approach | Time | Extra Space |
|---|---:|---:|
| Brute Force | O(n²) | O(1) |
| HashMap | O(n) average | O(n) |

**Student:** So we're spending additional memory to reduce the amount of searching.

**Mentor:** Exactly.

And that's a much bigger interview concept than Two Sum:

```text id="kbenqy"
Extra Memory
     ↓
Remember useful information
     ↓
Avoid repeated work
     ↓
Faster algorithm
```

That's called a **time-space trade-off**.

---

# 🐼 Step 17 — What pattern did we actually learn?

**Student:** So should I remember:

```text id="bcup38"
Two Sum → HashMap
```

?

**Mentor:** That's useful, but too shallow.

Remember this reasoning:

```text id="dfvudd"
I have a current value.
        ↓
I can calculate exactly what other value I need.
        ↓
I need to know whether I've already seen that value.
        ↓
I need fast lookup.
        ↓
HashMap
```

For Two Sum:

```text id="bg281v"
current = 7
target  = 9

        ↓

needed = target - current

        ↓

needed = 2

        ↓

Have I seen 2?

        ↓

HashMap says YES

        ↓

Return both indices
```

That's your first real interview pattern.

---

# 🎯 Interview Simulation

**Interviewer:** How would you solve Two Sum?

**Student:** I would first clarify that I need to return the indices of two different elements whose values add up to the target.

A straightforward solution is to use two nested loops and check every possible pair. That works, but it takes `O(n²)` time.

To optimize it, for each number I calculate the complement:

```text id="mh3plz"
target - currentNumber
```

I use a HashMap to store numbers I've already visited along with their indices.

Before storing the current number, I check whether its complement already exists in the map. If it does, I return the stored index and the current index.

Since I traverse the array once and HashMap lookup is `O(1)` on average, the optimized solution takes `O(n)` time and `O(n)` extra space.

**Mentor:** Good.

Notice that you didn't merely say:

> "I use a HashMap."

You explained **why**.

That's what I want from you in interviews.

---

# 🧠 Lesson 1 Memory Chain

```text id="k3nph2"
Understand Input/Output
        ↓
Solve It Somehow
        ↓
Brute Force
        ↓
Notice Repeated Searching
        ↓
current + ? = target
        ↓
? = target - current
        ↓
Remember Previous Values
        ↓
HashMap
        ↓
O(n²) → O(n)
```

---

# 📘 Lesson 1 — Test Your Understanding

Don't search for the answers. Don't worry about interview-quality wording yet.

I want to see **how you're thinking**.

### Question 1

Given:

```text id="t2ue39"
nums   = [4, 6, 2, 8]
target = 10
```

Which indices could the algorithm return, and why?

---

### Question 2

Why does the brute-force solution take `O(n²)` time?

Don't simply answer:

> "Because there are two loops."

Explain what repeated work those loops are performing.

---

### Question 3

Given:

```text id="bhixlb"
nums   = [3, 2, 4]
target = 6
```

Trace the optimized algorithm yourself.

Show:

```text id="co05ld"
current number
complement
map before lookup
what gets stored
```

until the answer is found.

---

### Question 4

Why does our code do this:

```java id="z3fdc7"
if (map.containsKey(complement)) {
    return new int[]{map.get(complement), i};
}

map.put(nums[i], i);
```

instead of putting the current number into the map **before** checking the complement?

Explain what could go wrong.

---

### Question 5 — Most Important

Forget the name **Two Sum**.

Imagine you've never seen this problem before.

Explain in your own words:

> **What problem in our brute-force approach caused us to introduce a HashMap?**

If you understand that answer, you've learned much more than just one LeetCode solution.

---

# 📊 Lesson 1 Progress

```text id="0qjwo8"
JAVA LEETCODE INTERVIEW WORLD

Lesson:                 001
Problem:                LeetCode 1 — Two Sum
Difficulty:             Easy

Problems presented:     1
Problems understood:    0
Problems solved alone:  0

Concepts introduced:
✓ Reading input/output carefully
✓ Brute-force thinking
✓ Identifying repeated work
✓ Complement thinking
✓ HashMap lookup
✓ Time complexity
✓ Space complexity
✓ Time-space trade-off

Pattern introduced:
HashMap / Complement Lookup

Status:
AWAITING UNDERSTANDING
```

🐯 **Mentor:** This is where Lesson 1 stops.

You do **not** need to rush to the next LeetCode problem.

You can answer the five questions above and I'll examine your reasoning with you. If one part is unclear, ask me about that exact part and we'll stay on Lesson 1.

Once you genuinely understand it, simply say:

**`Understood`**

Then I will preserve **this exact Lesson 1 without rewriting it** in `Java-Leetcode`, update our progress tracker so future sessions know exactly what you've covered, and only then move us to **Lesson 2**.