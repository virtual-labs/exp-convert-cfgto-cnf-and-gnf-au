<u><h3>Theory</h3></u>
<p>A grammar is a set of production rules which are used to generate strings of a language.</p>
<p> We can converts context-free grammars to different normal forms.</p>
<li>Chomsky normal form (CNF)</li>
<li>Greibach normal form (GNF)</li>
<h6>Simplifying Context Free Grammars</h6>
<p>By simplifying CFGs we remove all the redundant productions from a grammar , while keeping the transformed grammar equivalent to the original grammar. Two grammars are called equivalent if they produce the same language. Simplifying CFGs is necessary to later convert them into Normal forms. 
</p>
<p>Types of redundant productions</p>
<li>Useless productions </li>
<li>Null productions</li>
<li>Unit production </li>
<h6>Useless productions</h6>
 The productions that can never take part in derivation of any string , are called useless productions. Similarly , a variable that can never take part in derivation of any string is called a useless variable. 
 <p>S -> abS | abA | abB</p>
<p>A -> cd</p>
<p>B -> aB</p>
<p>C -> dc</p>
<p>production ‘C -> dc’ is useless because the variable ‘C’ will never occur in derivation of any string. The other productions are written in such a way that variable ‘C’ can never reached from the starting variable ‘S’. </p>
<p>Production ‘B ->aB’ is also useless because there is no way it will ever terminate . If it never terminates , then it can never produce a string. Hence the production can never take part in any derivation. </p>
<p>To remove useless productions , we first find all the variables which will never lead to a terminal string such as variable ‘B’. We then remove all the productions in which variable ‘B’ occurs. 
So the modified grammar becomes – 
 

S -> abS | abA
A -> cd
C -> dc</p>
<p>Try to identify all the variables that can never be reached from the starting variable such as variable ‘C’. We then remove all the productions in which variable ‘C’ occurs. 
The grammar below is now free of useless productions – </p> 
<h6>Unit productions</h6>
<p> The productions of type ‘X -> Y’ are called unit productions. </P>
<li>Step 1 − To remove X->Y add production X->a to the grammar rule whenever Y->a occurs in the grammar.</li>
<li>Step 2 − Now delete X->Y from the grammar</li>
<li>Step 3 − Repeat Step 1 and 2 until all unit productions are removed</li>

<p>Example:</p>
<p>S->0A|1B|C

A->0S|00

B->1|A

C->01>
</p>
<p>step1:</p>
<p>S->C is unit production but while removing S->C we have to consider what C gives so we can add a rule to S.

   S->0A|1B|01</p>
   <p>Step 2:</p>
  <p>B->A is also unit production</p>

   <p>B->1|0S|00</p>
<p> we can write CFG without unit production as follows −

S->0A|1B|01

A->0S|00

B->1|0S|00

C->01</p>


<h6>Chomsky normal form (CNF)</h6>
<p>A context free grammar is in chomsky normal form if every rule is of the form </p>
<li>A ->BC</li>
<li>A ->a</li>
<p>where a is any terminal and A,B are any  non-terminals (variables) execpt that B and C may not be the start variable. in addition we permit the rule S->	ε,where S is the start variable</p>
<h6> Greibach  normal form (CNF)</h6>
<p>A Context Free Grammar (CFG) is said to be in Greibach Normal Form(GNF), if production rules satisfy one of the following criteria −</p>
<li>Only a start symbol can generate ε. For example, if S is the start symbol then S → ε is in GNF.</li>
<li>A non-terminal can generate a terminal. For example, if A is Non terminal and a is terminal then, A → a is in GNF.</li>
<li>A non-terminal can generate a terminal followed by any number of non-terminals. For Example, S → aAS is in GNF.
</li>
<h6>Steps for converting CFG into GNF</h6>
<li>Step 1 − Convert the grammar into CNF. If the given grammar is not in CNF, convert it into CNF.</li>

<li>Step 2 − If the grammar consists of left recursion, eliminate it. If the context free grammar contains any left recursion, eliminate it.</li>

<li>Step 3 − In the grammar, convert the given production rule into GNF form. If any production rule in the grammar is not in GNF form, convert it.</li