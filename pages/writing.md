---
layout: default
---

# Effective Technical Writing

Good research consists of two essential components: having good ideas and being able to communicate those ideas to others.  Unless you are able to clearly and efficiently express your ideas in writing, no one in the broader research community will ever be aware of your work.  These days, technical writing is made more challenging by the huge number of publications being generated by research groups around the world.  This flood of publications results in a fundamental problem that you need to always keep in mind while you are writing: **No one who is looking at your paper has enough time to read it in any amount of detail.**  This is true for the reviewers assigned to assess your work as part of the publication process, anyone in the general research community who might be looking at your work after its publication and even sometimes your own supervisor.

This means that you need to structure your document in a way that makes it easy for a rushed reader to understand the important points of your work.  The good news is that this is very possible and the purpose of this page is to teach you how to do this.  However, you need to be very careful and disciplined.  

The discussion in this page will focus primarily on conference and journal papers.  However, these techniques are equally useful for your thesis.  A discussion of some of the differences between writing a paper and a thesis is provided at the end of this wiki page.


## Telling Your Story
All papers have a story or central message.  For example: "This paper presents a new indoor WiFi wireless channel model based on measurements.  It captures the large scale variations that occur when a user is confined to a small area."    The method in this page will ensure that you have the proper document structure to ensure your message is clear to the reader even if he/she is reading your paper in a hurry.

You start by creating a skeleton or framework for your paper and then filling in the details by using the following steps.

### Step 1: Creating Your Sections
Start by deciding what sections you want in your paper and what the titles of those sections should be.  Of course, the first section will be called "Introduction" and the last section "Conclusion".  However, the titles of the sections in the main part of your paper should be chosen with care.  Think about how you want to divide the discussion in your paper.

For example, you might decide that you want to tell the reader about your measurement equipment, describe the environment where you collected your measurements, present some raw measurement results and then describe how you used the measurements to develop a model.  Each of these steps in telling your story would then correspond to sections called "Measurement Apparatus", "Measured Environment", "Measurement Results" and "Propagation Model Derivation".

Once you've decided on your primary section headings, think about whether the discussion in each section needs to be divided into subsections.  This takes a bit of practice but the rule of thumb is to try and separate distinct ideas or discussion topics.  For example, your "Propagation Model Derivation" discussion might include a description of the actual equipment and a discussion of your calibration procedure.  Those two topics should go into different subsections.  Another rule of thumb is that a single section should usually not be longer than a double column page or smaller than two paragraphs.

### Step 2: Create Your Figures and Tables
The figures and tables you use to present your results are a critical part of your message.  You need to give these a lot of thought and create them before you even start writing.  Try to imagine yourself presenting or explaining your work to a colleague.  What figures, diagrams and/or tables would you want to really show why your work is interesting and important?

