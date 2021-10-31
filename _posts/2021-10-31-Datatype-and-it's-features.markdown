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

For all the above elements we can rely on these two libraries offered by python, [datetime library](https://docs.python.org/3/library/datetime.html) and [calender library](https://docs.python.org/3/library/calendar.html)

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

Now that we know how to collect the static elements of date features, we'll look briefly into the ways to collect the dynamic elements of it since date and time comes under cyclic categorical data type.

For this, we will entirely rely on a open source library called tsfresh
>This code has been taken from the book Approaching Almost Any ML Problem by [Abhishek Thakur](https://www.linkedin.com/in/abhi1thakur/)

{% highlight python %}
from tsfresh.feature_extraction import feature_calculators as fc
# tsfresh based features. x being the date column
feature_dict['abs_energy'] = fc.abs_energy(x)
feature_dict['count_above_mean'] = fc.count_above_mean(x)
feature_dict['count_below_mean'] = fc.count_below_mean(x)
feature_dict['mean_abs_change'] = fc.mean_abs_change(x)
feature_dict['mean_change'] = fc.mean_change(x)
{% endhighlight %}


### Geo/Location

This is one of the less commonly used datatype. It appears only in problems involving transporation.
Location can be given in terms of `geo code, name, geo co-ordinates`

It is better to convert all other types to geo co-ordinates because we can extract interesting features out of it. The list of elements that can be extracted using geographical co-ordinates are as follows

1. Distance between two geographical co-ordinates
2. Distance between given geo coordinates and popular landmark of that area
3. Design a hotspot circle and check if given co-ordinates falls into it or not.
>If you can collect external data associated with these co-ordinates like population, area type, no.of buildings and so on then way more related features can be extracted but you need to be careful in this case as we number of features in not directly proportional to model performance and very minimal we might end up in overfitting.

As far as finding distances between tqo geo points, we can rely on one of the three distances; Manhattan distance, Euclidean distance and Haversine Distance. More information regarding pros and cons of each distance can be found [here](https://towardsdatascience.com/spatial-distance-and-machine-learning-2cab72fc6284)

I'll go through the simplest distance metric of geo points i.e., Haversine distance

{% highlight python %}
import haversine as hs
def haversine_np(lon1, lat1, lon2, lat2):
    loc1=(lat1, lon1)
    loc2=(lat2, long2)
    return hs.haversine(loc1,loc2)
{% endhighlight %}

#### References
1. [Approaching Almost Any Machine Learning Problem](https://github.com/abhishekkrthakur/approachingalmost/blob/master/AAAMLP.pdf)
2. [GeoPy](https://geopy.readthedocs.io/en/stable/#module-geopy.distance)
3. [Date time Cheat sheet](https://www.pythoncheatsheet.org/blog/python-datetime-objects-and-strings/)
