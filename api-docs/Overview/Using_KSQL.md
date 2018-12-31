TEMP

<H1>Introduction</H1>

The Kaltura Search Query Language (KSQL) maximizes the content filtering experience for end users, enabling content filtering, personalized filtering, cross asset types, and any logical expression.

<H2>KSQL Capabilities</H2>
KSQL provides a collection of nested expressions with key, comparison operators, value, and logical conjunctions, and search assets that use dynamic criteria.
**Note:** Values are surrounded by apostrophes. Date values are sent as epoch times.
If the value contains an apostrophe, it should be replaced with %27.

<H3>KSQL Keys</H3>
KSQL keys include:
•	Any Tag or Meta defined in the system and the following reserved keys: 
o	start_date
o	end_date
o	geo_block – The only valid value is "true"; when enabled, only the assets that are not restricted for the user by geo-block rules will return. 
o	parental_rules – The only valid value is "true"; when enabled, only the assets that the user does not need to provide PIN code for will be returned. 
o	user_interests – The only valid value is "true”; when enabled, only the assets that the user defined as his or her interests (by tags and metas) will be returned.
o	epg_channel_id – This is the channel identifier of the EPG program.
o	epg_id – Used for searching programs with specific IDs. 
o	media_id – Used for searching media with specific IDs.
o	entitled_assets –The valid values are: "free", "entitled", "both". 
	free - Gets only free to watch assets. 
	entitled – Gets only the assets that the user is entitled to watch implicitly. 
o	asset_type – Used for searching for asset types, the valid values are: "media", "epg", "recording", or any number that represents a media type in the group.
2.2.2	KSQL Operators
2.2.2.1	Search Operands
The following are the search operators for KSQL:
•	For numerical fields =, >, >=, <, <=. 
•	For alpha-numerical fields =, != (not), ~ (like), !~, ^ (starts with). 
•	For searching one value in a list of numeric values: ‘:’  (For example: media_id: ‘347457,45687,457845’)
•	For autocomplete searches: The operand “^=” represents autocomplete from the beginning of the text only. The operand is similar to the operand “^”, which represents “autocomplete” in the sense of “word starts with” (as in, if any of the words in the field start with the given text, it should be returned). “^=” now represents autocomplete from the beginning of the text only. 
For example, given an asset with the name “John Johanson”, using a KSQL search of “name^Johan’” it will return a result, but for “name^=’Johan’” it will not.
2.2.2.2	Logical Conjunctions
Logical conjunctions include: and, or. 
2.2.2.3	Exists / Not Existed Operator
This KSQL comparison operator enables you to filter media assets that are with or without any value for a specific tag or meta field:
•	value exists operator:    +  
•	value not exists operator: !+ 
When used within a KSQL search phrase, the exists/not exited operators should be followed by a double quote character (")
Examples: 
•	Genre+’’ - Search for assets that have ANY value in the genre tag (note that these are double apostrophes, not quotation marks)
•	Genre!+’’ - Search for assets that have NO value in the genre tag (note that these are double apostrophes, not quotation marks)
2.2.3	Search Values
Search values are limited to 20 characters each (the maximum length of the entire filter is 4096 characters)
Example: Genre is drama or action and actor is brad pitt and start date is greater than 1.1.2014): (and (or genre=’drama’ genre=’action’) actor=’brad pitt’ start_date >= ‘1388534400’)
2.3	Searching for Recordings
KSQL supports the option to search for recordings and for the state of recordings, which are treated like any other asset in the system (i.e., recordings are subject to standard content discovery).
The recordings entities search is subject to all KSQL search attributes (similar to EPG – name, description, tags, metas, and dates).
Note that when using date/time searches, padding is not taken into account. For example: if the program starts at 7PM, due to padding, the recording will begin at 6:30PM. Therefore, when searching for recordings > 6:59 PM. this program should be included
2.3.1	Multi-Language Recording Search Support
The recording search feature for EPG also supports multi-language capability. Unlike VOD, if the required language does not exist for a specific parameter, the default language will not be used instead. In this case, no value will be provided.
Note: Numeric metadata do not support the multilingual search.
