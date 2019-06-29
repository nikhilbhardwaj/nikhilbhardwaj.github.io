---
id: 151
title: Microsoft Interview Experience
date: 2012-08-14T23:49:37-04:00
author: nikhil
layout: post
guid: http://nikhilbhardwaj.in/?p=151
permalink: /2012/08/14/microsoft-interview-experience/
categories:
  - Life
  - nitt
---
A few days back Microsoft visited our campus, this had generated quite the buzz for it is not everyday that you have a giant like MS visiting the campus. They had a team of two people who had come for the presentation one of them was <a href="http://www.linkedin.com/pub/keith-auer/1/b76/53" target="_blank">Keith Auer</a> and the other one was an HR from MS-IT. The ppt was same as usual with them telling us why MS is such a great place to work and about the products that they have etc etc, you know the drill. There were two profiles that Microsoft opened for MS-IDC and MS-IT, the packages were 16Lacs p.a. and 10Lacs p.a. respectively.<!--more-->

After this there was an online test which was conducted by <a href="http://www.elitmus.com" target="_blank">elitmus</a>, this was easy and had questions from probability, set theory and general quantitative aptitude, next there were online coding rounds for both the IDC and IT profiles. The name coding round is slightly misleading as there was no compiler, we basically needed to write code in a browser window. The questions for the IDC profile were
1. Convert a doubly linked list into a BST.
2. Remove Duplicates from a string and print the remaining characters in ascending order.
3. Given a Sorted array, a sub-array has been reversed. Write a function to fix it.

and for the IT profile were,
1. Replace all occurrences of spaces in a string with &#8216;%20&#8217;
2. Given two sorted arrays A and B, A has extra space at the end to accommodate the elements of B. Write a function to merge the two in a sorted manner. ( I mean A should contain both in sorted order )
3. During winters, planes are not able to land @ the delhi airport due to the excess fog.
As a result, they keep cycling around the airport waiting for the runway to be free and conditions to be suitable for landing. In such a condition the planes could also run out of reserved fuel having disastrous consequences.
What steps would you take to avoid such a situation!
The problem statement asked to provide an immediate solution and a long term one.
4. Given a tree, write a function to determine if it is a valid binary tree.

Both these rounds went well for me and by the time it ended it was late in the night. The results were announced when the interview panels of MS came to campus the next week. I cleared the test for both the profiles and was slated to have interviews for both the profiles.

Depending on your score there are two classifications that MS, full loop and group fly. For the full loop candidates, their interviews start immediately but for the group fly candidates, they are given a few coding problems that they must write solutions on paper and those who clear that have interviews. I was in the full loop category but I&#8217;ll post the group fly questions here.
1. Check given binary tree is bst or not.
2. Implement strstr
3. Implement malloc and free.

As you can see that these questions are much harder than the interview questions itself and only 2 of the 17 candidates moved further from the group fly round.
Due to an issue with the limited time, I had interviews only for the IDC profile. In the first round, I was asked the following questions

1. Tell me about a recent project that you worked on.

2. How would you generate all the permutations of a given string?

After I did that, he asked me how I would remove duplicate permutations that would occur if characters were repeated.

After this I was asked to write test cases for the function that I had written.

3. How would you add two really large numbers?

I used a linked list, he wanted me to optimize my solution. As seems the norm with MS, I was asked to write test cases for this one too.

4. Any questions that you&#8217;d like to ask me?

I don&#8217;t remember what I asked him but I do ask interviewers something either about tips that would help me improve or about their experience. This is a question that every interviewer asks at the end of an interview.

For the next round, the interviewer asked me the following questions :

1. Do you use paint?

Me> No, Haven&#8217;t done so for a long time.

That&#8217;s ok let&#8217;s do some painting today.

Me> Ok, sure.

Then he drew multiple shapes that partially overlapped with each other and asked me to write the code for the fill function which would paint a particular region on which the mouse was clicked with the chosen fill color.

I thought about it and came up with a recursive solution in which I moved to the adjacent pixels and colored them if their color was the same as the current pixel and then make a call to the same function with each of the adjacent pixels on the lines of Breadth First Search. He wasn&#8217;t too impressed with my solution but after some convincing he was ok with it.

2. In ten minutes write code to insert a node in a doubly linked list sorted in ascending order in C.

I told him that I didn&#8217;t know C so he said I could use C++ instead.

There was a silly mistake with the greater than and lesser than sign in one of the conditions, he asked me to examine my code and to find and fix it. After reading it a couple of times I was able to fix it.

3. Any questions for me?

After these rounds were done we waited for a couple of hours, the final round was an interview with the Vice President of the Windows group, he asked me to write code to remove consecutive duplicates in a given string in place.

I did this with two pointers, again there were a couple of small errors where my pointers were off by one place. he asked me to find and fix the errors which I did. I was then asked to write test cases for the function that I had written.

That was the end of the interview process, we had to wait for a couple more hours for the results to be announced. I was quite optimistic but my name wasn&#8217;t there amongst the 3 candidates that they had selected for the IDC profile. It was very disappointing at that time because I felt that I stood a fair chance. Looking back I think that I should have been more careful when writing code so as to avoid off by one errors but in the tense interview environment, these things do creep in, no matter how careful you are.

Someone with a good grasp of the fundamentals of data structures and algorithms specially trees, linked lists and elementary graph algorithms has a good chance when it comes to clearing a MS interview. Also a lot of questions were typical interview problems that can be found in most books and also around on the internet. If you want a job at Microsoft then prepare well for your interview. Let me know in comments if you found this post useful. If people are interested, then I&#8217;ll post other experiences here too. Don&#8217;t ask me questions about MS or the profiles or for the answers to the questions that I&#8217;ve posted for all of those are freely available online.
