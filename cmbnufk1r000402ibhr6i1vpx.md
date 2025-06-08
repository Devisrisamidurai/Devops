---
title: "An Introductory Guide for YAML"
datePublished: Sun Jun 08 2025 15:54:12 GMT+0000 (Coordinated Universal Time)
cuid: cmbnufk1r000402ibhr6i1vpx
slug: an-introductory-guide-for-yaml
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1749022932217/2211dc43-5447-4dd2-93af-fc265c33536e.jpeg
tags: devops, yaml, configuration, yaml-jsondevops

---

Hello everyone 👋,

This week, we're diving into **YAML**, a language that's quietly powering the configurations of some of the most powerful tools in tech, like **Kubernetes**, **Docker**, and your favorite CI/CD pipelines! Whether you're building cloud-native apps, writing automation scripts, or just trying to figure out those .yaml files you see everywhere, this blog is here to help you get started.

In this post, we'll explain what YAML is, why it was created, and how it fits into today's tech world. We'll guide you from writing your first YAML file to understanding its syntax, data types, data structures, and how it compares to JSON or XML. We'll cover everything with simple examples, real-world use cases, and a bit of its use cases in the cloud-native space.

---

## What is YAML?

First things first, what does **YAML** stand for? It's actually a playful acronym: ***YAML Ain’t Markup Language*** (recursive, right?). It used to be known as **Yet Another Markup Language**. YAML is a data format language that's great for exchanging data. It's in the same family as XML (Extensible Markup Language) and JSON (JavaScript Object Notation).

These languages are all about storing and parsing data. When you store data in files, it's called data serialization. But what exactly is serialization?

> Serialization is the process of turning complex data structures into a stream of bytes (or chunks of data). It involves converting an object, which combines data and code, into a series of bytes that capture the object's state in a way that's easy to transmit.

With YAML, you can store data in a single format that ***can be shared anywhere***. This means the data you save in YAML for a web app can also be used in machine learning or mobile applications without any changes. How cool is that?

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749377057714/c813d753-341e-4e16-9ba1-fba261ff82db.png align="center")

---

## The Why behind YAML?

Well, that's a great question! With XML and JSON already doing similar things, why do we need another language?

The problem with **XML and JSON is that they have strict structures**, with curly braces and closing tags, which can make it tough to follow the information in large configuration files. The syntax can get messy, and developers often spend extra time ensuring the structure is correct while trying to keep the code clean and readable.

YAML was designed to be **simple, with a human-friendly syntax** and a neat code structure. It has a clean, minimalistic style that's easy to learn, making life easier for developers. Even complex data structures can be shown in very straightforward ways. Plus, it works well with almost all programming languages, which is why it's widely used in the cloud-native space.

> **YAML is for humans first, and machines second!**

We'll dive deeper into comparing YAML, XML, and JSON in this blog post.

### Features:

* Easy to read and understand with minimal fuss.
    
* Uses **indentation** to keep things neat, but you gotta be precise.
    
* Can **switch back and forth** with **JSON or XML** easily.
    
* Handles complex stuff like lists and nested maps without breaking a sweat.
    
* Works with tons of programming languages and tools.
    
* YAML is like JSON's big sibling; **if it's valid JSON, it's valid YAML** too.
    

---

## Getting started with YAML Syntax

Alright, let's dive into writing a YAML file and check out the different data structures it supports. We'll learn how to declare them and use literals as we create our first YAML file. Ready? Let's go!

> **You can name your YAML file anything you like, just make sure it ends with the .yaml or .yml extension.**

### Understanding Indentation in YAML

Indentation is **key** in YAML. Much like Python, YAML uses **spaces (not tabs!)** to show structure and nesting. It's how YAML figures out what belongs where. Let's break it down with a simple example:

```yaml
tutorial:        # level 1
  - yaml:        # level 2 (2 spaces in)
      name: "YAML Ain't Markup Language"  # level 3 (4 spaces)
      type: awesome
      born: 2001
```

YAML uses spaces, not tabs, for indentation to show nesting and define structure. Be consistent with your spacing, like using **2 or 4 spaces**, or YAML will give you an error.

