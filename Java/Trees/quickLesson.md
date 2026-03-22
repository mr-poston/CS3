# Unit Plan: Introduction to Trees in Java

**Target Audience:** High School Computer Science<br>
**Class Length:** 90 Minutes per block<br>
**Unit Duration:** 4 Days<br>
**Prerequisites:** Basic Java syntax, object instantiation, basic recursion (helpful but will be reviewed).

## Day 1: The "Why" and "What" of Trees (Concepts & Terminology)

**Objective:** Students will be able to define tree terminology, identify tree properties, and distinguish between general trees and binary trees.

### 1. Warm-up: Unplugged Activity (15 mins)

- **Prompt:** Ask students to sketch out the folder structure of their computer's documents, or their family tree going back to their grandparents.

- **Discussion:** Have a few students share. Ask: "How is this different from an Array or an ArrayList?" Guide them to the realization that arrays are a straight line (linear), while these sketches branch out (hierarchical/nonlinear).

### 2. Direct Instruction: Tree Terminology (25 mins)

- Visual Lecture: Draw a large tree on the whiteboard.

- Define and Label:

    - Root: The single top element (no parent).

    - Node / Edge: The circles (data) and lines (connections).

    - Parent / Child / Sibling: The familial relationships between connected nodes.

    - Leaf (External Node): A node with no children (the end of the line).

    - Internal Node: A node with at least one child.

    - Path & Depth: How many steps from the root to a specific node.

- Check for Understanding: Point to random nodes on the board and ask the class to shout out if it's a leaf, root, or internal node. Ask "Who is the parent of this node?"

### 3. Direct Instruction: Binary Trees (15 mins)

- Transition: General trees can have infinite children. In computer science, we often restrict this to make it easier to code.

- The Binary Rule: Every node has at most two children (Left and Right).

- Proper vs. Improper: Draw a "proper" binary tree (every internal node has exactly 2 children) and an "improper" one (some nodes have 1 child).

### 4. Group Activity: Tree Detective (25 mins)

- Task: Break students into small groups. Give them a handout with 5 different diagrams (some linear lists, some general trees, some binary trees, some non-trees/graphs that loop back on themselves).

- Action: For each diagram, they must identify: Is it a tree? Is it a binary tree? Which nodes are leaves? What is the depth of the tree?

### 5. Wrap-up (10 mins)

- Review the handout answers as a class.

- Exit Ticket: "In your own words, why would a programmer choose to use a tree instead of an array?"

## Day 2: Building Trees in Java & Decision Trees

Objective: Students will translate tree concepts into Java code by creating a Node class and manually linking nodes to build a playable Decision Tree game.

1. Warm-up (10 mins)

Prompt: "If we wanted to represent a single 'Node' in Java, what variables would that object need to store?" (Guide them to: the data itself, and variables pointing to the left and right children).

2. Code-Along: The Node Class (20 mins)

Open your IDE and have students follow along. Keep it simple—use String data instead of complex generics for this disrupted year.
```java
public class TreeNode {
    String data;
    TreeNode left;
    TreeNode right;

    public TreeNode(String data, TreeNode left, TreeNode right) {
        this.data = data;
        this.left = left;
        this.right = right;
    }
}
```

Teacher Tip: Explicitly show how left and right are just references (pointers) to other TreeNode objects.

3. Activity 1 Introduction: The Decision Tree (15 mins)

Explain that decision trees are the foundation of early AI (like the Akinator game or spam filters).

The Rule: Internal nodes are Questions (e.g., "Does it have fur?"). Leaf nodes are Answers/Guesses (e.g., "It's a Dog!"). Left = Yes, Right = No.

4. Independent Coding: "Hardcode" a Decision Tree (35 mins)

Task: Students will instantiate TreeNode objects and link them together to create a guessing game.

Step 1: Map out the tree on paper first (at least 3 levels deep).

