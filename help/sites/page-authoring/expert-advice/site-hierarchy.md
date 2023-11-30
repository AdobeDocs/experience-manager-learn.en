---
title: Site Hierarchy, Taxonomy, and Tagging Guide
seo-title: AEM Sites Site Hierarchy, Taxonomy, and Tagging Guide
description: A full overview of AEM Sites metadata, tagging, taxonomy, and hierarchy. Use this guide to ensure your content strategy is consistent and following best practices
seo-description: A full overview of AEM Sites metadata, tagging, taxonomy, and hierarchy. Use this guide to ensure your content strategy is consistent and following best practices
audience: author, marketer
topic: Content Management
feature: Learn From Your Peers
role: Admin, User
jira: KT-14254
level: Beginner, Intermediate
doc-type: Article
exl-id: c88c3ec7-9060-43e2-a6a2-d47bba6f7cf3
---
# Tags, Taxonomy, and Metadata Best Practices: High-level Summary

Metadata and tags are key to driving efficiency in AEM. Users, leaders, and management realize the need for holistic strategy, but they find it difficult make headway. Often knowledge is siloed among users, making holistic strategy difficult—and makes adjustments even more problematic. 

What is the difference between metadata and tags? What are the business aspects to take into consideration when driving your strategy?  

## What is purpose of metadata? 

Metadata adds structure to less structured content. 
Example: A basic image has pixels. We can call those "core data." It is the metadata that describes the format, the category, licensing details, etc. 
Metadata is most frequently used for assets. But there is a large number of use cases for metadata in content pages or experience fragments as well. 

## Sources of Metadata 

The following are the categories of which metadata can be generated: 

* Extracted Metadata – The information already is available in the document, e.g. in natural language. 
* Derived Metadata – The information is not available in the original data but can be derived by cross-referencing prior knowledge.  
* Manually Added Metadata – This is metadata that does not fall into either of the first categories and needs to be added manually by a human.

## Types of Metadata

Within the categories listed above there are four major types: 

* Technical & Descriptive Metadata: Provides info about technical details of content (i.e. tite, language, etc.)
* Operational Metadata: Documents the lifecycle of an asset (i.e. approved, in creative, campaign)
* Administrative Metadata: The status or state of an asset within an organization (i.e. license information, ownership)
* Structural Metadata: Helps categorize assets or pages to smooth business process (applies to most tags and taxonomies) 

## Folder and File Names

Folders are a natural way to navigate and browse the content in AEM. How are your stakeholders going to interact with AEM? This will determine how your folders are structured. Normally folder structure architected with one (or two) of the following in mind:  

* Navigation
* Browsing
* Categorization 
* Access control

For AEM Sites, navigation is key. Folders are used to control access to the assets and pages. 

Which tiers of authors are going to need access to homepages? What about product pages? Or campaign? Use permissions plus folder structure to put in the right governance.

## Storing Metadata

There are three ways methods to store metadata: 

* Binary: Binary format related the nature of the asset (Photoshop, InDesign, PNG, JPG). 
* Asset node: This is metadata on the asset itself, regardless of the system or process being used. 
* External location: Metadata that is not directly on the asset, but can be used as a descriptor of the "state" of an asset (example: a workflow that can affect an asset but not directly applied to it)

## Metadata Model

The structure of how metadata is captured and formatted is called the metadata model or metadata schema. This must be agreed upon before assets or pages are ingested into the system. 

A metadata model usually is architected to meet the following use cases:

* Search & Retrieve: Helps store key aspects of content that helps easy retrieval by business.
* Reuse: Helps utilize old assets for repurpose (saving time and money)
* License Management: Tracks organization ownership of asset (often for legal reasons)
* Distribute: Make content available to consumers, or syndicate assets to business partners. 
* Archive: Metadata that notes an asset is outdated (always best practice to put an "archived" flag on asset so as not to lose vital information)/
* Cross-Reference: Associative metadata that captures the relation of two or more assets to each other (synthesis of metadata enables cross-referencing and coherent group organization)
* Navigate: The folder structure in which assets are stored (used to retrieve information by browsing)

