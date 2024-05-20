Sample DAX Measure to Return % Count Specific Orders


% of # of VMI Orders = 
var _allorders = CALCULATE([Count VMI Orders]+[Count ZEDI Orders]+[Count ZF2E Orders])
RETURN
CALCULATE(DIVIDE([Count VMI Orders],_allorders))
