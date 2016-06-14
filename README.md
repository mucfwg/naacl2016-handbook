These are instructions for preparing the NAACL handbook.

Production of the handbook is only semi-automated. The scripts
provided here do some of the work for you, but not all parts of
the handbook production are automated. The scripts in this 
directory are not (yet) robust to formatting errors in the many 
different input formats, and new bugs are discovered every time
they are run. Furthermore, the input comes from many different
people, and they all make different types of mistakes.

You should start your preparation by clearing the entire week before
the printed deadline---really. The process of assembling the
handbook is a little bit of scripting and auto-generation followed by
an immense manual effort. You will take the proceedings from the
various workshops and pieces of the main conference, use the scripts
in the `scripts/` subdirectory to generate some LaTeX, and then
hand-assemble and munge everything until it is complete. Then you will
read through it finding and correcting errors. You will find many of
these errors after you have uploaded the document to the printer, and
the last errors will not be found until after printing has begun. Sorry!

Now that you know what to expect, here are the instructions.

# Handbook contents 

The conference handbook typically has the following

- A customized cover
- Letters from the General Chair and PC Chairs
- Schedules for the main conference, workshops, and any co-located conferences
- Overviews for each day that summarize the main events
- An "at-a-glance" overview page for each parallel session listing times, 
  locations, titles, and authors
- Abstracts for all papers presented in the main conference
- Full pages for special events (the banquet, business meeting, special
  awards and ceremonies)
- An index pointing to every mention of a name within the document, 
  ideally containing no duplicate names (with spelling variations)
- Sponsors and ads

To see what this looks like, take a look at some past examples. They're 
included in the `examples` directory.

# Things to arrange months in advance

Since your handbook will include a custom cover and ads, and be printed, 
make sure the right people know when they will need to get you:

- The printing contract. In recent years, printing has been done by Omnipress
  (at least for North American conferences), and organized with the help
  of Priscilla. They will probably contact you well in advance. Most
  importantly, they will set the actual deadline for electronic delivery 
  of the handbook, probably about three weeks before the actual conference. 
  Since the electronic form  takes a week to produce, this means that you
  will need to ensure that the publications and workshop chairs have
  completed production of their proceeedings and schedules at least four
  weeks in advance. And since some of them will run into trouble with
  this, that means their deadline will require some slack in it, so
  they should plan to have it complete about six weeks in advance.
  All of the remaining items on this list should also be in your hands at 
  least a week before the handbook is due to the printer.
- The cover. In 2016, this was provided by the logo designer through
  the website chair.
- Ads. Technically, these are part of the sponsorship packages offered
  to companies, though print advertising has fallen enough out of favor
  that many of them forget to supply their ads. But if you want to offer
  that opportunity, make sure that the sponsorship knows well in advance
  what the sponsors should get to you.
- Special event and room information. Priscilla and the program chairs
  will get these to you.
- Letters from the general chair(s) and program chairs.

# Main conference versus workshops

There are two main types of events whose schedules appear in the
handbook: the main conference, and workshops. The differences are that:

- Main conferences are multi-track and require you to assemble
  schedules from multiple sessions whose schedules may be interleaved.
  Traditionally, these are main conference papers, short papers,
  demos, student research workshop papers, tutorials, and, since 2013,
  TACL papers. The hanbook contains a daily overview, session overviews,
  and abstracts for each paper.
- Workshops are single-track: the schedule and all papers are
  contained in a single session, e.g., `softconf.com/acl2014/WMT14`.

Workshops require less work to format since the schedule is linear and
abstracts are not included in the handbook. The information in the 
handbook mostly relies on the workshop `order` file.

The main conference is another matter. The papers that are presented
are contained in separate subconferences, whose separate schedules re
interleaved to produce the consolidated main conference schedule.

# Notes for Publications Chairs

The downside of being the handbook chair is that there is all sorts of
upstream events you have no power to enforce (except through friendly
pub chairs) but that have a large impact on how difficult your job
is. It will be helpful to read this section and pass this information
on to the publications chairs, in the case where you are not them. In
recent years, the publications chairs have also been responsible for the 
handbook, but if you are the "handbook chair" and are not also the
pub chair, you should be in touch with them early and often to
minimize the amount of hand-correction you'll have to do.

