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

## Using this data directly

You can just pull the data directly from github at `https://tonioloewald.github.io/population_data/population-data.tsv`.
Github has an awesome CDN and everything so it's just that simple.

In vanillajs you can get the data thus:

```
async function getPopulationData () {
  const response = await fetch('https://tonioloewald.github.io/population_data/population-data.tsv')
  const text = await response.text()
  const rows = text.split('\n').map(line => line.split('\t'))
  const headings = rows.unshift()
  const countryColumnIndex = 1
  const populationColumnIndex = 2
  const  getColumnIndex = (column) =>  column === 'string' ? headings.findIndex(column) : column
  const getCell = (country, column = populationColumnIndex) => {
    const columnIndex = getColumnIndex(column)
    return rows.find(row => row[countryColumnIndex] === country)[columnIndex]
  }
  // population column is formatted with commas, e.g. "25,499,884"
  const getPop = country => parseInt(p.getCell(country).replace(/,/g, ''))
  return {
    headings,
    rows,
    getColumnIndex,
    getCell,
    getPop,
  }
}
```

Using the above:

```
p = await getPopulationData()
p.getPop('Australia')
```

## Why .tsv?

`<rant>`

`.csv` is the dumbest file format ever devised. It requires a stateful parser rather than simple
string splitting to parse and has no proper standard.

If you want to parse a `.tsv` in Javascript, you simply split it by '\n' to get the rows and then
'\t' to get the cells. It's smaller, simpler, easier to read, and easier to write.

`</rant>`