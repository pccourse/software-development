# Part 3. Recursion, objects and references

## Files, threads and data streams

The memory in, or which constitutes, primary storage, the fastest memory used for storage, is subdivided into pages, as was mentioned in the text of part 2 of the course. Each process, each computer program, uses one or more pages (often at least four, where one is for storing instructions for the computer, one for data that won't be changed during execution of the program and one for data that can be changed, added and removed during execution, when the computer follows the instructions, and one for working memory).

Most computers can switch from one context, a set of pages and (other) data in the working memory of the computer (which isn't just the page with working memory; the computer has another type of working memory which is (a copy of) the part of working memory the computer focuses on) belonging to (or at least used by) a process, to another. The computer then shifts its "broad" focus away from one context of one task or tasks, one process, one program, to another. As mentioned before, this is called multitasking.

If there isn't enough memory space available for all programs at any one time, some pages (usually those not used very often; those where a program doesn't do much but is still active) are stored in secondary storage. Secondary storage contains memory that, as mentioned before, is usually slower and less changeable (that its less changeable is a choice; using slower memory as working memory, requiring data manipulation, slows down, or would slow down, processes, programs, considerably).

Programs that aren't active at all, programs that have "quit" or haven't been "started", are also stored in secondary storage. While "active" pages are often grouped together, non-active pages, non-active programs, processes, are stored separately and filed under a name. The (filing) system and type of structuring of data, the data structure, is called a (computer) file system. But other than is usual in a normal (or "real") file system, files may contain less than a page or one or more pages and just a partial page, one part of a page being part of one file and another part of another file. If the computer retrieves one part of a page from one file, it often also retrieves the rest of the page from one (or more) other pages.

Because some processes, some programs, only have one page in primary storage that is used for storing data that can be manipulated (and just another for all working memory), it might be a bit excessive to retrieve an entire page, which would mean the computer has to spend another page on the process, especially if the file that is retrieved only has enough data to fill just a tiny bit of a page. A program may choose to retrieve just one-eighth of a page, which is called a block, maybe like a paragraph of text on a page, a block of text, a block of data. Most pages contain 4096 bytes of data, so a block then contains 512 bytes.

A process may also request just a byte or a character (which can be between 1 and 4 bytes long; contain one to four bytes) at a time. There are two advantages to this: firstly, you just need to use one byte or, at most, 4 bytes of data in a page and secondly, you don't have to know the size of the filed data beforehand (you will be notified when there are no more bytes, or characters, to read). Since a computer can use, find meaning in, data as small as one byte, but reads and (initially) processes (at least) one word at a time (or a "double" or "quad word", as some refer to them as, on modern computers, as mentioned and explained in the previous part of the course), it might still "use up" four bytes of memory, but no more.

The computer would still retrieve, load into memory, in software development parlance, a block of memory, a block of data stored in secondary storage, but it would only provide the program with one (or a few) bytes at a time.

Loading larger chunks of data into memory (the context, containing the structured data, the information, of a process) even though the computer only processes one word at a time (of which maybe only a byte is a (part of) meaningful data), is called buffered reading. A buffer of the size of a block or a page (or maybe more), an allocated part of memory, is used to load data of that size, after which the computer might only request and process one byte or a character at a time (but no more than one word at a time; modern computers can process more than one word, but they use a specialised kind of computer to do it; what we call modern computers are actually multiple computers, Turing-complete, data processing machines, working as one).

Any such buffered reading where the size, the length, of the data is unknown and the process requests, and has access to, just one byte or character (or a word) at a time (even though it can of course safe each character or byte it reads in a row, an array or collection in software development parlance, keeping it in memory, storing it in a page). A process may use, and often does use, many subprocesses that use the same data, the same process context, but they act like separate processes, each subprocess, or thread in software development parlance, following a different set of instructions, multitasking, just as if each thread was a separate process, with the only difference being that they use the same context, the same data (but as for the instructions within the data, they focus on different parts, different sets of instructions, serving different functions). If one thread processes data faster than another, using the same data that is read one byte (or a bit more) at a time, such "internal buffering", creating rows of data and maybe adding pages to do so, might be necessary, so that each thread can process data at its own speed and one thread, the one that reads the data, can just focus on that, adding to the row, the array, the collection, quicker than the other threads, other subprocesses, can process process the same data (of course, if the "reading thread" just reads and stores data, it's most likely quick enough, speedier than the other threads that (probably) do more complex data manipulation).

There might be situations where reading one byte (or a character of word) is not just convenient, but a necessity. That's not the case with (most) secondary storage, but it is the case with (some) other peripherals, devices that do useful things for the computer (or the user of a computer, depending on your point of view), like a mouse, a computer display or a secondary storage device. A mouse, for example, sends relative coordinates continuously to the computer. The amount of data that the computer mouse provides is (potentially) limitless. The computer can't just allocate one or two pages, because that might be too much or too little memory. But more importantly, the data doesn't have to be stored for a long time but is immediately processed to change the position of the cursor on the computer screen. After that, the data is useless.

Another example is a network (interface) device (or "controller"). When a computer sends data to another computer using a computer network, it's not always known how much data will be send. The start of the message might indicate the length of the transmission, the size of the message, but that's not always the case. At the very least, to get the information about the length of a message, the computer can't assume to receive such an indicator at all or the size of that message metadata (or "envelope"), the data about the data. So networking is another example where data can only be accessed one small unit of data at a time. The computer software system should read the data as quickly as possible, straight into a buffer, to allow "worker threads" (or other processes) to do the more complex processing, to do the actual work.

## Recursion

Most languages (and, as far as we know, all natural languages) are recursive: they make use of recursion. Recursion means that one thing is (only a) part of another thing of the same type. Recursion can be functional and formal. Formal, as the word is used here, has to do with form, representations or expressions, while functional has to do with the way something is done. If something formal, a form, like a phrase, is contained within something of the same type or if a method, a function, like interpreting a phrase is done repeatedly, the form and the function, the thing repeated, is (equally) said to be recursive. Subordinate clauses are examples of recursion in language: one clause is embedded in another. A recursive method, a function, can be applied to the inner clause and then the outer clause to interpret the the entire clause (such as a sentence).

Another characteristic of languages (both natural and formal and formal in the sense that all the rules are known and exact) is that they're serial: each part is part of a series, one after the other, in a row. Sounds are strung together to make words and words are strung together to make phrases and phrases to make (clauses and) sentences, in one series.

Because languages are recursive and serial, the length of a language expression is highly variable. In theory, its length can be infinite, is unlimited. In practice, both computers and humans have a limited amount of working memory which limits the number of recursions and the length of expressions that can be interpreted.

To interpret a recursive language expression, we first interpret part of it, which becomes a meaningful abstraction, something remembered separately, and then we interpret the rest by including that abstraction. We apply this method as long as their are parts we can interpret that have similar parts contained within them or which are contained within those parts and are similar to them.

Using such a recursive method, we take a language expression, we interpret each part and memorise each part separately and we also memorise how these parts were fitted together by replacing language expressions contained within other language expressions with a reference to the (interpreted) language expression, an abstraction, something that has a meaning. We use such references to interpret the language expression within which the other language expression was contained.

## Objects in general

Computers do essentially the same thing as humans when interpreting recursive language expressions. The meaningful abstractions computers use are called objects and they are very much like what can be an object in (natural languages). They are things that can be interpreted separately from the rest of a sentence and used in interpreting the whole of the sentence, using the recursive method of language interpretation humans use or one of the many that computers use (each formal language uses a different method, a different interpreting function).

Most programming languages use the imperative mood and are said to be imperative programming languages. Imperative sentences don't have a subject (ordinarily), because the subject is the person (or thing) that is being addressed, telling the addressee what to do, and is therefore implied. The verb (using modifiers to fill in more details about the way things should be done) should be applied to the object (maybe using an indirect object). In programming languages, the addressee is, not surprisingly, the computer.

In most programming languages, the order of imperative statements where we use a verb which is applied to an object or just executed (if no object is required, the verb is intransitive; not a special verb that describes a part of, a property, either something belonging to an object or an aspect, a characteristic quality, including a state, of an object, as a proposition) is the reverse of the order used in English. English is said to be a VO language, where the object follows the verb. Most programming languages can be said to be OV languages, where the verb follows the object.

A property of an object (a belonging or quality, including a description of the object's state) can (but doesn't have to be) itself an object. If that is the case for a property, it refers to that property (like when interpreting language, where the language expressions are made non-recursive with references between objects).The object can be said to be normalised, where each object is similar in size and complexity, similar in structure, normal. The objects are in normal form.

The same can be done with language, where complex, recursive sentences are normalised, simplified, and words called anaphors (or anaphora), mostly personal and demonstrative pronouns and other types of demonstratives, are used to refer to other sentences, describing objects (and functions of the subject, the computer, in programming languages, applied to objects).

Examples:
The sentence "a man that slept woke up" can be normalised, simplified, using three sentences, where each has the same, a normal, structure and uses anaphors to connect the sentences: "there is a man", "the man was sleeping", "he woke up".

The exceptional verb that describes an object  (or subject) is called a copula (or a linking verb) in natural languages and in programming languages it is called an assignment operator or an equality operator, depending on whether the statement is a proposition about things that were already described, any such assertion or assumption, or a statement of fact, also a proposition, invariably true and (generally) new information, respectively. Another type of proposition which would use a copula (and sometimes a meaningless word called an expletive) in a natural language uses a connector punctuation mark to refer to a property of an object or just the object.

Examples:
"There" is an expletive in English. A proposition using this expletive (and a copula) would be "There is a man".
"The man is happy" is a sentence in English which uses the copula "is" to describe the state that the man (a subject; also referred to as an object in software development parlance; "the" is a demonstrative determiner (and a definite article), a reference to another phrase; there would have to be another sentence like "there is a man").

Object (or noun) phrases in programming languages, a type of expression (propositions are also called expressions), are called identifiers. In natural languages, if we talk about a property (which includes object parts) we may use a possessive affix. In English we use a possessive suffix (or apostrophe). Most programming languages also use a possessive punctuation mark, but rather than being a suffix, it's a infix. There's no space after the infix (hence the name). An identifier can't have any spaces (except in special language constructs which we won't discuss at this time).

Example:
In the noun phrase "the man's hair", the possessive apostrophe is used to refer to a property (or part) of "the man".
The same noun phrase in C, the programming language that has had a lot of influence on most newer programming languages, called, not just in C, an identifier, would be written as "theman.hair".
If we want to tell the computer the man is happy, as in a statement (more on statements later), in languages based on C, we use the connector punctuation mark, the assignment operator and something that has a value, like "true" (more on that later), like so: "theman.happy = true". If we want to change the statement into an expression (more on what that implies later), we should use "==" as the copula (the word copula isn't generally used to describe programming languages), like so: "theman.happy == true".

Not all functions can be applied (apply) to all objects. Functions that do use objects are considered part, "members" of, an object or a type of object (called its class). If functions are part of an object, they might also be (and generally are) referred to as methods. If they aren't part of any object (class), they aren't called methods, but just functions.

If we tell the computer to apply a function it can perform to an object (or if we use a function which doesn't apply to an object; like a transitive verb can be applied to an object), we use a similar syntax we use for referencing properties of an object, but we generally add some punctuation marks to reference other objects (what would be indirect objects in natural language) or (what would be) modifiers (identifiers or literal values; more on that later). These other values (or identifiers referencing those values) are the arguments, or parameters, to the function (the object itself is generally not (considered) an argument). Even if no arguments are used, we still use the punctuation marks. Arguments don't have to be objects, but only objects can be associated with functions (but functions might have no object, as mentioned before).

Examples:
If there exists a function (maybe that function was defined in the same source code, the same text, as the statement which tells the computer to execute it) to wash someone's hair, we might apply it to the hair of the man we just described and referenced using the identifier "theman". The identifier for his hair was "theman.hair" and if we want to tell the computer to wash it, we may use (in many languages influenced by C) "theman.hair.wash()". If we were to have a shampoo object, we might use "theman.hair.wash(shampoo)".

An imperitive language consists of statements. In imperative programming languages, if we don't state what the computer should do, it won't do anything (or it might, but it's not productive). If we use a language expression that is not a statement, it should be used in a larger sentence (in software development parlance, when we use an imperative programming language, we don't usually use the word "sentence", but we refer to sentences simply as statements). An expression can also be a statement. When we tell the computer to apply a function it can perform to an object (or we just tell it to perform a function, without the use of an object, if the language allows that) we use an expression which is a statement. Unlike other statements, we can use this "expression statement" as an expression in another statement.

Example:
In C (and languages influenced by C), we use a semicolon (";") to end a statement

When we tell the computer to perform a function, the computer expects something to be returned (like mathematical functions, functions have an input and an output). If a function doesn't change anything, any object or identifier value, but it does something with some input (which may include the object it is associated with and one or more arguments) and returns it as its output, its said to be pure (as in mathematically pure). But if we consider the object the function applies to to be both input and output, where the function changes parts or a part of the object, it works pretty much the same. This latter approach is used most often (by far), but pure functions have the advantage that after the function execution, the computer can be instructed to decide whether it wants to change the (or another) object or not, which allows for more flexibility (and possibly (added) security).

Expressions can be interpreted and used in expressions or statements: they can be used recursively.

There are noun phrases (or things that would be called noun phrases in natural languages) which aren't complex: they don't have any properties, no parts, qualities or state. They just are. Examples are numbers and quotations. These types of NPs are called primitives and are said to be of a primitive type (not a reference type). Primitive types can be referred to using identifiers or directly. When no identifier is used, we call these expressions literal expressions or literals, for short.

Examples:
We can use a quotation like you'd expect, in most programming languages, using double (and only sometimes single) quotation marks. An example would be: "theman.name = 'John'. Numbers may be written as decimal numbers, like you do in English, for example: "18547". "true" and "false" are truth values. Propositions using equality or relational operators (more on both in a later part of the course), like "1 == 2", are either true or false. Using "if" (more on that later, most of it in a later part of the course), you might write something like "if (1 == 2) theman.hair.wash()". The expression is said to evaluate to false and the condition isn't satisfied and therefore what follows the expression isn't done (much like we use the word if in English).

## Keywords and identifiers

Natural languages use content words and function words. Content words are used in phrases that can (easily) be used recursively and the number of content words is always growing. Function words are used to create statements and they are used to make statements that can't be (further) embedded (or not as freely).

Identifiers are like content word phrases and can be used in expressions. Expressions can be propositions which are true (they are said to evaluate to "true") or false. These expression can be used to change the series of instructions to execute, choosing between two series, like (climbing) a tree with (two) branches, choosing (to climb on) one or the other.

The function words used in (most) programming languages, called keywords or control structures (but not all keywords necessarily control branching; called control structures because they control the flow of execution), are all English words.

## Objects on your computer

Every part of computer software is made up of objects that reference objects. If you were to describe all objects, all things, all abstractions, in one sentence (using recursion) the sentence would very easily be a hundred times as long as this text, maybe a thousand or tens of thousands of times or more. If you were to describe everything a computer (and you) could do with these objects (or what it could do without reference to an object), the sentence would probably be about twice as long.

Objects don't contain objects (not really), but they appear to be. All objects are stored in rows of objects in memory, in a normal form, all structures containing values and references to objects that are (conceptually) part of those objects, like simple sentences with anaphors to link them together, (only) seemingly recursive and recursive functions can be applied to them (where references are followed as if objects contain objects). Objects (or rows of them) may be stored in files (called object files), referencing objects in the same or other files. Some objects are shared between programs and others are the programs.

The operating system (like macOS, iOS, Android or Windows) is one object referencing (directly or indirectly) all other objects. Most of the objects are (considered) part of the operating system and any program may use these to show characters in a text field or a button on the computer screen. All of these things, including individual characters, (often) are objects. But not all objects are visible and most are not. A word processor document (generally) is an object, as is an email and the program that controls all these objects (called an operating system kernel).

If you start a program, it is loaded into primary storage and (a program called) the dynamic linker loads many other objects that the program uses and also when they're shared and are already loaded into primary storage it links all these objects together as one (but simply by storing (or updating) references from one object to another).

Besides storing values and references to objects, (the data structures describing) the objects also reference functions that can be applied, that apply, to them. These functions may be shared in a class, a description of functions that apply to all objects that are part of that class (of objects).

The method by which all these objects (in memory) are linked together has to be standardised, otherwise two different programs (one of which might be the operating system) that want to share objects, which they will extensively if they use an operating system to do most things, like providing a user interface or allowing objects to be dragged from one application to another using a mouse, can't work together. The methods used (and which the dynamic linker supports) and that every (static) linker that translates source code into object code, objects in a format that conforms to the standard, should use, is called an Application Binary Interface. Like any interface, it allows one thing (or a person) to interact with another.

Identifiers reference these objects in source code. As far as the software developer is concerned, when using a programming language, objects may be contained in, be part of, other objects and each object of a certain class can use all functions, methods, of that class as if it were methods only used by that object.

When objects are created to be shared, like those that are part of an operating system, if that object contains (rows of) objects (or references them) that are "exposed" to the software developer through a programming language, the names of the objects and their members, properties or methods (properties and methods are sometimes the same as far as the programming language is concerned, in what are called dynamic languages, in which case methods are also properties) and the arguments that should be provided to execute a function are all described in a document or a source code header (or both; the latter may also be used by the static linker). What is described in such a document is referred to as an Application Programming Interface: the interface that is used to instruct the language interpreter or compiler (the program that together with the static linker creates a program or shared object in a format specified in an ABI).

Shared objects may be part of a larger file which is called a library. Many libraries use a similar API for many different objects. Operating systems consist of many libraries. Libraries are sometimes also referred to as frameworks. The terms library and framework are also used to describe (shared) files used on websites. The language that we will use in the exercises is called JavaScript and (as good as) all web applications are written in JavaScript. Many parts of Firefox, the browser that we'll use, are (even) written in JavaScript. Many applications for Android and iOS are also written in JavaScript.
