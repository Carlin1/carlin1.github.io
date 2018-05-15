    opiateuse <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_prevalence_of_opiates_use")
    opiateuse2 <- html_nodes(opiateuse, css = "table")
    opiateusetable <- as.tibble(html_table(opiateuse2, header = TRUE, fill = TRUE)[[1]])

    cannabisuse <- read_html("https://en.wikipedia.org/wiki/Annual_cannabis_use_by_country")
    cannabisuse2 <- html_nodes(cannabisuse, css = "table")
    cannabisusetable <- as.tibble(html_table(cannabisuse2, header = TRUE, fill = TRUE)[[1]])

    cocaineuse <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_prevalence_of_cocaine_use")
    cocaineuse2 <- html_nodes(cocaineuse, css = "table")
    cocaineusetable <- as.tibble(html_table(cocaineuse2, header = TRUE, fill = TRUE)[[1]])

    governmentsystem <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_system_of_government")
    governmentsystem2 <- html_nodes(governmentsystem, css = "table")
    governmentsystemtable <- as.tibble(html_table(governmentsystem2, header = TRUE, fill = TRUE)[[6]])

    governmentbudget <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_government_budget")
    governmentbudget2 <- html_nodes(governmentbudget, css = "table")
    governmentbudgettable <- as.tibble(html_table(governmentbudget2, header = TRUE, fill = TRUE)[[1]])

    gdppercapita <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_GDP_(nominal)_per_capita")
    gdppercapita2 <- html_nodes(gdppercapita, css = "table")
    gdppercapitatable <- as.tibble(html_table(gdppercapita2, header = TRUE, fill = TRUE)[[5]])

    pop <- read_html("https://en.wikipedia.org/wiki/List_of_countries_by_population_(United_Nations)")
    pop2 <- html_nodes(pop, css = "table")
    poptable <- as.tibble(html_table(pop2, header = TRUE, fill = TRUE)[[3]])

    mastertable <- gdppercapitatable%>%
      left_join(governmentbudgettable, by = "Country")%>%
      left_join(poptable, by = c("Country" = "Country or area"))%>%
      select("Country", "Population\n(1 July 2017)[3]", "US$", "Revenues", "Expenditures", "Surplus (or deficit)", "Year")%>%
      left_join(governmentsystemtable, by = c("Country" = "Name"))%>%
      left_join(opiateusetable, by = c("Country" = "Country or Entity"))%>%
      left_join(cannabisusetable, by = c("Country" = "Country or entity"))%>%
      left_join(cocaineusetable, by = c("Country" = "Country or entity"))%>%
      select("Country", "Year.x", "Population\n(1 July 2017)[3]", "US$", "Revenues", "Expenditures", "Surplus (or deficit)", "Constitutional form", "Head of state", "Annual prevalence (percent).x", "Annual prevalence\n(percent)","Annual prevalence (percent).y")%>%
      rename("Population" = "Population\n(1 July 2017)[3]","Head_of_State" = "Head of state", "Constitutional_Form" = "Constitutional form", "Revenues" = "Revenues", "GDP_per_Capita" = "US$", "Expenditures" = "Expenditures", "Surplus_or_Deficit" = "Surplus (or deficit)","Year" = "Year.x", "Opiate_Prevalence" = "Annual prevalence (percent).x", "Cannabis_Prevalence" = "Annual prevalence\n(percent)", "Cocaine_Prevalence" = "Annual prevalence (percent).y")
    mastertable

    ## # A tibble: 219 x 12
    ##    Country      Year       Population GDP_per_Capita Revenues Expenditures
    ##    <chr>        <chr>      <chr>      <chr>          <chr>    <chr>       
    ##  1 Monaco       2011 est.… 38,695     168,004        915      973         
    ##  2 Liechtenste… 2012 est.… 37,922     164,437        995      890         
    ##  3 Luxembourg   2016 est.… 583,455    101,835        25,850   25,520      
    ##  4 Bermuda      2016 est.… 61,349     99,363         960      1,154       
    ##  5 Switzerland  2016 est.… 8,476,005  79,609         215,900  213,400     
    ##  6 Macau        2016 est.… 622,567    73,187         12,120   7,004       
    ##  7 Norway       2016 est.… <NA>       70,617         199,800  188,800     
    ##  8 Ireland      2016 est.… 4,761,657  64,497         78,470   80,860      
    ##  9 Cayman Isla… 2016 est.… 61,559     63,261         860      742         
    ## 10 Iceland      2016 est.… 335,025    60,966         10,350   7,911       
    ## # ... with 209 more rows, and 6 more variables: Surplus_or_Deficit <chr>,
    ## #   Constitutional_Form <chr>, Head_of_State <chr>,
    ## #   Opiate_Prevalence <dbl>, Cannabis_Prevalence <dbl>,
    ## #   Cocaine_Prevalence <dbl>

    groupedConstituation <- mastertable%>%
      group_by(Constitutional_Form)%>%
      summarize(average_GDPpC = mean(parse_number(GDP_per_Capita), na.rm=TRUE),
                average_Opiate = mean(parse_number(Opiate_Prevalence), na.rm=TRUE),
                average_Cannabis = mean(parse_number(Cannabis_Prevalence), na.rm=TRUE),
                average_Cocaine = mean(parse_number(Cocaine_Prevalence), na.rm=TRUE))

    groupedHead <- mastertable%>%
      group_by(Head_of_State)%>%
      summarize(average_GDPpC2 = mean(parse_number(GDP_per_Capita), na.rm=TRUE),
                average_Opiate2 = mean(parse_number(Opiate_Prevalence), na.rm=TRUE),
                average_Cannabis2 = mean(parse_number(Cannabis_Prevalence), na.rm=TRUE),
                average_Cocaine2 = mean(parse_number(Cocaine_Prevalence), na.rm=TRUE))



    groupedHead[c(1,2),]%>%
      ggplot()+
      geom_bar(stat = "identity", mapping = aes(x = Head_of_State, y = average_GDPpC2))

