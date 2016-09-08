# Assignments (Part 1)

If you have any questions about any of the assignments, don't hesitate to ask. Please, if possible, let me know what you think might be correct. You'll find the short course overview and outline by scrolling all the way down (the messages are ordered chronologically, starting from the bottom of the page).

Please keep track of the number of hours you spend on these assignments.

1. Please read the text titled "Computers" (scroll almost all the way down to start reading).

2. Read the Wikipedia article at https://en.m.wikipedia.org/wiki/Hyponymy_and_hypernymy. Write a paragraph explaining what you've read (purely the basics).

3. Please give a description of 5 (isolated) things. Things include (abstract) concepts. Make sure you describe all attributes/aspects, parts and behaviour or use of each thing. Use language constructions like "A has a B", "A has a B C", "A is a B", "A is used for B", "A (does/is) B" (where be may be a verb or a "-ble" adjective), "An A is a part of a B". Not included in the 5 things are descriptions of each attribute or part. You have to describe each of those in the same manner and any attributes or parts of those things too, and so on. You'd be wise to choose simple things.

Examples: "A McIntosh is an apple", "A Macintosh has a kernel".

4. Make a list of things a computer can do. Then group similar things together and write another description that holds true for all the things you've grouped together, for each group. If it's difficult to find similarities, you should break down the processes you describe into separate steps, until you can assign each part to a (likely different) group. The aim is to come up with the most basic things a computer does. You'd probably end up with processes that require at least a few different steps.

Now we're going to make sure once we start with the exercises, you're tools (different parts of Firefox) are working correctly.

5. Open Firefox. Enter "about:config" into the text field on the address bar and press on the 'Enter' key. Click on the button saying you'll be careful (and be careful). Type "devtools.chrome" into the text field labelled "Search:". There should be one table record/row visible. Doubleclick on the row. Make sure the value has changed from "false" to true. Now remove "devtools.chrome" from the search field and enter "devtools.debugger.remote". You should see four rows. Doubleclick on the first row and make sure the value changed to "true".

Side note: in case you're worried that others might have remote access to your browser (which could have been the case): the value of the second row (the text in the 4th column) should read "localhost". This means the connection is "bound" to an Internet address that's only accessible from the machine you're working on (even others on the same network can't remotely access your browser). The use of Internet connections will be discussed a few weeks from now.

6. You might want to open a new tab and close the one with the configuration table (the table you just used to change two settings) to avoid accidentally changing other settings. Type "forums.psychcentral.com/bipolar" into the text field on the address bar and press 'Enter'. You should see the PC Bipolar forum. Hold down the 'Shift' key and press at the same time on the 'F4' key (if your keyboard has an 'Fn' key, you may have to hold down that key as well). You should see a new window with the "Scratchpad" tool (basically a large text area with some text between "/*" and "*/").

7. Enter the following code (you don't need to know how the code works (not yet); it's not an exercise): "document.createExpression("tr[5]/td[3]/div/a[2]/child::text()", null).evaluate(document.getElementById("threadbits_forum_11"), XPathResult.STRING_TYPE, null).stringValue;" and click on the button marked 'Display'. Again between "/*" and "*/", inside a text selection, you see a line of text. Please write down what you see (copy the text).

8. Write down the number of hours it took you to finish the assignments (this helps me to make sure the course load stays within the expected/promised margins).
