# SQL-data-cleaning-
## Upload dadta
Đây là file SQL dữ liệu đâu tiên của tôi
### First 10 row of data 
|full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|addie lush|40|married|alush0@shutterfly.com|254-389-8708|3226 Eastlawn Pass,Temple,Texas|Assistant Professor|7/31/2013|
|      ROCK CRADICK|46|married|rcradick1@newsvine.com|910-566-2007|4 Harbort Avenue,Fayetteville,North Carolina|Programmer III|5/27/2018|
|Sydel Sharvell|46|divorced|ssharvell2@amazon.co.jp|702-187-8715|4 School Place,Las Vegas,Nevada|Budget/Accounting Analyst I|10/6/2017|
|Constantin de la cruz|35||co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|  Gaylor Redhole|38|married|gredhole4@japanpost.jp|917-394-6001|88 Cherokee Pass,New York City,New York|Legal Assistant|5/29/2019|
|Wanda del mar       |44|single|wkunzel5@slideshare.net|937-467-6942|10864 Buhler Plaza,Hamilton,Ohio|Human Resources Assistant IV|3/24/2015|
|Joann Kenealy|41|married|jkenealy6@bloomberg.com|513-726-9885|733 Hagan Parkway,Cincinnati,Ohio|Accountant IV|4/17/2013|
|   Joete Cudiff|51|divorced|jcudiff7@ycombinator.com|616-617-0965|975 Dwight Plaza,Grand Rapids,Michigan|Research Nurse|11/16/2014|
|mendie alexandrescu|46|single|malexandrescu8@state.gov|504-918-4753|34 Delladonna Terrace,New Orleans,Louisiana|Systems Administrator III|3/12/1921|
| fey kloss|52|married|fkloss9@godaddy.com|808-177-0318|8976 Jackson Park,Honolulu,Hawaii|Chemical Engineer|11/5/2014|
### Creating a new table for cleaning 
#### Let's generate a new table where we can manipulate and restructure the data without modifying the origanal dataset
```
CREATE TABLE club_member_info_cleaned (
	full_name VARCHAR(50),
	age INTEGER,
	martial_status VARCHAR(50),
	email VARCHAR(50),
	phone VARCHAR(50),
	full_address VARCHAR(50),
	job_title VARCHAR(50),
	membership_date VARCHAR(50)
);
```
### Copy all value from original table 
```
INSERT INTO club_member_info_cleaned
Select * FROM club_member_info;
```
### Cleaning age that out of range from 0 to 100
#### Find averange age = 44.85 with outlier  using SQL

```SELECT AVG(AGE) FROM club_member_info_cleaned```

