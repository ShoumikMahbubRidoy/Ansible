# Ansible - YAML Basics
YAML (YAML Ain't Markup Language) is a human-readable data serialization format that is often used in Ansible for creating playbooks. It's designed to be simple and easy for humans to work with, making it a popular choice for configuration files. Let's break down the basics of YAML with an example for beginners.

In YAML, you create data structures using key-value pairs, and indentation is crucial to represent the structure. Here's a simple example of a student record in YAML:

```yaml
Copy code
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
- 1. The document starts with ---, which is optional and used to indicate the beginning of a YAML document.
- 2. We define a dictionary or key-value pair named student. The key (in this case, "student") is followed by a colon and a space.
- 3. The student's details are represented as nested key-value pairs, indented with spaces. For example, name: John Doe indicates the student's name is "John Doe."
- 4. The grades field is also a dictionary, but it has a list of subjects and scores. This is represented using a hyphen - followed by a space for each item in the list. For example, - subject: Math indicates the subject is "Math," and the student's score is 95.

Here's a breakdown of the structure:
- The outermost level represents the "student" dictionary.
- Within "student," you have key-value pairs for name, age, major, and grades.
- The "grades" field contains a list of dictionaries, each representing a subject and a score.

Remember that in YAML, spaces and indentation are critical for defining the structure. It's also essential to use colons and dashes correctly. YAML's simplicity and readability make it a good choice for creating Ansible playbooks, as it's easy for both humans and automation to understand.
