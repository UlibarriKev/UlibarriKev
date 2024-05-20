Measure % of # of VMI Orders = 

var _allorders = CALCULATE([Count VMI Orders]+[Count ZEDI Orders]+[Count ZF2E Orders])
RETURN
CALCULATE(DIVIDE([Count VMI Orders],_allorders))

Measure % of VMI Invoiced Sales =

CALCULATE(DIVIDE([Total VMI Invoiced Value],[Total Invoiced Value]))

Measure % Of VMI Order Value = 

CALCULATE(DIVIDE([Total VMI Order Value],[Total Order Value]))

Measure % of VMI Orders meeting FFA =

CALCULATE(DIVIDE([Count of VMI Orders Meeting FFA],[Count VMI Orders]))

Measure % of VMI Value = 

var _allorders1 =
CALCULATE([Total ZEDI Order Value]+[Total ZF2E Order Value]+[Total VMI Order Value])

RETURN
CALCULATE(DIVIDE([Total VMI Order Value],_allorders1))

Measure▲ Cumulative VMI Order v. Run Rate = 

[2024 Cumulative VMI Order Value]-[2024 Cumulative VMI Run Rate]

Measure 2024 Cumulative VMI Run Rate = 

VAR CumulativeTotal =

CALCULATE(SUM('KEY-DAX-Calendar'[2024 Average VMI Daily Run Rate]),
FILTER(ALLSELECTED('KEY-DAX-Calendar'[Date]),'KEY-DAX-Calendar'[Date] <= MAX('KEY-DAX-Calendar'[Date])),'KEY-DAX-Calendar'[Date]>=DATE(2024,1,1))
RETURN
IF(ISBLANK([Total VMI Order Value]),BLANK(),CumulativeTotal)

Measure Total 2023 Potential VMI Order Value = 

VAR ACTIVEVMIVALUE = CALCULATE(sum('FACT-Monthly SAP VA05'[Net value]),'KEY-Customer'[KEY-VMI.Status]="Active In VMI",'KEY-DAX-Calendar'[Year]="2023")

VAR INPROCESSVALUE = CALCULATE(SUM('FACT-Monthly SAP VA05'[Net value]),'KEY-Customer'[KEY-VMI.Status]="In Process",'KEY-DAX-Calendar'[Year]="2023")

RETURN

CALCULATE(ACTIVEVMIVALUE+INPROCESSVALUE)
