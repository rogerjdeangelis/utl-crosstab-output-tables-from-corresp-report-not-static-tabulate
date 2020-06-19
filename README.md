# utl-crosstab-output-tables-from-corresp-report-not-static-tabulate
Crosstab output tables frm corresp and report 
    Crosstab output tables frm corresp and report                                                                                    
                                                                                                                                     
      Two Solutions                                                                                                                  
                                                                                                                                     
        a. PROC REPORT you need to do this                                                                                           
           proc report data=have  noheader box formchar='|';                                                                         
           title "|date|flag_0|flag_1|tot";                                                                                          
           Noheader turns off the report colum header                                                                                
           We are replacing the _c#_ column headers with meaningfull names                                                           
                                                                                                                                     
        b. PROC CORRESP  (has options for count, sums, row and column percents)                                                      
           we use the weight option to avoid getting just counts                                                                     
                                                                                                                                     
    github                                                                                                                           
    https://tinyurl.com/y7dxgedy                                                                                                     
    https://github.com/rogerjdeangelis/utl-crosstab-output-tables-from-corresp-report-not-static-tabulate                            
                                                                                                                                     
    SOAPBOX ON                                                                                                                       
                                                                                                                                     
       I don't think tabulate is worth the trouble to learn, spend your time on report.                                              
       You can get painted into a corner with tabulate.                                                                              
       It is a shame that  report, freq crosstabs, and tabulate do not honor ods output.                                             
       But hey, we have four degraded editors: EE, EG, Studio and University edition.                                                
                                                                                                                                     
       One thing I really hate about the classic editor, is the inability to tutn off vertical scrollbar.                            
       Every time I look at it I get upset.                                                                                          
       If you do turn it off, you lose the mouse scroll wheel. I have talked to SAS out it but there                                 
       is not stomach for fixing the old classic editor.                                                                             
                                                                                                                                     
       I never use the vertical scrollbar because page down, page up, arrow down, arrow up and best of all just                      
       type a line number in the clean old classic editor command line, and of course find.                                          
                                                                                                                                     
       You can turn off the horizontal scroll bar, I use f1(left 3) and f2(right 3) to scroll,repeats when held down.                
       Also it would be nice if the row space consummed by the SAS icon could be colapsed into the 'file-edit-view-help bar.         
       I don't have any emojis on the top task bar.                                                                                  
                                                                                                                                     
    SOAPBOX OFF                                                                                                                      
                                                                                                                                     
                                                                                                                                     
    SAS Forum                                                                                                                        
    https://communities.sas.com/t5/SAS-Programming/summarize-data-and-sum/m-p/663451                                                 
                                                                                                                                     
    *_                   _                                                                                                           
    (_)_ __  _ __  _   _| |_                                                                                                         
    | | '_ \| '_ \| | | | __|                                                                                                        
    | | | | | |_) | |_| | |_                                                                                                         
    |_|_| |_| .__/ \__,_|\__|                                                                                                        
            |_|                                                                                                                      
    ;                                                                                                                                
                                                                                                                                     
    data have;                                                                                                                       
     input date $11. balance flag ;                                                                                                  
    cards4;                                                                                                                          
    01.04.2020 10 0                                                                                                                  
    01.04.2020 20 1                                                                                                                  
    02.04.2020 10 0                                                                                                                  
    02.04.2020 10 0                                                                                                                  
    02.04.2020 10 1                                                                                                                  
    ;;;;                                                                                                                             
    run;quit;                                                                                                                        
                                                                                                                                     
    WORK.HAVE total obs=5                                                                                                            
                                                                                                                                     
         DATE       BALANCE    FLAG                                                                                                  
                                                                                                                                     
      01.04.2020       10        0                                                                                                   
      01.04.2020       20        1                                                                                                   
      02.04.2020       10        0                                                                                                   
      02.04.2020       10        0                                                                                                   
      02.04.2020       10        1                                                                                                   
                                                                                                                                     
    *            _               _                                                                                                   
      ___  _   _| |_ _ __  _   _| |_                                                                                                 
     / _ \| | | | __| '_ \| | | | __|                                                                                                
    | (_) | |_| | |_| |_) | |_| | |_                                                                                                 
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                                
                    |_|        _                                                                                                     
     _ __ ___ _ __   ___  _ __| |_                                                                                                   
    | '__/ _ \ '_ \ / _ \| '__| __|                                                                                                  
    | | |  __/ |_) | (_) | |  | |_                                                                                                   
    |_|  \___| .__/ \___/|_|   \__|                                                                                                  
             |_|                                                                                                                     
                                                                                                                                     
    Up to 40 obs from WANT total obs=2                                                                                               
                                                                                                                                     
    Obs       DATE       FLAG_0    FLAG_1    TOT                                                                                     
                                                                                                                                     
     1     01.04.2020      10        20       30                                                                                     
     2     02.04.2020      20        10       30                                                                                     
                                                                                                                                     
      ___ ___  _ __ _ __ ___  ___ _ __                                                                                               
     / __/ _ \| '__| '__/ _ \/ __| '_ \                                                                                              
    | (_| (_) | |  | | |  __/\__ \ |_) |                                                                                             
     \___\___/|_|  |_|  \___||___/ .__/                                                                                              
                                 |_|                                                                                                 
                                                                                                                                     
    WORK.WANT total obs=3                                                                                                            
                                                                                                                                     
      LABEL         _0    _1    SUM                                                                                                  
                                                                                                                                     
      01.04.2020    10    20     30                                                                                                  
      02.04.2020    20    10     30                                                                                                  
                                                                                                                                     
      Sum           30    30     60                                                                                                  
                                                                                                                                     
    *          _       _   _                                                                                                         
     ___  ___ | |_   _| |_(_) ___  _ __  ___                                                                                         
    / __|/ _ \| | | | | __| |/ _ \| '_ \/ __|                                                                                        
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \                                                                                        
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/                                                                                        
     _ __ ___ _ __   ___  _ __| |_                                                                                                   
    | '__/ _ \ '_ \ / _ \| '__| __|                                                                                                  
    | | |  __/ |_) | (_) | |  | |_                                                                                                   
    |_|  \___| .__/ \___/|_|   \__|                                                                                                  
             |_|                                                                                                                     
                                                                                                                                     
    * don't worry aout the warnings - trying to prevent filelocks;                                                                   
                                                                                                                                     
    proc datasets lib=work nolist;                                                                                                   
      delete want;                                                                                                                   
    run;quit;                                                                                                                        
                                                                                                                                     
    %utl_odsrpt(setup);                                                                                                              
    proc report data=have nowd missing noheader box formchar='|';                                                                    
    title "|date|flag_0|flag_1|tot";                                                                                                 
    cols date flag  ,balance balance=bal;                                                                                            
    define date / group f=$quote15.;                                                                                                 
    define bal / sum;                                                                                                                
    define flag / across;                                                                                                            
    define balance / analysis sum;                                                                                                   
    run;quit;                                                                                                                        
    proc printto;                                                                                                                    
    run;quit;                                                                                                                        
    %utl_odsrpt(outdsn=want);                                                                                                        
                                                                                                                                     
      ___ ___  _ __ _ __ ___  ___ _ __                                                                                               
     / __/ _ \| '__| '__/ _ \/ __| '_ \                                                                                              
    | (_| (_) | |  | | |  __/\__ \ |_) |                                                                                             
     \___\___/|_|  |_|  \___||___/ .__/                                                                                              
                                 |_|                                                                                                 
                                                                                                                                     
    proc datasets lib=work nolist;                                                                                                   
      delete want;                                                                                                                   
    run;quit;                                                                                                                        
                                                                                                                                     
    ods exclude all;                                                                                                                 
    ods output observed=want;                                                                                                        
    proc corresp data=have observed dim=1;                                                                                           
    tables date, flag;                                                                                                               
    weight balance;                                                                                                                  
    run;quit;                                                                                                                        
    ods select all;                                                                                                                  
                                                                                                                                     
                                                                                                                                     
