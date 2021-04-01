---
title: (정리) Data Analysis with R 
layout: post
---

### About this doc 

- This post address technique about datahandling in R with Hadley Wichham's packages. 

- cookbook

- see https://r4ds.had.co.nz/ 

---
### tidydata: tibble, readr 
---

***tibble()***

- prepare data. 
```r
> library(tidyverse)
> x<-c(0,2,3,5,1,4,1,4,2.5)
> y<-c(0,0,0,0,1,1,2,2,3)
> z<-c(5,4,-4,-5,4,-4,2,-2,0)
```

- make tibble with 3 columns. 
```r
> tibble(x=x,y=y,z=z)
```

***as_tibble()***

- prepare data. 
```r
> library(tidyverse)
> x<-c(0,2,3,5,1,4,1,4,2.5)
> y<-c(0,0,0,0,1,1,2,2,3)
> z<-c(5,4,-4,-5,4,-4,2,-2,0)
```

- make tibble. 
```r
> as_tibble(cbind(x,y,z))
```

***read_csv()***

- read csv file 
```r
> read_csv("1906_Solar`data_result_add.csv")
```

***write_csv()***

- to use *write_csv()* we make the input data tibble. 
```r
write_csv(as_tibble(W),"W.csv")
```

---
### Data Transformation 
---

***select()***

- prepare data 
```r
> A <- itb(10,5)
```

- the matrix A looks like: 
```r
> A
# A tibble: 10 x 5
        X1     X2     X3     X4      X5
     <dbl>  <dbl>  <dbl>  <dbl>   <dbl>
 1 -0.463  -1.08  -0.125  0.952 -1.58  
 2  1.38   -1.23  -0.129  0.396  1.42  
 3 -0.0462  2.19   0.604  1.51   0.0223
 4 -0.607  -1.65  -0.416 -0.360 -0.336 
 5  0.718   0.115 -0.980 -0.316  0.850 
 6  2.02    1.09   0.869  1.18  -0.795 
 7  0.952  -0.527 -1.31   0.612 -0.303 
 8 -0.307  -1.40  -0.199  0.953 -0.341 
 9  0.0403  0.612 -0.685 -0.858  1.14  
10  0.778   0.464 -1.53  -0.401  0.711 
```

- select first 3 variable and last variable
```r
> A %>% select(1:3,5)
> A %>% select(X1:X3,X5)
```

- it could be possible 
```r
> A %>% select(1:3,X5)
> A %>% select(X1:X3,5)
```

- select variable and save it B. 
```r
> A %>% select(1:3,5) -> B
> A %>% select(X1:X3,X5) -> B
```

***select(...,-c())***

- prepare data
```r
> A <- itb(10,5)
```

- select all columns except from X1 to X3. 
```r
> A %>% select(-(X1:X3))
> A %>% select(-(1:3))
> A %>% select(c(-1,-2,-3))
```

***select(...,start_with())***

- make tibble data using *itb()*. 
```r
> A <- itb(10,5,vname=c('XY1','XY2','XZ1','XZ2','X5'))
```

- select columns whose name starts with "XY". 
```r
> A %>% select(starts_with("XY"))
```

***select(...,end_with())***

- make tibble data using *itb()*. 
```r
> A <- itb(10,5,vname=c('XY1','XY2','XZ1','XZ2','X5'))
```

- select columns whose name ends with "2". 
```r
> A %>% select(ends_with("2"))
```

***select(...,contains())***

- make tibble data using *itb()*. 
```r
> A <- itb(10,5,vname=c('XY1','XY2','XZ1','XZ2','X5'))
```

- select columns whose name contains "Y". 
```r
> A %>% select(contains("Y"))
```


***select(...,everyting())***

- make tibble data using *itb()*. 
```r
> A <- itb(10,5,vname=c('XY1','XY2','XZ1','XZ2','X5'))
```

- pull the columns whose name contains "Z" to start of dataframe. 
```r
> A %>% select(contains("Z"),everything())
```

***rename()*** 

- make tibble data using *itb()*. 
```r
> A <- itb(10,5,vname=c('XY1','XY2','XZ1','XZ2','X5'))
```

- select "X5" and chage the variable name to "XZ3". 
```r
> A %>% rename(XZ3=X5)
```

***filter()***

- some useful logical operations with filter: *>=*, *<=*, *!=*, *!*, *&*, *|*, *%in%*. 

***filter(..., !is.na())***

- let me explain the missing value, *NA*. note that you can't check missing value by *x==NA*.
```r
# Let x be Mary's age. We don't know how old she is.
> x <- NA
# Let y be John's age. We don't know how old he is.
> y <- NA
# Are John and Mary the same age?
> x == y
[1] NA
# We don't know!```
```

- you should ckeck it by 
```r
> is.na(x)
#> [1] TRUE
```

- filtering the missing value by 
```r
> df <- tibble(x = c(1, NA, 3, 4, 5))
> filter(df, !is.na(x))
```

***mutate()***

- load *nycflights13* for *flights* data set.
```r
> library(nycflights13)
```

- make new variable named "gain".
```r
> flights %>%
  mutate(gain = dep_delay - arr_delay)
```

- (1) make new variable named "gain" and (2) remove the missing values in "gain" and (3) make another new varible named "gain_zscore" using "gain".
```r
> flights %>% 
  mutate(gain = dep_delay - arr_delay) %>%
  filter(!is.na(gain)) %>%
  mutate(gain_zscore = (gain-mean(gain)) / sd(gain))
```

- the following is same as the above. 
```r
> flights %>% 
  mutate(gain = dep_delay - arr_delay) %>%
  mutate(gain_zscore = (gain-mean(gain,na.rm=TRUE)) / sd(gain,na.rm=TRUE))
```

***group_by() %>% summarize()***

- load *nycflights13*. 
```r
> library(nycflights13)
```

- grouby by *dest* and applying some aggregate function like *n()*.
```r
> flights %>% 
  group_by(dest) %>%
  summarize(count=n())
```

- it is useful to include *na.rm=TRUE* in function like *mean()*, *sd()*, etc. 
```r
> flights %>% 
  group_by(year, month, day) %>% 
  summarize(delay = mean(dep_delay, na.rm = TRUE))
```

***pivot_longer()***

- break 2D-indexed data. to do this, (1) select some column-name (2) pivoting it and bring up new name (which can hug all selected variable) and save it *names_to* (3) *values_to*. 
```r
> subway2019 %>% pivot_longer(str_c(5:24),names_to='time',values_to='passenger') 
```

- note that 2D-indexed data deliberately omit (1) what each index means, that is, the name of each index (eg latitude longitude) (2) variable name mapped to index (eg earthquake intensity). 

***pivot_wider()*** 
- make 2D-indexed data. 


---
### stringr 
---

***str_c()***
- convert int to string 
```r
> str_c(1)
[1] "1"
```

- if you diliver multi input, *str_c()* combine letters. 
```r
> str_c("x",1,2) # number of input = 3 / dimension of input data = 1
[1] "x12"
```

- it is helpful to understanding above process as: 
\begin{align}
\begin{bmatrix} 
\mbox{"x"} & 1 & 2
\end{bmatrix} \Longrightarrow 
\mbox{"x12"}
\end{align}

- note that the function *str_c()* could be applied to col-vector as follwing: 
```r
> str_c(1:5) # number of input = 1 / dimension of input data = 5 
[1] "1"  "2"  "3"  "4"  "5" 
```

- it is 
\begin{align}
\begin{bmatrix} 
1 \\\\ \\
2 \\\\ \\
3 \\\\ \\
4 \\\\ \\
5
\end{bmatrix} \Longrightarrow 
\begin{bmatrix} 
\mbox{"1"} \\\\ \\
\mbox{"2"} \\\\ \\
\mbox{"3"} \\\\ \\
\mbox{"4"} \\\\ \\ 
\mbox{"5"} 
\end{bmatrix}
\end{align}

- note that in the case of *str_c("x",1,2)* we diliver 3 inputs with dimension 1 and in the case of  *str_c(1:5)* we diliver only 1 input with dimension 5. Thus in the case *str_c("x",1,2)* we toss row-vector such that 
\begin{align}
["x",1,2]
\end{align} 
and in the case of *str_c(1:5)* we toss the column vector such that 
\begin{align}
[1,2,3,4,5]^T
\end{align}

- the form like *str_c(col-vec,scalar,col-vec)* also possible, i.e., the following is also possible: 
```r
> str_c(1:5,'-',2:6)
[1] "1-2" "2-3" "3-4" "4-5" "5-6"
```

***str_replace_all()***

- find "(" in names of *dfdata* and convert it "."
```r
> names(dfdata) <- str_replace_all(names(dfdata),"[(]",".")
```

- find "(" in names of *dfdata* and remove it. 
```r
> names(dfdata) <- str_replace_all(names(dfdata),"[(]","")
```

- find "[" in names of *dfdata* and remove it. 
```r
> names(dfdata) <- str_replace_all(names(dfdata),"[\\[]","")
```

***str_sub()***
- get first 3 letters. 
```r
> str_sub("12345",1,3)
[1] "123"
```

- get from 2 to 5. 
```r
> str_sub("12345",2,4)
[1] "234"
```

- get last 2 letter. 
```r
> str_sub("12345",-2,-1)
[1] "45"
```

***mutate(... = str_c(X1,X2,X3))***

- make data set. 
```r
> year<-c("2020","2020","2020","2020","2020")
> date<-c("03-24","03-25","04-23","04-25","04-26")
> time<-c("15:00:00","15:02:00","16:00:00","16:00:02","16:00:03")
> ymd_data<-tibble(year=year,date=date,time=time)
```

- data looks like: 
```r
> ymd_data
# A tibble: 5 x 3
  year  date  time    
  <chr> <chr> <chr>   