Sometimes students wonder whether they should use a figure or a table to present data.  Here are a few things to think about when making your decision:
- If you have a large number of data points, figures are almost always the way to go.  Tables get hard to look at when they have more than 10 rows or columns.
- Figures do a much better job of showing trends.
- Tables are better when the specific value of the data is important and you want to compare two specific data points together (ie. It's important to discuss how a simulated value of 2.42 compares to a second simulation yielding a value of 10.19).

The IEEE requires the captions of your figures to be written in sentence capitalization and punctuation.  For example, you would write "A comparison of the FIFO and LRU caching algorithms." rather than "A Comparison of the FIFO and LRU Caching Algorithms".  In general, your captions should be short, one sentence descriptions of the figures.  They should not contain multiple sentences or attempt to explain what is going on in the figure in detail.  That's what the discussion in your text is for.

### Step 3: Write the Opening Sentence for Your Paragraphs
Proper use of paragraphs is a **huge** part of effective writing for a busy reader.  When used properly, good paragraph structure allows a reader to skim through a full journal paper in just a few minutes and take away all the key points of that paper's message.  The golden rules for using proper paragraph structure are:

- Each paragraph in your document should present only one idea. Never present more than one idea in the same paragraph.
- The starting sentence in each of your paragraphs should summarize what your paragraph is going to talk about. 

If you follow these two rules, a reviewer or examiner should be able to read only the first word in each of your paragraphs and understand the basic ideas behind your entire paper. A reader should only have to read the rest of your paragraphs if they want more detail.  

Think of each paragraph as a box and the first sentence as a label describing the contents of that box.  A reader can read the label and, if they are interested in it, can read the rest of the paragraph (ie. open the box) for more information.  If not, they can skip ahead to the next paragraph.  This makes it extremely easy to read a document quickly.

An example of poor paragraph technique is:

"The measurement vector is normalized by the square root of the average tap energy.  The tap utilized for normalization is the first tap in the impulse response surface above the 10 dB threshold  As the measurements are connected within a small neighbourhood this removes the path loss component from the tap and allows the small scale fading histogram to be calculated with a normalized mean.  Interestingly, none of the small scale fading histograms exhibit Rayleigh fading but instead display Ricean fading with a high K-factor.  This is due to the small size of the cells where the measurements were collected.  At most measurement locations, a line of sight path exists between mobile and base station.  Thus, contrary to the conventional opinion held in past studies, MIMO techniques will offer very little benefit in a small cell environment."

There are a couple of things wrong with the paragraph above.  First, you'll see that it's one paragraph talking about two very different things: measurement processing and interpretation of the fading histograms.  These are two distinct ideas that deserve two separate paragraphs.  Plus, the most important statement in the text that is likely to be most interesting to the reader is the last sentence in the paragraph.  Most sentences at the end of paragraphs will be missed by a reader in a hurry.  Finally, the first sentence in the example paragraph doesn't summarize anything in the paragraph.  Instead, it dives right into the details.

A better version of these paragraphs would be:

"The measurements are processed to isolate the small scale fading variations. The measurement vector is normalized by the square root of the average tap energy.  The tap utilized for normalization is the first tap in the impulse response surface above the 10 dB threshold  As the measurements are connected within a small neighbourhood this removes the path loss component from the tap and allows the small scale fading histogram to be calculated with a normalized mean. 

In contrast to the commonly held opinion in existing research, the small scale fading histograms suggest that MIMO techniques will not perform well in small cell scenarios.  Interestingly, none of the small scale fading histograms exhibit Rayleigh fading but instead display Ricean fading with a high K-factor.  This is due to the small size of the cells where the measurements were collected.  At most measurement locations, a line of sight path exists between mobile and base station."

When creating your first draft, you should start by writing only the opening sentence for each of the paragraphs in your sections but none of the sentences in the body of the paragraphs.  Think of this as creating the idea "boxes" that you will then fill in later on once you're happy with the document structure.  Once you have written all of your opening sentences **STOP** and proceed to the next step.

### Step 4: Give Your Draft Document Framework to Your Supervisor

Without question, the vast majority of the time I spend reviewing papers for my students is spent trying to modify the structure of their documents so their message is clear.  This is a much more efficient and less frustrating process both for me and the student if the entire paper hasn't been written before I see it for the first time.  So, when you submit the first draft of your paper to me, it must consist of **only** the following things:
- Sections and section titles..
- Figures, tables and diagrams with captions.  These should be as close as possible to the final versions of the figures and tables you expect to put in your paper.
- The opening sentences for each paragraph in the document but NOT the rest of the paragraph.

In this format, I can review your document very quickly and get you early feedback on whether the structure of your document is correct and your message is clear.  At this stage, it's also very easy for you to change things around since you haven't invested a lot of time writing a bunch of text yet.

### Step 5: Create a Full Draft by Filling in Your Framework

Once you and your supervisor agree that your framework is ok, fill in the details by writing the bodies of your paragraphs.  As you do this, it's very likely that you may find that you want to add new paragraphs to discuss ideas that you didn't think of when putting together your framework.  This is fine.  Simply create a new paragraph with a good opening sentence that summarizes the idea in that paragraph.

Whatever you do, be very careful that you don't just jam a bunch of separate ideas into one paragraph simply because you want to keep all your opening sentences unchanged.  It's perfectly ok for the structure of your document to evolve during this stage.  However, if you find your structure radically changing, it's a good idea to go back and modify the basic framework you produced for Step 4 just to make sure your message isn't getting confused.


## The Paper Sections 

The techniques I describe above should be used in every part of your paper.  However, each section of a paper isn't the same and some sections deserve to be talked about in a bit more detail.

### The Introduction
In many ways, the introduction is the most important part of the paper since it should completely describe what the work you're doing in the paper and why that work is important.  By the end of the introduction, most reviewers will have already made a preliminary accept/reject decision.  They will then read the rest of the paper for things that will confirm this preliminary decision.  It is **essential** that your introduction is written in such a way as to ensure the reviewer will look at the rest of your paper in a positive way.

An introduction should have a 'V' structure.  It should start broad and narrow down until it concludes by stating the exact contribution of your work.  An example of how to achieve this is shown below.  Note that each sentence in quotes could be the opening sentence for a paragraph (see proper paragraph writing techniques below).
- Start with a general statement justifying why your general research area is important: 
  - "Digital subscriber loop (DSL) technology will remain a major technology for delivering home Internet service for the foreseeable future."
- You can then provide a bit more information about the problem you are tackling: 
  - "An important part of maintaining good network throughput is ensuring DSL systems are robust in the presence of interference sources."
  - "One potential source of DSL interference is power line communication (PLC) networks."
- Discuss the existing research that has been done on the problem you are addressing in your paper.  When doing this, point out the holes in this work that you will be filling with your research.
- State the contribution of your work.  This should be done in a separate paragraph that starts with the words "The primary contribution of this paper is ...".  If you've written your summary of existing research in the previous paragraphs correctly, the reviewers should have no trouble seeing: 1) that your work is new and 2) that it's important.

### The Results Section
All of your papers will have some kind of section that discusses the results of your research.  This most often takes the form of paragraphs that discuss the figures or tables you've included in your paper.  In this discussion, avoid making statements that are obvious from the figures (ie. "As we can see, the red curve is below the blue curve.")  That's obvious from looking at the figure and will frustrate your reader.  You need to focus not on what is happening in the plot but **why the plot looks the way it does** and **why the plot is important**.  For example, "The red curve falls below the blue curve since, as suggested by our analysis, the FIFO caching algorithm does not perform as well as the PCO algorithm under high load.  This why the curves diverge under a high load factor.  This is an important result since this form of caching algorithm is most often used in very heavily loaded networks."


## Formatting Rules 
In addition to achieving proper document structure and using effective writing, you must also attend to the formatting details that are standard for our research area.


### IEEE Standard Writing Style
Since virtually all of the papers written in our lab are submitted to IEEE conferences or journals, it's important to adopt the standard IEEE writing style.  Detailed information on IEEE conventions, including the up to date IEEE Latex templates can be found [here](http://www.ieee.org/publications_standards/publications/authors/authors_journals.html).  In particular, please adopt the following conventions:
- Equations with numbers are referred to using only the equation number contained in round brackets.  For example, you would say "The result is shown in (4)." rather than "The result is shown in Eq. 4" or "The result is shown in Equation 4".
- Figure captions should be a complete sentence terminated by a period.
- When referring to figures and tables in the text, you use "Fig." or "Table" and then the figure or table number.


### Italics
Italics are generally used to refer to a formula.  So, *ABC* is equivalent to "A multiplied by B multiplied by C".  This means:
- Units (like kHz or MHz) should not be in italics.
- Acronyms like SNR should not be in italics because //SNR// means "S multiplied by N multiplied by R".  Similarly, if you are using an abbreviation in a superscript or a subscript like, $F_{opt}$ where "opt" is supposed to be short for "optimal", you need to make sure that "opt" is also not in italics.  To remove the italics in latex, use the command $F_{\rm opt}$ and opt will be put in Roman text.

### Equations
An equation is always considered a part of a sentence, even when it's on it's own line with a number.  That means you sometimes have to include a period after the equation if it's the end of the sentence.  Consider the following example:

```
  My equation is x=y.
  
  My equation is
     x=y.          (1)    
```

There are other times when the equation occurs in the middle of the sentence.  Again, the sentence needs to still make sense even if the equation gets its own line and the portion of the sentence following the equation is never indented.

```
  My equation is x=y where x represents one quantity and y another quantity.
  
  My equation is
    x=y              (1)
  where x represents one quantity and y another quantity.
```