# PAUP* BUG

Together with the 3 data files provided (1 matrix file and 2 trees) you can replicate the AgD1 treedist bug yourself in PAUP* v4.0b10 


execute REDstranderson.nex;
gettrees file=REDstranderson.nexorg.head.strict mode=3;
gettrees file=REDstranderson.nexorg.tail.strict mode=7;
treedist metric=agd1;

#symmdiff = 45
