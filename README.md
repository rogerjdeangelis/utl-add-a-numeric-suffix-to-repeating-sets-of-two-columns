# utl-add-a-numeric-suffix-to-repeating-sets-of-two-columns
Add a numeric suffix to repeating-sets-of-two-columns
    %let pgm = utl-add-a-numeric-suffix-to-repeating-sets-of-two-columns;

    Add a numeric suffix to repeating sets of two columns;

      Two Solutions
         1. SAS datastep
         2. WPS datastep (Altair/World Programming)

    StackOverflow
    https://tinyurl.com/ywtmzuat
    https://stackoverflow.com/questions/75884145/add-counter-of-values-for-only-1-record-in-sql-sas

    github
    https://tinyurl.com/yrmf9fpa
    https://github.com/rogerjdeangelis/utl-add-a-numeric-suffix-to-repeating-sets-of-two-columns

    many macros
    https://tinyurl.com/2w6aejec
    https://github.com/rogerjdeangelis/utl-macros-used-in-many-of-rogerjdeangelis-repositories

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    libname sd1 "d:/sd1";

    /*---- output to work and sd1 ----*/
    data have sd1.have;
        length var1-var7 $15.;
        input var1$ var2$ var3$ var4$ var5$ var6$ var7$ var8$ var9$ var10$ var11$;
    cards4;
    client goal State goal State goal State  goal State  goal State
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  Up to 40 obs from HAVE total obs=1 05APR2023:10:31:04                                                                 */
    /*                                                                                                                        */
    /*  Obs     VAR1     VAR2    VAR3     VAR4    VAR5     VAR6    VAR7     VAR8    VAR9     VAR10    VAR11                   */
    /*                                                                                                                        */
    /*   1     client    goal    State    goal    State    goal    State    goal    State    goal     State                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
     ___  __ _ ___   _ __  _ __ ___   ___ ___  ___ ___
    / __|/ _` / __| | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    \__ \ (_| \__ \ | |_) | | | (_) | (_|  __/\__ \__ \
    |___/\__,_|___/ | .__/|_|  \___/ \___\___||___/___/
                    |_|
    */

    data want;

      set have;

      array vrs[*] var:;

      inc = 1;
      do idx=1 to dim(vrs);
        if mod(idx,2) = 0 then do; inc=idx/2; vrs[idx] = catx('_',vrs[idx], inc); end;
        else                                  vrs[idx] = catx('_',vrs[idx], inc);
      end;

      drop inc idx;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* 40 obs from last table WORK.WANT total obs=1 05APR2023:10:32:38                                                        */
    /*                                                                                                                        */
    /*    VAR1       VAR2      VAR3       VAR4      VAR5       VAR6      VAR7       VAR8      VAR9      VAR10      VAR11      */
    /*                                                                                                                        */
    /*   client_1    goal_1    State_1    goal_2    State_2    goal_3    State_3    goal_4    State_4    goal_5    State_5    */
    /*                                                                                                                        */
    /*               =================    =================    =================    =================    =================   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*
    __      ___ __  ___   _ __  _ __ ___   ___ ___  ___ ___
    \ \ /\ / / `_ \/ __| | `_ \| `__/ _ \ / __/ _ \/ __/ __|
     \ V  V /| |_) \__ \ | |_) | | | (_) | (_|  __/\__ \__ \
      \_/\_/ | .__/|___/ | .__/|_|  \___/ \___\___||___/___/
             |_|         |_|
    */

    %utl_submit_wps64("

    libname sd1 'd:/sd1';

    data want;

      set sd1.have;

      array vrs[*] var:;

      inc = 1;
      do idx=1 to dim(vrs);
        if mod(idx,2) = 0 then do; inc=idx/2; vrs[idx] = catx('_',vrs[idx], inc); end;
        else                   vrs[idx] = catx('_',vrs[idx], inc);
      end;

      drop inc idx;
    run;quit;

    proc print;
    run;quit;

    ");

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* The WPS System                                                                                                         */
    /*                                                                                                                        */
    /*    VAR1       VAR2      VAR3       VAR4      VAR5       VAR6      VAR7       VAR8      VAR9      VAR10      VAR11      */
    /*                                                                                                                        */
    /*   client_1    goal_1    State_1    goal_2    State_2    goal_3    State_3    goal_4    State_4    goal_5    State_5    */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

     /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
