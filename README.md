# utl_generating_a_non-normal_distribution_with_specified_skewness_and_kurtosis
Generating a non-normal distribution with specified skewness and kurtosis. Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverfl SAS community.
    Generating a non-normal distribution with specified skewness and kurtosis

    github
    https://tinyurl.com/y9qa6slj
    https://github.com/rogerjdeangelis/utl_generating_a_non-normal_distribution_with_specified_skewness_and_kurtosis

    see
    https://tinyurl.com/y7duvngv
    https://www.rdocumentation.org/packages/SimMultiCorrData/versions/0.1.0/topics/nonnormvar1

    Generate 10,000 observarions form a probability distribution with these cumulants(moments)

      MEAN       SD     SKEW KURTOSIS

         2        2        2        6

    INPUT
    =====

      MEAN       SD     SKEW KURTOSIS

         2        2        2        6

    PROCESS  (WPS proc R working code)
    ===================================

       * this generates standard cululants(moments);

       stcums <- calc_theory(Dist = "Exponential", params = 0.5) # rate = 1/mean;

       * this creates a polynomial and generates 10,000 realizations od a random variable;

       H_exp <- nonnormvar1("Polynomial", means = 2, vars = 2, skews = stcums[3],
                           skurts = stcums[4], fifths = stcums[5],
                           sixths = stcums[6], n = 10000, seed = 1234);

    OUTPUT
    ======


      Up to 40 obs from wantwps total obs=10,000

        Obs      WANT

          1    0.75398
          2    1.91082
          3    3.39320
        ...
       9998    0.71993
       9999    1.26072
      10000    1.12118

    * It has the correct Skewness and Kurtosis

    The UNIVARIATE Procedure

    Variable:  WANT

                                Moments

    N                       10000    Sum Weights              10000
    Mean               1.99990541    Sum Observations    19999.0541
    Std Deviation      1.41590728    Variance            2.00479344

    Skewness           2.03412151    Kurtosis            6.18436338

    Uncorrected SS     60042.1462    Corrected SS        20045.9296
    Coeff Variation    70.7987125    Std Error Mean      0.01415907


    *                _              _       _
     _ __ ___   __ _| | _____    __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \  / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/ | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|  \__,_|\__,_|\__\__,_|

    ;

     stcums <- calc_theory(Dist = "Exponential", params = 0.5) # rate = 1/mean;

     *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    %utl_submit_wps64('
    libname sd1 "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.2";
    libname wrk "%sysfunc(pathname(work))";
    libname hlp "C:\Program Files\SASHome\SASFoundation\9.4\core\sashelp";
    proc r;
    submit;
    source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
    library(SimMultiCorrData);
    stcums <- calc_theory(Dist = "Exponential", params = 0.5) # rate = 1/mean;
    stcums;
    H_exp <- nonnormvar1("Polynomial", means = 2, vars = 2, skews = stcums[3],
                        skurts = stcums[4], fifths = stcums[5],
                        sixths = stcums[6], n = 10000, seed = 1234);
    want<-H_exp$continuous_variable$V1;
    endsubmit;
    import r=want data=wrk.wantwps;
    run;quit;
    ');

    proc univariate data=wantwps;
    var want;
    run;quit;

