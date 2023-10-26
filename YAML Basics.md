# Ansible - YAML Basics
YAML (YAML Ain't Markup Language) is a human-readable data serialization format that is often used in Ansible for creating playbooks. It's designed to be simple and easy for humans to work with, making it a popular choice for configuration files. Let's break down the basics of YAML with an example for beginners.

## Key-value pair
In YAML, you create data structures using key-value pairs, and indentation is crucial to represent the structure. Here's a simple example of a student record in YAML:
**Copy code**
```yaml
student:
  name: John Doe
  age: 20
  major: Computer Science
  grades:
    - subject: Math
      score: 95
    - subject: History
      score: 88
```
Let's break this down:
1. `name` is the key, and `John Doe` is the value. This key-value pair represents the student's name.
2. `age` is the key, and `20` is the value. Here, the key-value pair represents the student's age.
3. `major` is the key, and `Computer Science` is the value, representing the student's major.
4. The document starts with `---`, which is optional and used to indicate the beginning of a YAML document.
5. We define a dictionary or key-value pair named `student`. The key (in this case, "student") is followed by a colon and a space.
6. The student's details are represented as nested key-value pairs, indented with spaces. For example, `name: John Doe` indicates the student's name is "John Doe."
7. The grades field is also a dictionary, but it has a list of subjects and scores. This is represented using a hyphen - followed by a space for each item in the list. For example, `- subject: Math` indicates the subject is "Math," and the student's score is 95.
   - In YAML, the hyphen (`-`) is used to indicate the beginning of a list or sequence. It represents individual elements in a list or an array. In the example you provided:
     **Copy code**
    ```yaml
    grades:
      - subject: Math
        score: 95
      - subject: History
        score: 88
    ```
    The hyphen before each item (e.g., `- subject: Math`) signifies that you are creating a list of dictionaries or key-value pairs. In this case, you have a list of "grades," and each grade is represented as a dictionary with two key-value pairs: "subject" and "score."

    So, the use of the hyphen (`-`) in YAML is a way to define sequences or lists of items within your data structure. It's an essential part of YAML's syntax for creating arrays or ordered collections of data.

Here's a breakdown of the structure:
- The outermost level represents the "student" dictionary.
- Within "student," you have key-value pairs for name, age, major, and grades.
- The "grades" field contains a list of dictionaries, each representing a subject and a score.

Remember that in YAML, spaces and indentation are critical for defining the structure. It's also essential to use colons and dashes correctly. YAML's simplicity and readability make it a good choice for creating Ansible playbooks, as it's easy for both humans and automation to understand.

### Abbreviation
In YAML, you can use an abbreviation to represent dictionaries, which are collections of key-value pairs. This abbreviation makes it even simpler to define data structures. Let's illustrate this concept with a beginner-friendly example.

Instead of explicitly stating "key: value" for each pair, you can use an abbreviation by listing the key and its associated value directly without a colon. Here's an example of a student record using this abbreviation:
**Copy code**
```yaml
student: John Doe, 20, Computer Science
```
In this abbreviated format:
`student` is the key, and it's followed immediately by the values: `John Doe`, `20`, and `Computer Science`. Each value corresponds to a specific aspect of the student's information, in order: name, age, and major.
This abbreviation can be handy when you have simple data structures and want to keep your YAML files concise. However, it's important to remember that it's less flexible than the full key-value pair format. It's best suited for cases where the structure is straightforward and doesn't require nested data or complex relationships.

Abbreviations can make your YAML files more compact and easier to read when dealing with basic data, but for more complex and structured data, using the full key-value pair format may be more appropriate.

## Representing List
In YAML, you can create lists by using the hyphen (-) followed by a space, and each element of the list is written in a new line. Here's an example of a student's course list in YAML:
**Copy code**
```yaml
courses:
  - Math
  - History
  - Computer Science
```
**In this example:**
- `courses` is the key, and it's followed by a colon and space.
    - After the courses key, the colon and space are used to indicate that what follows is a value associated with the key. In YAML, the colon (:) and space are used to separate keys from their corresponding values in key-value pairs.

      - In this case:
        - `courses` is the key, indicating that you are about to specify the student's courses.
        - The colon and space, `:`, immediately following `courses`, indicate that the value associated with the key is a list of courses. In YAML, the colon-space combination is used to define this association between keys and their values.
      - So, the structure `courses`: tells you that the key "courses" is associated with a list of courses, and the list itself is defined using the hyphen (`-`) and space for each course item. This structure helps organize and       represent data in a clear and human-readable way in YAML.
- Underneath the courses key, you see a list of courses.
- Each course in the list is represented by a hyphen (-) followed by a space. This indicates the start of a new item in the list.
- The courses, like "Math," "History," and "Computer Science," are each listed on a new line with the same level of indentation.
This creates a list of courses for the student, making it easy to understand and organize related information. Lists are very useful in YAML for situations where you need to represent multiple items or values in a structured manner.

### List inside Dictionaries
We can use lists inside dictionaries in YAML, where the value of a key is a list. This is a common way to represent structured data, especially when you need to associate multiple items with a single key. Here's an example of a student's extracurricular activities where the value of a key is a list:
```yaml
student:
  name: John Doe
  age: 20
  major: Computer Science
  activities:
    - Basketball
    - Chess Club
    - Coding Club
```
- `student` is the main dictionary (or key) containing information about the student.
- Inside the `student` dictionary, there are key-value pairs like `name`, `age`, and `major` that provide details about the student.
Now, let's focus on the activities key:
- `activities` is another key in the `student` dictionary, and its value is a list of extracurricular activities in which the student is involved.
- The list is represented using the hyphen (`-`) and space for each activity item, such as "Basketball," "Chess Club," and "Coding Club."

### List of Dictionaries
you can create a list of dictionaries in YAML, which is a powerful way to represent structured data, especially when you have multiple items with different properties. Let's use an example of a student with a list of courses and their grades to illustrate this concept:
```yaml
student:
  name: John Doe
  age: 20
  major: Computer Science
  courses:
    - course:
        name: Math
        grade: 95
    - course:
        name: History
        grade: 88
    - course:
        name: Computer Science
        grade: 92
```
**In this example:**
- `student` is the main dictionary (or key) that contains information about the student.
- Inside the `student` dictionary, there are key-value pairs for the student's `name`, `age`, and `major`, which provide details about the student.
- Now, let's look at the `courses` key:
  - `courses` is another key in the `student` dictionary, and its value is a list.
  - This list is made up of dictionaries, where each dictionary represents a course taken by the student. Each course dictionary has its own set of key-value pairs.
  - For instance, the first course is represented as a dictionary with a `name` key and a `grade` key. The `name` key holds the course name (e.g., "Math"), and the grade key holds the student's `grade` for that course (e.g., 95).

By using a list of dictionaries, you can organize and represent structured data efficiently. It's a useful approach when you need to handle complex data where each item has multiple properties, like in this example where each course has a name and a grade associated with it.

YAML provides two ways to control the formatting of multiple lines: using the `|` character to include newlines and `>` to suppress newlines. Additionally, YAML allows you to represent boolean (true/false) values, and it's generally case-insensitive. Let's illustrate these concepts with a student's information.

1. **Using `|` to Include Newlines:**
    The `|` character allows you to include newlines, making it useful for preserving line breaks, especially when you have long text. Here's an example:
    ```yaml
    student:
      name: John Doe
      age: 20
      major: Computer Science
      description: |
        John Doe is a dedicated student.
        He is passionate about learning
        and excels in his coursework.
    ```
  In this example, the `description` field includes multiple lines of text. The `|` character preserves the line breaks, allowing you to maintain the formatting of the description.

2. **Using `>` to Suppress Newlines:**
    The `>` character, on the other hand, is used to suppress newlines, making it helpful when you want to represent multiple lines of text as a single paragraph:
    ```yaml
    student:
      name: John Doe
      age: 20
      major: Computer Science
      notes: >
      John Doe is a dedicated student. He is passionate about learning and excels in his coursework.
    ```  
    In this case, the notes field combines the text into a single paragraph, even though it spans multiple lines.
