# strftime is a time utility extracted and modified from [leekchan/timeutil](https://godoc.org/github.com/leekchan/timeutil)

## Quick Start

```
go get github.com/devmarwen/strftime
```

example.go

```Go
package main

import (
    "fmt"
    "time"

    "github.com/devmarwen/strftime"
)

func main() {
    date := time.Date(2015, 7, 2, 15, 24, 30, 35, time.UTC)
    str := strftime.Strftime(&date, "%a %b %d %I:%M:%S %p %Y") // default to locale "en"
    fmt.Println(str) // "Thu Jul 02 03:24:30 PM 2015"
    
    // Unicode support
    str = strftime.Strftime(&date, "작성일 : %a %b %d %I:%M:%S %p %Y")
    fmt.Println(str) // "작성일 : Thu Jul 02 03:24:30 PM 2015"


    // Locale support
    // only "en" and "fr" at the moment free to add your own
	date = time.Date(1989, 12, 31, 0, 24, 30, 35000, time.UTC)
	StrftimeL(&date, "%a %A %w %d %b %B %", "fr") // "Dim. Dimanche 0 31 Déc. Décembre "
}
```


## Strftime

Strftime formats time.Date according to the directives in the given format string. The directives begins with a percent (%) character.

(Strftime supports unicode format string.)


Directive | Meaning | Example
-------------| ------------- | -------------
%a | Weekday as locale’s abbreviated name. | Sun, Mon, ..., Sat
%A | Weekday as locale’s full name.     | Sunday, Monday, ..., Saturday 
%w | Weekday as a decimal number, where 0 is Sunday and 6 is Saturday | 0, 1, ..., 6     
%d | Day of the month as a zero-padded decimal number. | 01, 02, ..., 31 
%b | Month as locale’s abbreviated name. | Jan, Feb, ..., Dec
%B | Month as locale’s full name. | January, February, ..., December
%m | Month as a zero-padded decimal number. | 01, 02, ..., 12
%y | Year without century as a zero-padded decimal number. | 00, 01, ..., 99
%Y | Year with century as a decimal number. |   1970, 1988, 2001, 2013
%H | Hour (24-hour clock) as a zero-padded decimal number. | 00, 01, ..., 23
%I | Hour (12-hour clock) as a zero-padded decimal number. | 01, 02, ..., 12 
%p | Meridian indicator. (AM or PM.) | AM, PM
%M | Minute as a zero-padded decimal number. | 00, 01, ..., 59
%S | Second as a zero-padded decimal number. | 00, 01, ..., 59
%f | Microsecond as a decimal number, zero-padded on the left. | 000000, 000001, ..., 999999
%z | UTC offset in the form +HHMM or -HHMM | +0000
%Z | Time zone name | UTC
%j | Day of the year as a zero-padded decimal number | 001, 002, ..., 366
%U | Week number of the year (Sunday as the first day of the week) as a zero padded decimal number. All days in a new year preceding the first Sunday are considered to be in week 0. | 00, 01, ..., 53 
%W | Week number of the year (Monday as the first day of the week) as a decimal number. All days in a new year preceding the first Monday are considered to be in week 0.   | 00, 01, ..., 53
%c | Date and time representation. | Tue Aug 16 21:30:00 1988
%x | Date representation. | 08/16/88
%X | Time representation. | 21:30:00
%% | A literal '%' character. | %