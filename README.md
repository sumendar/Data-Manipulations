```python
#creating of dataframe by using 4 vectors
fy <- c(2010,2011,2012,2010,2011,2012,2010,2011,2012)
company <- c("Apple","Apple","Apple","Google","Google",
"Google","Microsoft","Microsoft","Microsoft")
revenue <- c(65225,108249,156508,29321,37905,50175,62484,
69943,73723)
profit <- c(14013,25922,41733,8505,9737,10737,18760,23150,
16978)
companiesData <- data.frame(fy, company, revenue, profit)
```

```python
#head(companiesData)
str(companiesData)
```

```python
summary(companiesData)
```

```python
#convert fy into factor
companiesData$fy <- factor(companiesData$fy,ordered = TRUE)

```

```python
# adding  a column to an existing dataframe
companiesData$margin <- (companiesData$profit/companiesData$revenue)*100

```

```python
head(companiesData)
```

```python
str(companiesData)

```

```python
companiesData$margin <- round(companiesData$margin, 1)
```

```python
head(companiesData)
```

```python
#Delete perticular column
companiesData <-companiesData[,c(1:4)]
```

```python
head(companiesData)
```

**Syntax 2: R’s transform() function:**  
sum of two columns and store that into
a new column with transform(), you would use code such as:
**Syntax:**
dataFrame
<- transform(dataFrame, newColumn =  
oldColumn1 + oldColumn2)

```python
companiesData <- transform(companiesData, margin =
round((profit/revenue) * 100, 1))
```

```python
companiesData

```

```python
#data manipulate by using apply function
#apply(companiesData, 1, function(x) sum(x))
    
```

```python
apply(companiesData[,c('revenue', 'profit')], 1,
function(x) sum(x))
```

```python
companiesData$sums <- apply(companiesData[,
c('revenue', 'profit')], 1, function(x) sum(x))
```

```python
companiesData
```

```python
companiesData$margin <- apply(companiesData[,
c('revenue', 'profit')], 1,
function(x) { (x[2]/x[1]) * 100 } )
```

```python
companiesData

```

```python
highestMargin <- max(companiesData$margin)
highestMargin
```

```python
highestMargin <- companiesData[companiesData$margin == max(companiesData$margin),]
highestMargin
companiesData$margin == max(companiesData$margin)
```

```python
#?subset


highestMargin <- subset(companiesData,margin==max(margin))
#airquality
#subset(airquality, Temp > 80, select = c(Ozone, Temp))
```

```python
highestMargin
```

# Dplyr