Now, let's have some fun and create a biodata using YAML. Here's a sample script for IRONMAN's biodata:

```yaml
name: Ironman
age: 30
skills: ["Flying", "Engineering", "Combat"]
phone:  +1-555-123-4567
```

As you can see, the file is simple and easy to read, which is one of YAML's greatest strengths.

In YAML:

* Each line is a **key-value pair**, separated by a colon (`:`), known as mappings.
    
* The `skills` field is a **list (or array)** of strings, enclosed in square brackets.
    
* The `phone` number is a **string**. Putting it in quotes ensures that special characters like `+` and `-` are correctly handled.
    

YAML supports a range of intuitive and human-friendly **data types**, making it perfect for configuration files. Let's start with a **single YAML file** that showcases all the major data types, and then we'll dive into a detailed explanation of each.

```yaml
# Basic scalar types
name: Ironman                   # String
age: 27                         # Integer
height: 6.1                     # Float
is_alive: true                  # Boolean
nickname: null                  # Null (no value)
```

1. ### Scalar datatypes
    

* `name`, `height`, `is_alive` are examples of scalars.
    
* Supported scalar types:
    
    * **String**: Can be quoted or unquoted.
        
    * **Integer**: Like `27`.
        
    * **Float**: Such as `6.1`.
        
    * **Boolean**: Values like `true` or `false`.
        
    * **Null**: Represented by `null`, `~`, or simply left empty.
        

Feel free to add comments to your YAML files to keep notes.

**Comments**: Unlike JSON, YAML allows comments, which start with a `#`.

2. ### Lists /Sequences
    

* Lists represent an **ordered collection** of items.
    
* Use `-` **for each item** on a new line or `[]` **for inline** lists.
    
* A sequence node contains an ordered series of zero or more nodes. Interestingly, a sequence can include the same node multiple times or even include itself.Let's list the languages Ironman knows.
    
    ```yaml
    languages:
      - Go
      - Python
      - Rust
    # similar as ["Go","Python","Rust"] in oneline
    ```
    

3. ### **Maps**
    

Maps in YAML are like **dictionaries or objects** in other programming languages. They consist of key/value pairs, where each key must be unique. YAML doesn't impose any additional rules on these nodes.

To create nested maps, simply use indentation. Alternatively, you can use `{}` for inline maps.

* ```yaml
    person:
      name: Bruce
      age: 40
    ```
    

---

## Folded vs Block Strings in YAML

YAML offers flexibility for writing multi-line strings, letting you choose whether to keep line breaks or not.

### **Folded Style (Using** `>` )

If you need to write a long message over several lines in the file but want it to be treated as a **single line** when used, you can use the **folded style** with the `>` symbol.

```yaml
message: >
  it looks like
  this is a multiline message,
  it is actually not(illusion🫠)
```

**How YAML interprets it:**

```yaml
message: "it looks like this is a multiline message, it is actually not(illusion🫠)"
```

This is handy when you want your file to look neat but don't need newlines in the final output.

### **Literal Block Style (Using** `|` )

On the other hand, if you want your message to **keep the line breaks**, you should use the **literal block style** with the `|` symbol.

```yaml
message: |
  this is
  a real multiline
  message
```

**How YAML interprets it:**

```yaml
message: "this is\na real multiline\nmessage\n"
```

Perfect for keeping the original formatting intact, like in long texts, logs, or descriptions.

You can also experiment with date and time. Here, the timestamp tag is used to declare a date.

```yaml
# dates and time
date: !!timestamp 2002-12-14
india time: 2001-12-15T02:59:43.10 +5:30
no time zone: 2001-12-15T02:59:43.10
```

---

### Documents

A YAML file can hold **multiple documents**, and each one kicks off with `---`. Unlike a single document where keys need to be unique, **duplicate keys are okay across different documents** because each document is seen as its own separate unit. Each document wraps up with triple dots `…`.

```yaml
---
# document 1 starts here
codename: Ironman
name: Anthony Edward "Tony" Stark
suit_release: 2008
---
# document 1 ends and document 2 starts here
tech_specs:
  - suit: Mark LXXXV
  - arc_reactor: True
  - ai_assistant: FRIDAY
  - power_level: 9000
creator: Howard Stark
active_avenger: true
...
# document 2 is completed
```

