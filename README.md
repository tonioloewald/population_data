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

## Why .tsv?

`<rant>`

`.csv` is the dumbest file format ever devised. It requires a stateful parser rather than simple
string splitting to parse and has no proper standard.

If you want to parse a `.tsv` in Javascript, you simply split it by '\n' to get the rows and then
'\t' to get the cells. It's smaller, simpler, easier to read, and easier to write.

`</rant>`