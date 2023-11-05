# pharr_format
## Add English vocabulary to ancient texts

<hr> </hr> 

This program is inspired by Clyde Pharr's edition of Vergil, which presented the Latin text along with English vocabulary on the same page to facilitate reading and avoid time spent looking up the more obscure vocabulary words in a dictionary. 

![Pharr image](https://cdn.shopify.com/s/files/1/0018/4723/0510/products/9604_VERGIL_S_AENEID_PAGE_6_1024x1024@2x.jpg?v=1583945371) 

The idea is to format a text and add glosses for infrequently used words. Currently, the program adds glosses for any word that appears five times or fewer in the text. 

Currently, only Latin texts that are available from either the [Tesserae](https://tesserae.caset.buffalo.edu/) corpus (via the University of Buffalo) or the Latin Library are available. 

<hr>

## Acknowledgements

Credit to the [CLTK](http://cltk.org/) and Luke Hollis/Archimedes Digital for the [Open Words](https://github.com/ArchimedesDigital/open_words) code that I used to make this project. 

Also thanks to [Perseus](http://www.perseus.tufts.edu/hopper/) and the [Latin Library](http://thelatinlibrary.com/) for use of their texts, including the Lewis & Short dictioanry. 

## Requirements and operation

### Updated October, 2023 

Since I wrote this program originally, the underlying software has undergone some significant revisions, including a major release update from the CLTK. Unfortunately for this project, however, the updates disrupted the original code, and I made some corresponding revisions to the way this program works. 

Instead of relying on the CLTK's corpus reader modules, I have instead opted to write my own parser for both Perseus and Latin Library texts; I include the data for the Perseus library in this repo, while Latin Library texts are sourced from URLs when called. I may opt to remove the Perseus data from the repo and generate texts when called (similar to what we do for the LL) if that feature is requested, as it would cut down on the required size of the repo. 

Further, to reduce the risk of future version conflicts, I've included a `requirements.txt` file here which specifies the required packages explicitly. 

Admittedly, I did not follow best practices by creating a fresh environment during development of this project. As a result, the requirements.txt file (and frankly, the code base here) is somewhat bloated. I recommend creating a new conda environment to run this program and install the rquired modules. 



### Original text, 2021

The program requires the CLTK and Open Words. The virtual environment that I used to create the program is included in the venv folder in this repo. To enable the environment, create a directory and clone the repo. Then run `python3 -m venv dir/pharr_format/venv`. You can use any Python environment compatible with CLTK (Python 3.7+) 

Clone the two required repos into a project folder and add steadman.py. Users will have to unzip the dictionary file in the `lexica` folder.

Operation is relatively simple: 

``` python 

# instantiate class

steadman = steadman.PharrBuilder('latin_text_latin_library') # or 'latin_text_perseus' 

cat = steadman.catalog

cat[cat['author'].str.contains('vergil')] # look at available texts by Vergil

text = 'vergil/aen6.txt' # I use the CLTK file system to grab the texts, so the `source` column of the catalog is required 

steadman.get_texts(text)

steadman.create_document(title = 'vergil_aeneid_6_.docx', output_format='poetry')
```

Other methods available in the PharrBuilder class include word counts for lexical analysis and vocabulary lists based on frequency. The .docx files included in the repository are samples of the final output. 

## Refinements and next steps 

- Improvements to the parser. There are a few bugs in the parser used to add word definitions that result in errant definitions (for example, glossing *fido fidere fisus* as *chord, instrument string, constellation Lyra, stringed instrument (pl.), lyre*) 

- Support for Greek 

- Options to control paragraph length and other printing options

- Direct to PDF option

- Adding a full vocabulary list of all words in a text to the end of the document
