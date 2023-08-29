Title: Wiki Comparison - ADO, SharePoint, Zoho
Date: 2023-08-29 10:48:00
Modified: 2023-08-29 10:48:00
Category: 
Tags: 
Slug: 
Summary: 
Status: published


Problem:
	- Want centralized documentation location
		○ Should be easy to locate as a whole
		○ Should be searchable - easy to find relevant information within it
		○ Should be easy to edit and maintain

Proposed Solutions:
	- Azure DevOps Wiki
		○ Current proposed option
	- Zoho Wiki
		○ Possible alternative suggested by Craig
	- SharePoint Pages (very wiki-like)
		○ Possible alternative suggested by Craig

Commonalities
	- All three offer "standard" wiki functionality:
		○ WYSIWIG and/or rich text editing
		○ Ability to link between pages and create arbitrary hierarchies
		○ Integrations with external systems to expedite e.g. referencing Projects or source code
	- (verify) Allows notifications and/or alerts to track changes made to content at some level
	- History functionality allows some level of 'change-tracking', probably rollback if needed

Differences
Azure DevOps Wiki
	- Alberto noted a number of features that make "ADW" advantageous for work in that platform
Advantages
		○ Different integrations into Azure as a whole
		○ Keeps docs tightly bound to a given repository
			§ Tying these together might force devs to make sure they update related documentation alongside significant code changes?
			§ README files can be maintained with Wiki links
Disadvantages
	- Tying documentation directly to a codebase will silo that information specifically to that project
		○ Not sure how well it works when trying to link to or 'relate' knowledge between projects
		○ How well does search work when trying to look through wikis for information spanning multiple projects?
	- How difficult does this make sharing info outside the dev team?
		○ Non-devs would need to access ADW to view and/or edit this, if we wanted to knowledge-share outside dept.; permissions?

SharePoint Pages
Advantages
	- Easier to allow most everybody to contribute to the knowledgebase
		○ Centralized access management - should be easy to grant most everyone access of some level
		○ Info about i.e. HACR is centralized, whether it's directly code-based or not; UI info and use cases all linked in one place
		○ Referencing libraries or other common 'parts' of multiple projects should be much easier
		○ Centrally locating in SP where a lot of documentation (files, images) already lives should encourage contribution and ease search/discovery of info
Disadvantages
	- Not sure about access yet for everyone
	- Will allowing more universal access cause any 'confusion', too many people modifying/etc.?
	- Is wiki meant to be more project specific, and thus DevOps Wiki would have the advantage?
	- Is tying a wiki more tightly to the Zoho suite (using Zoho Wiki) as opposed to SP more advantageous?

Zoho Wiki
	- I don't have access yet but I have to assume it's largely "SharePoint Pages in Zoho"
	- Might integrate better with Projects, Connect, other Zoho tools?
	- Doesn't seem to get a lot of press on home page or elsewhere on Zoho's site; what is the product's future?
		○ Could this possibly be sunsetted or possibly require migration at some point?
	
