# utl-little-used-datastep-array-techniques
Little used datastep array techniques 
    Little used datastep array techniques                               
                                                                        
    Dumb examples but perhaps they can be useful?                       
                                                                        
       1. Odd way to sum two arrays                                     
       2. Simplified test if value in an array                          
                                                                        
                                                                        
    INPUT                                                               
    =====                                                               
                                                                        
    data have;                                                          
     input val $;                                                       
    cards4;                                                             
    1                                                                   
    2                                                                   
    3                                                                   
    ;;;;                                                                
    run;quit;                                                           
                                                                        
                                                                        
    PROCESS                                                             
    =======                                                             
                                                                        
    1. Odd way to sum two arrays                                        
                                                                        
       data _null_;                                                     
                                                                        
          array one [3]  (1,1,1);                                       
          array two [6]  (1,1,1);   * double the size of one;           
                                                                        
          * put one on the end of two                                   
              (could use addr, peek and poke if speed is important);    
                                                                        
          do i=4 to 6;                                                  
             two[i]=one[i-3];                                           
          end;                                                          
                                                                        
          top=sum(of two[*]);                                           
                                                                        
          put top=;                                                     
                                                                        
       run;quit;                                                        
                                                                        
       TOP=6                                                            
                                                                        
     2. Simplified test if value in an array                            
                                                                        
        Data _null_;                                                    
                                                                        
          array one [3]  (1,1,1);                                       
                                                                        
          set have;                                                     
                                                                        
          if val in one then put val= 'in array one    ';               
          else put val= 'not in array one ';                            
                                                                        
        run;quit;                                                       
                                                                        
        VAL=1 in array one                                              
        VAL=2 not in array one                                          
        VAL=3 not in array one                                          
                                                                        
