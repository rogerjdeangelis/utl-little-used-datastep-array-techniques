# utl-little-used-datastep-array-techniques
Little used datastep array techniques 
    Little used datastep array techniques                               
                                                                        
    Dumb examples but perhaps they can be useful?                       
                                                                        
       1. Odd way to sum two arrays                                     
       2. Simplified test if value in an array   
       
    Nice additional functionality on end by                                               
                                                                                          
    Keintz, Mark                                                                          
    <mkeintz@WHARTON.UPENN.EDU>                                                           
                                                                                                                                                                            
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
                                                                        

    *                     _                                                               
     _ __ ___   __ _ _ __| | __                                                           
    | '_ ` _ \ / _` | '__| |/ /                                                           
    | | | | | | (_| | |  |   <                                                            
    |_| |_| |_|\__,_|_|  |_|\_\                                                           
                                                                                          
    ;                                                                                     
                                                                                          
                                                                                          
    Nice additional functionality on end by                                               
                                                                                          
    Keintz, Mark                                                                          
    <mkeintz@WHARTON.UPENN.EDU>                                                           
                                                                                          
                                                                                          
    Roger:                                                                                
                                                                                          
    I can't think of a good use case for the array summing technique you describe.        
    As long as you are summing whole  arrays, just use  "of"  for each array,             
    instead of using it once, but only after modifying one of  arrays.                    
                                                                                          
                                                                                          
    data _null_;                                                                          
      array one{3} (1,1,1);                                                               
      array two{3} (1,1,1);                                                               
      total=sum(of one{*},of two{*});                                                     
      put total=;                                                                         
    run;                                                                                  
                                                                                          
    And you can even efficaciously use this for summing parts of arrays.                  
    Say you want to sum elements of two arrays except for their respective last elements: 
                                                                                          
    total=sum(of one{*},of two{*},-one{dim(one)},-two{dim(two)});                         
                                                                                          
    It can save a whole lot of iteration.                                                 
                                                                                          
    regards,                                                                              
                                                                                          
