# AMI-Chem

## Overview

Extracts complete chemical structures and 2-D coordinates from vector-based chemical diagrams

* Input: SVG diagram or PDF containing PDFs
* Output: CML including group expansion and coordinates from image
* Output: PNG (coordinates generated by CDK)
* Output: SVG (coordinates generated by CDK)
* Output: SMILES 
* Output: results.xml (contains CML)
* Method: extracts vectors and characters from diagram and builds an (organic) chemical structure
* Note: Does NOT run OSCAR or OPSIN and does not translate names
* Limitation: Does not run on HTML or XML or PDF text (will have separate plugin for that)
* Limitation: Does not run on pixel images (but will very soon)
* Limitation: Can extract, but does not understand, dotted bonds, thick bonds, wiggly bonds (and nor do most humans)
* Limitation: hardcoded list of chemical groups.

## Example

Taken from Metabolites 2012, 2, 39-56; doi:10.3390/metabo2010039. "Comparative Chemistry of Aspergillus oryzae (RIB40) and
A. flavus (NRRL 3357" which contains names and structures on many metabolites and metabolic reactions.

[PDF of article](https://raw.githubusercontent.com/ContentMine/ebi_workshop_20141006/master/sessions/4_AMI/chem_files/metabolites-02-00039.pdf) 

We'll use Page 2 (screenshot)

![image of Figure 2](https://raw.githubusercontent.com/ContentMine/ebi_workshop_20141006/master/sessions/4_AMI/chem_files/metabo2010039.png)

``IN THE PDF`` visit Page 2 and verify that the image can be scaled may times without fuzziness or jaggies. This shows that it's preserved the vectors.

AMI has extracted all subsets of vectors into chunks (g.2.12.3 is page 2 section 12 image 3). Here's the SVG).

![svg of kojic acid](https://raw.githubusercontent.com/ContentMine/ebi_workshop_20141006/master/sessions/4_AMI/chem_files/image.g.2.13.svg)

Your browser may show a broken link to the source which looks like:

```
<?xml version="1.0" encoding="UTF-8"?>
<svg height="800.0" width="700.0" xmlns="http://www.w3.org/2000/svg">
 <g title="org.xmlcml.svg2xml.page.MixedAnalyzer2" id="g.2.13" transform="matrix(1.0,0.0,0.0,1.0,-386.04,-508.02000000000004)">
   <path stroke="black" fill="#000000" stroke-width="0.0" svgx:z="1775" d="M415.26 526.26 L415.26 517.98 C415.26 517.86 415.38 517.74 415.5 517.74 C415.62 517.74 415.74 517.86 415.74 517.98 L415.74 526.26 C415.74 526.44 415.62 526.56 415.5 526.56 C415.38 526.56 415.26 526.44 415.26 526.26 " xmlns:svgx="http://www.xml-cml.org/schema/svgx"/>
   <path stroke="black" fill="#000000" stroke-width="0.0" svgx:z="1776" d="M417.42 526.26 L417.42 517.98 C417.42 517.86 417.54 517.74 417.72 517.74 C417.84 517.74 417.96 517.86 417.96 517.98 L417.96 526.26 C417.96 526.44 417.84 526.56 417.72 526.56 C417.54 526.56 417.42 526.44 417.42 526.26 " xmlns:svgx="http://www.xml-cml.org/schema/svgx"/>
   ...
   <text stroke="none" fill="#000000" svgx:fontName="CDPKAC+ArialMT" svgx:width="778.0" font-family="Helvetica" font-weight="normal" svgx:z="1774" x="413.22" y="516.6" font-size="8.58" xmlns:svgx="http://www.xml-cml.org/schema/svgx">O</text>
   <text stroke="none" fill="#000000" svgx:fontName="CDPKAC+ArialMT" svgx:width="722.0" font-family="Helvetica" font-weight="normal" svgx:z="1777" x="386.04" y="528.84" font-size="8.58" xmlns:svgx="http://www.xml-cml.org/schema/svgx">H</text>
   ...
 </g>
</svg>

The ``path``s are the bond and the ``text`` are the element symbols (atoms). AMI-chem can interpret this:


```

So we run:

```
ami-chem -i /home/workshop/ebi_workshop_20141006/sessions/4_AMI/chem_files/image.g.2.13.svg
```

and get output something like:

```
245  [main] INFO  org.xmlcml.xhtml2stm.visitor.chem.ChemVisitor  - SVGContainer name: /Users/pm286/workspace/xhtml2stm/./src/test/resources/org/xmlcml/xhtml2stm/molecules/image.g.2.13.svg
245  [main] INFO  org.xmlcml.xhtml2stm.visitor.chem.ChemVisitor  - Working with svgContainer: /Users/pm286/workspace/xhtml2stm/./src/test/resources/org/xmlcml/xhtml2stm/molecules/image.g.2.13.svg
1686 [main] DEBUG org.xmlcml.xhtml2stm.visitor.chem.MoleculeCreator  - Looking for reactions
2138 [main] DEBUG org.xmlcml.xhtml2stm.visitor.chem.MoleculeCreator  - Molecule potentially part of a reaction ((384.63977442374846,459.1559855762515),(508.7623916951517,554.7226083048484)) 16 C1(C(=C(OC(=C1[H])C(O[H])([H])[H])[H])O[H])=O

...

3219 [main] DEBUG org.xmlcml.xhtml2stm.visitor.VisitorOutput  - outputFile: target/image.g.2.13.xml

```

The "C1(C(=C(OC(=C1[H])C(O[H])([H])[H])[H])O[H])=O" is an inline chemical formula ("SMILES");

There will also be images (PNG and SVG):

![png from ami-chem](https://raw.githubusercontent.com/ContentMine/ebi_workshop_20141006/master/sessions/4_AMI/chem_files/image.g.2.13.svg.molecule0.png)

![SVG from ami-chem](https://raw.githubusercontent.com/ContentMine/ebi_workshop_20141006/master/sessions/4_AMI/chem_files/image.g.2.13.svg.molecule0.svg)

Note that the image is NOT a copy of the original. It is completely generated from the semantic representation. Therefore it cannot infringe copyright.

## checking results!

### Daylight Depict

Visit [Daylight Depict site](http://www.daylight.com/daycgi/depict), paste in the string C1(C(=C(OC(=C1[H])C(O[H])([H])[H])[H])O[H])=O and you'll see a picture confirming the structure (it uses a different drawing convention, with circles, but it's the same molecule).

![png from depict](https://raw.githubusercontent.com/ContentMine/ebi_workshop_20141006/master/sessions/4_AMI/chem_files/image.g.2.13.smiles.png)

### ChEBI

Visit ChEBI [ChemicalStructuresOfBiologicalInterest](http://www.ebi.ac.uk/chebi/) and search for "kojic acid" which should return 
![search in chebi](https://raw.githubusercontent.com/ContentMine/ebi_workshop_20141006/master/sessions/4_AMI/chem_files/kojic.chebi.png)

![search result in chebi](https://raw.githubusercontent.com/ContentMine/ebi_workshop_20141006/master/sessions/4_AMI/chem_files/kojic.chebi.2.png)


## Molecules

ami-chem also generates CML (Chemical Markup Language) files which contain the complete sematic results for the molecule:

```
 target/image.g.2.13.xml/image.g.2.13.svg.molecule0.cml 
```
which looks like:

<?xml version="1.0" encoding="UTF-8"?>
<molecule x2="421.89788" y2="531.7425000000001" xmlns="http://www.xml-cml.org/schema">
  <atomArray>
    <atom id="a11" elementType="C" x2="41.641" y2="-52.553" hydrogenCount="0"/>
    <atom id="a12" elementType="C" x2="40.62" y2="-53.19" hydrogenCount="0"/>
 ....
  </atomArray>
  <bondArray>
    <bond atomRefs2="a11 a12" id="a11_a12" order="S"/>
    <bond atomRefs2="a13 a11" id="a13_a11" order="S"/>
 ....
  </bondArray>
  <name>/Users/pm286/workspace/...xhtml2stm/molecules/image.g.2.13.svg</name>
</molecule>

and can be viewed in Avogadro (distributed with the system) - screenshot:

![Avogadro screenshot](https://raw.githubusercontent.com/ContentMine/ebi_workshop_20141006/master/sessions/4_AMI/chem_files/avogadro.2.13.png)