### Tags

In YAML, **tags** help you clearly define the **data type** of a value. While YAML usually figures out types on its own (like recognizing `true` as a boolean or `123` as an integer), you can use **type tags** (such as `!!str`, `!!int`, `!!bool`) to manage or change how it interprets these values.

```yaml
---
# Ironman's profile 
name: !!str Tony Stark
alias: !!str Ironman
age: !!int 45
isAvenger: !!bool true
suits:
  - !!str Mark III
  - !!str Mark XLII
  - !!str Mark LXXXV
ai_assistant:
  name: !!str FRIDAY
  version: !!int 2
active: !!bool true
```

You can also include numbers in different types and ranges, as shown below. Remember, everything is marked with an integer (!!int) tag(later).

```yaml
# Integer types
zero: !!int 0                  # Zero as integer
positiveNum: !!int 45          # Positive integer
negativeNum: !!int -45         # Negative integer
binaryNum: !!int 0b11001       # Binary representation 
octalNum: !!int 06574          # Octal number (deprecated style in YAML)
hexa: !!int 0x45               # Hexadecimal 
commaValue: !!int +540_000     # Underscore used for readability (540000)

# Floating point numbers
exponential numbers: 6.023E56  # Scientific notation (float)
marks: !!float 56.89           # Standard float value
infinite: !!float .inf         # Positive infinity
not a num: .nan                # Not-a-Number (NaN)
```

But wait, see below yaml code,

```yaml
example:
  - true
  - hello
```

What is "true" interpreted as?  
Unless you explicitly specify it as a string using string tag or inside quotations, it is read as a boolean value. Here, it is a boolean.

### Anchors (&) and Aliases (\*)

* **Anchor (**`&`): This lets you assign a name to a block of content.
    
* **Alias (**`*`): This allows you to reuse that content elsewhere in the file.
    

These features are very useful when you have values or settings that repeat. They help maintain consistency by providing a single place to update if something changes. Here, the Ironman block is anchored as &tony, and in the War Machine block, \*tony is used. It allows for code reusability.

```yaml
ironman: &tony
  suit: Mark LXXXV
war_machine:
  <<: *tony
  suit: War Machine Armor
```

---

## YAML Vs JSON Vs XML

As you can see below, each of these data serialization languages has its own style. YAML is clean and neat, JSON uses curly braces, and XML is full of opening and closing tags.

Who really wants to bother with curly braces or opening and closing tags every time they need to store data? That's where YAML stands out.

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1749395340519/42a002e8-1cfc-4b88-a1cb-9ec2f9ff18a5.png align="center")

## YAML in cloudnative

* YAML is a top choice for cloud-native configurations because it's simple, clean, and easy to read.
    
* Its indentation-based style naturally handles complex data like lists and maps, making even large setups easy to manage.
    
* Unlike JSON, YAML allows you to add comments, making it simple to document your configurations.
    
* Features like anchors help cut down on repetition, keeping your files tidy.
    
* Tools like Kubernetes and Docker Compose use YAML because it makes configuring infrastructure and apps more intuitive and less prone to errors.
    

---

## Conclusion

And that's a wrap 🎉.

We've covered a lot in this blog, diving into the history and uses of YAML, exploring its syntax, literals, and data structures, and explaining why it's so popular in the cloud-native world. We also compared it to other data formats like XML and JSON and even created our first YAML file.

Spend a day or two experimenting with YAML, and you'll quickly get the hang of the syntax. Just remember to keep an eye on your indentation.

That's it for this blog. If you've made it this far, thank you so much for reading 💙. See you in the next blog soon 😄. Until then, bye 👋.

![Bye Dog GIFs | Tenor](https://media.tenor.com/X2FM1MIFqy4AAAAM/hi-bye.gif align="left")

💡**Let’s connect!** Feel free to reach out:  
[**LinkedIn**  
**GitHu**](https://www.linkedin.com/in/devisri-s-0987b6256/)[**b**](https://github.com/Devisrisamidurai)