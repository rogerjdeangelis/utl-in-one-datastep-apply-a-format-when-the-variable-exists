# utl-in-one-datastep-apply-a-format-when-the-variable-exists
    If variable sex exists apply the format $sex. otherwise do nothing.                                                      
                                                                                                                             
       Two Solution                                                                                                          
                                                                                                                             
          1.  Call symputx  (for numeric variable require non missing vlue on first ob )                                     
              a. when variable exists                                                                                        
              b. when variable does not exist (same code only diff input table)                                              
          2.  Open/Close SAS table                                                                                           
              a. when variable exists                                                                                        
              b. when variable does not exist (same code only diff input table)                                              
                                                                                                                             
     Since you decided on a use format then you know the varibale type.                                                      
                                                                                                                             
     This should work for a character variables even if it is missing on the first ob                                        
     because SAS will assume the value is numeric and use '.' instead of char missing ' '.                                   
                                                                                                                             
     When a numeric variable exits it must be non missing on the first observation.                                          
                                                                                                                             
    github                                                                                                                   
    https://tinyurl.com/yxar46zg                                                                                             
    https://github.com/rogerjdeangelis/utl-in-one-datastep-apply-a-format-when-the-variable-exists                           
                                                                                                                             
    SAS Forum                                                                                                                
    https://tinyurl.com/y4arfmob                                                                                             
    https://communities.sas.com/t5/SAS-Programming/Apply-the-user-defined-format-to-the-variable-within-the/m-p/550560       
                                                                                                                             
    *_                   _                                                                                                   
    (_)_ __  _ __  _   _| |_                                                                                                 
    | | '_ \| '_ \| | | | __|                                                                                                
    | | | | | |_) | |_| | |_                                                                                                 
    |_|_| |_| .__/ \__,_|\__|                                                                                                
            |_|                                                                                                              
    ;                                                                                                                        
                                                                                                                             
    %let varChk=SEX;                                                                                                         
    %let varFmt=$SEX;                                                                                                        
                                                                                                                             
    proc format;                                                                                                             
       value $sex                                                                                                            
         "F"="female"                                                                                                        
         "M"="Male"                                                                                                          
    ;run;quit;                                                                                                               
                                                                                                                             
    data havOne havTwo(drop=sex);                                                                                            
        set sashelp.class(obs=5 keep=name sex age);                                                                          
    run;quit;                                                                                                                
                                                                                                                             
    WORK.HAVONE total obs=5                                                                                                  
                                                                                                                             
    Obs     NAME      SEX    AGE                                                                                             
                                                                                                                             
     1     Alfred      M      14                                                                                             
     2     Alice       F      13                                                                                             
     3     Barbara     F      13                                                                                             
     4     Carol       F      14                                                                                             
     5     Henry       M      14                                                                                             
                                                                                                                             
                                                                                                                             
    WORK.HAVTWO total obs=5                                                                                                  
                                                                                                                             
    Obs     NAME      AGE                                                                                                    
                                                                                                                             
     1     Alfred      14                                                                                                    
     2     Alice       13                                                                                                    
     3     Barbara     13                                                                                                    
     4     Carol       14                                                                                                    
     5     Henry       14                                                                                                    
                                                                                                                             
    *            _               _                                                                                           
      ___  _   _| |_ _ __  _   _| |_                                                                                         
     / _ \| | | | __| '_ \| | | | __|                                                                                        
    | (_) | |_| | |_| |_) | |_| | |_                                                                                         
     \___/ \__,_|\__| .__/ \__,_|\__|                                                                                        
                    |_|                                                                                                      
    ;                                                                                                                        
                                                                                                                             
    * When SEX variAble exists;                                                                                              
                                                                                                                             
    WANT total obs=5                                                                                                         
                                                                                                                             
    Obs     NAME     SEX    AGE                                                                                              
                                                                                                                             
     1     Alfred   Male     14                                                                                              
     2     Alice    female   13                                                                                              
     3     Barbara  female   13                                                                                              
     4     Carol    female   14                                                                                              
     5     Henry    Male     14                                                                                              
                                                                                                                             
    #    Variable    Type    Len    Format                                                                                   
                                                                                                                             
    1    SEX         Char      6    $SEX.  =====> sex format added                                                           
    2    NAME        Char      8                                                                                             
    3    AGE         Num       8                                                                                             
                                                                                                                             
    * When SEX variAble DOES NOT exists;                                                                                     
                                                                                                                             
    WANT total obs=5                                                                                                         
                                                                                                                             
    Obs     NAME    AGE                                                                                                      
                                                                                                                             
     1     Alfred    14                                                                                                      
     2     Alice     13                                                                                                      
     3     Barbara   13                                                                                                      
     4     Carol     14                                                                                                      
     5     Henry     14                                                                                                      
                                                                                                                             
    *                                                                                                                        
     _ __  _ __ ___   ___ ___  ___ ___                                                                                       
    | '_ \| '__/ _ \ / __/ _ \/ __/ __|                                                                                      
    | |_) | | | (_) | (_|  __/\__ \__ \                                                                                      
    | .__/|_|  \___/ \___\___||___/___/                                                                                      
    |_|                                                                                                                      
    ;                                                                                                                        
                                                                                                                             
    =============================================================================                                            
    1.  Call symputx  (for numeric variable require non missing vlue on first ob )                                           
    ===============================================================================                                          
                                                                                                                             
    %let varChk=SEX;                                                                                                         
    %let varFmt=$SEX;                                                                                                        
                                                                                                                             
    proc format;                                                                                                             
       value $sex                                                                                                            
         "F"="female"                                                                                                        
         "M"="Male"                                                                                                          
    ;run;quit;                                                                                                               
                                                                                                                             
    data havOne havTwo(drop=sex);                                                                                            
        set sashelp.class(obs=5 keep=name sex age);                                                                          
    run;quit;                                                                                                                
                                                                                                                             
    **********************                                                                                                   
    * a SEX IS IN THE TABLE;                                                                                                 
    **********************                                                                                                   
                                                                                                                             
    %symdel varXis / nowarn;                                                                                                 
    data want ;                                                                                                              
      if _n_=0 then do; %let rc=%sysfunc(dosubl('                                                                            
          data _null_;                                                                                                       
             set havOne(obs=1);                                                                                              
             call symputx("varXis",&varchk);                                                                                 
          run;quit;                                                                                                          
          '));                                                                                                               
          %sysfunc(ifc(&varXis=.,,%str(format &varchk. &varFmt..;)));                                                        
      end;                                                                                                                   
                                                                                                                             
      set havOne;                                                                                                            
                                                                                                                             
    run;quit;                                                                                                                
                                                                                                                             
    **************************                                                                                               
    * b SEX IS NOT IN THE TABLE;                                                                                             
    **************************                                                                                               
                                                                                                                             
    %symdel varXis / nowarn;                                                                                                 
    data want ;                                                                                                              
      if _n_=0 then do; %let rc=%sysfunc(dosubl('                                                                            
          data _null_;                                                                                                       
             set havtWO(obs=1);                                                                                              
             call symputx("varXis",&varchk);                                                                                 
          run;quit;                                                                                                          
          '));                                                                                                               
          %sysfunc(ifc(&varXis=.,,%str(format &varchk. &varFmt..;)));                                                        
      end;                                                                                                                   
                                                                                                                             
      set havOne;                                                                                                            
                                                                                                                             
    run;quit;                                                                                                                
                                                                                                                             
                                                                                                                             
    =============================================================================                                            
    1.  Call symputx  (for numeric variable require non missing vlue on first ob )                                           
    ===============================================================================                                          
                                                                                                                             
    **********************                                                                                                   
    * a SEX IS IN THE TABLE;                                                                                                 
    **********************                                                                                                   
                                                                                                                             
    %let varChk=SEX;                                                                                                         
    %let varFmt=$SEX;                                                                                                        
                                                                                                                             
    %symdel varXis / nowarn;                                                                                                 
    data want ;                                                                                                              
      if _n_=0 then do; %let rc=%sysfunc(dosubl('                                                                            
         %let varXis=;                                                                                                       
         data _null_;                                                                                                        
           dsid=open("havOne");                                                                                              
             chk=varnum(dsid,"&varChk");                                                                                     
             if chk ne 0 then call symputx("varXis","format &varchk. &varFmt..");                                            
           dsid=close(dsid);                                                                                                 
           run;quit;                                                                                                         
         '));                                                                                                                
           &varXis;                                                                                                          
      end;                                                                                                                   
                                                                                                                             
      set havOne;                                                                                                            
                                                                                                                             
    run;quit;                                                                                                                
                                                                                                                             
                                                                                                                             
    **************************                                                                                               
    * b SEX IS NOT IN THE TABLE;                                                                                             
    **************************                                                                                               
                                                                                                                             
    %let varChk=SEX;                                                                                                         
    %let varFmt=$SEX;                                                                                                        
                                                                                                                             
    %symdel varXis / nowarn;                                                                                                 
    data want;                                                                                                               
      if _n_=0 then do; %let rc=%sysfunc(dosubl('                                                                            
         data _null_;                                                                                                        
           %let varXis=;                                                                                                     
           dsid=open("havTwo");                                                                                              
             chk=varnum(dsid,"&varChk");                                                                                     
             if chk ne 0 then call symputx("varXis","format &varchk. &varFmt..";                                             
           dsid=close(dsid);                                                                                                 
           run;quit;                                                                                                         
         '));                                                                                                                
         &varXis;                                                                                                            
      end;                                                                                                                   
                                                                                                                             
      set havTwo;                                                                                                            
                                                                                                                             
    run;quit;                                                                                                                
                                                                                                                             
