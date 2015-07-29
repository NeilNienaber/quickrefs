


# YAML (YAML Ain't Markup Language)

_a human friendly data serialization standard for all programming languages_


## What's human friendly?

#### Let's you use comments or blank lines


Example: `themes.yml`.

```yaml
#########################################
# Dr. Jekyll's Themes - Add Your Theme!

- title:     Bootstrap
  github:    drjekyllthemes/jekyll-bootstrap-theme
  branch:    gh-pages
  author:    Dr. Henry Jekyll et al
  thumbnail: drjekyll-bootstrap.png
  license:   Public Domain

- title:     Classics Book    ## Todo: Rename to World Classics - Why? Why Not?
  github:    drjekyllthemes/jekyll-book-theme
  branch:    gh-pages
  author:    Dr. Henry Jekyll et al
  thumbnail: drjekyll-book.png
  license:   Public Domain  
```

is the same as:

~~~
- title: Bootstrap
  github: drjekyllthemes/jekyll-bootstrap-theme
  branch: gh-pages
  author: Dr. Henry Jekyll et al
  thumbnail: drjekyll-bootstrap.png
  license: Public Domain
- title: Classics Book
  github: drjekyllthemes/jekyll-book-theme
  branch: gh-pages
  author: Dr. Henry Jekyll et al
  thumbnail: drjekyll-book.png
  license: Public Domain
~~~


#### Let's you use strings or keys without (requiring) quotes

~~~
title:   Bootstrap
github:  drjekyllthemes/jekyll-bootstrap-theme
author:  Dr. Henry Jekyll et al
~~~

is the same as:

~~~
"title": "Bootstrap"
"github": "drjekyllthemes/jekyll-bootstrap-theme"
"author": "Dr. Henry Jekyll et al"
~~~


**Gotschas**

When to use quotes for your strings?

If you string includes a colon (`:`) you MUST quote your string. Example:

~~~
title: "Text Processing with Ruby: Extract Value from the Data That Surrounds You"
title: "Sinatra: Up and Running - Ruby for the Web, Simply"
~~~



## List of Key/Value Records

Book List Example (e.g. `books.yml`):

~~~
- title:     "Text Processing with Ruby: Extract Value from the Data That Surrounds You"
  author:    Rob Miller
  cover:     2015/text-processing-with-ruby.jpg
  publisher: Pragmatic Bookshelf
  date:      Nov 2015
  pages:     200 pages (est)
  book_url:  https://pragprog.com/book/rmtpruby/text-processing-with-ruby

- title:     "Learn Ruby the Hard Way"
  subtitle:  A Simple and Idiomatic Introduction to the Imaginative World Of Computational Thinking with Code
  edition:   3rd Edition
  author:    Zed Shaw
  cover:     2014/learn-ruby-the-hard-way.jpg
  publisher: Addison-Wesley Professional (Zed Shaw's Hard Way Series)
  date:      Dec 2014
  pages:     336 pages
  book_url:  http://www.informit.com/store/learn-ruby-the-hard-way-a-simple-and-idiomatic-introduction-9780321884992

- title:     "Sinatra: Up and Running - Ruby for the Web, Simply"
  author:    Alan Harris, Konstantin Haase
  cover:     2011/sinatra-up-and-running.jpg
  publisher: O'Reilly Media
  date:      Dec 2011
  pages:     122 pages
  book_url:  http://shop.oreilly.com/product/0636920019664.do
~~~

Use like:

~~~
{% for book in site.data.books %}
  <div>
  <a href="{{ book.book_url }}">
    <img src="{{site.url}}/i/{{book.cover}}">
  </a>
  {{ book.title }}
  {% if book.edition %}
    ({{ book.edition}})
  {% endif %}
  by
  {{ book.author }};
  {{ book.publisher }},
  {{ book.date }};
  {{ book.pages}}
{% endfor %}
~~~



## Nested List of Key/Value Records

Navigation Menu Example: e.g. `nav.yml`

~~~
- title: Home
  href:  /

- title: Learn
  href:  /learning-resources/
  subcategories:
  - title: Learning topic one
    href:  /learn1/
  - title: Learning topic two
    href:  /learn2/
  - title: Learning topic three
    href:  /learn3/

- title: Tools
  subcategories:
  - title: Tools one
    href:  /tools1/
  - title: Tools two
    href:  /tools2/

- title: About Us
  href:  /about-us/
~~~


Use like:

~~~
<nav>
  <ul>
    {% for nav in site.data.nav %}
      {% if nav.subcategories != null %}
        <li>
          <a href="{{ site.url }}{{ nav.href }}">{{ nav.title }} ▼</a>
          <ul>
          {% for subcategory in nav.subcategories %}
            <li><a href="{{ site.url }}{{ subcategory.href }}">{{ subcategory.title }}</a></li>
          {% endfor %}
          </ul>
        </li>
      {% else %} 
        <li>
          <a href="{{ site.url }}{{ nav.href }}">{{ nav.title }}</a>
        </li>
      {% endif %}
    {% endfor %}
  </ul>
</nav> 
~~~



## Hash (Dictionary) of Key/Value Records

Author List Example: e.g. `people.yml`

~~~
henry:
  name:    Dr. Henry Jekyll
  twitter: henryjekyll

edward:
  name:    Edward Hyde
  twitter  edhyde
~~~


Use like:

Example 1) Lookup author info in a post

~~~
---
title:  sample post
author: henry
---

{% assign author = site.data.people[ page.author ] %}
<a href="{{ author.twitter }}">
         {{ author.name }}
</a>
~~~~



## Multi-Line Strings

### Unfolded (e.g. Keep Newlines) - `|`

~~~
text: |
   There once was a short man from Ealing
   Who got on a bus to Darjeeling
       It said on the door
       "Please don't spit on the floor"
   So he carefully spat on the ceiling
~~~

The leading indent (of the first line) and trailing white space gets stripped e.g. becoming:

~~~
There once was a short man from Ealing\n
Who got on a bus to Darjeeling\n
    It said on the door\n
    "Please don't spit on the floor"\n
So he carefully spat on the ceiling\n
~~~




### Folded (e.g. Strip Newlines) - `>`

~~~
text: >
   Wrapped text
   will be folded
   into a single
   paragraph
   
   Blank lines  denote
   paragraph breaks
~~~

Folded text converts newlines to spaces
and removes leading whitespaces e.g. becoming:

~~~
Wrapped text will be folded into a single paragraph\n
\n
Blank lines denote paragraph breaks\n
~~~




## Literal Keys

Note: You can use upper case letters in your keys (e.g. `Teams`),
add spaces (e.g. `Bundesliga Teams`) and
even start with numbers (e.g. `18 Teams`). Example:

~~~
18 Teams:
  - Austria Wien
  - SC Salzburg
  - Sturm Graz
~~~



## More Gotschas

**Predefined Constants**

Boolean true constants:

~~~
true
Y
Yes
ON
~~~~

Will become => boolean true

Boolean false constants:

~~~
FALSE
n
No
off
~~~

Will become => boolean false


Null constants:

~~~
~
null
~~~

Will become => null (no value)





## References

**YAML Headquarters**
- YAML (web: [yaml.org](http://yaml.org))
     - [YAML Reference Card](http://yaml.org/refcard.html)


**More**

- [YAML @ Wikipedia](https://en.wikipedia.org/wiki/YAML)



## Meta

**License** 

The YAML Quick Reference is dedicated to the public domain. 
Use it as you please with no restrictions whatsoever.

**Questions? Comments?**

Post them to the [jekyll talk forum](https://talk.jekyllrb.com). Thanks!
