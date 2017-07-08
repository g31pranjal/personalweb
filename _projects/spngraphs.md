---
title : "Modelling of Natural language sentences using SPN Graphs"
enddate :      2016-11-25T16:00:00Z+0530
date : 2016-11-05T16:00:00Z+0530
author : in-arena
desc : A question answering system based on Natural Language Processing techniques
keyword : nlp, natural language processing, spn graphs, ai, artificial intelligence
layout : projectTemplate
---

*This was done as a term project for the partial fulfillment of course 'Artificial Intelligence'*

The project explores the use of new methodology called as **Stochastic Petri Nets(SPNs)** to model the understanding of Natural Language sentences. Using the technique of representation of NL sentences as SPN Graphs, we have been able to parse sentences and add to the knowledge base of a Questioning and Answering system. The parsed sentence is representation by means of data structures in Python and is stored is a list. The element of the list represents a single atomic sentence, which is parsed as **Noun Phrase (NP)** and a **Verb phrase (VP)** and then further classified into subclasses till we reach terminals, that is, the individual words of the sentence. Ultimately, each sentence is converted to a tuple of 2 elements : Noun Phrase (NP) and Verb Phrase (VP). 

The representation follows the scheme of - 

<img style="display: block; margin : auto" src="/assets/img/proj-ai-1.png">

where, **Agent** is the Noun Phrase which does the action, **Action** is the verb phrase which represents the action being done, and, **Patient** is the Noun phrase on which the action is being done. This constitutes the kernel of a sentence. We extract the kernel(Agent->Action->Patient) structure of the given sentence, and represent these using the SPN graphs, that will help us understanding the semantics and syntax of the sentences. 

We have used Stanford NLTK parser to get POS tagged structure of the sentence, which in turn will be used to generate a simple graph structure by extracting kernel. Once we have this kernel structure at our disposal we will be able to create Knowledge Base and represent it as SPN graphs from the simple graphs.This will be utilized to answer User queries from the constructed knowledge Base.

### # Creating basic SPN Graphs

To get the SPN structure, we make use of the syntactical structure of the sentence based on predefined english grammar. We take the main noun of the NP subtree and mark it out as the agent for the SPN graph. This Agent word might have some adjectives or prepositions associated with it. Also, there can be more than one possible Agent of the sentence, thus we generate separate SPN unit structures for each of them. Verb along with the Patient, forming the VP subtree, is taken and joined with the Agent to complete our kernel for a SPN unit structure. Likewise there can be more than one action (by the agent) (eg. "Ram is singing a song and eating lunch") and more than one patient (eg. "Hari likes donuts and cake"). Hence, or a given sentence we can have multiple possible SPN unit, formed by taking different permutation over multiple Agents, Actions and Patients. Each of the SPN unit will correspond to a different meaning that can be made out of a sentence.

<img style="display: block; margin : auto" src="/assets/img/proj-ai-2.png">

Due to the excess complexity of the compound sentences, we have limited our implementation to only kernels having simple to moderate structures which are discussed later.

We have worked with the following structures of sentences : 

<img style="display: block; margin : auto" src="/assets/img/proj-ai-4.png">

### # Knowledge base 

Multiple sentences comprises the entire knowledge base. Each triplet of a kernel **(agent->action->patient)** forms the unit structure. Hence, multiple units make the full graph.

example : <br>
**"Ram loves singing. Ram and Shyam are playing cricket. Cricket and football are getting popular"**

<img style="display: block; width : 60%; margin : auto" src="/assets/img/proj-ai-3.png">

The knowledge of the system gets enriched as more and more sentences are continuously add to the the system. This can then be used to query the system about any of the given facts. 

### # Question answering system
 
If the above system is queried about “cricket”, it would return all the facts that it knows about "cricket", which are : 
Ram -> playing -> cricket
cricket -> getting -> popular

The system can also be queried based on the action, like “singing”, “playing” etc. In this case the system returns all the sentences which has its agent or patient under the influence of the queried action.

### <i class="fa fa-github"></i>&nbsp;Github
<a href="https://github.com/g31pranjal/spn-graphs" target="_blank">https://github.com/g31pranjal/spn-graphs</a>

### # References 
- Modeling Natural Language Sentences into SPN Graphs
M. Mills, A. Psarologou and N. Bourbakis 
2013 IEEE 25th International Conference on Tools with Artificial Intelligence
	
- Natural language understanding for document and event association using Stochastic Petri Net modelling
M. Mills, M.S. Wright State University

- The Stanford Parser : A statistical parser
The Stanford Natural Language Processing Group
<a href="http://nlp.stanford.edu/software/lex-parser.shtml" target="_blank">http://nlp.stanford.edu/software/lex-parser.shtml</a>

- Natural Language Toolkit 3.0 Documentation<br>
	<a href="http://www.nltk.org/" target="_blank">http://www.nltk.org/</a>

