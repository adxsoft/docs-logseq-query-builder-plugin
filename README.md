<div id="top"></div>


<!-- This README.md is the full documentation and is kept separately at
https://github.com/adxsoft/docs-logseq-query-builder-plugin
 -->

## Logseq Query Builder Plugin - Documentation

To install the plugin go to https://github.com/adxsoft/logseq-query-builder-plugin 

## logseq-query-builder-plugin
- builds advanced logseq queries from [Simple Commands](#simple-commands) contained in a logseq code block. 
- Choosing **Advanced Query Builder** in the code blocks menu (right click on block's bullet)
    - will generate an advanced query in a **new** child block
    - You can alter the code block and generate another query which will add another new child block. 
    - In this way you can experiment with generating multiple advanced queries.
<p>

- [How to Use the plugin](#how-to-use-this-plugin)
- Simple Commands
    - [Overview](#simple-commands-overview)
    - [Important Concept](#important-concept)
    - [Wildcards](#wildcards)
    - [Detailed](#commands)
- [About](#about)

<div id="how-to-use-this-plugin"></div>


## How to use  the plugin
The [Simple Commands](#simple-commands) are entered into a logseq code block in the structure shown below. _Note there are three backticks that surround the commands_<br>
<pre>
```
- commandname
    - argument
    - argument
- commandname
    - argument
    - argument
```
</pre>
Optionally arguments can begin with any of these words
```
and
or
not
```

Here is an example that selects pages in namespace physics with page property pagetype 'fluids'
<pre>
```
title: Example Commands
- pages
    - *
- pageproperties
    - pagetype, "fluids"
- namespace
    - physics 
```
</pre>
You can include a title for the generated query like this
```
title: your text for the query title
```
You can request comments describing the generated query lines by adding this line at the start of the code block
```
option: includecomments
```


<p align="right">(<a href="#top">back to top</a>)</p>

<div id="simple-commands-overview"></div>

## Simple Commands - Overview
_Alphabetical Order_

| Simple Command | Description |
|---|---|
|[blocks](#blocks-command) |select logseq blocks by wildcards |
|[blockproperties](#blockproperties-command) |select blocks by property values |
|[blocktags](#blocktags-command) |select blocks by tag |
|[deadline](#deadline-command) |select pages or blocks that have a deadline |
|[deadlinebetween](#deadlinebetween-command) |select pages or blocks that have a deadline in a date range |
|[journalsbetween](#journalsbetween-command) |only select journal pages in a date range |
|[journalonly](#journalonly-command) |only select journal pages |
|[namespace](#namespace-command) |select pages or blocks within a namespace |
|[option](#option-command) | query generation option |
|[pages](#pages-command) |select pages by wildcards |
|[pageproperties](#pageproperties-command) |select pages by page properties |
|[pagetags](#pagetags-command) |select pages by tag |
|[pagelinks](#pagelinks-command) |select blocks that have links to pages<br>- note. Journal page link is your chosen format in your settings. For example <i>Dec 25th, 2022</i> |
|[tasks](#tasks-command) |select tasks |
|[scheduled](#scheduled-command) |select pages or blocks that are scheduled |
|[scheduledbetween](#scheduledbetween-command) |select pages or blocks that are scheduled in a date range |

<p align="right">(<a href="#top">back to top</a>)</p>

<div id="important-concept"></div>

#### Important Concept 
Queries filter in two ways - pages or blocks

<b>pages</b> command retrieves the special blocks that have ONLY the page information<br> such as name, page tags, page properties
<small><i>- these page blocks are placed into the ?block variable</i></small><br>
<b>blocks</b> command retrieves every single block in the graph including the special page blocks
<small><i>- these page blocks are placed into the ?block variable and the page this block belongs to is placed in the ?page variable</i></small><br><br>
You must choose a <b>pages</b> command <b>OR</b> a <b>blocks</b> command (you cannot use both together) 

<p align="right">(<a href="#top">back to top</a>)</p>
                   
<div id="wildcards"></div>

#### Wildcards
Wildcards can be full name or partial name using \* character<br>

- `test\*` - argument starts with text 'test'
- `\*end` - argument ends with text 'end'
- `\*tax\*` - argument contains text 'tax' anywhere

Note.
- Wildcards are used with pages or blocks command at this stage
- Unfortunately Logseq Advanced queries do not yet support partial strings for properties
    - see (https://github.com/logseq/logseq/issues/7410). 
        - Once this is implemented in Logseq I will be able to have wildcards for  _pageproperties_ and _blockproperties_ commands and perhaps for partial references to tags

<p align="right">(<a href="#top">back to top</a>)</p>

<div id="commands"></div>

## Simple Commands in Detail

### Main extraction commands
- [pages](#pages-command) - select pages by wildcards
- [blocks](#blocks-command) - select logseq blocks by wildcards

### Properties
- [pageproperties](#pageproperties-command) - select pages by page properties
- [blockproperties](#blockproperties-command) - select blocks by block properties

### Tags
- [pagetags](#pagetags-command) - select pages by tag
- [blocktags](#blocktags-command) - select blocks by tag

### Tasks
- [tasks](#tasks-command) - select tasks

### Journals
- [journalonly](#journalonly-command) - only select journal pages
- [journalsbetween](#journalsbetween-command) - only select journal pages in a date range

### Deadline
- [deadline](#deadline-command) - select pages or blocks that have a deadline
- [deadlinebetween](#deadlinebetween-command) - select pages or blocks that have a deadline in a date range

### Scheduled
- [scheduled](#scheduled-command) - select pages or blocks that are scheduled
- [scheduledbetween](#scheduledbetween-command) - select pages or blocks that are scheduled in a date range     

### Namespaces
- [namespace](#namespace-command) - select pages or blocks within a namespace

### Links
- [pagelinks](#pagelinks-command) - select blocks that have links to pages<br>- note. Journal page link is your chosen format in your settings. For example <i>Dec 25th, 2022</i>

### Query Results commands
- [collapse](#collapse-command) - collapse query results
- [expand](#collapse-command) - expand query results
- [showbreadcrumbs](#showbreadcrumbs-command) - show query breadcrumbs
- [hidebreadcrumbs](#hidebreadcrumbs-command) - hide query breadcrumbs

### Query Builder options
- [option](#option-command) - options for query generation

<p align="right">(<a href="#top">back to top</a>)</p>

## Simple Commands - Detailed Examples
<div id="pages-command"></div>

### pages
A page is a special block of its own that contains page-specific information including page tags, page properties etc. It is a parent to any blocks that belong to the page. Each page has a title and you can choose pages using their full title or wildcards patterns of their title.

    ```
    title: pages command - select all pages
    - pages
        - *
    ```
    
    ```
    title: pages command - specific pages
    - pages
        - testpage001
        - testpage002
    ```

    ```
    title: pages command - pages by wildcards
    - pages
        - testpage00*
    ```

    ```
    title: pages command - pages by wildcards
    - pages
        - *002
    ```

    ```
    title: pages command - pages by wildcards
    - pages
        - *page00*
    ```

    ```
    title: pages command - ignore pages (including wildcards)
    - pages
        - not testpage*
        - not Queries*
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>

<div id="blocks-command"></div>

### blocks
Blocks are the basic unit of information in Logseq. Blocks can contain text, tags, properties, links to other pages or blocks.Each block has a content property and you can choose blocks using their content or wildcards patterns of their content.

    ```
    title: select all blocks
    - blocks
        - *
    ```

    ```
    title: select blocks by wildcards using *
    - blocks
        - startingtext*
        - *endingtext
        - *textanywhere*
    ```

    ```
    title: blocks command - ignore blocks using wildcards
    - blocks
        - not And sir dare view*
        - not *here leave merit enjoy forth.
        - not *roof gutters*
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>

<div id="blockproperties-command"></div>

### blockproperties
Every Logseq block can contains user properties which consist of the property name and the property value. Property name cannot contains spaces. Values can be a string (in double quotes) or a number. 

    ```
    title: select and exclude blocks with block properties
    - blocks
        - *
    - blockproperties
        - category, "b-thriller"
        - category, "b-western"
        - grade, "b-fiction"
    ```

    ```
    title: block property combinations using and and or
    - blocks
        - *
    - blockproperties
        - category, "b-fiction"
        - or grade, "b-western"
        - and category, "b-travel"
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>

<div id="blocktags-command"></div>


### blocktags
Every Logseq block can contain tags. Tags can be selected by their full name (excluding #) or by wildcards of the tag full name.

    ```
    title: blocktags - select and exclude block level tags
    - blocks
        - *
    - blocktags
        - tagA
        - tagD
        - not tagB
    ```

    ```
    title: blocktags and pages don't mix
    - pages
        - testpage00*
    - blocktags
        - tagA
        - not tagB
    ```

    ```
    title: block tag combinations using and and or
    - blocks
        - *
    - blocktags
        - tagA
        - or tagB
        - and tagD
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="deadline-command"></div>


### deadline
Every Logseq block can contain a deadline date. Include this command to select only these blocks.

    ```
    title: find blocks with deadlines
    - blocks
        - *
    - deadline
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="deadlinebetween-command"></div>


### deadlinebetween
Every Logseq block can contain a deadline date. Include this command to select only these blocks whose deadline date falls within a from and to date. Dates are specified as :today or :ddd-xxxxxx where ddd is no of days and xxxxxx is before or after.

    ```
    title: find blocks with deadlines in a date range
    - blocks
        - *
    - deadlinebetween
        - :120d-before :30d-after
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="journalsbetween-command"></div>


### journalsbetween
Every Logseq journal belongs to a specific date. Include this command to select only those journals which fall within a from and to date. Dates are specified as :today or :ddd-xxxxxx where ddd is no of days and xxxxxx is before or after.
    ```
    title: find journal in a date range
    - pages
        - *
    - journalsbetween
        - :today :30d-after
    ```

    ```
    title: find journals between dates
    - blocks
        - *
    - journalsbetween
        - :30d-before :today
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="journalonly-command"></div>


### journalonly
Use this command to limit the query results to journals only, pages get excluded.

    ```
    title: find journals
    - pages
        - *
    - journalonly
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="namespace-command"></div>


### namespace
use this command to restrict query results to one of more namespaces. Note pages or blocks have to exist at the specified level of the namespace in order for you see any results. 
_(Note. If you only have one page which is physics/fluids and no page exists called physics then using physics as the namespace will not find physics/fluids page you must specify physics/fluid to see it in the query results. This behaviour will hopefully change one day to show all lower level pages under physics.)_

    ```
    title: only search pages in specific namespace
    - pages
        - *
    - namespace
        - physics
    ```

    ```
    title: find block properties in a namespace
    - blocks
        - *
    - namespace
        - tech/python
    - blockproperties
        - grade, "b-fiction"
    ```

    ```
    title: find scheduled blocks in a namespace
    - blocks
        - *
    - namespace
        - physics
    - scheduled
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="pageproperties-command"></div>


### pageproperties
Every Logseq page can contains user properties which belong to the page. Page properties are not block properties, they belong only to the page. Page properties consist of the property name and the property value. Property name cannot contains spaces. Values can be a string (in double quotes) or a number. 

    ```
    title: select and exclude pages with page properties
    - pages
        - *
    - pageproperties
        - pagetype, "p-major"
        - pagetype, "p-minor"
        - not pagetype, "p-advanced"
    ```

    ```
    title: page property combinations using and and or
    - pages
        - *
    - pageproperties
        - pagecategory, "p-minor"
        - or pagecategory, "p-minimum"
        - and pagetype, "p-type1"
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="pagetags-command"></div>


### pagetags
Every Logseq page can contains tags which belong to the page. Page tags are not block tags, they belong only to the page. Page tags can be selected by their full name (excluding #) or by wildcards of the tag full name.

    ```
    title: pagetags - page level tags
    - pages
        - testpage*
    - pagetags
        - classA
    ```

    ```
    title: pagetags and pages
    - pages
        - *dynamics*
    - pagetags
        - classB
    ```

    ```
    title: page tag combinations using and and or
    - pages
        - *
    - pagetags
        - classA
        - or classB
        - and classH
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="pagelinks-command"></div>


### pagelinks
Every logseq block can contain links to other pages or journals. This command will restrict query results to blocks that contains one or more link references. Note the date format to link to journals should be in the same format the journal titles are set in Logseq settings. 

    ```
    title: select blocks with links to journals that use the default date setting for journals
    - blocks
        - *
    - pagelinks
        - Dec 25th, 2022
        - Jan 1st, 2019
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="tasks-command"></div>


### tasks
Every Logseq block can contains one or more tasks. This command will restrict results to include (or exclude) specific task types

    ```
    title: select and exclude task types
    - tasks
        - TODO
        - not DOING
    ```

    ```
    title: select and exclude task types
    - pages
        - testpage00*
    - tasks
        - TODO
        - not DOING
    ```

    ```
    title: task and or combintions
    - blocks
        - *
    - tasks
        - TODO
        - and WAITING
        - or LATER
        - not DOING
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="scheduled-command"></div>


### scheduled
Every Logseq block can contain a schedule date. Include this command to select only these blocks.

    ```
    title: find scheduled blocks
    - blocks
        - *
    - scheduled
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="scheduledbetween-command"></div>


### scheduledbetween
Every Logseq block can contain a schedule date. Include this command to select only these blocks whose schedule date falls within a from and to date. Dates are specified as :today or :ddd-xxxxxx where ddd is no of days and xxxxxx is before or after.

    ```
    title: scheduled - find scheduled blocks in a date range
    - blocks
        - *
    - scheduledbetween
        - :20d-before :20d-after
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="option-command"></div>


### option
Currently there is only one option available. 
_includecomments_ option will include a comment line which explains the generated query line.

    ```
    title: option - include comments for each generated query line
    option: includecomments
    - blocks
        - *
    - pagelinks
        - Dec 25th, 2022
        - Jan 1st, 2019
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="collapse-command"></div>


### collapse 
This command will cause the query results to be collapsed.

    ```
    title: collapse results
    - pages
        - testpage00*
    - collapse
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="expand-command"></div>


### expand 
This command will cause the query results to be expanded fully.

    ```
    title: expand results
    - pages
        - testpage00*
    - expand
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="showbreadcrumbs-command"></div>


### showbreadcrumbs 
Show breadcrumb trail (parent levels in the outline) of the retrieved blocks in query results

    ```
    title: show breadcrumbs
    - pages
        - testpage00*
    - showbreadcrumb
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>
<div id="hidebreadcrumbs-command"></div>


### hidebreadcrumbs 
Hide the breadcrumb trail (parent levels in the outline) of the retrieved blocks in query results

    ```
    title: hide breadcrumbs
    - pages
        - testpage00*
    - hidebreadcrumb
    ```
<p align="right">(<a href="#commands">back to Simple Commands</a>)</p>

<div id="about"></div>


## About

#### Why this plugin?
The reasons I created this plugin are
- Advanced Queries have a complicated syntax that causes errors eg. missing brackets  
- For non developers they can build advanced queries and avoid having to learn coding in clojure and datalog
- Logseq users can learn by using the examples to in this documentation

#### Caution
_This plugin will generate an advanced query for you. It covers the basics and will save you time and allow you to experiment with advanced queries. It will not however cover all situations and the generated query may require you to add further lines. Further help is always available at the [Logseq Discord forum](https://discord.com/invite/KpN4eHY)_

#### Built from the original online tool
The plugin is an implementation of the functions of the online tool [_Logseq Advanced Query Builder_](https://adxsoft.github.io/logseqadvancedquerybuilder/). The underlying software for both the online tool and this plugin are shared so all commands work consistently. 

Currently plugins are not supported in the mobile versions of Logseq. However you can use the online tool to buid advanced queries from a mobile browser. See the FAQ at  for detailed instructions for using the online tool. 


##### End of Documentation
<p align="right">(<a href="#top">back to top</a>)</p>