Step 2: Code it bottom-up (create the leaves first, then the parents, passing the leaves into the parent's constructor).

Step 3: Write a Scanner loop.

Hint for students: Start a currentNode variable at the root. Use a while(currentNode.left != null) loop. Ask the question, get user input, and set currentNode = currentNode.left (or right).

5. Wrap-up (10 mins)

Have students swap computers and play each other's decision trees.

Day 3: Tree Traversals & Recursion

Objective: Students will understand and trace Preorder, Inorder, and Postorder traversals, and use basic recursion to calculate tree properties.

1. Warm-up (10 mins)

Prompt: "If you have 100 folders inside folders on your computer, and you want to print the name of every single file, how would you do it?" (Review the concept of recursion—a method calling itself).

2. Direct Instruction: Traversals (25 mins)

Draw a binary tree with letters in the nodes.

Explain the three Depth-First Traversals using the "flag" method or tracing:

Preorder (Root, Left, Right): Print the node as soon as you touch it.

Inorder (Left, Root, Right): Print the node after visiting its left child, before its right. (Show how this prints binary search trees in alphabetical/numerical order).

Postorder (Left, Right, Root): Print the node only after visiting BOTH children.

Visual tracing: Trace the tree as a class, writing down the output for all three methods.

3. Code-Along: Recursive Traversals (20 mins)

Provide students with a pre-built tree in Java.

Write the preOrder(TreeNode n) method together. Show them how shockingly short the code is:
```java
public void preOrder(TreeNode n) {
    if (n == null) return; // Base case
    System.out.println(n.data); // Root
    preOrder(n.left);           // Left
    preOrder(n.right);          // Right
}
```

Have students write inOrder and postOrder on their own by simply moving the System.out.println line.

4. Activity 3: Calculating Tree Height (25 mins)

Task: Write a recursive method public int getHeight(TreeNode n) that returns the maximum depth of the tree.

Logic Guide for Students: * Base case: If n == null, return 0.

Recursive step: Get the height of the left child, get the height of the right child.

Return: Whichever is bigger (Math.max), plus 1 (for the current node).

5. Wrap-up (10 mins)

Review the getHeight solution. Discuss how this uses a Postorder thought process (you need to know the height of the children before you can determine the height of the parent).

Day 4: Advanced Application - Expression Evaluator

Objective: Students will apply postorder traversal to evaluate mathematical expression trees.

1. Warm-up (10 mins)

Prompt: Write (3 + 5) * 2 on the board. Ask what the answer is, and why. Discuss Order of Operations.

2. Direct Instruction: Math Trees (15 mins)

Show how math equations can be perfectly represented by a proper binary tree.

Rule: Internal nodes are operators (+, -, *, /). Leaves are numbers.

Draw the tree for (3 + 5) * 2. The root is *. Left child is +. The + has children 3 and 5. The * right child is 2.

Explain that the computer evaluates this using Postorder Traversal: It must look at 3 and 5, then apply the +. It takes that result and looks at 2, then applies the *.

3. Activity 2: Expression Evaluator Project (45 mins)

Setup: Provide students with a boilerplate Java file that already constructs the tree:
```java
TreeNode num1 = new TreeNode("3", null, null);
TreeNode num2 = new TreeNode("5", null, null);
TreeNode plus = new TreeNode("+", num1, num2);
TreeNode num3 = new TreeNode("2", null, null);
TreeNode root = new TreeNode("*", plus, num3);
```

Task: Students must write the method public double evaluate(TreeNode n).

Scaffolding/Hints provided to students:

If the node is a leaf (both children are null), convert the String data to a double (Double.parseDouble(n.data)) and return it.

If it is NOT a leaf, recursively call evaluate() on the left child and save it to a variable double leftVal.

Recursively call evaluate() on the right child and save it to double rightVal.

Use an if or switch statement on n.data. If it is "+", return leftVal + rightVal, etc.

4. Group Debugging & Testing (10 mins)

Have students test their code against different math equations. Provide a massive equation on the board, have them hardcode the tree, and see if their program spits out the correct math answer.

5. Unit Wrap-up (10 mins)

Discussion: Ask students to reflect on the unit. What was the hardest part? What was the most interesting?

Mention real-world applications of what they just built: Compilers (how Java turns their code into machine language) use Expression Trees exactly like the one they just built!