#### Find averange age by Power BI without outlier  and blank value
##### Divorced  
![Age by status](https://github.com/khanhnl2001/SQL-data-cleaning-/blob/main/Image/Divorced%20by%20age.png)
##### Married 
![Age by status](https://github.com/khanhnl2001/SQL-data-cleaning-/blob/main/Image/Married%20by%20age.png)
##### Single 
![Age by status](https://github.com/khanhnl2001/SQL-data-cleaning-/blob/main/Image/Single%20by%20age.png)

#### Update all blank age and outlifter age in SQL to averange age of 44

```
UPDATE club_member_info_cleaned
SET age = 44
WHERE age>100 OR age ISNULL
```

#### Remove Leading and trailing whitespaces

```
UPDATE club_member_info_cleaned
SET full_name = TRIM(full_name)
```

#### Inconsistent letter case
##### Set name upper case first letter and lower case the rest 
```
UPDATE club_member_info_cleaned
SET full_name = UPPER(SUBSTR(full_name, 1, 1)) || SUBSTR(full_name, 2);
```
##### Fill missing martial_status value
|full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|Constantin de la cruz|35||co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|Nixie january|44||njanuaryp@youtu.be|415-318-7190|65 Stephen Circle,San Francisco,California|Chemical Engineer|7/29/2017|
|Danila teague|42||dteague39@nydailynews.com|610-889-3130|9 Sugar Way,Philadelphia,Pennsylvania|Administrative Assistant III|8/29/2021|
|Tyrone shillum|25||tshillum57@sina.com.cn|502-336-9009|698 Sundown Circle,Frankfort,Kentucky|Structural Engineer|4/10/2018|
|Prentiss epton|42||pepton59@oracle.com|303-233-8382|58217 Holmberg Avenue,Boulder,Colorado|Professor|6/21/2014|
|Deny grainger|55||dgrainger7g@skyrock.com|650-380-1663|5 Corry Hill,Los Angeles,California|Budget/Accounting Analyst IV|3/29/2016|
|Niccolo crosser|46||ncrosserjv@imgur.com|954-707-4900|0155 Kensington Avenue,Hollywood,Florida|Technical Writer|11/11/2015|
|Dusty baccus|48||dbaccus8j@elegantthemes.com|763-502-9649|5893 Milwaukee Plaza,Loretto,Minnesota|Computer Systems Analyst II|9/30/2017|
|Marjy rain|27||mrain9b@feedburner.com|713-699-1324|568 Oneill Way,Houston,Texas|Analyst Programmer|2/14/2022|
|Nobie boldero|51||nbolderobx@blinklist.com|915-591-9005|34 Vera Plaza,San Juan, Puerto Rico|Account Coordinator|7/14/2021|
|Hilary von helmholtz|22||hvone2@symantec.com|601-743-4686|220 Waubesa Lane,Jackson,Mississippi|VP Marketing|2/19/2019|
|Sunshine dunbleton|63||sdunbletonee@yellowpages.com|704-231-0109|79497 Milwaukee Point,Charlotte,North Carolina||2/10/2018|
|Roxanne yvon|46||ryvong5@phoca.cz|518-419-0786|127 Mockingbird Road,Albany,New York|Environmental Specialist|1/31/2017|
|Bunny axon|51||baxonij@microsoft.com|281-943-2013|769 Annamark Parkway,Houston,Texas|Account Representative II|6/18/2018|
|Laure frier|62||lfrierkx@europa.eu|719-900-0790|1 Vahlen Street,Pueblo,Colorado|Actuary|3/18/2016|
|Gerry gonnel|23||ggonnellm@ftc.gov|203-181-0550|6 Elka Parkway,Waterbury,Connecticut|Senior Cost Accountant|9/29/2018|
|Junina held|22||jheldnx@va.gov|315-201-6127|043 Forest Dale Way,Syracuse,New York|Librarian|8/4/2021|
|Callean corradini|19||ccorradiniox@microsoft.com|941-391-8386|97 Dapin Avenue,Sarasota,Florida|Staff Scientist|4/29/2021|
|Conroy hartil|47||chartilpx@loc.gov|828-639-3011|298 Oak Valley Avenue,Asheville,North Carolina|Pharmacist|3/30/2021|
|Alfreda roches|40||arochesrd@tumblr.com|770-444-9152|83 Clove Plaza,Alpharetta,Georgia|Human Resources Manager|5/26/2021|

Because married people and single people have much larger amount in group and there only a few missing value. So we fill single for age <30 and married > 35
```
Update club_member_info_cleaned 
Set martial_status = CASE 
		When martial_status ='' and age < 30 then 'single' 
		When martial_status ='' and age >= 35 then 'married' 
		Else martial_status
End;
```

### Result First 10 row of clean data
|full_name|age|martial_status|email|phone|full_address|job_title|membership_date|
|---------|---|--------------|-----|-----|------------|---------|---------------|
|Addie lush|40|married|alush0@shutterfly.com|254-389-8708|3226 Eastlawn Pass,Temple,Texas|Assistant Professor|7/31/2013|
|Rock cradick|46|married|rcradick1@newsvine.com|910-566-2007|4 Harbort Avenue,Fayetteville,North Carolina|Programmer III|5/27/2018|
|Sydel sharvell|46|divorced|ssharvell2@amazon.co.jp|702-187-8715|4 School Place,Las Vegas,Nevada|Budget/Accounting Analyst I|10/6/2017|
|Constantin de la cruz|35|married|co3@bloglines.com|402-688-7162|6 Monument Crossing,Omaha,Nebraska|Desktop Support Technician|10/20/2015|
|Gaylor redhole|38|married|gredhole4@japanpost.jp|917-394-6001|88 Cherokee Pass,New York City,New York|Legal Assistant|5/29/2019|
|Wanda del mar|44|single|wkunzel5@slideshare.net|937-467-6942|10864 Buhler Plaza,Hamilton,Ohio|Human Resources Assistant IV|3/24/2015|
|Joann kenealy|41|married|jkenealy6@bloomberg.com|513-726-9885|733 Hagan Parkway,Cincinnati,Ohio|Accountant IV|4/17/2013|
|Joete cudiff|51|divorced|jcudiff7@ycombinator.com|616-617-0965|975 Dwight Plaza,Grand Rapids,Michigan|Research Nurse|11/16/2014|
|Mendie alexandrescu|46|single|malexandrescu8@state.gov|504-918-4753|34 Delladonna Terrace,New Orleans,Louisiana|Systems Administrator III|3/12/1921|
|Fey kloss|52|married|fkloss9@godaddy.com|808-177-0318|8976 Jackson Park,Honolulu,Hawaii|Chemical Engineer|11/5/2014|

