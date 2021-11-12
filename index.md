# CMS Attributes

The following is a description of all attributes that can be used in the Coot-CMS.

## 📝 Table of Contents

- [data-cms-block](#data-cms-block)
  - [data-cms-block-update="disabled"](#data-cms-block-update-disabled)
- [data-cms-createdat](#data-cms-createdat)
- [data-cms-pattern](#data-cms-pattern)
- [data-cms-structured](#data-cms-structured)
- [data-cms-short-code](#data-cms-short-code)
  - [data-cms-filters](#data-cms-filters)
  - [data-cms-short-code-type](#data-cms-short-code-type)
- [data-cms-attribute](#data-cms-attribute)
  - [data-cms-attribute="seperator"](#data-cms-attribute-seperator)
  - [data-cms-attribute="tag-list"](#data-cms-attribute-tag-list)
    - [data-cms-tag-slug="allow"](#data-cms-tag-slug-allow)
    - [data-cms-tag-display="true"](#data-cms-tag-display-true)
    - [data-cms-tag-group](#data-cms-tag-group)
  - [data-cms-attribute="single-tag"](#data-cms-attribute-single-tag)
  - [data-cms-attribute="slug"](#data-cms-attribute-slug)
  - [data-cms-attribute="list-wrapper"](#data-cms-attribute-list-wrapper)
    - [data-cms-list-index](#data-cms-list-index)
    - [data-cms-display-limit](#data-cms-display-limit)
    - [data-cms-filters](#data-cms-filters-list)
    - [data-cms-limit](#data-cms-limit)
    - [data-cms-sorts](#data-cms-sorts)
    - [data-cms-skip](#data-cms-skip)
    - [data-cms-url-filter="true"](#data-cms-url-filter-true)
  - [data-cms-attribute="google-analytics-placeholder"](#data-cms-attribute-google-analytics-placeholder)
  - [data-cms-attribute="facebook-pixel-placeholder"](#data-cms-attribute-facebook-pixel-placeholder)
- [data-cms-breadcrumb](#data-cms-breadcrumb)
- [data-cms-breadcrumb-data](#data-cms-breadcrumb-data)
- [data-cms-page](#data-cms-page)
- [Easy Edit](#data-cms-ideal)
  - [data-cms-ideal](#data-cms-ideal)
    - [data-cms-ideal-label](#data-cms-ideal-label)
    - [data-cms-ideal-icon](#data-cms-ideal-icon)
    - [data-cms-order](#data-cms-order)
    - [data-cms-easy-edit-group](#data-cms-easy-edit-group)
  - [data-cms-form-structure](#data-cms-form-structure)
  - [data-cms-easy-edit-list](#data-cms-easy-edit-list)
- [data-cms-editor-modified="true"](#data-cms-editor-modified-true)
- [data-cms-modified-css="true"](#data-cms-modified-css-true)
- [data-cms-tag](#data-cms-tag)
  - [data-cms-tag-url](#data-cms-tag-url)
  - [data-cms-alias](#data-cms-alias)
- [data-cms-slug](#data-cms-slug)
- [Sitemap Properties](#sitemap-properties)
  - [data-cms-sitemap-priority](#data-cms-sitemap-priority)
  - [data-cms-sitemap-frequency](#data-cms-sitemap-frequency)
  - [data-cms-sitemap-lastmod](#data-cms-sitemap-lastmod)
- [data-cms-viewport="true"](#data-cms-viewport-true)
- [data-cms-dimensions](#data-cms-dimensions)
- [data-cms-purge](#data-cms-purge)
- [data-cms-disabled](#data-cms-disabled)

---

### data-cms-block <a name="data-cms-block"></a>

- This attribute identifies a block in the html code.

- When a file is uploaded with data-cms-block="block_id" assigned to a html tag the backend creates a editable block code html object and saves a copy of the block code for further use.

- When the block code is updated through the CMS editor all the pages using the same block will be updated. This feature is optional and user can decide whether to update all the affected pages or not.

- The purpose of this attribute is to minimize the need to update the same code in multiple pages as for many pages in a site some of the areas remain uneffected. For Eg: Header and Footer of a website.

---

#### data-cms-block-update="disabled" <a name="data-cms-block-update-disabled"></a>

- This attribute is assigned to the element already having the [data-cms-block](#data-cms-block).

- The purpose of this attribute is to signify that the block code in this particular html page should not be updated when the central block code is updated.

---

### data-cms-createdat <a name="data-cms-createdat"></a>

- This attribute is used to create a page with a custom date assigned by the user. This date can also be updated after the page has been created.

- The purpose for this tag is for sorting. while using list builders in CMS i.e. [data-cms-attribute="list-wrapper"](#data-cms-attribute-list-wrapper).

- The format for date should be as follows:
  data-cms-createdat="YYYY-MM-DD".

---

### data-cms-pattern <a name="data-cms-pattern"></a>

- This attribute is assigned to an element that make use of page properties and project properties to create a dynamic html code.

- Example:
  Code inside html before creation/updation

  ```html
  <link
    rel="canonical"
    data-cms-pattern="https://www.{{domain_name}}/{{slug}}"
  />
  ```

  Code after processing from backend

  ```html
  <link
    rel="canonical"
    data-cms-pattern="https://www.{{domain_name}}/{{slug}}"
    href="https://www.example.com/home"
  />
  ```

- Possible variable that can be used for creating a pattern

  1. short_codes.short_code_name
  2. domain_name
  3. slug

- The purpose for this attribute is to avoid manually updating some variable code with the help of a few page properties.

- The format for data-cms-pattern should be in [handlebars](https://handlebarsjs.com/) format.

---

### data-cms-structured <a name="data-cms-structured"></a>

- This attribute identifies a custom SEO Markup in the html code.

- The JSON Schema for SEO Markup is saved in the backend for further updation.

- The content of this attribute should be a unique structured data id.

- Example:

  - Let's say we have a BlogPost structured data the html code will be as follows:
    ```html
        <script type="application/json" 
        data-cms-structured="blog-post"
        >{"@context":"http://schema.org","@type":"Blog","name":"{{short_codes.blog-title}}","url":"{{domain_name}}{{slug}}","description":"{{short_codes.blog-description}}","blogPosts":[{"@type":"blogPosting","mainEntityOfPage":"{{domain_name}}{{slug}}","headline":"{{short_codes.blog-title}}","author":"{{short_code.blog-author-text}}","datePublished":"{{short_codes.blog-date}}","image":{"@type":"ImageObject","url":"{{short_codes.blog-image}}"}"dateModified":"{{short_codes.blog-date}}"}]}</script>
    ```

    This data will be processed in all the pages using the same structured data so that the user doesnt have to update this information in every page.

---

### data-cms-short-code <a name="data-cms-short-code"></a>

- The purpose of this short code is to save a value assigned to a key for using them in other pages and list builders.

- Default short codes for each project:

  1. blog-long-desc
  2. blog-short-desc
  3. blog-author-text
  4. blog-author-image
  5. blog-date
  6. blog-read-time
  7. blog-title
  8. blog-image

- Example:

  ```html
    <div|span|p|h*|pre|main|section
     data-cms-short-code="div-example"
    >TEST</div|span|p|h*|pre|main|section>
  ```

  ```html
  <a
    data-cms-short-code="anchor-example"
    href="https://example.com/about-us"
  >Some Anchor Text</a>
  ```

  ```html
  <img
    data-cms-short-code="image-example"
    src="https://example.com/image.jpg"
  />
  ```

  The backend will save these values as :

  ```json
  short_codes : {
  "div-example":"TEST",
  "anchor-example":{"text" : "Some Anchor Text","href":"https://example.com/about-us"},
  "image-example":"https://example.com/image.jpg"
  }
  ```

- These values can be used in [data-cms-pattern](#data-cms-pattern).

---

#### data-cms-filters <a name="data-cms-filters"></a>

- This attribute is used with the data-cms-short-code attribute. When the short code value is being called rather than assigned.

- The filter value usually is a query for an individual page.

- For more details regarding the format of the value of this attribute refer [data-cms-filters](#data-cms-filters-list)

---

#### data-cms-short-code-type <a name="data-cms-short-code-type"></a>

- This attribute is used with the data-cms-short-code attribute.

- There is currently only one option i.e. int

- Example:
  ```html
  <div|span|p|h*|pre|main|section 
   data-cms-short-code="div-example" data-cms-short-code-type="int"
  >4<|div|span|p|h*|pre|main|section>
  ```
  The value extracted from this will be treated as an integer instead of a string.

---

### data-cms-attribute <a name="data-cms-attribute"></a>

#### data-cms-attribute="seperator" <a name="data-cms-attribute-seperator"></a>

- This attribute is a system tag (DO NOT REMOVE IF ENCOUNTERED).

---

#### data-cms-attribute="tag-list" <a name="data-cms-attribute-tag-list"></a>

- This attribute is assigned to a "list item" for listing tags for that "list item".

- The element should have atleast a single child to be treated as a template to build all tags.

- Other attributes related to this attribute:

  _data-cms-tag-slug="allow" <a name="data-cms-tag-slug-allow"></a>_

  - This attribute is assigned with data-cms-attribute="tag-list" to signify that every element in the tag list is an anchor and it shoud have the tag's associated slug.

  _data-cms-tag-display="true" <a name="data-cms-tag-display-true"></a>_

  - This attribute is assigned with data-cms-attribute="tag-list" to signify that every element in the tag should be a visible element in the DOM and the inner html of each element should have either the tag alias if provided if not then the tag name.

  _data-cms-tag-group <a name="data-cms-tag-group"></a>_

  - This attribute is assigned with data-cms-attribute="tag-list" to filter out the tags of a certain tag group out of all tags for the "list item" to display in the tag list.

---

#### data-cms-attribute="single-tag" <a name="data-cms-attribute-single-tag"></a>

- This attribute is assigned to the first child of an element with [data-cms-attribute="tag-list"](#data-cms-attribute-tag-list) attribute.

- The purpose of this tag is to identify the element to be used as a template to build the tag list of a single list item.

---

#### data-cms-attribute="slug" <a name="data-cms-attribute-slug"></a>

- This attribute is assigned to an anchor tag in a "list item".

- The purpose of this attribute is to assign the slug associated with the corresponding "list item".

---

#### data-cms-attribute="list-wrapper" <a name="data-cms-attribute-list-wrapper"></a>

- This attribute is assigned to an element to build a list of items based on the defined filters, limits, sorting and skips.

- The element should have atleast a single child to be treated as a template to build the list of items.

- The main element should also have a [data-cms-list-index](#data-cms-list-index) attribute the content of attribute should be an integer.

- Every CMS attribute used with data-cms-attribute="list-wrapper"

  - _data-cms-list-index_ <a name="data-cms-list-index"></a>

    - This attribute is <strong>required</strong> to every element with data-cms-attribute="list-wrapper".

    - The content of attribute should be an integer. The integer values sould be unqiue in a page html.

    ***

  - _data-cms-display-limit_ <a name="data-cms-display-limit"></a>

    - This attribute is <strong>optional</strong> to elements with data-cms-attribute="list-wrapper".

    - The content of attribute should be an integer.

    - The value of display limit tells cms to build the list according to the list properties but all the elements above the display limit will not be visible by the user but still be available in the DOM.

    ***

  - _data-cms-filters_ <a name="data-cms-filters"></a>

    - This attribute is <strong>required</strong> to every element with [data-cms-attribute="list-wrapper"](#data-cms-attribute-list-wrapper) to filter out the items to be displayed in the list.

    - This attribute uses the first child of the list-wrapper element as a template for the generated item. So every list-wrapper element should atleast have one item in it.

    - The content of this attribute is JSON.

    - Examples of some data-cms-filters:

      - data-cms-filters='{"tags":"sometag"}'.
      - data-cms-filters='{"\$and":[{tags:"sometag"},{tags:"someothertag"}}]}'

    - It is recommended to use tags for making any queries.

    - The operators that can be used inside data-cms-filters :

      - \$or: The content of this operator is an array of queries. The result of this query follows basic [OR](https://docs.mongodb.com/manual/reference/operator/query/or/) behaviour.
      - \$and: The content of this operator is an array of queries. The result of this query follows basic [AND](https://docs.mongodb.com/manual/reference/operator/query/and/) behaviour.
      - \$in: The content of this operator is an array of values ; selects the documents where the value of a field equals any value in the specified array.
      - \$nin: The content of this operator is an array of values ; ignored the documents where the value of a field equals any value in the specified array.
      - \$regex : The content of this operator is a Regex string. [More Details...](https://docs.mongodb.com/manual/reference/operator/query/regex/).

      ***

  - _data-cms-limit_ <a name="data-cms-limit"></a>

    - This attribute is <strong>optional</strong> to every element with data-cms-attribute="list-wrapper".

    - Accepted value in integer. This value limits the search for elements upto the specified integer value which is not the same behaviour as [data-cms-display-limit](#data-cms-display-limit) as the items will not present even in the DOM above the selected value.

  ***

  - _data-cms-sorts_ <a name="data-cms-sorts"></a>

    - This attribute is <strong>optional</strong> to every element with data-cms-attribute="list-wrapper".

    - The format of the content is space seperated string values with "-" to signify descending.
      Example : data-cms-sorts="-slug createdAt" . This example means the more precedent ordering is by slug descending and then by createdAt ascending.

    - This attribute is used to sort the items that are fetched by the filters and limit.

    ***

    - _data-cms-skip_ <a name="data-cms-skip"></a>

        - This attribute is <strong>optional</strong> to every element with data-cms-attribute="list-wrapper".

        - The content of this attribute should be an integer value which means that the items that are being fetched will skip the specified amount of items before sending the final result.

    ***

    - _data-cms-url-filter="true"_ <a name="data-cms-url-filter-true"></a>

        - This attribute is <strong>optional</strong> to every element with data-cms-attribute="list-wrapper".

        - This attribute is only used during "generating dynamic url based pages".

        - Dynamic pages are pages that are generated from a template page and a url pattern based on tag groups.

        Example:
        url pattern = prefix:"/blog", pattern:"[tag_name=year-]/[tag-name=month-]", postfix:"/"

        Here, year- and month- are tag groups. They can have many tag related to them such as month-01 and year -2020 etc.

        Then based on the number of year and month tags Following pages will be created.

        - /blog/2020/01/
        - /blog/2020/02/
        - /blog/2020/03/ ... and so on.

        - The list wrapper inside the template page should have data-cms-url-filter="true" attribute for the pages to be generated properly.

---

#### data-cms-attribute="google-analytics-placeholder" <a name="data-cms-attribute-google-analytics-placeholder"></a>

- This attribute is assigned to a script tag in a page html.

- During publishing of the page this tag is replaced by google analytics script according to google analytics id provided in the project settings.

---

#### data-cms-attribute="facebook-pixel-placeholder" <a name="data-cms-attribute-facebook-pixel-placeholder"></a>

- This attribute is assigned to a script tag in a page html.

- During publishing of the page this tag is replaced by facebook-pixel script according to facebook-pixel id provided in the project settings.

---

### data-cms-breadcrumb <a name="data-cms-breadcrumb"></a>

- This attribute is assigned to an element being used as a breadcrumb element in the page html.

- The content of this attribute should be a unique breadcrumb id in the html page.

- This element should have list of anchor elements (LTR) containing the title and the url of the page the breadcrumb is pointing to.

- A new script tag is created with the [data-cms-breadcrumb-data](#data-cms-breadcrumb-data) the content for this attribute is equal to the breadcrumb id. The content for the script is the corresponding SEO markup for the breadcrumb element in the page html.

---

### data-cms-breadcrumb-data <a name="data-cms-breadcrumb-data"></a>

- This attribute is created/maintained by the CMS for their corresponding breadcrumb elements in the page html.

---

### data-cms-page <a name="data-cms-page"></a>

- This attribute is assigned by the CMS to all the internallly references instances for all pages managed by cms.

- Example:
  ```html
  <a href="/page-slug" data-cms-page="page_id"></a>
  ```

---
### Easy Edit

#### data-cms-ideal <a name="data-cms-ideal"></a>

- This attribute should be assigned to the page if the page is under an easy edit category.

- The content of this attribute should be the path of the page from root. 
   Example: blog/blog-ideal.html

- For example:
Let's say we have an easy edit category named Doctors in our CMS dashboard.

We want to add a new page to this category so that you can easily edit the short codes through easy edit forms.

For this you'll have to add the following anywhere inside the body of that page.

```html
<span data-cms-ideal="doctors/doctor-easy-edit.html"></span>
```

On save this page will start appearing in th easy edit category of Doctors from wher you can use easy edit forms for editing the dynamic content of your page.

- Attributes that are used with data-cms-ideal

    - data-cms-ideal-label <a name="data-cms-ideal-label"></a>
        - This attribute defines the label of the ideal page. This attribute only needs to assigned to the main ideal page.
        - Example: For the same example as data-cms-ideal
            ```html
            <span data-cms-ideal="doctors/doctor-easy-edit.html" 
                data-cms-ideal-label="Doctors"></span>
            ```
    - data-cms-ideal-icon <a name="data-cms-ideal-icon"></a>
        - This attribute defines the icon for the ideal page for cms ui. This attribute only needs to assigned to the main ideal page.
        - Example: For the same example as data-cms-ideal
            ```html
            <span data-cms-ideal="doctors/doctor-easy-edit.html" 
                data-cms-ideal-label="Doctors"
                data-cms-ideal-icon="plus"></span>
            ```
        - List of icons available:
            - 500px
            - add-files
            - adobe
            - agenda
            - airbnb
            - alarm
            - alarm-clock
            - amazon
            - amazon-original
            - amazon-pay
            - ambulance
            - amex
            - anchor
            - android
            - android-original
            - angellist
            - angle-double-down
            - angle-double-left
            - angle-double-right
            - angle-double-up
            - angular
            - apartment
            - app-store
            - apple
            - apple-pay
            - archive
            - arrow-down
            - arrow-down-circle
            - arrow-left
            - arrow-left-circle
            - arrow-right
            - arrow-right-circle
            - arrow-top-left
            - arrow-top-right
            - arrow-up
            - arrow-up-circle
            - arrows-horizontal
            - arrows-vertical
            - atlassian
            - aws
            - backward
            - baloon
            - ban
            - bar-chart
            - basketball
            - behance
            - behance-original
            - bi-cycle
            - bitbucket
            - bitcoin
            - blackboard
            - blogger
            - bluetooth
            - bold
            - bolt
            - bolt-alt
            - book
            - bookmark
            - bookmark-alt
            - bootstrap
            - bricks
            - bridge
            - briefcase
            - brush
            - brush-alt
            - bubble
            - bug
            - bulb
            - bullhorn
            - burger
            - bus
            - cake
            - calculator
            - calendar
            - camera
            - candy
            - candy-cane
            - capsule
            - car
            - car-alt
            - caravan
            - cart
            - cart-full
            - certificate
            - checkbox
            - checkmark
            - checkmark-circle
            - chef-hat
            - chevron-down
            - chevron-down-circle
            - chevron-left
            - chevron-left-circle
            - chevron-right
            - chevron-right-circle
            - chevron-up
            - chevron-up-circle
            - chrome
            - circle-minus
            - circle-plus
            - clipboard
            - close
            - cloud
            - cloud-check
            - cloud-download
            - cloud-network
            - cloud-sync
            - cloud-upload
            - cloudy-sun
            - code
            - code-alt
            - codepen
            - coffee-cup
            - cog
            - cogs
            - coin
            - comments
            - comments-alt
            - comments-reply
            - compass
            - construction
            - construction-hammer
            - consulting
            - control-panel
            - cpanel
            - creative-commons
            - credit-cards
            - crop
            - cross-circle
            - crown
            - css3
            - cup
            - customer
            - cut
            - dashboard
            - database
            - delivery
            - dev
            - diamond
            - diamond-alt
            - diners-club
            - dinner
            - direction
            - direction-alt
            - direction-ltr
            - direction-rtl
            - discord
            - discover
            - display
            - display-alt
            - docker
            - dollar
            - domain
            - download
            - dribbble
            - drop
            - dropbox
            - dropbox-original
            - drupal
            - drupal-original
            - dumbbell
            - edge
            - emoji-cool
            - emoji-friendly
            - emoji-happy
            - emoji-sad
            - emoji-smile
            - emoji-speechless
            - emoji-suspect
            - emoji-tounge
            - empty-file
            - enter
            - envato
            - envelope
            - eraser
            - euro
            - exit
            - exit-down
            - exit-up
            - eye
            - facebook
            - facebook-filled
            - facebook-messenger
            - facebook-original
            - facebook-oval
            - figma
            - files
            - firefox
            - firefox-original
            - fireworks
            - first-aid
            - flag
            - flag-alt
            - flags
            - flickr
            - flower
            - folder
            - forward
            - frame-expand
            - fresh-juice
            - full-screen
            - funnel
            - gallery
            - game
            - gift
            - git
            - github
            - github-original
            - goodreads
            - google
            - google-drive
            - google-pay
            - google-wallet
            - graduation
            - graph
            - grid
            - grid-alt
            - grow
            - hacker-news
            - hammer
            - hand
            - handshake
            - harddrive
            - headphone
            - headphone-alt
            - heart
            - heart-filled
            - heart-monitor
            - helicopter
            - helmet
            - help
            - highlight
            - highlight-alt
            - home
            - hospital
            - hourglass
            - html5
            - image
            - inbox
            - indent-decrease
            - indent-increase
            - infinite
            - information
            - instagram
            - instagram-filled
            - instagram-original
            - invention
            - invest-monitor
            - investment
            - island
            - italic
            - java
            - javascript
            - jcb
            - joomla
            - joomla-original
            - jsfiddle
            - juice
            - key
            - keyboard
            - keyword-research
            - laptop
            - laptop-phone
            - laravel
            - layers
            - layout
            - leaf
            - library
            - life-ring
            - line
            - line-dashed
            - line-dotted
            - line-double
            - line-spacing
            - lineicons
            - lineicons-alt
            - link
            - linkedin
            - linkedin-original
            - list
            - lock
            - lock-alt
            - magnet
            - magnifier
            - mailchimp
            - map
            - map-marker
            - mashroom
            - mastercard
            - medium
            - megento
            - menu
            - mic
            - microphone
            - microscope
            - microsoft
            - minus
            - mobile
            - money-location
            - money-protection
            - more
            - more-alt
            - mouse
            - move
            - music
            - network
            - night
            - nodejs
            - nodejs-alt
            - notepad
            - npm
            - offer
            - opera
            - package
            - page-break
            - pagination
            - paint-bucket
            - paint-roller
            - pallet
            - paperclip
            - patreon
            - pause
            - paypal
            - paypal-original
            - pencil
            - pencil-alt
            - phone
            - phone-set
            - php
            - pie-chart
            - pilcrow
            - pin
            - pinterest
            - pizza
            - plane
            - play
            - play-store
            - plug
            - plus
            - pointer
            - pointer-down
            - pointer-left
            - pointer-right
            - pointer-up
            - popup
            - postcard
            - pound
            - power-switch
            - printer
            - producthunt
            - protection
            - pulse
            - pyramids
            - python
            - question-circle
            - quora
            - quotation
            - radio-button
            - rain
            - react
            - reddit
            - reload
            - remove-file
            - reply
            - restaurant
            - revenue
            - road
            - rocket
            - rss-feed
            - ruler
            - ruler-alt
            - ruler-pencil
            - rupee
            - save
            - school-bench
            - school-bench-alt
            - scooter
            - scroll-down
            - search
            - search-alt
            - select
            - seo
            - service
            - share
            - share-alt
            - shield
            - shift-left
            - shift-right
            - ship
            - shopify
            - shopping-basket
            - shortcode
            - shovel
            - shuffle
            - signal
            - sketch
            - skipping-rope
            - skype
            - slack
            - slice
            - slideshare
            - slim
            - snapchat
            - sort-alpha-asc
            - sort-amount-asc
            - sort-amount-dsc
            - souncloud-original
            - soundcloud
            - spellcheck
            - spiner-solid
            - spinner
            - spinner-arrow
            - spotify
            - spotify-original
            - spray
            - sprout
            - stackoverflow
            - stamp
            - star
            - star-empty
            - star-filled
            - star-half
            - stats-down
            - stats-up
            - steam
            - sthethoscope
            - stop
            - strikethrough
            - stripe
            - stumbleupon
            - sun
            - support
            - surf-board
            - swift
            - syringe
            - tab
            - tag
            - target
            - target-customer
            - target-revenue
            - taxi
            - teabag
            - telegram
            - telegram-original
            - text-align-center
            - text-align-justify
            - text-align-left
            - text-align-right
            - text-format
            - text-format-remove
            - thought
            - thumbs-down
            - thumbs-up
            - thunder
            - thunder-alt
            - ticket
            - ticket-alt
            - timer
            - train
            - train-alt
            - trash
            - travel
            - tree
            - trees
            - trello
            - trowel
            - tshirt
            - tumblr
            - twitch
            - twitter
            - twitter-filled
            - twitter-original
            - ubuntu
            - underline
            - unlink
            - unlock
            - upload
            - user
            - users
            - ux
            - vector
            - video
            - vimeo
            - visa
            - vk
            - volume
            - volume-high
            - volume-low
            - volume-medium
            - volume-mute
            - wallet
            - warning
            - website
            - website-alt
            - wechat
            - weight
            - whatsapp
            - wheelbarrow
            - wheelchair
            - windows
            - wordpress
            - wordpress-filled
            - world
            - world-alt
            - write
            - yahoo
            - ycombinator
            - yen
            - youtube
            - zip
            - zoom-in
            - zoom-out

    - data-cms-order <a name="data-cms-order"></a>
        - This attribute defines the order of the ideal page for cms ui. This attribute only needs to assigned to the main ideal page.
        - This value is optional.
        - Example: For the same example as data-cms-ideal
            ```html
            <span data-cms-ideal="doctors/doctor-easy-edit.html" 
                data-cms-ideal-label="Doctors"
                data-cms-order="1"></span>
            ```

    - data-cms-easy-edit-group <a name="data-cms-easy-edit-group"></a>
        - This attribute groups the ideal page into a group. This attribute only needs to assigned to the main ideal page.
        - This value is optional.
        - Example: For the same example as data-cms-ideal
            ```html
            <span data-cms-ideal="doctors/doctor-easy-edit.html" 
                data-cms-ideal-label="Doctors"
                data-cms-order="1"
                data-cms-easy-edit-group="Main Pages"></span>
            ```

####  data-cms-form-structure <a name="data-cms-form-structure"></a>

- This is a script of type application/json containing a json with attributes defining all the fields present in the page and the properties of these fields.

- Properties for the form structure JSON
    - "title": This key defines the UI value of the Form Properties Tab in Easy Edit Form for Coot CMS UI. This is not a required field.
        Example: 
        ```html
            <script type="application/json" data-cms-form-structure>
                {
                    "title":"Doctor Properties"
                ...
                ...
                ...
                }
            </script>
        ```
    - Other key values signify the name of the field or group
        Example: 
        ```html
        <script type="application/json" data-cms-form-structure>
                {
                    "title":"Doctor Properties"
                    "Doctor Details": {
                        "type":"group|field", // required
                        "grid-property":"1fr 1fr|html grid format", // only if type = group
                        "children":{ // only if type=group
                            "Doctor Name": {
                                "type":"field",
                                "field_code":"doctor-name", // required if type = field
                                "field_type":"input/text",
                                "class":"doctor-name-897", // if the element that needs to be a modifiable field has a unique class, then use this property 
                                "id":"doctor--name", // if the element that needs to be a modifiable field has a unique class, then use this property
                                "short_code":"doctor-name" // if the element has a data-cms-short-code attribute then use this property

                                // only of the above three values can be used at once either class, id or short_code
                            }
                            ...other type = field objects
                        },
                        "field_code":"unique code for the form field", // required if type = field
                        "field_type":"custom-list|input/text|input/number|textarea|input/date|link|image|wizwig", // required if type = field
                        "class|id|short_code":""
                    }
                ...other field objects
                }
            </script>
        ```
        - Details for the different field_type fields
            - custom-list - This type of field allows the edit a list of items in a page.
            - input/* - Basic html input fields. *does not support input/file.
            - textarea - Textarea input field.
            - link - link item field is used to edit anchor elements.
            - image - image item field is used to edit image elements.
            - wizwig - wizwig item field is used to edit HTML sections.

        - Field JSON in case of custom-list
            ```json
                {
                    "type":"field",
                    "field_code":"doctor-achievements",
                    "field_type":"custom-list",
                    // html selector for the element containing the list items
                    "container_selector": ".doctor-ach",
                    // html selector for an item element
                    "item_selector": "#ach-item",
                    "props": { 
                        "image": { 
                            "selector": ".ach-item-image",
                            "type": "text|image|link|wizwig",
                            "name": "Achievement Image" 
                        },
                        "name": {
                            "selector": ".ach-item-name",
                            "type": "text",
                            "name": "Achievement Name"
                        },
                        "description": {
                            "selector": ".ach-item-des",
                            "type": "text",
                            "name": "Achievement Description"
                        }
                    }
                }
            ```



---

####  data-cms-easy-edit-list <a name="data-cms-easy-edit-list"></a>
- This is a script of type application/json containing a json with attributes defining all the fields present in the page to be displayed in the list of easy edit pages of a category.

Example:
```html
<script type="application/json" data-cms-easy-edit-list>
        {"Doctor Name": { "field_code": "doctor-name", "hotlink": true, "sorting": true, "filtering": true, "text_search": true }, "Doctor Image": { "field_code": "doctor-image", "image":true, "hotlink": false, "sorting": false, "filtering": false, "text_search": false }}
    </script>
```


### data-cms-editor-modified="true" <a name="data-cms-editor-modified-true"></a>

- This is a system attribute used by the CMS for enabling modification of files through the editor.

- Make sure to not change any of these values while editing your files as this can affect how the assets are being used in the pages.

- This is a temporary attribute which does not even appear in the draft version of the page.

---

### data-cms-modified-css="true" <a name="data-cms-modified-css-true"></a>

- This is a CMS attributes used by the CMS during the publishing process of a page.

- This is also a temporary attribute used only within a certain block of code within CMS.

---

### data-cms-tag <a name="data-cms-tag"></a>

- This attribute is used within the body of a page to assign a page a tag.

- There can be multiple data-cms-tag attribute in a single page.

- If the tag is not already created the after saving the page with the data-cms-tag="sometag". The sometag tag will be created and then can be further used in other pages using the GUI editor.

- There are some other properties related to data-cms-tag :

  - _data-cms-tag-url_ <a name="data-cms-tag-url"></a>
    - This denotes the url for the tag.
    - This url can be used whenever the tag is used in the page.
    - This is an optional property.
    - Example:
        ```html
        <body data-cms-tag="category-ctrt" data-cms-tag-url="/blog/cataract">
        ```
  - _data-cms-alias_ <a name="data-cms-alias"></a>
    - This is also an optional property. This property is used in case the tag cannot be used as such during use in other pages. So an alias is assigned instead.
    - Example:
        ```html
        <body data-cms-tag="category-ctrt" data-cms-tag-url="/blog/cataract" data-cms-alias="cataract">
        ```
### data-cms-slug <a name="data-cms-slug"></a>

- This tag is used in the page whenever you want to customize the slug of a page which means the slug generated based on the page path.

Example:
```html
    <span data-cms-slug="/custom-url"></span>
```