The single-most important thing you can do is to ensure that the
`order` files are properly formatted, for the workshops, but most
importantly, for all parts of the main conference proceedings.

The `order` file is a human- and machine-readable file that is part of
the ACLPUB package (which Softconf's START system helps you
assemble). It is used to generate the schedule in the proceedings,
where computer-readability isn't very important, but it is also used
to generate the schedules in the handbook, where computer-readability
is very important, since the schedules from many different workshops
and pieces of the main conference (papers, shortpapers, SRW, demos,
tutorials, and, since 2013, TACL) are assembled.

Publications chairs should ensure the following:

- If at all possible, convince the PC chairs **not** to use START's
  "ScheduleMaker" tool. This is a complicated Excel front-end setup
  that generates the "order" file, which is already fairly simple to
  edit. They should just edit the order file directly. It is much
  simpler. 

- The order files should be machine readable. Workshop chairs
  are sometimes tempted to play with the formatting lines in
  order to get a custom look, but this introduces a host of problems
  generating the handbook.
  
  To help ensure compliance, a script has been provided:
  
     cat papers/order | ./scripts/verify_schedule.py

  This will help catch some, but not all errors, since the format
  of the order file is undocumented, and evolves in ad hoc ways each
  year to serve new purposes.

- The main conference schedule---the one containing all sorts of
  non paper-related events like "Lunch" and "Coffee Break" and
  "Keynote address"---should be placed in the "papers"
  subconference, which represents the main conference proceedings. The
  other order files should contain _only_ events relevant to those
  workshops. For example, do not repeat coffee breaks and lunches
  in the "shortpapers"; "shortpapers" should contain only lines
  listing days, session titles, and the papers that are presented in
  those sessions. This is to aid in merging the schedules for these
  subconferences into a single unified schedule: the code in
  `scripts/` will group papers in identically-named sessions across
  files. While events like lunches could also be merged, it is better
  to just list them in one place so that changes to one file (e.g.,
  you decide to rename "Coffee Break" to "Tea time" for this year's
  meeting in Cambridge) do not require changes to be made all over the
  place. 

- Parallel sessions should be named using the convention "Session NL: NAME", where
  N is a session number (1..as many as necessary), L is a letter (A..number of parallel tracks),
  and NAME is the session name. Session names should be globally distinct. For example,

       = Session 6D: Machine Translation II

  This aids immensely in generating the handbook and also the poster placards that sit
  outside the rooms and provide a summary of all papers in each track. 
  
- If papers are mixed across workshops (e.g., SRW papers mixed into a
  regular session), the session headers should be identical across the
  order files. e.g., in `papers/order`, you could have
  
       = Session 1D: Syntax, Parsing, and Tagging I 
       247 11:00--11:25 # Tagging The Web: Building A Robust Web Tagger with Neural Network   

  and in `srw/order`, you would put
  
       = Session 1D: Syntax, Parsing, and Tagging I
       6 10:10--10:35 # A Tabular Method for Dynamic Oracles in Transition-Based Parsing
       5 10:35--11:00 # Joint Incremental Disfluency Detection and Dependency Parsin
       12 11:25--11:50 # A Crossing-Sensitive Third-Order Factorization for Dependency Parsing

  The identical session name allows them to be merged and formatted
  automatically when you generate the handbook.
  
