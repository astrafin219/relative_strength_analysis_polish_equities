# relative_strength_analysis_polish_equities

The project tackles top-down momentum of Warsaw Stock Exchange (GPW) equities. It specifically produces relative strength (RS) analysis by identifying outperforming Polish sector indices vs. WIG20 index and ranking the best-performing stocks within those indices using top-down momentum and relative strength comparison models.

The project uses **Python** and **SQLite**.

## How the Code Works

1.  The code downloads **data** for WIG20, sector indices and the components of the sector indices. Source: https://www.gpw.pl/.
2.  The code determines the winning sectors based on 3 metrics:

- how much the sector grew vs. how much WIG20 grew (should outperform the market and therefore be more than 1)
- on how many days did sector outperform WIG20 (should win more than 55% of days)
- downside capture for sectors - if a sector fell, whether if fell more or less than the market (should fall less during bad days).

3.  Within the winning sectors, the code computes the winning stocks based on the criteria mentioned above and ranks them.

## EDA (as of 2026-05-08)

SELECT name  
FROM sqlite_master  
WHERE type='table'  
ORDER BY name;

| name |
|------|
|firms|
|prices|

SELECT *
FROM (
SELECT *
FROM prices
ORDER BY Date ASC
LIMIT 1
)
UNION ALL
SELECT *
FROM (
SELECT *
FROM prices
ORDER BY Date DESC
LIMIT 1
);

*Shortened version:*

| Date | WIG20 | WIG-BANKI | WIG-BUDOW | WIG-CHEMIA | WIG-ENERG | WIG-GORNIC | WIG-GRY | WIG-INFO | WIG-LEKI | WIG-MEDIA | ... |
|------|------|-----------|-----------|-------------|-----------|-------------|---------|----------|----------|-----------|-----------|
| 1987-01-02 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | ... |
| 2026-05-08 | 3535.94 | 21496.99 | 9501.83 | 8077.4 | 4454.68 | 10675.11 | 22415.72 | 9080.42 | 3035.54 | 6681.33 | ... |

SELECT * FROM firms;

