# utl-reorder-the-sas-program-vector-from-smallest-to-largest-column-median
Reorder the sas program vector from smallest to largest column median
    Reorder the sas program vector from smallest to largest column median                                                    
                                                                                                                             
    github                                                                                                                   
    https://tinyurl.com/ybykwbun                                                                                             
    https://github.com/rogerjdeangelis/utl-reorder-the-sas-program-vector-from-smallest-to-largest-column-median             
                                                                                                                             
                                                                                                                             
      Two Solutions                                                                                                          
          b. SAS                                                                                                             
          a. R                                                                                                               
             https://stackoverflow.com/users/3962914/ronak-shah                                                              
                                                                                                                             
    github                                                                                                                   
    https://tinyurl.com/ybq5xcse                                                                                             
    https://stackoverflow.com/questions/62100013/how-to-sort-a-dataframe-columns-by-the-median-of-all-its-columns            
                                                                                                                             
    * you need this macro;                                                                                                   
    %macro dosubl(arg);                                                                                                      
      %let rc=%qsysfunc(dosubl(&arg));                                                                                       
    %mend dosubl;                                                                                                            
                                                                                                                             
                                                                                                                             
    *_                   _                                                                                                   
    (_)_ __  _ __  _   _| |_                                                                                                 
    | | '_ \| '_ \| | | | __|                                                                                                
    | | | | | |_) | |_| | |_                                                                                                 
    |_|_| |_| .__/ \__,_|\__|                                                                                                
            |_|                                                                                                              
    ;                                                                                                                        
                                                                                                                             
    options validvarname=upcase;                                                                                             
    libname sd1 "d:/sd1";                                                                                                    
                                                                                                                             
    data sd1.have;                                                                                                           
                                                                                                                             
    v1=int(100*uniform(4321)); v2=int(100*uniform(4321)); v3=int(100*uniform(4321));output;                                  
    v1=int(100*uniform(4321)); v2=int(100*uniform(4321)); v3=int(100*uniform(4321));output;                                  
    v1=int(100*uniform(4321)); v2=int(100*uniform(4321)); v3=int(100*uniform(4321));output;                                  
                                                                                                                             
    run;quit;                                                                                                                
                                                                                                                             
    SD1.HAVE total obs=3                                                                                                     
                                                                                                                             
    Obs    V1    V2    V3                                                                                                    
                                                                                                                             
     1     22    75    64                                                                                                    
     2     86    24    24                                                                                                    
     3     21    43    15                                                                                                    
                                                                                                                             
    *           _                                                                                                            
     _ __ _   _| | ___  ___                                                                                                  
    | '__| | | | |/ _ \/ __|                                                                                                 
    | |  | |_| | |  __/\__ \                                                                                                 
    |_|   \__,_|_|\___||___/                                                                                                 
                                                                                                                             
    ;                                                                                                                        
                                                                                                                             
    1  Get the median of each column                                                                                         
                                                                                                                             
       Medians                                                                                                               
                                                                                                                             
         V1   V2  V3                                                                                                         
                                                                                                                             
         22   43  24   Move column 3 to column 2 position to get pdv in median order                                                                                                       
                                                                                                                             
    2. Reorder pdv from lowest to largest median                                                                             
                                                                                                                             
        V1   V3   V2  ** all we want to do is reorder the pdv;                                                               
                                                                                                                             
        22   64   75                                                                                                         
        86   24   24                                                                                                         
        21   15   43                                                                                                         
    *            _               _                                                                                           
      ___  _   _| |_ _ __  _   _| |_                                                                                         
     / _ \| | | | __| '_ \| | | | __|                                                                                        
    | (_) | |_| | |_| |_) | |_| | |_                                                                                         
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                        
                                                                                                                             
    ;                                                                                                                        
    WORK.WANT total obs=3                                                                                                    
                                                                                                                             
      V1    V3    V2                                                                                                         
                                                                                                                             
      22    64    75                                                                                                         
      86    24    24                                                                                                         
      21    15    43                                                                                                         
                                                                                                                             
    *          _       _   _                                                                                                 
     ___  ___ | |_   _| |_(_) ___  _ __  ___                                                                                 
    / __|/ _ \| | | | | __| |/ _ \| '_ \/ __|                                                                                
    \__ \ (_) | | |_| | |_| | (_) | | | \__ \                                                                                
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|___/                                                                                
     ___  __ _ ___  |_|                                                                                                      
    / __|/ _` / __|                                                                                                          
    \__ \ (_| \__ \                                                                                                          
    |___/\__,_|___/                                                                                                          
                                                                                                                             
    ;                                                                                                                        
    data want;                                                                                                               
                                                                                                                             
                                                                                                                             
      if _n_=0 then do;                                                                                                      
                                                                                                                             
         * get medians and sort by median hoding onto variable names;                                                        
         %dosubl('                                                                                                           
         proc sql;                                                                                                           
            select                                                                                                           
              pos into :_pos separated by " "                                                                                
            from                                                                                                             
             (                                                                                                               
              %do_over(vars,                                                                                                 
                 phrase=%str(                                                                                                
              select                                                                                                         
                 "?" as pos                                                                                                  
                 ,median(?) as mdn                                                                                           
              from                                                                                                           
                 sd1.have                                                                                                    
                  ),between=union corr)                                                                                      
             )                                                                                                               
             order                                                                                                           
                 by mdn                                                                                                      
           ;quit;                                                                                                            
          ');                                                                                                                
                                                                                                                             
      end;                                                                                                                   
                                                                                                                             
      * template for pdv v1 v3 v2;                                                                                           
      retain &_pos;                                                                                                          
                                                                                                                             
      set sd1.have;                                                                                                          
                                                                                                                             
    run;quit;                                                                                                                
                                                                                                                             
    *____                                                                                                                    
    |  _ \                                                                                                                   
    | |_) |                                                                                                                  
    |  _ <                                                                                                                   
    |_| \_\                                                                                                                  
                                                                                                                             
    ;                                                                                                                        
                                                                                                                             
    %utl_submit_r64('                                                                                                        
    library(haven);                                                                                                          
    library(SASxport);                                                                                                       
    have<-read_sas("d:/sd1/have.sas7bdat");                                                                                  
    want<-have[order(sapply(have, median))];                                                                                 
    write.xport(want,file="d:/xpt/want.xpt");                                                                                
    ');                                                                                                                      
                                                                                                                             
    libname xpt xport "d:/xpt/want.xpt";                                                                                     
    data want;                                                                                                               
      set xpt.want;                                                                                                          
    run;quit;                                                                                                                
    libname xpt clear;                                                                                                       
                                                                                                                             
                                                                                                                             
