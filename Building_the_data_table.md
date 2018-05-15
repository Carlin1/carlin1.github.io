Web Scraping Ideas
------------------

    opiateuse <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_prevalence_of_opiates_use")
    opiateuse2 <- html_nodes(opiateuse, css = "table")
    opiateusetable <- as.tibble(html_table(opiateuse2, header = TRUE, fill = TRUE)[[1]])
    opiateusetable

    ## # A tibble: 130 x 5
    ##     Rank `Country or Entity` `Annual prevalence (… Year  `Sources and not…
    ##    <int> <chr>                               <dbl> <chr> <chr>            
    ##  1     1 Afghanistan                         2.65  2009  [1]              
    ##  2     2 Ukraine                             1.64  2007  [1]              
    ##  3     3 United States                       1.60  2012  [4]              
    ##  4     4 Myanmar                             1.16  2006  [1]              
    ##  5     5 Russia                              1.13  2010  [1]              
    ##  6     6 Macau                               1.10  2003  [2]              
    ##  7     7 Thailand                            0.940 2009  [1]              
    ##  8     8 Seychelles                          0.910 2007  [1]              
    ##  9     9 Iran                                0.900 2012  [1]              
    ## 10    10 Luxembourg                          0.900 2000  [2]              
    ## # ... with 120 more rows

    cannabisuse <- read_html("https://en.wikipedia.org/wiki/Annual_cannabis_use_by_country")
    cannabisuse2 <- html_nodes(cannabisuse, css = "table")
    cannabisusetable <- as.tibble(html_table(cannabisuse2, header = TRUE, fill = TRUE)[[1]])
    cannabisusetable

    ## # A tibble: 164 x 4
    ##    `Country or entity` `Annual prevalence\n(percen…  Year `Sources, notes`
    ##    <chr>                                      <dbl> <int> <chr>           
    ##  1 Afghanistan                                 4.30  2010 [1]             
    ##  2 Albania                                     1.80  2006 [1]             
    ##  3 Algeria                                     5.70  2006 [1]             
    ##  4 American Samoa                              7.00  2007 [1]             
    ##  5 Andorra                                    14.6   2008 [1]             
    ##  6 Angola                                      2.10  1999 [2]             
    ##  7 Antigua and Barbuda                        10.6   2005 [1]             
    ##  8 Argentina                                   7.20  2006 [1]             
    ##  9 Armenia                                     3.50  2003 [1]             
    ## 10 Australia                                  10.6   2007 [1]             
    ## # ... with 154 more rows

    cocaineuse <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_prevalence_of_cocaine_use")
    cocaineuse2 <- html_nodes(cocaineuse, css = "table")
    cocaineusetable <- as.tibble(html_table(cocaineuse2, header = TRUE, fill = TRUE)[[1]])
    cocaineusetable

    ## # A tibble: 111 x 4
    ##    `Country or entity` `Annual prevalence (perce…  Year `Sources and note…
    ##    <chr>                                    <dbl> <int> <chr>             
    ##  1 England and Wales                         2.40  2013 (Age 16-59)[1]    
    ##  2 Spain                                     2.20  2013 (Age 15-64)[1]    
    ##  3 Scotland                                  2.20  2013 (Age 16-64)[1]    
    ##  4 United States                             2.10  2014 (Age 15-64)[1]    
    ##  5 Australia                                 2.10  2013 (Age 14+)[1]      
    ##  6 Uruguay                                   1.80  2014 (Age 15-65)[1]    
    ##  7 Brazil                                    1.75  2011 (Age 15-64)[1]    
    ##  8 Chile                                     1.73  2014 (Age 15-64)[1]    
    ##  9 Netherlands                               1.60  2014 (Age 15-64)[1]    
    ## 10 Ireland                                   1.50  2011 (Age 15-64)[1]    
    ## # ... with 101 more rows

    governmentsystem <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_system_of_government")
    governmentsystem2 <- html_nodes(governmentsystem, css = "table")
    governmentsystemtable <- as.tibble(html_table(governmentsystem2, header = TRUE, fill = TRUE)[[6]])
    governmentsystemtable

    ## # A tibble: 195 x 4
    ##    Name                `Constitutional … `Head of state` `Basis of execut…
    ##    <chr>               <chr>             <chr>           <chr>            
    ##  1 Afghanistan         Republic          Executive       Presidency is in…
    ##  2 Albania             Republic          Ceremonial      Ministry is subj…
    ##  3 Algeria             Republic          Executive       Presidency indep…
    ##  4 Andorra             Constitutional m… Ceremonial      Ministry is subj…
    ##  5 Angola              Republic          Executive       Presidency is in…
    ##  6 Antigua and Barbuda Constitutional m… Ceremonial      Ministry is subj…
    ##  7 Argentina           Republic          Executive       Presidency is in…
    ##  8 Armenia             Republic          Ceremonial      Ministry is subj…
    ##  9 Australia           Constitutional m… Ceremonial      Ministry is subj…
    ## 10 Austria             Republic          Ceremonial      Ministry is subj…
    ## # ... with 185 more rows

    governmentbudget <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_government_budget")
    governmentbudget2 <- html_nodes(governmentbudget, css = "table")
    governmentbudgettable <- as.tibble(html_table(governmentbudget2, header = TRUE, fill = TRUE)[[1]])
    governmentbudgettable

    ## # A tibble: 233 x 7
    ##    Rank  Country  Revenues  Expenditures `Surplus (or de… `Surplus percen…
    ##    <chr> <chr>    <chr>     <chr>        <chr>            <chr>           
    ##  1 1     United … 5,731,627 6,541,465    -809,838         -12.3%          
    ##  2 2     China    3,177,252 3,596,330    -419,075         -11.66%         
    ##  3 3     Japan    1,678,000 1,902,000    -224,000         -12.2%          
    ##  4 4     Germany  1,598,000 1,573,000    25,000           1.5%            
    ##  5 5     France   1,334,000 1,412,000    -78,000          -5.9%           
    ##  6 6     United … 984,300   1,076,000    -92,700          -9.2%           
    ##  7 7     Italy    884,500   927,800      -43,000          -5.3%           
    ##  8 8     Brazil   726,000   749,200      -23,000          -6.7%           
    ##  9 9     Canada   623,700   657,400      -34,000          -6.0%           
    ## 10 10    India    476,560   623,410      -146,850         -23.6%          
    ## # ... with 223 more rows, and 1 more variable: Year <chr>

    gdppercapita <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_GDP_(nominal)_per_capita")
    gdppercapita2 <- html_nodes(gdppercapita, css = "table")
    gdppercapitatable <- as.tibble(html_table(gdppercapita2, header = TRUE, fill = TRUE)[[5]])
    gdppercapitatable

    ## # A tibble: 217 x 3
    ##    Rank  Country        `US$`  
    ##    <chr> <chr>          <chr>  
    ##  1 1     Monaco         168,004
    ##  2 2     Liechtenstein  164,437
    ##  3 3     Luxembourg     101,835
    ##  4 —     Bermuda        99,363 
    ##  5 4     Switzerland    79,609 
    ##  6 —     Macau          73,187 
    ##  7 5     Norway         70,617 
    ##  8 6     Ireland        64,497 
    ##  9 —     Cayman Islands 63,261 
    ## 10 7     Iceland        60,966 
    ## # ... with 207 more rows

    pop <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_population_(United_Nations)")
    pop2 <- html_nodes(pop, css = "table")
    poptable <- as.tibble(html_table(pop2, header = TRUE, fill = TRUE)[[3]])
    poptable

    ## # A tibble: 234 x 7
    ##    Rank  `Country or area` `UN continental\nregio… `UN statistical\nregio…
    ##    <chr> <chr>             <chr>                   <chr>                  
    ##  1 —     World             —                       —                      
    ##  2 1     China[a]          Asia                    Eastern Asia           
    ##  3 2     India             Asia                    Southern Asia          
    ##  4 3     United States     Americas                Northern America       
    ##  5 4     Indonesia         Asia                    South-eastern Asia     
    ##  6 5     Brazil            Americas                South America          
    ##  7 6     Pakistan          Asia                    Southern Asia          
    ##  8 7     Nigeria           Africa                  Western Africa         
    ##  9 8     Bangladesh        Asia                    Southern Asia          
    ## 10 9     Russia            Europe                  Eastern Europe         
    ## # ... with 224 more rows, and 3 more variables: `Population\n(1 July
    ## #   2016)[3]` <chr>, `Population\n(1 July 2017)[3]` <chr>, Change <chr>

    # gdp <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_GDP_(nominal)")
    # gdp2 <- html_nodes(gdp, css = "table")
    # gdptable <- html_table(gdp2, header = TRUE, fill = TRUE)[[5]]
    # gdptable

    # intentionalhomocide <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_intentional_homicide_rate")
    # intentionalhomocide2 <- html_nodes(intentionalhomocide, css = "table")
    # intentionalhomocidetable <- html_table(intentionalhomocide2, header = TRUE, fill = TRUE)[[3]]
    # intentionalhomocidetable

    # prisonrate <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_incarceration_rate")
    # prisonrate2 <- html_nodes(prisonrate, css = "table")
    # prisonratetable <- html_table(prisonrate2, header = FALSE, fill = TRUE)[[1]]
    # prisonratetable

    mastertable <- gdppercapitatable%>%
      left_join(governmentbudgettable, by = "Country")%>%
      select("Country", "US$", "Revenues", "Expenditures", "Surplus (or deficit)", "Year")%>%
      left_join(governmentsystemtable, by = c("Country" = "Name"))%>%
      left_join(opiateusetable, by = c("Country" = "Country or Entity"))%>%
      left_join(cannabisusetable, by = c("Country" = "Country or entity"))%>%
      left_join(cocaineusetable, by = c("Country" = "Country or entity"))%>%
      select("Country", "Year.x", "US$", "Revenues", "Expenditures", "Surplus (or deficit)", "Constitutional form", "Head of state", "Annual prevalence (percent).x", "Annual prevalence\n(percent)","Annual prevalence (percent).y")%>%
      rename("Revenues(millions)" = "Revenues", "GDP per Capita" = "US$", "Expenditures(millions)" = "Expenditures", "Surplus/Deficit(millions)" = "Surplus (or deficit)","Year" = "Year.x", "Opiate Prevalence(percent)" = "Annual prevalence (percent).x", "Cannabis Prevalence(percent)" = "Annual prevalence\n(percent)", "Cocaine Prevalence(percent)" = "Annual prevalence (percent).y")

    mastertable

    ## # A tibble: 219 x 11
    ##    Country   Year    `GDP per Capita` `Revenues(millio… `Expenditures(mil…
    ##    <chr>     <chr>   <chr>            <chr>             <chr>             
    ##  1 Monaco    2011 e… 168,004          915               973               
    ##  2 Liechten… 2012 e… 164,437          995               890               
    ##  3 Luxembou… 2016 e… 101,835          25,850            25,520            
    ##  4 Bermuda   2016 e… 99,363           960               1,154             
    ##  5 Switzerl… 2016 e… 79,609           215,900           213,400           
    ##  6 Macau     2016 e… 73,187           12,120            7,004             
    ##  7 Norway    2016 e… 70,617           199,800           188,800           
    ##  8 Ireland   2016 e… 64,497           78,470            80,860            
    ##  9 Cayman I… 2016 e… 63,261           860               742               
    ## 10 Iceland   2016 e… 60,966           10,350            7,911             
    ## # ... with 209 more rows, and 6 more variables:
    ## #   `Surplus/Deficit(millions)` <chr>, `Constitutional form` <chr>, `Head
    ## #   of state` <chr>, `Opiate Prevalence(percent)` <dbl>, `Cannabis
    ## #   Prevalence(percent)` <dbl>, `Cocaine Prevalence(percent)` <dbl>
