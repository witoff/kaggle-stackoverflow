Code submission for Kaggle Stack Overflow challenge

Initial development was based on [this](http://fastml.com/predicting-closed-questions-on-stack-overflow/)

And some of the code is derived from there. The data extraction (data2vw.py)
was rewritten from scratch, integrating the two scripts from the above post.

Another area I expanded was to automate the whole process using a Makefile, 
and additionally introducing cross-validation implemented entirely using
shell tools (GNU parallel was very useful).

I generated an expanded set of features, based on segmenting the documents
into code and non-code sections. The non-code section was further segmented
into sentences, and then into words (using NLTK). I also looked at some
metrics about the user, as well as some aspects of the sentence structure,
such as number of questions, exclamations etc.

Data can be downloaded kaggle from [here](https://www.kaggle.com/c/predict-closed-questions-on-stack-overflow/data) (recommend using chrome's copy as cURL to pull directly to processing machine)

### Example Data

Source CSV data looks like this:
```csv
PostId, PostCreationDate, OwnerUserId, OwnerCreationDate, ReputationAtPostCreation,
OwnerUndeletedAnswerCountAtPostTime, Title, BodyMarkdown, Tag1, Tag2, Tag3, Tag4, Tag5,
PostClosedDate, OpenStatus

4,07/31/2008 21:42:52,8,07/31/2008 21:33:24,1,0,Decimal vs Double?,"I'm new to C#, 
and I want to use a trackbar for the forms opacity This is my code....<FULL TEXT>",
c#,vb.net,timer,,,,open

<and 70 million more lines>
```

Which is then converted into the vowpal input format to look likes this:
```bash
4 1.0 4|xsnum digit:0 istart:0 textblock:2 url:0 lines:11 tags:1 question:1 period:2 
finalthanks:0 initcap:4 exclam:0 nonword:13 sent:4 codeblock:1 |yslen code:67 lasttext:222 
title:18 text:304 lastcode:67 firsttext:82 firstcode:67 |zsratio esent:0.0 ftext:0.269736842105 
qsent:0.25 psent:0.5 fcode:1.0 ftc:1.22388059701 tc:4.53731343284 |wsmean text:152.0 
code:67.0 sent:75.0 |user good_posts:0 age:568.0 reputation:1 userid:8 |titlewords double 
decimal vs |bodywords and control code is suggestions it vbnet doesnt im want in fine any 
trackbar use for when forms to build new type opacity then tried get implicitly convert 
but me not worked a c i double decimal work try this can error making the trans my |vtags c
```

Marco Lui <saffsd@gmail.com>, October-November 2012