| name | sector |
|------|--------|
| alr | WIG-BANKI |
| bhw | WIG-BANKI |
| bnp | WIG-BANKI |
| bos | WIG-BANKI |
| gtn | WIG-BANKI |
| ing | WIG-BANKI |
| mbk | WIG-BANKI |
| mil | WIG-BANKI |
| peo | WIG-BANKI |
| pko | WIG-BANKI |
| san | WIG-BANKI |
| atr | WIG-BUDOW |
| bdx | WIG-BUDOW |
| cpr | WIG-BUDOW |
| dbe | WIG-BUDOW |
| dcr | WIG-BUDOW |
| dek | WIG-BUDOW |
| elt | WIG-BUDOW |
| eni | WIG-BUDOW |
| equ | WIG-BUDOW |
| erb | WIG-BUDOW |
| fro | WIG-BUDOW |
| hrs | WIG-BUDOW |
| ink | WIG-BUDOW |
| izo | WIG-BUDOW |
| lbt | WIG-BUDOW |
| mcr | WIG-BUDOW |
| mdi | WIG-BUDOW |
| mfo | WIG-BUDOW |
| mrb | WIG-BUDOW |
| msp | WIG-BUDOW |
| msw | WIG-BUDOW |
| msz | WIG-BUDOW |
| nva | WIG-BUDOW |
| pbx | WIG-BUDOW |
| pjp | WIG-BUDOW |
| prm | WIG-BUDOW |
| pxm | WIG-BUDOW |
| rmk | WIG-BUDOW |
| rpc | WIG-BUDOW |
| sel | WIG-BUDOW |
| ska | WIG-BUDOW |
| tor | WIG-BUDOW |
| tsg | WIG-BUDOW |
| ulm | WIG-BUDOW |
| uni | WIG-BUDOW |
| zue | WIG-BUDOW |
| cez | WIG-ENERG |
| clc | WIG-ENERG |
| ecb | WIG-ENERG |
| ena | WIG-ENERG |
| kgn | WIG-ENERG |
| mls | WIG-ENERG |
| nvg | WIG-ENERG |
| ond | WIG-ENERG |
| pen | WIG-ENERG |
| pep | WIG-ENERG |
| pge | WIG-ENERG |
| tpe | WIG-ENERG |
| zep | WIG-ENERG |
| att | WIG-CHEMIA |
| pcr | WIG-CHEMIA |
| pce | WIG-CHEMIA |
| pwx | WIG-CHEMIA |
| jsw | WIG-GORNIC |
| lwb | WIG-GORNIC |
| kgh | WIG-GORNIC |
| cle | WIG-GORNIC |
| grx | WIG-GORNIC |
| cdr | WIG-GRY |
| 11b | WIG-GRY |
| plw | WIG-GRY |
| huu | WIG-GRY |
| blo | WIG-GRY |
| 3rg | WIG-GRY |
| art | WIG-GRY |
| bbt | WIG-GRY |
| bcs | WIG-GRY |
| cig | WIG-GRY |
| crj | WIG-GRY |
| dge | WIG-GRY |
| gif | WIG-GRY |
| gop | WIG-GRY |
| hug | WIG-GRY |
| mov | WIG-GRY |
| pcf | WIG-GRY |
| rnd | WIG-GRY |
| sim | WIG-GRY |
| ten | WIG-GRY |
| ulg | WIG-GRY |
| vvd | WIG-GRY |
| acp | WIG-INFO |
| abs | WIG-INFO |
| all | WIG-INFO |
| ase | WIG-INFO |
| atd | WIG-INFO |
| bcm | WIG-INFO |
| cmp | WIG-INFO |
| dat | WIG-INFO |
| dtr | WIG-INFO |
| fab | WIG-INFO |
| gpp | WIG-INFO |
| ifi | WIG-INFO |
| lsi | WIG-INFO |
| ntt | WIG-INFO |
| opm | WIG-INFO |
| pas | WIG-INFO |
| sgn | WIG-INFO |
| sho | WIG-INFO |
| spr | WIG-INFO |
| svrs | WIG-INFO |
| tlx | WIG-INFO |
| txt | WIG-INFO |
| vrc | WIG-INFO |
| was | WIG-INFO |
| wpr | WIG-INFO |
| xpl | WIG-INFO |
| yan | WIG-INFO |
| yrl | WIG-INFO |
| bio | WIG-LEKI |
| mab | WIG-LEKI |
| cln | WIG-LEKI |
| crm | WIG-LEKI |
| krk | WIG-LEKI |
| phr | WIG-LEKI |
| sve | WIG-LEKI |
| asm | WIG-MEDIA |
| ago | WIG-MEDIA |
| atg | WIG-MEDIA |
| cpl | WIG-MEDIA |
| dig | WIG-MEDIA |
| ims | WIG-MEDIA |
| kci | WIG-MEDIA |
| kpl | WIG-MEDIA |
| lrq | WIG-MEDIA |
| mza | WIG-MEDIA |
| pgm | WIG-MEDIA |
| ptw | WIG-MEDIA |
| wpl | WIG-MEDIA |
| car | WIG-MOTO |
| acg | WIG-MOTO |
| apr | WIG-MOTO |
| snk | WIG-MOTO |
| 1at | WIG-NRCHOM |
| aat | WIG-NRCHOM |
| arh | WIG-NRCHOM |
| bbd | WIG-NRCHOM |
| cav | WIG-NRCHOM |
| cpd | WIG-NRCHOM |
| cpi | WIG-NRCHOM |
| dom | WIG-NRCHOM |
| dvl | WIG-NRCHOM |
| ech | WIG-NRCHOM |
| ekp | WIG-NRCHOM |
| gtc | WIG-NRCHOM |
| inp | WIG-NRCHOM |
| itb | WIG-NRCHOM |
| lkd | WIG-NRCHOM |
| mlg | WIG-NRCHOM |
| mur | WIG-NRCHOM |
| mvp | WIG-NRCHOM |
| phn | WIG-NRCHOM |
| plz | WIG-NRCHOM |
| rnk | WIG-NRCHOM |
| wik | WIG-NRCHOM |
| wxf | WIG-NRCHOM |
| 4ms | WIG-ODZIEZ |
| arl | WIG-ODZIEZ |
| lpp | WIG-ODZIEZ |
| ccc | WIG-ODZIEZ |
| cdl | WIG-ODZIEZ |
| eah | WIG-ODZIEZ |
| hrp | WIG-ODZIEZ |
| lbw | WIG-ODZIEZ |
| mir | WIG-ODZIEZ |
| mon | WIG-ODZIEZ |
| prt | WIG-ODZIEZ |
| snw | WIG-ODZIEZ |
| vrg | WIG-ODZIEZ |
| wtn | WIG-ODZIEZ |
| pkn | WIG-PALIWA |
| mol | WIG-PALIWA |
| unt | WIG-PALIWA |
| agt | WIG-SPOZYW |
| amb | WIG-SPOZYW |
| ast | WIG-SPOZYW |
| atp | WIG-SPOZYW |
| fhb | WIG-SPOZYW |
| hel | WIG-SPOZYW |
| imc | WIG-SPOZYW |
| ksg | WIG-SPOZYW |
| wwl | WIG-SPOZYW |
| mak | WIG-SPOZYW |
| mbw | WIG-SPOZYW |
| mlk | WIG-SPOZYW |
| otm | WIG-SPOZYW |
| pps | WIG-SPOZYW |
| sek | WIG-SPOZYW |


