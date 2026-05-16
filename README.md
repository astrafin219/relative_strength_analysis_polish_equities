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

| Date | WIG20 | WIG-BANKI | WIG-BUDOW | WIG-CHEMIA | WIG-ENERG | WIG-GORNIC | WIG-GRY | WIG-INFO | WIG-LEKI | WIG-MEDIA | WIG-MOTO | WIG-NRCHOM | WIG-ODZIEZ | WIG-PALIWA | WIG-SPOZYW | ALR | BHW | BNP | BOS | GTN | ING | MBK | MIL | PEO | PKO | SAN | EBP | UCG | ATR | BDX | CPR | DBE | DCR | DEK | ELT | ENI | EQU | ERB | FRO | HRS | INK | IZO | LBT | MCR | MDI | MFO | MRB | MSP | MSW | MSZ | NVA | PBX | PJP | PRM | PXM | RMK | RPC | SEL | SKA | TOR | TSG | ULM | UNI | ATT | PCE | PCR | PWX | CEZ | CLC | ECB | ENA | GVT | KGH | MLS | NVG | OND | PEN | PEP | PGE | TPE | ZEP | CLE | GRX | JSW | LWB | 11B | 3RG | ART | BBT | BCS | BLO | CDR | CIG | CRJ | DGE | GIF | GOP | HUG | MOV | PCF | PLW | RND | SIM | TEN | ULG | VVD | OML | ABS | ACP | ALL | ASE | ATD | BCM | CMP | DAT | DTR | FAB | GPP | IFI | NTT | OPM | PAS | SGN | SHO | SPR | SVRS | TLX | TXT | VRC | WAS | WPR | XPL | YAN | YRL | BIO | CLN | CRM | KRK | MAB | PHR | SVE | AGO | ASM | ATG | CPL | DIG | IMS | KCI | KPL | LRQ | MZA | PGM | PTW | WPL | ACG | APR | CAR | SNK | 1AT | AAT | ARH | BBD | CAV | CPD | CPI | DOM | DVL | ECH | EKP | GTC | INP | ITB | LKD | MLG | MUR | MVP | PHN | PLZ | RNK | WIK | WXF | 4MS | ARL | CDL | EAH | HRP | LBW | LPP | MDV | MIR | MON | PRT | SNW | VRG | WTN | MOL | PKN | UNT | AGT | AMB | AST | ATP | FHB | HEL | IMC | KSG | MAK | MBW | MLK | OTM | PPS | SEK | TAR | WWL |
|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|------|
| 1987-01-02 00:00:00 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 38.3855 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 | 0.0 |
| 2026-05-08 00:00:00 | 3535.94 | 21496.99 | 9501.83 | 8077.4 | 4454.68 | 10675.11 | 22415.72 | 9080.42 | 3035.54 | 6681.33 | 10765.13 | 6196.29 | 12124.32 | 16440.38 | 3304.04 | 123.5 | 115.8 | 146.6 | 10.2 | 0.498 | 391.0 | 1148.5 | 18.05 | 231.0 | 94.65 | 43.945 | 613.2 | 296.75 | 65.3 | 660.0 | 1.135 | 9.5 | 72.7 | 73.0 | 61.15 | 2.2 | 1.11 | 26.85 | 29.0 | 1.46 | 37.9 | 3.84 | 1.265 | 13.8 | 1.035 | 33.2 | 11.09 | 13.1 | 4.78 | 6.49 | 16.3 | 9.0 | 17.75 | 24.4 | 8.3 | 10.4 | 22.5 | 48.5 | 86.6 | 72.0 | 1.935 | 63.0 | 14.92 | 19.5 | 7.7 | 69.5 | 0.996 | 213.2 | 0.0 | 22.4 | 21.2 | 1.668 | 338.65 | 15.5 | 0.675 | 9.12 | 1.36 | 49.9 | 10.54 | 9.5 | 18.56 | 2.3 | 2.31 | 28.39 | 23.85 | 153.7 | 0.674 | 23.65 | 6.14 | 4.995 | 26.0 | 260.8 | 3.04 | 598.0 | 18.85 | 5.0 | 13.3 | 21.95 | 8.72 | 3.67 | 249.5 | 76.0 | 1.606 | 107.3 | 15.0 | 0.639 | 2.82 | 90.6 | 192.45 | 17.2 | 59.7 | 3.32 | 5.22 | 58.0 | 130.0 | 10.7 | 24.9 | 44.8 | 28.0 | 11.4 | 6.0 | 123.0 | 81.0 | 39.6 | 416.0 | 5.55 | 17.9 | 40.1 | 122.6 | 8.46 | 2.87 | 2.62 | 15.1 | 5.9 | 4.18 | 21.3 | 0.58 | 1048.0 | 7.58 | 3.44 | 3.18 | 8.36 | 0.241 | 4.21 | 4.8 | 199.8 | 2.0 | 0.946 | 19.9 | 2.0 | 9.05 | 2.05 | 136.0 | 58.4 | 21.7 | 22.6 | 769.0 | 21.6 | 61.0 | 1.645 | 53.6 | 5.4 | 13.6 | 1.68 | 0.0 | 260.0 | 10.54 | 4.85 | 1.645 | 2.63 | 7.6 | 1.945 | 23.4 | 99.4 | 41.0 | 11.35 | 9.58 | 1.548 | 3.9 | 7.7 | 2.44 | 4.2 | 30.2 | 8.25 | 32.9 | 5.42 | 9.115 | 20820.0 | 77.8 | 0.61 | 5.86 | 1.4 | 1.29 | 5.26 | 15.9 | 49.5 | 140.3 | 166.8 | 4.86 | 18.46 | 52.7 | 18.0 | 2.15 | 57.0 | 37.25 | 3.75 | 21.5 | 11.2 | 1.74 | 5.66 | 0.868 | 10.3 | 122.0 | 778.0 |

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


