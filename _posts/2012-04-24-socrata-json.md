---
layout: post
title: Make Chicago Data JSON Look Like JSON
---

The [City of Chicago Data Portal](https://data.cityofchicago.org/) is a great
source of open data, and they allow you to export datasets in a variety of
formats. Unfortunately, if you export JSON, you get what I consider to be sort
of a mess. Since JavaScript objects are just key value pairs, what I would
like to see in an export of, for example,
[towed vehicles](https://data.cityofchicago.org/Transportation/Towed-Vehicles/ygr5-vcbg),
is a list of objects that looks something like this:

    [
      {
        "Tow Date": "04/24/2013",
        "Make": "FORD",
        "Style": "4D",
        ...
      },
      {
        "Tow Date": "04/24/2013",
        "Make": "DODG",
        "Style": "VN",
        ...
      },
      ...
    ]

Instead, all the column names are stored in a `meta` object, along with other
metadata, while all the data is stored in arrays in a `data` object. While this
might be useful in some cases, I've found that often what I want is something
that resembles the example above. So, I wrote a very short  Ruby script that
will read in a Chicago Data JSON file and spit out those key value pairs.

<script src="https://gist.github.com/matthewheston/5456179.js">

</script>

You can either pass in the JSON from stdin or give the script a file name.
Python also includes a utility to pretty print JSON from the command line,
so to read in the towed vehicle data and write out a pretty version that looks
like the JSON above to a new file, you could do the following.

`$ ruby socrata_json.rb towed_vehicles.json | python -mjson.tool > new_towed_vehicles.json`


