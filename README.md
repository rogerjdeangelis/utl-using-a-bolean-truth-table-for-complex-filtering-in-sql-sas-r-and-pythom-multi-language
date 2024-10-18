# utl-using-a-bolean-truth-table-for-complex-filtering-in-sql-sas-r-and-pythom-multi-language
Using a bolean truth table for complex filtering in sql sas r and pythom 
    %let pgm=utl-using-a-bolean-truth-table-for-complex-filtering-in-sql-sas-r-and-pythom-multi-language;

    SQL is built for this kind of problem

    Using a bolean truth table for complex filtering in sql sas r and pythom

    github
    https://tinyurl.com/24xj52bs
    https://github.com/rogerjdeangelis/utl-using-a-bolean-truth-table-for-complex-filtering-in-sql-sas-r-and-pythom-multi-language

         SOLUTIONS
              1 sas sql
              2 r sql
              3 python sql
              4 r I sould not get the dplyr language to work

    VERBAL LOGIC  (from OP)

    2024-01-01 is ruled out because it has purple - and because it has 3 unique colors, so it's impossible that it can only be yellow and blue
    2024-03-27 is OK since it only has blue
    2024-05-15 is OK since it has blue AND yellow
    2024-06-08 is ruled out because it has orange (this is the situation I don't know how to do hence the ??????)


    2024-01-01 blue
    2024-01-01 purple
    2024-01-01 yellow
    2024-03-27 blue
    2024-05-15 blue
    2024-05-15 yellow
    2024-06-08 yellow
    2024-06-08 orange
    /*               _     _
     _ __  _ __ ___ | |__ | | ___ _ __ ___
    | `_ \| `__/ _ \| `_ \| |/ _ \ `_ ` _ \
    | |_) | | | (_) | |_) | |  __/ | | | | |
    | .__/|_|  \___/|_.__/|_|\___|_| |_| |_|
    |_|
    */

    /**************************************************************************************************************************/
    /*                           |                                                             |                              */
    /*                           |                                                             |                              */
    /*        INPUT              |                 PROCESS                                     |      OUTPUT                  */
    /*                           |  (SELF EXPLANATORY SQL - SAME CODE SAS, R and PYTHON)       |   (TRUE CASES)               */
    /*                           |                                                             |                              */
    /* SD1.HAVE total obs=24     |                                                             |                              */
    /*                           |  select                                                     |       DATES                  */
    /*     DATES       COLOR     |    dates                                                    |                              */
    /*                           |  from                                                       |     2024-02-01               */
    /*   2024-01-01    other     |     sd1.have                                                |     2024-04-01               */
    /*   2024-01-01    other     |  group                                                      |     2024-06-01               */
    /*   2024-02-01    yellow    |     by dates                                                |                              */
    /*   2024-02-01    yellow    |  having                                                     | You could join back if       */
    /*   2024-03-01    yellow    |     (max(color in ('blue','yellow'))=1) and                 | you want the original data   */
    /*   2024-03-01    yellow    |     (max(color not in ('blue','yellow'))=0)                 |                              */
    /*   2024-03-01    other     |                                                             |                              */
    /*   2024-03-01    other     |                                                             |                              */
    /*   2024-04-01    blue      |                                                             |                              */
    /*   2024-04-01    blue      |        TRUTH TABLE (ALL POSSIBLE CASES)                     |                              */
    /*   2024-05-01    blue      |                                                             |                              */
    /*   2024-05-01    blue      |  blue  yellow     other   truth     dates     case  State   |                              */
    /*   2024-05-01    other     |                                                             |                              */
    /*   2024-05-01    other     |    0      0       other     F     2024-01-01   001          |                              */
    /*   2024-06-01    blue      |    0   yellow       0       T     2024-02-01   010  True    |                              */
    /*   2024-06-01    blue      |    0   yellow     other     F     2024-03-01   011          |                              */
    /*   2024-06-01    yellow    |  blue     0         0       T     2024-04-01   100  True    |                              */
    /*   2024-06-01    yellow    |  blue     0       other     F     2024-05-01   101          |                              */
    /*   2024-07-01    blue      |  blue  yellow       0       T     2024-06-01   110  True    |                              */
    /*   2024-07-01    blue      |  blue  yellow     other     F     2024-07-01   111          |                              */
    /*   2024-07-01    yellow    |                                                             |                              */
    /*   2024-07-01    yellow    |  USAGE CASES                                                |                              */
    /*   2024-07-01    other     |                        CASES                                |                              */
    /*   2024-07-01    other     |  2024-01-01    other                                        |                              */
    /*                           |  2024-01-01    other   001                                  |                              */
    /*                           |                                                             |                              */
    /*                           |  2024-02-01    yellow                                       |                              */
    /*                           |  2024-02-01    yellow  010                                  |                              */
    /*                           |                                                             |                              */
    /*                           |  2024-03-01    yellow                                       |                              */
    /*                           |  2024-03-01    yellow                                       |                              */
    /*                           |  2024-03-01    other                                        |                              */
    /*                           |  2024-03-01    other   011                                  |                              */
    /*                           |                                                             |                              */
    /*                           |  2024-04-01    blue                                         |                              */
    /*                           |  2024-04-01    blue    100                                  |                              */
    /*                           |                                                             |                              */
    /*                           |  2024-05-01    blue                                         |                              */
    /*                           |  2024-05-01    blue                                         |                              */
    /*                           |  2024-05-01    other                                        |                              */
    /*                           |  2024-05-01    other   101                                  |                              */
    /*                           |                                                             |                              */
    /*                           |  2024-06-01    blue                                         |                              */
    /*                           |  2024-06-01    blue                                         |                              */
    /*                           |  2024-06-01    yellow                                       |                              */
    /*                           |  2024-06-01    yellow  110                                  |                              */
    /*                           |                                                             |                              */
    /*                           |  2024-07-01    blue                                         |                              */
    /*                           |  2024-07-01    blue                                         |                              */
    /*                           |  2024-07-01    yellow                                       |                              */
    /*                           |  2024-07-01    yellow                                       |                              */
    /*                           |  2024-07-01    other  110                                   |                              */
    /*                           |  2024-07-01    other                                        |                              */
    /*                           |                                                             |                              */
    /**************************************************************************************************************************/
    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */
    /* all possible cases each date repeated onece */
    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
     input  dates $10.color$;
    cards4;
    2024-01-01 other
    2024-01-01 other
    2024-02-01 yellow
    2024-02-01 yellow
    2024-03-01 yellow
    2024-03-01 yellow
    2024-03-01 other
    2024-03-01 other
    2024-04-01 blue
    2024-04-01 blue
    2024-05-01 blue
    2024-05-01 blue
    2024-05-01 other
    2024-05-01 other
    2024-06-01 blue
    2024-06-01 blue
    2024-06-01 yellow
    2024-06-01 yellow
    2024-07-01 blue
    2024-07-01 blue
    2024-07-01 yellow
    2024-07-01 yellow
    2024-07-01 other
    2024-07-01 other
    ;;;;
    run;quit;

    /*                             _
    / |  ___  __ _ ___   ___  __ _| |
    | | / __|/ _` / __| / __|/ _` | |
    | | \__ \ (_| \__ \ \__ \ (_| | |
    |_| |___/\__,_|___/ |___/\__, |_|
                                |_|
    */
    proc sql;
      create
         table want as
      select
        dates
      from
         sd1.have
      group
         by dates
      having
         (max(color in ('blue','yellow'))=1) and
         (max(color not in ('blue','yellow'))=0)
    ;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*     DATES                                                                                                              */
    /*                                                                                                                        */
    /*   2024-02-01                                                                                                           */
    /*   2024-04-01                                                                                                           */
    /*   2024-06-01                                                                                                           */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                     _
    |___ \   _ __   ___  __ _| |
      __) | | `__| / __|/ _` | |
     / __/  | |    \__ \ (_| | |
    |_____| |_|    |___/\__, |_|
                           |_|
    */

    %utl_rbeginx;
    parmcards4;
    library(sqldf)
    library(haven)
    source("c:/oto/fn_tosas9x.r")
    set.seed(1)
    have<-read_sas("d:/sd1/have.sas7bdat")
    have;
    want <- sqldf("
      select
        dates
      from
         have
      group
         by dates
      having
         (max(color in ('blue','yellow'))=1) and
         (max(color not in ('blue','yellow'))=0)
    ")
    want
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="rwant"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.rwant;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* R                SAS                                                                                                   */
    /*                                                                                                                        */
    /*  > want                                                                                                                */
    /*         DATES    ROWNAMES      DATES                                                                                   */
    /*                                                                                                                        */
    /*  1 2024-02-01        1       2024-02-01                                                                                */
    /*  2 2024-04-01        2       2024-04-01                                                                                */
    /*  3 2024-06-01        3       2024-06-01                                                                                */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____               _   _                             _
    |___ /   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
      |_ \  | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
     ___) | | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
    |____/  | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
            |_|    |___/                                |_|
    */

    proc datasets lib=sd1 nolist nodetails;
     delete pywant;
    run;quit;

    %utl_pybeginx;
    parmcards4;
    exec(open('c:/oto/fn_python.py').read());
    have,meta = ps.read_sas7bdat('d:/sd1/have.sas7bdat');
    want=pdsql("""
      select
        dates
      from
         have
      group
         by dates
      having
         (max(color in ('blue','yellow'))=1) and
         (max(color not in ('blue','yellow'))=0)
       """);
    print(want);
    fn_tosas9x(want,outlib='d:/sd1/',outdsn='pywant',timeest=3);
    ;;;;
    %utl_pyendx;

    proc print data=sd1.pywant;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* PYTHON                SAS                                                                                              */
    /*                                                                                                                        */
    /*        DATES          DATES                                                                                            */
    /*                                                                                                                        */
    /* 0 2024-02-01        2024-02-01                                                                                         */
    /* 1 2024-04-01        2024-04-01                                                                                         */
    /* 2 2024-06-01        2024-06-01                                                                                         */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*  _            _   _     _
    | || |    _ __  | |_(_) __| |_   ___   _____ _ __ ___  ___
    | || |_  | `__| | __| |/ _` | | | \ \ / / _ \ `__/ __|/ _ \
    |__   _| | |    | |_| | (_| | |_| |\ V /  __/ |  \__ \  __/
       |_|   |_|     \__|_|\__,_|\__, | \_/ \___|_|  |___/\___|
                                 |___/
    */

    %utl_rbeginx;
    parmcards4;
    library(tidyverse)
    library(haven)
    source("c:/oto/fn_tosas9x.r")
    set.seed(1)
    have<-read_sas("d:/sd1/have.sas7bdat")
    have;
    want <- have |>
      mutate(VAR1_MEAN = if_else(PK<= 3, cummean(VAR1), NA)) |>
      fill(VAR1_MEAN)
    want
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="rrwant"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.rrwant;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  R                         SAS                                                                                         */
    /*                                                        VAR1_                                                           */
    /*       PK  VAR1 VAR1_MEAN   ROWNAMES    PK    VAR1      MEAN                                                            */
    /*    <dbl> <dbl>     <dbl>                                                                                               */
    /*  1     1    87      87         1        1      87    87.0000                                                           */
    /*  2     2   104      95.5       2        2     104    95.5000                                                           */
    /*  3     3    83      91.3       3        3      83    91.3333                                                           */
    /*  4     4   132      91.3       4        4     132    91.3333                                                           */
    /*  5     5   107      91.3       5        5     107    91.3333                                                           */
    /*  6     6    84      91.3       6        6      84    91.3333                                                           */
    /*  7     7   110      91.3       7        7     110    91.3333                                                           */
    /*  8     8   115      91.3       8        8     115    91.3333                                                           */
    /*  9     9   112      91.3       9        9     112    91.3333                                                           */
    /* 10    10    94      91.3      10       10      94    91.3333                                                           */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */

