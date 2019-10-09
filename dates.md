
### Date and Time DataTypes in DB

### DATE 
   Default date format is YYYY-MM-DD, between 1000-01-01 and 9999-12-31.
   For example, August 30th, 1991 would be stored as 1991-08-30.

### DATETIME 
   Default date and time format is YYYY-MM-DD HH:MM:SS, between 1000-01-01 00:00:00 and 9999-12-31 23:59:59. 
   For example, 4:30 in the afternoon on August 30th, 1991 would be stored as 1991-08-30 16:30:00.
   
### TIMESTAMP
   A timestamp between midnight, January 1st, 1970 and sometime in 2037. This looks like the previous DATETIME format, only      without the hyphens between numbers; 3:30 in the afternoon on December 30th, 1973 would be stored as 
   19731230153000 (YYYYMMDDHHMMSS).

### TIME
   Default time format HH:MM:SS format.

### YEAR(M)
   It stores a year in a 2-digit or a 4-digit format. If the length is specified as 2 (for example YEAR(2)), 
   YEAR can be between 1970 to 2069 (70 to 69). If the length is specified as 4, then YEAR can be 1901 to 2155. 
   The default length is 4.
   
### Internal Storage of Date

All Date, Time, Datetime, Timestamp are stored as Integers internally but different date types have different integers values as follows: 

YEAR: A one-byte integer

DATE: A three-byte integer packed as YYYY×16×32 + MM×32 + DD
For example: 2019--09-13= 2019x16x32 + 9x32 + 13= 1034029, it means 2019--09-13 date is stored as 1034029 integer format in database.

TIME: A three-byte integer packed as HH×3600 + MM×60 + SS
For example: 04:22:10 = 4x3600+22x60+10=15730 , it means 04:22:10 time is stored as 15730 integer format in database.

TIMESTAMP: A four-byte integer representing seconds UTC since the epoch ('1970-01-01 00:00:00' UTC)
DATETIME: Eight bytes: A four-byte integer for date packed as YYYY×10000 + MM×100 + DD and a four-byte integer for time packed as HH×10000 + MM×100 + SS




