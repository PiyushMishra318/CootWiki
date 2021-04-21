# Generate Dynamic Pages
 This is to generate multiple pages based on the pattern defined for the url pattern for the pages.
The following parameters are required to generate dynamic pages for a certian page: 

 - Prefix : The prefix to the dynamically generated url.
 - Pattern : This is the dynamic part of the url that is generated based on the tag category. For Example: 
	 If you want to create blog pages based on authors and you have tagged all the blog pages with the author-x tag then you can create the basic template page for the author list page and using the generate dynamic pages functionality with the pattern = [tag_name=author-]. If there are two authors author-A and author-B.
	 Two pages will be generated with the following urls.
	 - /A
	 - /B
- Postfix: This is the postfix to the dynamically generated url.
- Skip Itermediate: This is a boolean(true/false) parameter that allows the user to skip generating intermediate value pages in case of multiple dynamic filters. For example: 
	If you want to create blog pages based on year and month and have already tagged all your blog pages with year-x and month-x tags. You can use skip intermediate parameter to skip generating the in-between pages that are created by default i.e /2020 and only generate pages for the joint outcome for year and month i.e /2020/01. The pattern for generating these types of pages will be : [tag_name=year-]/[tag_name=month-].

Few things to note about the process:

 - The page that is used to generate dynamic pages are considered "master pages" and Coot CMS doesn't allow them to be published as these pages don't need to contain actual content instead the page can contain patterns based on the tags that are being used to generate the page. For example:
	```<html>
		<head>
			<title>Blogs authored by {{tag_name}}</title>
		</head>
		<body>//Content</body>
	</html>```
	
	In case of multiple tag filters :
	
	```<html>
		<head>
			<title>
				Blogs created in {{tag_name_1}}, {{tag_name_2}}
			</title>
		</head>
		<body>//Content</body>
	</html>```

- There are only a few pattern variables that can be used while using a pattern in the master page:
	- {{tag_name}} in case of single dynamic filter in case of multiple tag filters {{tag_name_1}}, {{tag_name_2}} and so on. The numbered tag_name corresponds to the order of the tag filter in the pattern parameter.
	- domain_name :  The domain name for the project
	- slug : This will be the slug generated for the page based on the prefix, postfix and pattern.
- {{tag_name(-_*)}} this particular pattern variable will be equal to the tag name after removing the tag group or the tag alias if it's available for the particular tag name. So in case you want to capitalize certain part of the tag which by default all the letters seperated by - will be capitalized. But in case you want it to be in a specific way for example in case of month-x tags if you want to use the tag_name_2 as letters then you can give aliases to all the month-x tags for example month-01 the alias for this tag will be January or Jan. 