*Author metadata mainly supports operational processes. Publish supports retrieval and distribution use cases.*

## Using Tags as Pre-Defined Terms

A tag is a keyword or term assigned to a piece of information.vFor example, instead of entering "car", "vehicle", "automobile", a tag system allows only one value to choose from, making searching more predictable.  Tags normalize and simplify the categorization of assets. 

*Note: Although AEM allows ad-hoc tagging it is best practice to stay from this as it could lead to undefined and unwieldy taxonomy.*

Common uses of tags: 

* Keyword searching:  A tag can describe, that a resource belongs to a certain group of entities. E.g. a tag "image/subject/car" describes the resource belongs to the set of images that show a car.
* Driving relations: All resources sharing the same tag can be considered connected. Tagging instead of directly linking is especially useful on websites that have a lot of dynamic and connected content. 
* Drive navigation: Tags ordered in hierarchical taxonomy can build navigation, a or link to similar documents. 
Tags should also be looked  information that connect various types of data, based on business terms rather than on technical properties.

## Common Applications of Tags

When used in AEM, tags can help in achieving a much shorter implementation of the complex feature, such as: 

* Faceted search 
* Personalized navigation
* Related Content
* Content References
* Search Engine Optimization
* Highlighting key concepts

## Taxonomies

A Taxonomy is a system of organizing tags based on shared characteristics, which are usually hierarchical structured per organizational need. The structure can help finding a tag faster or impose a generalization. 
Example: There is a need to subcategorize stock imagery of cars.  The taxonomy could look like:

/subject/car/ 
/subject/car/sportscar
/subject/car/sportscar/porsche
/subject/car/sportscar/ferrari
…
/subject/car/minivan
/subject/car/minivan/mercedes
/subject/car/minivan/volkswagen
…
/subject/car/limousine
…

Now a user can choose whether he wants to look up images of sportscars in general or a "Porsche" in particular. After all, both are sportscars. 
Best Practice: Avoid flat taxonomies. Flat taxonomies lack the benefits described above and require constant maintenance 

**Using a Taxonomy as Thesaurus.**  When a user searches for a keyword, the system creates a second search for all synonyms found there. 
Additionally, Instead of typing "car" manually, the system can provide a list of keywords to improve consistency.  

**Using a Taxonomy as a Dictionary.** Instead of just printing "car", you can expand the single tag and use all the tag's synonyms.

**Multiple Categories.** In contrast to a folder hierarchy, tags can be used to express multiple categorizations at the same time. An asset tagged with:

/subject/car/minivan/mercedes
/subject/people/family
/color/red

## Metadata vs Tag

Not all metadata should be considered as a candidate for tagging system. Technical metadata can, unnecessarily duplicate the information. The best candidate for tags is business metadata. .Tags are a good choice to enforce consistent vocabulary, facetted search, and navigation.

## Tag Management

Tag management benefits from a dedicated core team. New members should learn purpose and function of the taxonomy first before adding new tags.  Seasoned experts, acting as gatekeepers to new tags, will reduce long-term inconsistency.

## Tag Creation

Taxonomies should be employed by content authors and understood by end users. They should be created before the content creation process. Any shortcuts will result in additional effort for management and maintenance.

## Ongoing Maintenance

Things change, and the needs of the tag list will too. Come-up with sound maintenance process that will reduce duplication.

Make sure content contributors know how they can propose changes, and that editors or content managers are reviewing the terms regularly.

## Best Practices with Tags and Taxonomies

**Standardize Tags.** Create glossary that provides an authoritative vocabulary. Without establishing standards, duplication will present problems. Additionally, it is advised to audit not only the taxonomy but also the usage of the tags.

