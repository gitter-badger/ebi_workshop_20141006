Highlighter Markup Exercise
============================

## The paper can be found [here](http://www.biomedcentral.com/1471-2148/14/70)

[This exercise has been run in all workshops as an "icebreaker" and works very well. 
Here we extend it for informatics professionals to include ideas of precision/recall and also final target vocabularies.]

 * You will be provided with paper copies of pages from one (or two) scientific articles. Although technical you should be able to
carry out this exercise without any deep scientific knowledge
 * Work in about 4 groups of up to 6 people. Each person has a different highlighter pen to markup up *entities* in the article. 
(code below)
 * Mark up all entities in each page starting at the top (only mark new entities and stop after 10). Swap the pages within the 
group so each gets exposed to every marker pen. Mark only the entity.

 Entities
 --------

An entity is a complete nounal word or phrase which can/could be found in a systematic taxonomy or definition. 
Thus "1984", "Pleistocene", "5 minutes" could be marked as date/times, while "recently" would be too fuzzy. 
*Where there is ambiguity, try to consider whether others would vote the same way*.

*For each entity type try to formulate the rules that you used and whether they could be computerised.* Examples are:

* syntactic context "The foo lives in bar" 
* lexical makeup of words
* style/fonts
* lookup in authorities (e.g. Wikimedia)
* computability - can the entity be analysed algorithmically?


Types of entity
===============

* YELLOW: Species and Genera. use only precise terms (e.g. omit generic terms such as "pets"). 
* ORANGE: Places. Anything that resolves to a usefully defined point or region. "London", Latitude+Longitude, not "further north". 
Exclude metadata
* PURPLE Date/times. Resolvable to an ISO 8601 datetime or an ontologically supported concept ("Eocene", "equinoctual"). Not "recently".
Exclude metadata.
* RED. Identifiers. Formal codes given by authorities, e..g PMIDs, Genbank IDS. 
* CYAN. Bibliographic and academic metadata, including rights, grants. Indicate precise lengths of phrase and constant/variable 
components
* GREEN. Chemical compounds. Resolvable in PubChem, or of generic chemical form. Not "diesel oil", "butter".

Precison and Recall
===================

When your group has finished swap your sheets with your neighbours. Critique *their* markkup, drawing a circle round where you
disagree - either for an omission ("false negative") or a wrongly marked entity ("false positive").

*Note there is NO absolutely right of wrong answer*, there is inter-annotator dis/agreemnt. The better the agreement the higher 
scores we should expect from programmatic output. 

Note also this is very tedious and generally impossible without Open material. Humans have to:

* write and agree th rules. We wrote 31 pages for chemistry.
* have several people independently mark up a test corpus. Calculate the interannotator agreement. We got 92% for chemistry.
* write a program and train it against a traing corpus (more work)
* use a validation corpus (even more work) to test how well the program performs.