- TACL papers are a recent addition to ACL conferences. Since TACL
  papers are published elsewhere, and are therefore not included with
  the conference proceedings, there is no ACLPUB package for them, and
  you must come up with an alternative. NAACL 2013 and ACL 2014, a fake
  subconference was created and the TACL papers were imported as if it
  TACL were a workshop. In NAACL 2015, we instead do the following:
  
   - Add the TACL papers to the file `input/tacl_papers.yaml`. This is
   a [YAML-formatted](http://yaml.org) document that is processed by
   the file `scripts/tacl_builder.py` to pull out the abstracts and
   paper metadata so they can be seamlessly integrated into the
   conference handbook.
   
   - Run the script:
   
        $ python2.7 ./scripts/tacl_builder.py
        Reading from file input/tacl_papers.yaml
        Write bibtex entries to auto/tacl/papers.bib
        Writing abstract auto/abstracts/tacl-485.tex
        ...

     This will generate the papers bibliography and the abstracts,
     which can then be treated like any paper.
     
   - In the main schedule (`data/papers/order`), you can now reference
     TACL papers using the format `XXX/TACL`, e.g.,
     
        498/TACL 11:05--11:30 # TACL-498: Extracting Lexically Divergent Paraphrases from Twitter %by Wei Xu, Alan Ritter, Chris Callison-Burch, William B. Dolan, and Yangfeng Ji

     The scripts that process this file will know how to transform
     this into a TACL paper reference, so long as it has been built
     from the TACL YAML file. In fact, this syntax works for any
     of the subconferences; for example, if you need to refer to
     demo paper #37, use 37/demos. The name must be the same as
     that used to refer to the subconference in START.

# The order file

The script `scripts/verify_schedule.py` does some minimal
sanity-checking on the order file, but it will not catch every problem.
Here is more detail on how to produce it and how to handle some common 
limitations.

The order file permits four types of lines:

- Comments: anything following a `#` character.
- Papers. Papers are either presented in oral sessions or in poster
  sessions. They are denoted by a number, which is tied to the paper
  submission ID, and is used to locate the paper and the paper's
  metadata in `proceedings/final/NUM/NUM_metadata.txt`. Papers
  presented as part of oral sessions have time ranges, while papers
  presented as posters do not. The `order` file generated by START
  will include paper titles on these lines as a comment, but this
  information is not used by the scripts that build the handbook,
  so editing it will not change the output. However, some of the
  scripts will fail if the comment is not present!
- '+' events, which are single events that have a time range but that
  are not associated with a paper. For example, lunch.
- Session headers, denoted by lines starting with '=', which are used
  to group together papers presented in a parallel track.

Here is a sample schedule excerpt (from `data/papers/proceedings/order`):

    + 07:30--08:45 Breakfast 
    + 09:00--09:15 Welcome %by Kevin Knight, Ani Nenkova, Owen Rambow
    + 09:15--10:30 Invited talk: "How can NLP help cure cancer?" %by Regina Barzilay
    + 10:30--11:00 Coffee break
    = 11:00--12:30 Parallel Session 1A: Machine translation  %chair David Chiang
    15 11:00--11:20  # Achieving Accurate Conclusions in Evaluation of Automatic Machine Translation Metrics
    187 11:20--11:40  # Flexible Non-Terminals for Dependency Tree-to-Tree Reordering
    503 11:40--12:00  # Selecting Syntactic, Non-redundant Segments in Active Learning for Machine Translation
    172 12:00--12:10  # Multi-Source Neural Translation
    206 12:10--12:20  # Controlling Politeness in Neural Machine Translation via Side Constraints
    648 12:20--12:30  # An Empirical Evaluation of Noise Contrastive Estimation for the Neural Network Joint Model of Translation

Note the session chair tag `%by`. If supplied, this will be pulled into the handbook.

As mentioned above, we can also refer to TACL papers using something
like the following (where the IDs correspond to those listed in `input/tacl_papers.yaml`):

    = 09:00--10:30 Parallel Session 4A: Semantic Parsing  %room Grande Ballroom A %chair Mike Lewis
    807/TACL 09:00--09:20  Transforming Dependency Structures to Logical Forms for Semantic Parsing [TACL] %by Siva Reddy, Oscar Täckström, Michael Collins, Tom Kwiatkowski, Dipanjan Das, Mark Steedman, and Mirella Lapata
    646/TACL 09:20--09:40 Imitation Learning of Agenda-based Semantic Parsers [TACL] %by Jonathan Berant and Percy Liang
    162 09:40--10:00  # Probabilistic Models for Learning a Semantic Parser Lexicon
    654/TACL 10:00--10:20  Semantic Parsing of Ambiguous Input through Paraphrasing and Verification [TACL] %by Philip Arthur, Graham Neubig, Sakriani Sakti, Tomoki Toda, and Satoshi Nakamura
    321 10:20--10:30  # Unsupervised Compound Splitting With Distributional Semantics Rivals Supervised Methods

These will be assembled automatically. Here's how to do a poster
session:

    + 18:50--21:30 Poster and Dinner Session I: TACL Papers, Long Papers, Short Papers, Student Research Workshop; Demonstrations
    249  # Interpretable Semantic Vectors from a Joint Model of Brain- and Text- Based Meaning
    416  # Single-Agent vs. Multi-Agent Techniques for Concurrent Reinforcement Learning of Negotiation Dialogue Policies
    161  # A Linear-Time Bottom-Up Discourse Parser with Constraints and Post-Editing
    178  # Negation Focus Identification with Contextual Discourse Information
    ...  

## Missing features

In START, the code used to verify the order file is not suited to the
handbook. Their verification ensures only that each paper in the final
version of the proceedings is listed exactly once. This prevents a
number of common situations that people require.

1. Listing a paper more than once in the schedule.

   Some people want this, say, when a paper is provided with both an
   oral presentation and is also present in a poster session. This
   can't be done in the current ACLPUB packages, which assert a 
   bijection between accepted paper IDs and papers listed in
   the schedule (the schedule is used to determine the paper's order
   in the proceedings, and this helps ensure that no paper is
   forgotten or has an ambiguous place). In EMNLP 2014, working with
   the SoftConf folks,
   [Yuval Marton](http://www1.ccls.columbia.edu/~ymarton/) arranged
   for a new notation, !, which is used to denote events that are a
   little more complicated than typical things like breaks, lunches,
   and so on, which use the '+' designator. You can use this to list a
   paper more than once and get it past START's verifications, e.g.,
   
      ! 11:05--11:30 Extracting Lexically Divergent Paraphrases from Twitter %by Wei Xu, Alan Ritter, Chris Callison-Burch, William B. Dolan, and Yangfeng Ji
   
   The '!' notation also permits keywords, some of which are parsed by the
   conference handbook code to create special formatting and to
   automatically add people to the index. e.g.,

      ! 09:00--10:10 Invited Talk: "A Quest for Visual Intelligence in Computers" %by Fei-fei Li

2. Publishing a paper in the proceedings but not listing it in the
schedule.

   START won't allow this, but you can just comment out the paper in
   the schedule for the handbook.
   
3. Listing a paper in the schedule that is not present in the
proceedings. 

   Sometimes there are papers not in the proceedings, but in the
   schedule, and you want the formatting to look the same. To
   accomplish this, you have to manually create new numbered entries
   for those papers in a separate proceedings tarball. Create new
   numbered entries and then the corresponding metadata in 
   
       SUBCONF/final/NUM/NUM_metadata.txt
     
   The handbook code will then find the entries in the metadata file.

# Data Layout

Now we get to assembling the handbook.

ACL 2014 had five parallel sessions. This should be useful for any handbook 
where parallel sessions are listed one per page with abstracts.

Directories:

- `input/`: fixed inputs
   - `input/conferences.txt`: list of conferences (used for auto-download)

- `data/`: where the ACLPUB tarballs are downloaded and unpacked to

- `scripts/`: scripts used to generate the handbook sections from the ACLPUB
  proceedings.

- `content/`: handbook tex files used to build the handbook. You will need
  to edit these files by hand.

- `auto/`: the output of scripts, used to generate first-pass LaTeX
  that is then pulled manually into the handbook content.

# Building the handbook

- Edit `input/conferences.txt` to include your list of subconferences.

- Download all the main conference proceedings and workshops using
  `scripts/download-proceedings.sh` This creates a proceedings tarball  
  for each SUBCONF in `data/SUBCONF/proceedings`.

- Verify the order files with `scripts/verify_schedule.py`:

        for file in $(ls data); do 
          num=$(cat data/$file/proceedings/order | python2.7 ./scripts/verify_schedule.py > /dev/null 2>&1; echo $?) 
          if test $num -ne 0; then 
            echo -e "$file\t$num"
          fi
        done

  Inevitably, some of the order files will contain errors. Most of them
  are due to formatting differences between what ACLPUB expects and what
  the handbook scripts expect, and whatever the book chair did to make
  the file acceptable for ACLPUB. You will need to manually fix them, 
  possibly with the help of the book chair if you can't reconstruct
  their intent.

- Generate the bibtex metadata from each workshop's paper metadata:

        for dir in $(ls data); do 
          [[ ! -d "auto/$dir" ]] && mkdir auto/$dir
          python2.7 ./scripts/meta2bibtex.py data/$dir/proceedings/final $dir
        done
    
  This creates abstracts in `auto/abstracts` (read in via LaTeX calls
  to `\paperabstract`) and BibTeX metadata used for the index and
  other things (in `auto/SUBCONF/papers.bib`)

- Generate the workshop schedules:

       for dir in $(ls data); do 
         [[ ! -d "auto/$dir" ]] && mkdir auto/$dir
         cat data/$dir/proceedings/order | ./scripts/order2schedule_workshop.pl $dir > auto/$dir/schedule.tex
       done
    
  This produces `schedule.tex` files which are imported into the handbook
  source using the LaTeX `\input` command.

- Generate the paper and poster session files:

       python2.7 ./scripts/order2schedule.py data/{demos,papers,NAACL-SRW16}/proceedings/order

- Generate the daily overviews:

       cat data/{demos,papers,tutorials}/proceedings/order | python2.7 ./scripts/order2schedule_overview.py
 
That's all of the auto-generated content. It produces LaTeX and BibTex files
that will be imported by the main handbook. This process does not always
produce valid LaTeX, so when you actually compile the handbook, these files
may be the source of errors, and you'll need to edit them by hand to fix
these. This may take several hours; you've been warned.

The remaining content is created manually, and lives in either the main
file, `handbook.tex`, or one of the many files imported from the `content`
directory and its subdirectories. 

- Edit `content/workshops/overview.tex` and
  `content/workshops/workshops.tex` to include these files and to be correct.

- Create the workshops bibtex entries in
  `content/workshops/papers.bib`. This is included in the main
  `handbook.tex` so that you can cite the workshop chairs and title automatically.

- Next, fill in the tutorials manually, editing
  `content/tutorials/tutorials-001.tex` and so on. Also edit the tutorial
  overview page in `content/tutorials/tutorials-overview.tex`.

- Edit other files in `content` as needed, including content in the `day1`,
  `day2`, `day3`, `fmatter`, and `sponsors` directory.

To build the handbook, run `make handbook`. It will actually build and 
rebuild the handbook multiple times to get the index right. A full handbook
build will take several minutes and produce a document nearly 200 pages
long. So it is easiest to do this incrementally, focusing on one section
at a time. This is easy to control from the `handbook.tex` by including
only certain sections. Producing and verifying the content from cover to
cover will take several days.

# Miscellaneous notes

- Email Dragomir Radev, who will run your index against
  [the ACL Anthology Network](http://clair.eecs.umich.edu/aan/index.php),
  correcting spellings and collapsing redundancies.

- Mononyms (e.g. Mausam) break LaTeX due to the way they are 
  formatted in the bibliography files produced by softconf. Grep
  for his name in these files and remove the unnecessary {}.
  
- Special characters in abstracts (e.g. alpha, funny latex, chinese, etc). 
  Really this should all be converted over to XeTeX.

# Appendix: Terminology

- The conference **proceedings** is the book containing all the
  conference's accepted papers and hosted in the
  [ACL anthology](http://aclweb.org/anthology). This is also sometimes
  called the **book**. Typically, separate books are produced for
  short and long papers, the student research workshop, and
  demonstrations. This is in contrast to the conference **handbook**,
  which is used to navigate the actual conference, and which this
  repository helps you to build.
  
- **ACLPUB** is the tool used to assemble the proceedings for a
  conference. It usually consists of a directory named
  `proceedings/`, within which are papers, paper metadata, files used to
  generate the proceedings PDF, and, most importantly for handbook,
  the `order` file, which specifies the conference schedule.
  
- **START** is the online system used to manage paper submission,
  reviewing, acceptance decisions, and camera-readies. It knows about ACLPUB
  and provides interfaces for editing the `order` file (directly or via the
  ScheduleMaker tool) and for generating the proceedings.tgz files.
  
- **Softconf** is the company that develops START

- **Subconferences**. Conferences hosted in START are assigned a top-level
  directory, e.g., `softconf.com/acl2014`. Beneath this are individual
  "subconferences" representing the workshops and also pieces of the
  the main conference. Main conference papers are typically hosted at
  `papers/`, short papers at `shortpapers`, and so on for "demos",
  "srw", "tutorials", and "tacl". Different sessions are
  self-contained and isolated and do not know about each other or have
  the ability to reference each other. The main conference spreads
  across multiple sessions, while workshops are typically contained in
  a single one.

# Credits

This document was written by Matt Post during assembly of the NAACL
2013 and ACL 2014 handbooks, and slightly revised by Adam Lopez in 
2016. Much of the code was inherited from Ulrich Germann in 2012.

