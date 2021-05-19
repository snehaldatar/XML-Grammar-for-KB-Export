# XML-Grammar-for-KB-Export

Businesses often need to export knowledge content from eGain cloud for auditing, sharing the content with external partners or other business reasons. Depending on the need, eGain offers different methods to export content from eGain. For business intelligence’s requirements, eGain data extract should be used and majority of other requirements, content can be exported in XML files. Exporting KM data from eGain System create a XML file for each object (folder, topic, article etc.). The XML files for each object is created in Knowledge folder structure to have a proper categorization of folders, topics and articles. Schema of those XML documents can be located at eGain Github library . The exported content can be requested from eGain’s Technical Support for X times in a quarter.

# Exported Content Includes

1. Exporting data from eGain System create the XML files for different objects (folder, topic, article etc.). The XML files for each object will be created in a defined file system folder path hierarchy to have a proper categorization of folders, topics and articles. 

2. eGain folder and article XMLs will reside in same folder hierarchy starting from file system folders inside  ExportedContent\<Department_Name>\FoldersAndArticles\Content\shared\ . 
3. eGain Topic XMLs will reside in topic folder hierarchy starting from root topic folders inside  ExportedContent\<Department_Name>\Topics\
4. Article XML version data nodes are in the order from lowest version to highest version.
5. Attachments will be present under ExportedContent\<Department_Name>\FoldersAndArticles\internal_attachments and reference will be present in the article xml.
6. Article to article linking is also supported through linkAlias and linkedAliases tags in Article XML.
7. Currently Personalization or tagging of content is not supported.

## Sample Files

This Sample in sample folder includes XSDs and a zip file which has the xmls in required hierarchy.

 XSDs -  Topic.xsd, Folder.xsd,  Article.xsd
 
 Sample zip with xmls - eGain_Exported_Content.zip
 

# XML Grammar

## Topic XSD
|Name | Description | Type | Mandatory
|-----|-------------|------|-------|
|id |Topic |Id |String |Yes 
|egainTopicPath |eGain Topic Path will be path to eGain Topic with all parent topics. This will slways start with "\Topics".
egainTopicPath :      " \Topics\Policy\Leaves:Paid leave"	|String |Yes 
|exportedTopicLangDataList |Language specific Topic Data. |ExportedTopicLangData |Yes
|translate |Field to convey whether this topic is translatable |Allowed values are :    0 - No translation, 1 - Do translate |int |No

### ExportedTopicLangData
|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|name |Name of the topic |String |Yes 
|description |Description of the topic |String |No
|language	|Language code. Please refer appendix for details. |String |Yes
|imageUrl |Image Url of the requested topic | String | No


## Folder XSD
|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|id |Folder |ID |String |Yes
|egainFolderPath |eGain Folder Path will be path to eGain Folder with all parent folders. egainFolderPath: "\Content\Shared\Texting#bSlash#SMS-MMS\Agent Calling" | String | Yes
|exportedFolderLangDataList	|Language specific Folder Data |ExportedFolderLangData| Yes
|translate |Specifies, whether, the articles in this folder to be considered for translation when the content is exported for translation. Allowed values are :  0 - No translation, 1 - Do translate| int| No

### ExportedFolderLangData
|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|name |Name of the folder |String | Yes
|description |Description of the folder| String| No
|language |Language code. Please refer appendix for details |String| Yes

## Article XSD
|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|id |This is unique ID of article. If content is exported from eGain environment then this ID can be of the source eGain object and in case exported XML files are created from HTML, PDF etc. then this ID should be programmatically generated and mentioned in ID element of object XML files. |String |	Yes
|egainArticlePath |eGain Article Path will be path to eGain Folder that contains article and article name. egainFolderPath:     "\Content\Shared\Texting#fSlash#SMS-MMS\Agent Calling" egainArticlePath:  "\Content\Shared\Texting#fSlash#SMS-MMS\Agent Calling\Leaves:Paid leave" | String	|Yes
| macro | This field denotes if this article can be used as a macro. If this element is present, it must have its 'name' element. Other elements of macro are optional.| Macro|	No
|langDataList |List of all languages and language specific versions. |LangData |Yes
| notes | List of notes attached to the article. If this element is present then it must contain atleast one 'Note' element and this 'Note' element must have the 'content' attribute. |Note | No
|relatedQuestions |Related Questins of the Article. |String |No
|egainTopicPathList | List of topics where the article is added. egainTopicPath: "\Topics\Policy\Leaves#col#Paid leave". |String |No
|createdDate |Creation date and time. |String |No
|lastModifiedDate |Last modification date and time.	|String |No
|createdBy |Name of user who created Article. (this would be eGain user name) |String |No
|lastModifiedBy| Name of user who modified the Article last. (this would be eGain user name) | String | No
|customAttributeList |List of custom attributes of Article.	|CustomAttribute |No
|relatedArticles |List of articles related to this article. e.g. "\Content\Shared\Texting#fSlash#SMS-MMS\Agent Calling\Leaves:Paid leave"| String| No
|linkAlias |UUID of article	|String |No

### Macro

|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|name |Name of the macro |String | Yes
|description |Description of the macro |String |No
|defaultArticle |Default article with the macro |String |No
|defaultValue |Default value of macro |String |No

### Lang Data

|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|language | Language code. Please refer appendix for details. |String |Yes
|versionDataList |Details of all the  versions of Article for this language. |VersionData |Yes

#### Version Data

|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|name |name of the the version |String |Yes
|versionNumber |Version number of the version |String |Yes
|createdDate |created date of the version |String |No
|lastModifiedDate| Last modification date of the version| String |No
|label |Label of the article version. (This is message entered by author while publishing a version) |String |No
|description |Description of the version| String| No
|keywords |article keywords |String |No
|summary |article summary |String |No
|additionInfo |Addition info of the version |String |No
|content |Content of the version |String |No
|availabilityDate|	Availability date of version |String |No
|expirationDate |Expiration date of the version |String |No
|imageUrl |ImageUrl of the version |String |No
|attachmentList |Attachments with the version |Attachment |No
|articleType |Article type , by default 'General' |String |No
|createdBy |Name of user who created Article. (this would be eGain user name) |String |No
|lastModifiedBy |Name of user who modified the Article last. (this would be eGain user name) |String |No
|linkedAliases |List of linkAliases of articles to which the present article has links within its content |String |No
|containsLinks |Boolean indicating whether content of version contains links to other eGain articles |boolean |Yes


### Note

|Attribute | Description | Type| Mandatory
|---------------|-------------|------|-------|
|content |Text of the note, should be of CDATA type |String |Yes
|createdBy |Name of user who created Note. (this would be eGain user name) |String |No
|createdDate | Creation date and time. |String |No


### Custom Attributes

|Attribute | Description | Type|Mandatory
|---------------|-------------|------|-------|
|name |Name of custom Attribute |String |Yes
|type |Type of custom attribute |String |Yes
|value| Value of Custom Attribute. |String |Yes
