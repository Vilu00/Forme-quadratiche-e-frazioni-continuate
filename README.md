Python codes: 

"frompolynomialtocontinuedfractions"
Given the coefficients of a polynomials (A,B,C) such that Ax^2+Bx+C, 
returns the roots (alpha_1, alpha_2)  and the respective continued fractions,
namely alpha=[preperiod, \overline{period}], and the same for alpha'
it also gives the successive tails alpha_0=alpha, alpha_1 etc 
the same for alpha'. 

"fromcontinuedfractionstopoly"
Viceversa: 
Given a continued fractions, alpha=[preperiod, \overline{period}], (the inputs are exaclty preperiod, which could be empty, and period.
called gamma=[\overline{period}] , it returns the irrational quadratic equivalent of gamma, and its relative polynomial.
Also returns the irrational quadratic equivalent of alpha. 

In this File there are also functions that given period and preperiod return the convergents 
In particular from_convergentsnumb_to_continued_fraction(convergents), given a list of convergents (as numbers), reconstructs the continued fraction representation, 
while from_convergentsstring_to_continued_fraction(convergents) does the same, but starting from a string, so in particular it must be something of the type "1/2", "3/4", etc...
Viceversa 
"Construct_convergentnth_from_continued_fraction(preperiod, period, n)" constructs the n-th convergent of the continued fraction with given preperiod and period, 
while  "Construct_convergentslist_from_continued_fraction(preperiod, period,n)" constructs the first n-th convergents, so it gives n+1 numbers, since it includes the 0-th convergent.
