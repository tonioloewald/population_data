# World Population Data

I needed population data to improve my [COVID-19 browser](https://tinyurl.com/covid19-browser) 
and couldn't find a simple, easy-to-use source.

I obtained this from [worldmeters](https://www.worldometers.info/world-population/population-by-country/)
and scraped the data using this snippet of code in the console:

```
[...document.querySelectorAll('#example2 tr')]
  .map(tr => [...tr.querySelectorAll('th,td')]
  .map(elt => elt.textContent).join('\t'))
  .join('\n')
```

I hope you find it useful.