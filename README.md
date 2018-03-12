-Steps to follow : 
  1. Unzip all three zips 
  2. Place journal_split folder under eclise-workspace folder 
  3. Include jars available in jars.zip  
  4. Change line no. 20 in split_and_conquer.java as the location where you will extract your tools.zip and place both pdftohtml.exe and
     convert.exe files. In my system it is : 
     
     bw.write("cd C:\\Users\\welcome\\Desktop"+"\n"); //location of pdftohtml.exe and convert.exe file
  
  5. Change the address in location string on line no. 16 in split_and_conquer.java to the location where you have kept   
     sample_input_file folder.
     
          String location = "C:\\Users\\welcome\\Desktop\\pdf"; //for testing
                      ---------change to------
          String location = "location/of/your/sample input files";
          
  6. Uncomment line 68 for getting images from pdf :
  
          c.executebatch(batchfile);
-----------------------------------------------------------------------------------------------------------------------------------
-Short Description : 

This java code basically used for extracting application number,journal number and page number from published Indian and International trademarks . The Office of Controller General of Patents ,Designs and Trademarks of India publishes trademarks in journals on weekly basis.Publication of a trademark application in the trademark journal provides the public a chance to raise a trademark opposition, if necessary. This code split the journals (which is in form of pdf file) containing trademark applications into seperate pdfs ; rename the pdf as per the format --> page-number_trademark-class_application-number_journal-number. Doing this will aid the data expert to easily index document in database like mysql or solr/elastic search platforms. It will also extract image using tools pdfimage.exe which will extract image in .ppm format and then converting the same in .jpg/.png format using convert tool.

------------------------------------------------------------------------------------------------------------------------------------
-Challenges Faced :

1. Trademark application  inside the journal may be of multipage (span to two or more pages). So splitting them in a way that the application containing multipage is splitted as a single pdf file is difficult. Also you will find some journals at the starting pages contain cover page and index which is of no use. For this two situation I have developed a concept of useless page. First I split all of the pages pdf file blindly without caring if the application inside it is a multipage or if it contains index. Then I have renamed all these pages either as per the format told above or as 'useless' if no regex of class number or application number is found and then merge the consecutive pages together in a manner that the first page is not a useless page and the other in a pair will be a useless page.In short merge all useless page to the page above them (to a 'not useless page') and then deleting the second.And then finally deleting the index pages from the starting if exists.

2. Writing regex for extracting application number is itself a challenging task as there are lot of different scenerios .
  
 I have provided sample_input_files.zip. You can also download more Journals from the following link : 
-http://www.ipindia.gov.in/journal-tm.htm
