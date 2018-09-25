# Djagno-Pagination-Tutorial

## Step 1:

* In your `views.py` file, import: 


  `from django.core.paginator import EmptyPage, PageNotAnInteger, Paginator`

  `from django.shortcuts import render`

## Step 2:

Create a function that returns the render of the HTML file 

    ` #define a function that takes request as an argument
        def feed(request):
      
      #define a variable to hold paginator and assign the value to Paginator from Django library which returns a list of 
      objects as the first parameter and the number of items to be included on each page.
        paginator = Paginator(photos, 10)
        
      #create a variable named page and assign it to request.GET.get('page') which takes the request parameter which contains       the GET variables. Append the .get() method to the request.GET to get the page value from the dictionary, if no value         exists, the method will return 1 for the first page.
      page = request.GET.get('page')
      
      #create a new variable and assign that to the value of paginator and call the .get_page method that gets the current  
      page number out of all of the pages 
      
      photos = paginator.get_page(page)
      
      #return the render of the page the pagination should appear on and pass back a dictionary with the value of the page   
      number 
    
        return render(request,'petpals_app/explore.html', {'photos':photos})`
        
## Step 3: 

In .html file, create a DIV class where pagination is expected to render:

`<div class="pagination">`

Create a span class to hold a links to go to previous and next pages.  &laquo represents a left arrow, &raquo represents a right arrow

        `<span class="step-links">
        {% if photos.has_previous %}
            <a href="?page=1"> &laquo;   First  | </a>
            <a href="?page={{ photos.previous_page_number }}">   Previous | </a>
        {% endif %}
        
Create a span tag to display what page the user is on out of the total number of pages contained on the site (ex. 2/4)
       ` <span ="current">
            Page {{ photos.number }} of {{ photos.paginator.num_pages }}
        </span>`
       
If the current page has a next page, render the next page number, then 

        `{% if photos.has_next %}
            <a href="?page={{ photos.next_page_number }}">  | Next |</a>
            <a href="?page={{ photos.paginator.num_pages }}">  Last |&raquo; </a>
        {% endif %}`
