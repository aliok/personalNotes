---
layout: post
title:  "Text line segmentation notes"
date:   2014-12-02 00:04:00
categories: public
---

# Terms

## General
document structure extraction
: TBD

word spotting
: "retrieve similar words in the image document through an image query"

fluctuation
: see baseline fluctuation below.

superfluous information
: non textual elements, textual elements from the verso (other side of the page)

verso
: other side of the page

recto
: frong side of the page (opposite of *verso*)

image binarization
: TBA

taxonomy
: classifying into groups (tasnif)

projection profiles
: TBA

smearing
: ?

Hough-based
: ?

repulsive-attractive network
: ?

stochastic method
: ?


## Lines and components
From paper1:[^paper1]
![]({{ '/post-assets/text-line-segmentation/reference-lines-and-components.png' | prepend: site.baseurl }})

baseline
: fictitious line which follows and joins the lower part of the character bodies in a text line

median line
: fictitious line which follows and joins the upper part of the character bodies in a text line

upper line
: fictitious line which joins the top of ascenders.

lower line
: fictitious line which joins the bottom of descenders

overlapping components
: descenders and ascenders located in the region of an adjacent line

touching components
: ascenders and descenders belonging to consecutive lines which are thus connected.


## Author style
baseline fluctuation
: the baseline may vary due to writer movement. It may be straight, straight by segments, or curved.

straight baseline
: straight (duz, ama acili (rotated) olabilir)

straight baseline by segments
: each segment is straight, but baseline is not continuous (kelime kelime duz olabilir baseline)

curved baseline
: curved (yazarin eli cevrilmis)

line orientations
: there may be different line orientations, especially on authorial works where there are corrections and annotations.

line spacing
: space between lines. overall, the problem is less complex when spacing is large.

insertions
: words or short text lines may appear between the principal text lines, or in the margins.


## Image quality
imperfect preprocessing
: smudges, variable background intensity and the presence of seeping ink from the other side of
  the document make image preprocessing particularly difficult and produce binarization errors.

stroke fragmentation and merging
: punctuation, dots and broken strokes due to low-quality images and/or binarization may produce many connected components; conversely, words,
  characters and strokes may be split into several connected components. The broken components are no longer linked to the median baseline of the
  writing and become ambiguous and hard to segment into the correct text line.


## Main problems
line fluctuation
: baseline has a different angle; or it is not linear (segmented); or it is curved

line
: Components too close to each other

writing fragmentation
: components are split into several components (mesela silik yazi)


# Text line representation
separating paths
: fictitious lines separating text lines. can be uniformly straight, made of straight segments, or of curving joined strokes.

delimited strip
: delimited strip between two separating lines receives the same text line label. So the text line can be represented by a strip with its couple of separating lines.

clusters
: general set-based way of defining text lines. A label is associated with each cluster. Units within the same cluster belong to the same text line. They may be pixels,
connected components, or blocks enclosing pieces of writing.

strings
: strings are lists of spatially aligned and ordered units. Each string represents one text line.

baselines
: baselines follow line fluctuations but partially define a text line. Units connected to a baseline are assumed to belong to it.



# Notes

### From paper1:[^paper1]

> There are two categories of text line segmentation approaches: searching for (fictitious)
  separating lines or paths, or searching for aligned physical units. The choice of a
  segmentation technique depends on the complexity of the text line structure of the document.

> After the text part has been extracted and restored, top-down and smearing techniques
  are generally applied for text line segmentation

#### Preprocessing

> Non-textual elements around the text such as book bindings, book sides, parts of fingers (thumb marks from
  someone holding the book open f.i.) should be removed upon criteria such as position and intensity level.

> On the document itself, holes, stains, may be removed by high-pass filtering :
From ext-paper1:[^ext-paper1]
![]({{ '/post-assets/text-line-segmentation/german_guy_highpass_filter.png' | prepend: site.baseurl }})

> Other non-textual elements (stamps, seals) but also ornamentation, decorated initials, can be removed
  using knowledge about the shape, the color or the position of these elements [[^ext-paper2]].

> Extracting text from figures (text segmentation) can also be performed on texture grounds [[^ext-paper3]] [[^ext-paper4]] or by morphological filters [[^ext-paper5]] [[^ext-paper6]].

> Linear graphical elements such as big crosses (called “St Andre’s crosses”) appear in some of Flaubert’s manuscripts. Removing these elements is performed through GUI by Kalman filtering in [[^ext-paper7]].

!!!!!!!!!!!!!!!BOOKMARK!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!BOOKMARK!!!!!!!!!!!!!!!!!!!!!!!!!!!!
!!!!!!!!!!!!!!!BOOKMARK!!!!!!!!!!!!!!!!!!!!!!!!!!!!

> Textual but unwanted elements such as the writing on the verso (bleed through text) may be removed by filtering and wavelet techniques [24][54][32]
  and by combining the verso image (the reverse side image) with the recto one (front side image).