**syntax:**
ddply(mydata, c('column name of a factor to group by',  
'column
name of the second factor to group by'), summarize  
OR transform, newcolumn =
myfunction(column name(s) I  
want the function to act upon))

```python
library("plyr")
companiesData
```

```python
highestProfitMargins <- ddply(companiesData,'company', summarize, bestMargin = max(margin))
highestProfitMargins
```

```python
highestProfitMargins <- ddply(companiesData,
'company', transform, bestMargin = max(margin))
```

```python
highestProfitMargins

```

```python
highestProfitMargins <- ddply(companiesData,
'company', function(x) x[x$margin==max(x$margin),])
```

```python
highestProfitMargins
companiesData


```

```python
companiesData[companiesData$margin==max(companiesData$margin),]
```

```python
highestProfitMargins <- ddply(companiesData,
'company', summarize, bestMargin = max(margin))
```

```python
highestProfitMargins
```

```python
#install.packages("dplyr",repos = "http://cran.us.r-project.org", type="source",dependencies=TRUE)
library("dplyr")
myresults <- companiesData %>%
group_by(company) %>%
mutate(highestMargin = max(margin), lowestMargin =
min(margin))
```

```python
myresults
```

```python
highestProfitMargins <- companiesData %>%
group_by(company) %>%
summarise(bestMargin = max(margin))
```

```python
highestProfitMargins
```

```python
vDates <- as.Date(c("2013-06-01", "2013-07-08",
"2013-09-01", "2013-09-15"))
```

```python
vDates
```

```python
vDates.bymonth <- cut(vDates, breaks = "month")
```

```python
vDates.bymonth
```

```python
dfDates <- data.frame(vDates, vDates.bymonth)
```

```python
#orddfDates
```

```python
#order functions

companyOrder <- order(companiesData$margin)
```

```python
companyOrder
```

```python
companiesOrdered <- companiesData[companyOrder,]
```

```python
companiesOrdered

```

```python
sort(companiesOrdered$margin)
```

# dplyr Package

1. filter – It filters the data based on a condition  
2. select – It is used to
select columns of interest from a data set  
3. arrange – It is used to arrange
data set values on ascending or descending order  
4. mutate – It is used to
create new variables from existing variables  
5. summarise (with group_by) – It
is used to perform analysis by commonly used operations such as min, max, mean
count etc

```python
library(dplyr)
```

```python
data("mtcars")
data('iris') 
```

```python
mydata <- mtcars
head(mydata)
```

```python
class(mydata)
```

```python
mynewdata <- tbl_df(mydata) # making the mtcars data  as local dataframe
myirisdata <- tbl_df(iris)  # making the iris data  as local dataframe
```

```python
#mynewdata
#myirisdata
```

```python
filter(mynewdata, cyl > 4 | gear < 2)  #use filter to filter data with required condition
```

```python
select(mynewdata, cyl,mpg,-hp)
#mtcars[,c(mtcars$cyl,mtcars$mpg)]
mtcars[,c(2,1)]
```

```python
select(mynewdata, cyl:gear)
```

```python
mynewdata %>% select(cyl, wt, gear) %>% filter(wt > 2)
```

```python
mynewdata %>% select(cyl, wt, gear) %>% arrange(wt,de) #arrange can be used to reorder rows
```

```python
mynewdata%>%select(cyl, wt, gear)%>%arrange(desc(wt)) #for descending
```

```python
mynewdata %>% select(mpg, cyl) %>% mutate(newvariable = mpg*cyl)
```

```python
df <- c(5,8,9,6,7,NA)

mean(df,na.rm=TRUE)
```

```python
myirisdata %>% group_by(Species) %>% summarise(Average = mean(Sepal.Length, na.rm = TRUE))
```

```python
myirisdata

```

```python
data("airquality")
mydata <- airquality
data(iris)
myiris <- iris
```

```python
install.packages("data.table",repos='http://cran.us.r-project.org')
```

```python
library(data.table)
```

```python
mydata <- data.table(mydata) 
mydata # in a form of data table 

myiris <- data.table(myiris) 
```

```python
mydata[2:4,]
airquality[2:4,]
```

```python
myiris[Species == 'setosa']
```

```python
subset(iris,iris$Species == 'setosa')
```

```python
myiris[Species %in% c('setosa', 'virginica')] 
```

```python
mydata[,Temp] # #select columns. Returns a vector
```

```python
airquality[,c("Wind","Temp")]
```

```python
mydata[,.(Temp,Month)]
```

```python
mydata[,sum(Ozone, na.rm = TRUE)]
```

```python
library(dplyr)
myiris[,{print(Sepal.Length) %>% plot(Sepal.Width)}]
```

```python
myiris[,.(sepalsum = sum(Sepal.Length)), by=Species] #grouping by a variable
```

```python
setkey(myiris, Species) #select a column for computation, hence need to set the key on column
```

```python
#selects all the rows associated with this data point
myiris['setosa']
#iris['setosa']
myiris[c('setosa', 'virginica')]
```

# reshape2 Package

```python
#create a data
ID <- c(1,2,3,4,5)
Names <- c('Joseph','Matrin','Joseph','James','Matrin')
DateofBirth <- c(1993,1992,1993,1994,1992)
Subject<- c('Maths','Biology','Science','Psycology','Physics')
```

```python
thisdata <- data.frame(ID, Names, DateofBirth, Subject)
```

```python
data.table(thisdata)
```

```python
library(reshape2)
```

```python
#melt
#?melt
mt <- melt(thisdata, id=(c('ID','Names')))
```

```python
thisdata
mt
```
