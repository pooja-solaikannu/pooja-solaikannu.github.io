---
layout: "post"
title: "DataTypes and It's Features"
---

Hi Everyone, welcome to yet another ML post. Recently I was unlearing about ML strategies and I thought this could be worth sharing.

As we all know and agree, ML problem is driven by data in various forms. Generic types of data that can come in Tabular form are `"Numeric", "Categorical", "Date and Time", "Geo/Location".` One of the interesting and challenging component in ML Pipeline is that based on the problem type, we have to extract features of the the data provided to us. 

In this post we'll explore the ways to extract useful data for datatypes Date&Time and Geo/Location.

I hope the context of the post is clear now and let's gets started.

### Date and Time

A date and time feature would look like this `2016-01-01 00:00:00`. From this we can extract the following information/date related attributes. 

* Date, Month, Year, Hour
* Day Number
* Week Number
* Is Weekend
* Is Weekday
* Is leap year
* Is daytime
* Is night time

For all the above elements we can rely on a single library offered by python, [datetime library](https://docs.python.org/3/library/datetime.html) and [calender library](https://docs.python.org/3/library/calendar.html)

I have included code sinppets to extract attributes/elements using the above libraries. 

{% highlight python %}
from datetime import datetime
import calendar

print(datetime.now())
# Date Number - isoweekday returns day number of a week 1-Monday and 7-Sunday
print(datetime.now().isoweekday())
# Week Number - isocalendar method returns (year, week, day)
print(datetime.now().isocalendar()[1])
# Is weekend and Is weekday
# Since isoweekday returns day number of a week, we can find using that information whether a particular day is a weekday or not
if datetime.now().isoweekday() < 6:
    print("It is a weekday")
else:
    print("It is weekend")
# Is leapyear - uses calendar package
print(calendar.isleap(datetime.now().year))
#  Is daytime/ nighttime - it is a simple solution. I'm sure there must be more sophisticated method for this that the one I have presented.
# So, feel free to comment out your approach. Always happy to learn :)
if datetime.now().hour >=0 and datetime.now().hour <= 24:
    if datetime.now().hour > 6 and datetime.now().hour < 18:
        print("It is day time")
    else:
        print("It is night time")
else:
    print('Provide a proper time element')
{% endhighlight %}

### Geo/Location



#### References
1. [Approaching Almost Any Machine Learning Problem](https://github.com/abhishekkrthakur/approachingalmost/blob/master/AAAMLP.pdf)
2. [GeoPy](https://geopy.readthedocs.io/en/stable/#module-geopy.distance)
3. [Date time Cheat sheet](https://www.pythoncheatsheet.org/blog/python-datetime-objects-and-strings/)
