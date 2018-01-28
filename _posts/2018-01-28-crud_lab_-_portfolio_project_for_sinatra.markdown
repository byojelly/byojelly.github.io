---
layout: post
title:      "CRUD LAB - Portfolio Project for Sinatra"
date:       2018-01-28 20:21:20 +0000
permalink:  crud_lab_-_portfolio_project_for_sinatra
---


Today I have completed my portfolio project for SInatra.  When given the assignment, we had the opportunity to create any application we wished. I decided to create a Library Inventory System.    The library inventory system that I created provides users the ability to use CRUD (create/read/update/destroy) functionalities for books, users (librarians and consumers), libraries, sections, and more. 

When looking back on the development process of my application, my most difficult coding challenge was persisting specific objects and data from a get request through the post request of the form.  Post requests yield data from the params hash depending on what input data is extracted from your form (located on the get request).   My challenge was to make a dynamic link within the post request that required object data that was not within the original form.

After some time thinking about a solution, I remebered that the sessions hash could also be used to store temporary information.  Therefore, in order to retain the specifc data that I needed to create a dynamic url (redirect) within the post request, I added the information into the session hash previous to the posts request and then deleted the information after its utility was realized. 

This portfolio project humbled my understanding of the associations of complex database tables and as a result, I believe that I benefited by becoming more confident with my code and ability to create Sinatra applications.

If interested take a look at my code and give it a try yourself.
https://github.com/byojelly/Library_Inventory_CRUD

Sincerly,
Byojelly