![](index_files/figure-markdown_strict/unnamed-chunk-3-1.png)

    groupedHead[c(1,2),]%>%
      ggplot()+
      geom_bar(stat = "identity", mapping = aes(x = Head_of_State, y = average_Opiate2))

![](index_files/figure-markdown_strict/unnamed-chunk-3-2.png)

    groupedHead[c(1,2),]%>%
      ggplot()+
      geom_bar(stat = "identity", mapping = aes(x = Head_of_State, y = average_Cannabis2))

![](index_files/figure-markdown_strict/unnamed-chunk-3-3.png)

    groupedHead[c(1,2),]%>%
      ggplot()+
      geom_bar(stat = "identity", mapping = aes(x = Head_of_State, y = average_Cocaine2))

![](index_files/figure-markdown_strict/unnamed-chunk-3-4.png)

    groupedConstituation[c(1,2,4),]%>%
      ggplot()+
      geom_bar(stat = "identity", mapping = aes(x = Constitutional_Form, y = average_GDPpC))

![](index_files/figure-markdown_strict/unnamed-chunk-3-5.png)

    groupedConstituation[c(1,2,4),]%>%
      ggplot()+
      geom_bar(stat = "identity", mapping = aes(x = Constitutional_Form, y = average_Opiate))

![](index_files/figure-markdown_strict/unnamed-chunk-3-6.png)

    groupedConstituation[c(1,2,4),]%>%
      ggplot()+
      geom_bar(stat = "identity", mapping = aes(x = Constitutional_Form, y = average_Cannabis))

![](index_files/figure-markdown_strict/unnamed-chunk-3-7.png)

    groupedConstituation[c(1,2,4),]%>%
      ggplot()+
      geom_bar(stat = "identity", mapping = aes(x = Constitutional_Form, y = average_Cocaine))

![](index_files/figure-markdown_strict/unnamed-chunk-3-8.png)

    mastertable%>%
      ggplot(mapping = aes(x = GDP_per_Capita))+
      geom_point(mapping = aes(y = Opiate_Prevalence))

    ## Warning: Removed 94 rows containing missing values (geom_point).

![](index_files/figure-markdown_strict/unnamed-chunk-3-9.png)

    mastertable%>%
      ggplot(mapping = aes(x = GDP_per_Capita))+
      geom_point(mapping = aes(y = Cannabis_Prevalence))

    ## Warning: Removed 68 rows containing missing values (geom_point).

![](index_files/figure-markdown_strict/unnamed-chunk-3-10.png)

    mastertable%>%
      ggplot(mapping = aes(x = GDP_per_Capita))+
      geom_point(mapping = aes(y = Cocaine_Prevalence))

    ## Warning: Removed 114 rows containing missing values (geom_point).

![](index_files/figure-markdown_strict/unnamed-chunk-3-11.png)