1 2020  03-24 15:00:00   
2 2020  03-25 15:02:00   
3 2020  04-23 16:00:00   
4 2020  04-25 16:00:02
5 2020  04-26 16:00:03
```

- combind each colums named *ymdhms*. 
```r
> ymd_data %>% mutate(ymdhms=str_c(year,'/',date,'/',time))
# A tibble: 5 x 4
  year  date  time     ymdhms             
  <chr> <chr> <chr>    <chr>              
1 2020  03-24 15:00:00 2020/03-24/15:00:00
2 2020  03-25 15:02:00 2020/03-25/15:02:00
3 2020  04-23 16:00:00 2020/04-23/16:00:00
4 2020  04-25 16:00:02 2020/04-25/16:00:02
5 2020  04-26 16:00:03 2020/04-26/16:00:03
```

- (homework) how to develope *sprod()* in R. 

---
### forcats 
---

---
### lubridate
---

***ymd_hms()***

- suppose that we get data like: 
```r
> ymd_data
# A tibble: 5 x 1
  ymdhms             
  <chr>              
1 2020/03-24/15:00:00
2 2020/03-25/15:02:00
3 2020/04-23/16:00:00
4 2020/04-25/16:00:02
5 2020/04-26/16:00:03
```

- convert *chr* to *dttm* by *ymd_hms()*. 
```r
> ymd_data %>% mutate(ymdhms2=ymd_hms(ymdhms))
# A tibble: 5 x 2
  ymdhms              ymdhms2            
  <chr>               <dttm>             
1 2020/03-24/15:00:00 2020-03-24 15:00:00
2 2020/03-25/15:02:00 2020-03-25 15:02:00
3 2020/04-23/16:00:00 2020-04-23 16:00:00
4 2020/04-25/16:00:02 2020-04-25 16:00:02
5 2020/04-26/16:00:03 2020-04-26 16:00:03
```

- note that following are also possible: 
  - *ymd_hm()* : ymd_hm("2020/03-24/17:00")
  - *ydm_hms()*
  - *ydm_hm()*
  - *ydm_h()*
  - *mdy_hms()*
  - *mdy_hm()*
  - *mdy_h()*,
  - *dmy_hms()*
  - *dmy_hm()*
  - *dmy_h()*

---
### magrittr
---

---
### functions
---

---
### vector
---

---
### purrr
---

