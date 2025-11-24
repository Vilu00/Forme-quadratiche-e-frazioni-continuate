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