**Don't Over-Tag.** Tags can lose their significance if too frequently distributed..Pprune extraneous tags for optimal efficiency. 

**Re-evaluate Tags Over Time.** Remember that business terminology and business context rarely stay static. You may find the need to re-standardize and re-apply tags.

**Using AI-powered Smart Tagging.** Smart tagging [see link] is an AI capability in AEM to reduce the effort of manually tagging assets. Smart tagging uses an AI to infer information about the subject of an image. It generates descriptive tags that describe the contents of an image.

## Metadata Quality and Maintenance 

Understanding business requirements is an important step in executing a metadata management model. Without definition, the information cannot be stored. It will be necessary to revisit the model periodically. This a vital quality control activity. 

Additionally, metadata should be captured as early as possible in the content creation process. If metadata isn't 'applied at the right time, there is little chance of applying it retroactively.

**Utilize metadata** to enhance collaboration:  Utilize Adobe Asset Link, Adobe Bridge and the AEM Desktop to tie creative process together and utilize metadata to streamline creative workflows. Using these tools will enrich metadata and the user experience across your creative process. 

## Best Practices for Metadata Management

*    Assign Core Team with Strong Executive Mandate: Form a metadata core team which has complete understanding of the business ecosystem and a strong mandate by the organization's management. 
*    Define Metadata Strategy and Governance: A good metadata strategy can help the organizations in explaining the need and benefits of the metadata.  A strategy consists of, metadata schema(s), taxonomy, business processes (for data quality and capture), roles and responsibilities, and governance processes. *
*    Define and Communicate Consistent Metadata Model: Defined strategy and reasoning should be well documented and communicated within the organizations. 
*    Standard Naming Convention: Create consistent and descriptive file naming convention for enhanced branding, information management, and usability. 
*    Safe Characters in Filenames: Filename should be able to be interpreted by all common operating system. You are safe to use characters, numbers, umlauts, space and underline. The minus symbol also is safe, but if you cut and paste, it might look like a "dash".
*    Version Naming Convention: AEM offers some capabilities to keep former versions of assets. In some cases, you might want to keep several versions. However, you should make sure that the versioning scheme is consistent. 

## Organizational vs Descriptive Metadata

A few guidelines might help you to decide how to categorize metadata: 

**Description** – If the data describes the asset or piece of content it should be part of the attached metadata.

**Search** – If the metadata shall be used in search it must be attached.

**Exposure** – If you are exposing the metadata on a distribution platform to a third party, be careful not to also expose "internal" metadata.

**Duration** – The longer the metadata is supposed to live, the more likely it is to be a good candidate for attached metadata. 

**Related Business Processes** – It definitely is helpful to have a permanent product ID as part of the metadata. But the category of an item in relation to the product catalog is a questionable metadata for the asset.

**Organization and Processing** – If the nature of the metadata is of organizational nature, such as state in an approval workflow or ownership of a certain department, external metadata should be considered over attaching the metadata to the asset.

*To create the strategy, ask the following questions:*

* What kind of content and "additional information" (= metadata) is needed to solve business problems / business questions / business issues?
* What are the variables, the "fields" in the schema, and what are possible values? What variables need a free-text input, which ones can be narrowed by type (number, date, boolean, ..), a set of fixed values (e.g. countries) or tags from a given taxonomy. How many tags are required, allowed? 
* What technical issues / problems / questions can be solved by metadata? 
* How can you obtain / create that content / metadata? How much will it cost to obtain / create that metadata?
* What types of metadata are needed for a particular user group?
* How will metadata be maintained and updated?
* Who is responsible for what part in the process?
* How can you assure that agreed business processes are followed?
* What standards should you follow? Should you adopt and modify an industry standard (Dublin Core, ISO 19115, PRISM, etc.) or should the organization create its own standards?
* Where is the strategy documented? How can you make sure all stakeholders have access? How can you make sure, newly onboarded staff adheres to the agreed standard (e.g. visit training before getting access?)
