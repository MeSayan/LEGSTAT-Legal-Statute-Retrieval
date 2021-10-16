This folder contains the dataset of the AILA Track organized in FIRE 2020.

Track Website : https://sites.google.com/view/aila-2020
Conference Website : http://fire.irsi.res.in/fire/2020/home

======================================
Description of the folders :


=======================================
1. Folder Name : Object_statutes
=======================================
* No. of files : 197
* Description : Contains the title and description of 197 statutes, that are relevant to some of the given queries. 
*Format : 
a. Each file in the folder is named as S<id>.txt; the numbers in the file names are the identifiers of the statutes.   
b. Each file contains 2 lines. The first line is the title of the statute. The format is Title:<space><Titletext>
c. The second line is the description. The format is Desc:<space><Descriptiontext>
For example, the file name "S1.txt" contains the title and description of S1 statute.
The first line gives the title: "Title: Power of High Courts to issue certain writs"
The second line gives the description: "Desc: (1) Notwithstanding anything in Article 32 every High Court shall have powers, throughout the territories..."

=======================================
2. File Name : Query_doc_train.txt
=======================================
* Description : This file contains the 50 queries which are description of situations. Each query has an id such as AILA_Q1, AILA_Q2, ..., AILA_Q50.
* Format of each line: QueryId||<QueryText>
* These queries may be used as training & validation.


=======================================
3. File Name : Query_doc_test.txt
=======================================
* Description : This file contains the 10 queries which are description of situations. Each query has an id such as AILA_TQ1, AILA_Q2, ..., AILA_TQ10.
* Format of each line: QueryId||<QueryText>
* These are the test queries on which the methods will be evaluated.


===================================================
4.  File Name : relevance_judgments_train.txt
===================================================
* Description : contains the relevant statutes for a query in Query_doc_train.txt
* Format : <query-id> Q0 <document-id> <relevance>
where, query_id : query identifier. eg., AILA_Q1, AILA_Q2,...., AILA_Q50
document-id : the prior case document (S1,S2,...,S197)
Relevance : 1, if the statute is the correct answer to the query ; 0, otherwise
*Example :
AILA_Q1 Q0 S10 1 : for the queryid AILA_Q1, S10 is the correct statute
AILA_Q4 Q0 S184 0 : for the queryid AILA_Q4, S184 is the wrong statute

===================================================
Evaluation : The trec_eval tool (version 8.1) was usued for evaluation (downloaded from https://trec.nist.gov/trec_eval/)

* The tool requires 
1. trec_rel_file --> this is the "relevance judgement file" (i.e., relevance_judgments_priorcases.txt / relevance_judgments_statutes.txt depending on the task) 
2. trec_top_file --> documents retreived by a method/system 

* The format of the trec_top_file is:
<qid> <iter> <docno> <rank> <sim> <run_id>
where,
qid : query identifier. eg., AILA_Q1, AILA_Q2,...., AILA_Q50, AILA_TQ1, ...., AILA_TQ10
iter : ignored by trec_eval, could be anything, eg. "Q0" for all the queries
docno : the statute or prior case document
rank : document position in the ranking
sim : a similarity value returned by the algorithm based on which the documents are ranked
run_id : in case you are submitting multiple runs, use an alphanumeric name

* For a particular query, the documents should be ranked (in ascending order) according to the "sim".
For e.g., consider the query e.g. AILA_Q1 . The system has retrieved doc S12.txt with a sim value of 0.87 and doc S45.txt with a sim value of 0.76 then
AILA_Q1 Q0 S12 1 0.87 R1
AILA_Q1 Q0 S45 2 0.76 R1


* To run the evaluation, in the command file type the following command : trec_eval trec_rel_file trec_top_file 
The tool will output was the IR metrics for evaluation like MAP, P@5, P@10. etc.

*Examples :
AILA_Q1 Q0 S14 5 0.11026615969581749 R1
For the queryid AILA_Q1 , statute S14 has rank 5 with cosine similarity value of 0.11026615969581749 in runid R1.

AILA_Q2 Q0 C395 744 0.0308289159925753 R2
For the queryid AILA_Q2 , prior case C395 has rank 744 with cosine similarity value of 0.0308289159925753 in runid R2.

* A sample file is provided sample_trec_top_file.txt
Run : trec_eval relevance_judgements_train.txt sample_trec_top_file.txt


* Read More here :
1. https://www-nlpir.nist.gov/projects/trecvid/trecvid.tools/trec_eval_video/A.README
2. http://www.rafaelglater.com/en/post/learn-how-to-use-trec_eval-to-evaluate-your-information-retrieval-system

===================================================
Evaluation for the IR Term Project

* you should submit the trec_top_file.txt for the 10 test set queries
* The submissions will be evaluated and put up on the leader-board
https://docs.google.com/spreadsheets/d/11q64zTRICb35LGngYLaVatBRLsAFjWfdOH0rOt_kTwk/edit?usp=sharing
* The metrics will be MAP, bpref, recip_rank, P@10

* There will be 30% weightage for mid-sem presentation on October, 18
* There will be 70% weightage for end-sem presentation on November, 14
* in the presentation you should explain the different methods and also run the code for the best method.

--> you should try atleast 2 methods for mid-sem and atleast 3 extra methods for end-sem