> Binarization, if necessary, can be performed by global or local thresholding. Global thresholding algorithms are not generally
  applicable to historical documents, due to inhomogeneous background. Thus, global thresholding results in severe deterioration in the quality
  of the segmented document image. Several local thresholding techniques have already been proposed to partially overcome such difficulties [21].
  These local methods determine the threshold values based on the local properties of an image, e.g. pixel-by-pixel or region-by-region, and yield
  relatively better binarization results when compared with global thresholding methods.
  Writing may be faint so that over-segmentation or under-segmentation may occur.


# Scratch pad

## My process for text line segmentation
* Find text part (get rid of the borders etc.) with preprocessing. **HOW**?
* Apply some additional preprocessing such as high-pass filters. That should make the text more clear.
* Some additional things like “St Andre’s crosses” are easy to get rid of. Use Kalman filtering and a GUI for removing them manually.
* I don't care about the verso image.
* Binarize the image. This basically means black-or-white kind of processing. Make text black, make everything else white.
*

# Papers
[^paper1]:
    [Text Line Segmentation of Historical Documents: a Survey]({{ '/post-assets/text-line-segmentation/01_0704.1267.pdf' | prepend: site.baseurl }})
    ^
    - Laurence Likforman-Sulem, Abderrazak Zahour, Bruno Taconet
    - 2006




[^ext-paper1]:
    [Generierung einer semantischen Reprasentation aus Abbildungen handschriftlicher Kirchenbuchaufzeichnungen]({{ '/post-assets/text-line-segmentation/diplom_feldbach.pdf' | prepend: site.baseurl }})
    ^
    - Markus Feldbach
    - 2000

[^ext-paper2]:
    Les documents anciens, Document numérique, Hermès, Vol. 3, no 1-2, june, pp. 57-7
    ^
    - [not open](http://jacques-andre.fr/japublis/andrechabin.pdf)
    - Gusnard de Ventadert, J. André, H. Richy, L. Likforman-Sulem, E. Desjardin
    - 1999

[^ext-paper3]:
    Text segmentation using Gabor filters for Automatic Document Processing, MVA, Vol5, pp. 169-184.
    ^
    - [not open](http://link.springer.com/article/10.1007/BF02626996)
    - Jain A., Bhattacharjee S.
    - 1992

[^ext-paper4]:
    Colorizing paper texture of green-scale image of historical documents, Proceedings of the 4th IASTED Conference on Visualization, Imaging and Image Processing, VIIP, Marbella, Spain.
    ^
    - [not open](http://www.actapress.com/Abstract.aspx?paperId=18852)
    - Mello C. A. B., Cavalcanti C. S.V.C., C. Carvalho
    - 2004

[^ext-paper5]:
    Extraction de textes et de figures dans les livres anciens à l’aide de la morphologie mathématique, Actes de CIFED’2000, Colloque International Francophone sur l’Ecrit et le Document, Lyon , pp. 81-90.
    ^
    - [not open](http://books.google.ch/books?id=s2INxlR0guEC&lpg=PA81&ots=DfRkaFNXhy&dq=%22%20Extraction%20de%20textes%20et%20de%20figures%20dans%20les%20livres%20anciens%20a%CC%80%20l%E2%80%99aide%20de%20la%20morphologie%20mathe%CC%81matique%22&lr&pg=PA89#v=onepage&q=%22%20Extraction%20de%20textes%20et%20de%20figures%20dans%20les%20livres%20anciens%20a%CC%80%20l%E2%80%99aide%20de%20la%20morphologie%20mathe%CC%81matique%22&f=false)
    - Granado I., Mengucci M., Muge F.
    - 2000

[^ext-paper6]:
    Morphological Segmentation of text and figures in Renaissance books (XVI Century), in Mathematical Morphology and its applications to image processing, Kluwer, pp. 397-404.
    ^
    - [not open](http://books.google.ch/books?id=nAu1HYVcQ2wC&lpg=PA396&ots=zO1-IFBkhH&dq=%22Morphological%20Segmentation%20of%20text%20and%20figures%20in%20Renaissance%20books%22&pg=PA396#v=onepage&q=%22Morphological%20Segmentation%20of%20text%20and%20figures%20in%20Renaissance%20books%22&f=false)
    - Mengucci M., Granado I., J. Goutsias, L. Vincent, D. Bloomberg( eds)
    - 2000

[^ext-paper7]:
    Extraction d'éléments graphiques dans les images de manuscrits, Colloque International Francophone sur l'Ecrit et le Document (CIFED'98), Québec, pp. 223-232.
    ^
    - not open, nowhere to buy
    - L. Likforman-Sulem
    - 1998



<style>
/** Some special overrides for this page **/
    blockquote{
        color: inherit;
        font-style: inherit;
        letter-spacing:inherit;
    }

    dt{
        width: 250px;
    }

    dd{
        margin-left: 270px;
    }
</style>