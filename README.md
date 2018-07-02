# IRR and NPV Utility
Utility Apex Class for Salesforce to compute IRR and NPV

## Use
This class was designed to be flexible to several applications and has no dependencies.

There are 2 methods
### Calculate
Calculate will compute the IRR from a List of cashflows. If you know your IRR value is extreme you can seed a guess. The default guess is 10%. It is configured to compute to the nearest whole percenatage. See modificiations on how to change this.

### NPV
NPV will compute the Net Present Value from a List of cashflows provided a discount rate. The First entry is at t=0 and will not be discounted. **Note:** [Excel NPV function](https://support.office.com/en-us/article/npv-function-8672cb67-2576-4d07-b67b-ac28acf2a568) assumes first entry in t=1. Prepend 0 to the list in this utility to do match excel computations.

### Exmaple

```java
Decimal[] cashflows = new Decimal[]{-2000,500,500,500,500,500,500,500};
Decimal x_irr = IRR.calculate(cashflows);
system.debug('Internal Rate of Return is approximately :' + X_irr);

Decimal discRate = 0.10;
Decimal x_npv = IRR.NPV(cashflows, discRate);
system.debug('Net Present Value with a discount rate of ' + discRate + ' is:' + x_npv);
```

The above will output in the Debug Console
```
Internal Rate of Return is approximately :0.16`
Net Present Value with a discount rate of 0.10 is:434.2094088464654
```

## Modification
### Decimal Precision
This utility is configured to compute the IRR to the nearest whole percentage. It can easily be modified to compute IRR to additional decimal percision. It may have a performance cost. Simply change the amount the calculate method steps. For instance to compute IRR to the nearest tenth of a percent Change the following lines
```java
Decimal next = here + 0.01;
Decimal next = here - 0.01;
```
 to this
```java
Decimal next = here + 0.001;
Decimal next = here - 0.001;
```
You can fine tune this ffor your needs. For instance to improve performance you may opt to coonfigure to the nearest tenth of a percent, in 2/10ths increments.
Change the following lines
```java
Decimal next = here + 0.01;
Decimal next = here - 0.01;
```
 to this
```java
Decimal next = here + 0.002;
Decimal next = here - 0.002;
```


