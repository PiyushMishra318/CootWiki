# CMS Attributes

## 📝 Table of Contents

- [data-cms-block](#data-cms-block)
  - [data-cms-block-update="disabled"](#data-cms-block-update-disabled)
- [data-cms-createdat](#data-cms-createdat)
- [data-cms-pattern](#data-cms-pattern)
- [data-cms-structured](#data-cms-structured)
- [data-cms-short-code](#data-cms-short-code)
  - [data-cms-filters](#data-cms-filters)
  - [data-cms-short-code-type](#data-cms-short-code-type)
  - [data-cms-form-field](#data-cms-form-field)
  - [data-cms-form-position](#data-cms-form-position)
  - [data-cms-field-type](#data-cms-field-type)
  - [data-cms-field-validation](#data-cms-field-validation)
  - [data-cms-form-required="true"](#data-cms-form-required-true)
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
- [data-cms-ideal](#data-cms-ideal)
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
- [data-cms-script-loader](#data-cms-script-loader)
- [data-cms-jquery](#data-cms-jquery)

---

### data-cms-block <a name="data-cms-block"></a>

- This attribute identifies a block in the html code.

- When a file is uploaded with data-cms-block="block_id" assigned to a any html tag the backend creates a editable block code html object and saves a copy of the block code for further use.

- When the block code is updated through the CMS editor all the pages using the same block will be updated. This feature is optional and user can decide whether to update all the affected pages or not.

- The purpose of this attribute is to minimize the need to update the same code in multiple pages as for many pages in a site some of the areas remain uneffected. For Eg: Header and Footer of a website.

---

#### data-cms-block-update="disabled" <a name="data-cms-block-update-disabled"></a>

- This attribute is assigned to the element having data-cms-block.

- The purpose of this attribute is to signify that the block code in this particular html page should not be updated when the central block code is updated.

---

### data-cms-createdat <a name="data-cms-createdat"></a>

- This attribute is used to create a page with a custom date assigned by the user. This date can also be updated after the page has been created.

- The purpose for this tag is for sorting. while using list builders in CMS.

- The format for date should be as follows:
  data-cms-createdat="YYYY-MM-DD".

---

### data-cms-pattern <a name="data-cms-pattern"></a>

- This attributes to assigned to an element having variable values based on project / page properties.

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

  1. short_codes.anyshortcode
  2. domain_name
  3. slug

- The purpose for this attribute is to avoid manually updating some variable code with the help of a few page properties.

- The format for data-cms-pattern should be in [handlebars](https://handlebarsjs.com/) format.

---

### data-cms-structured <a name="data-cms-structured"></a>

- This attribute identifies a custom SEO Markup in the html code.

- The JSON Schema for SEO Markup is saved in the backend for further updation.

- The content of this attribute should be a unique structured data id.

---

### data-cms-short-code <a name="data-cms-short-code"></a>

- The purpose of this short code is to save a string value assigned to a key for using them in other pages and list builders.

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
    <div/span/p/h*/pre data-cms-short-code="div-example">TEST</div/span/p/h*/pre>
  ```

  ```html
  <a
    data-cms-short-code="anchor-example"
    href="https://example.com/about-us"
  ></a>
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
  "anchor-example":"https://example.com/about-us",
  "image-example":"https://example.com/image.jpg"
  }
  ```

- These values can be used in [data-cms-pattern](#data-cms-pattern).

- Every CMS attribute used with data-cms-short-code.

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
  <div/span/p/h*/pre data-cms-short-code="div-example" data-cms-short-code-type="int">4</div/span/p/h*/pre>
  ```
  The value extracted from this will be treated as an integer instead of a string.

---

#### data-cms-form-field <a name="data-cms-form-field"></a>

- This attribute is used with the data-cms-short-code attribute.

- The value for this attribute signifies the label of the field in the form.

---

#### data-cms-form-position <a name="data-cms-form-position"></a>

- This attribute is used with the data-cms-short-code attribute.

- The value for this attribute signifies the position of the field in the form. The value type should be integer. Range (1-10).

---

#### data-cms-field-type <a name="data-cms-field-type"></a>

- This attribute is used with the data-cms-short-code attribute.

- The value for this attribute signifies type of the field in the form.

- Options:
  - text
  - file
  - textarea
  - checkbox
  - email
  - number
  - date

---

#### data-cms-field-validation <a name="data-cms-field-validation"></a>

- This attribute is used with the data-cms-short-code attribute.

- The content for this attribute can either be:
  - accept for data-cms-field-type="file".
    #### or
  - ; seperated list of attributes for form fields. For Example: - "max-length:3;min:0;max:100"

---

#### data-cms-form-required="true" <a name="data-cms-form-required-true"></a>

- This attribute is used with the data-cms-short-code attribute.

- It signifies whether the field is required in the easy edit form.

---

### data-cms-attribute <a name="data-cms-attribute"></a>

#### data-cms-attribute="seperator" <a name="data-cms-attribute-seperator"></a>

- This attribute is for CMS editor to identify the start of body tag.

---

#### data-cms-attribute="tag-list" <a name="data-cms-attribute-tag-list"></a>

- This attribute is assigned to a list item for listing tags for that list item.

- The element should have atleast a single child to be treated as a template to build all tags.

- Other attributes related to this attribute:

  _data-cms-tag-slug="allow" <a name="data-cms-tag-slug-allow"></a>_

  - This attribute is assigned with data-cms-attribute="tag-list" to signify that every element in the tag list is an anchor and it shoud have the tag's associated slug.

  ***

  _data-cms-tag-display="true" <a name="data-cms-tag-display-true"></a>_

  - This attribute is assigned with data-cms-attribute="tag-list" to signify that every element in the tag should be a visible element in the dom and the inner html of each element should have either the tag alias if provided if not then the tag name.

  _data-cms-tag-group <a name="data-cms-tag-group"></a>_

  - This attribute is assigned with data-cms-attribute="tag-list" to filter out the tags of a certain tag group out of all tags in the page to display in the tag list.

---

#### data-cms-attribute="single-tag" <a name="data-cms-attribute-single-tag"></a>

- This attribute is assigned to the first child of an element with [data-cms-attribute="single-tag"](#data-cms-attribute-single-tag) attribute.

- The purpose of this tag is to identify the element to be used as a template to build the tag list of a single list item.

---

#### data-cms-attribute="slug" <a name="data-cms-attribute-slug"></a>

- This attribute is assigned to an anchor tag in a list item.

- The purpose of this attribute is to assign the slug associated with the corresponding list item.

---

#### data-cms-attribute="list-wrapper" <a name="data-cms-attribute-list-wrapper"></a>

- This attribute is assigned to an element to build a list of items based on the defined filters, limits, sorting and skips.

- The element should have atleast a single child to be treated as a template to build the list of items.

- Every list item should also have a [data-cms-list-index](#data-cms-list-index) attribute the content of attribute should be an integer.

- Every CMS attribute used with data-cms-attribute="list-wrapper"

  - _data-cms-list-index_ <a name="data-cms-list-index"></a>

    - This attribute is assigned to every element with data-cms-attribute="list-wrapper".

    - The content of attribute should be an integer. The integer values sould be unqiue in a page html.

    ***

  - _data-cms-display-limit_ <a name="data-cms-display-limit"></a>

    - This attribute is assigned to every element with data-cms-attribute="list-wrapper".

    - The content of attribute should be an integer.

    - The value of display limit tells cms to build the list according to the list properties but all the elements above the display limit will have an inline style of "display:none".

    ***

  - _data-cms-filters_ <a name="data-cms-filters"></a>

    - This attribute is assigned to every element with [data-cms-attribute="list-wrapper"](#data-cms-attribute-list-wrapper) to filter out the items to be displayed in the list.

    - This attribute uses the first child of the list-wrapper element as a template for the generated item. So every list-wrapper element should atleast have one item in it.

    - The content of this attribute is a stringified json.

    - Examplesof some data-cms-filters:

      - data-cms-filters='{"tags":"sometag"}'.
      - data-cms-filters='{"\$and":[{tags:"sometag"},{tags:"someothertag"}}]}'

    - It is recommended to use tags for making any queries.

    - The operators that can be used inside data-cms-filters :

      - \$or: The content of this operator is an array of queries. The result of this query follows basic [OR](https://docs.mongodb.com/manual/reference/operator/query/or/) behaviour.
      - \$and: The content of this operator is an array of queries. The result of this query follows basic [AND](https://docs.mongodb.com/manual/reference/operator/query/and/) behaviour.
      - \$in: The content of this operator is an array of values ; selects the documents where the value of a field equals any value in the specified array.
      - \$regex : The content of this operator is string. [More Details...](https://docs.mongodb.com/manual/reference/operator/query/regex/).

      ***

  - _data-cms-limit_ <a name="data-cms-limit"></a>

    - This attribute is assigned to every element with data-cms-attribute="list-wrapper".

    - Accepted value in integer. This value limits the search for elements upto the spcified integer value which is not the same behaviour as [data-cms-display-limit](#data-cms-display-limit)

  ***

  - _data-cms-sorts_ <a name="data-cms-sorts"></a>

    - This attribute is assigned to every element with data-cms-attribute="list-wrapper".

    - The format of the content is space seperated string values with "-" to signify descending.
      Example : data-cms-sorts="-slug createdAt" . This example means the more precedent ordering is by slug descending and then by createdAt ascending.

    - This attribute is used to sort the items that are fetched by the filters and limit.

    ***

    -_data-cms-skip_ <a name="data-cms-skip"></a>

    - This attribute is assigned to every element with data-cms-attribute="list-wrapper".

    - The content of this attribute should be an integer value which means that the items that are being fetched will skip the specified amount of items before sending the final result.]

    ***

    -_data-cms-url-filter="true"_ <a name="data-cms-url-filter-true"></a>

    - This attribute is assigned to every element with data-cms-attribute="list-wrapper".

    - This attribute is only used during generating dynamic url based pages.

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

### data-cms-ideal <a name="data-cms-ideal"></a>

- This attribute should be assigned to the page if the page is under an easy edit category.

- For example:
  Let's say we have an easy edit category named Doctors in our CMS dashboard.

  We want to add a new page to this category so that you can easily edit the short codes through easy edit forms.

  For this you'll have to add the following anywhere inside the body of that page.

  ```html
  <span data-cms-ideal="doctor-easy-edit"></span>
  ```

  On save this page will start appearing in th easy edit category of Doctors from wher you can use easy edit forms for editing the dynamic content of your page.

---

### data-cms-editor-modified="true" <a name="data-cms-editor-modified-true"></a>

- This is a CMS attribute used by the CMS for enabling modification of files through the editor.

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

  -_data-cms-tag-url_ <a name="data-cms-tag-url"></a>
