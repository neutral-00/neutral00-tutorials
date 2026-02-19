# Database Design Process

Let's ask ourselves 3 fundamental question:
1. What kind of thing we are storing?
2. What properties does this thing have?
3. What type of data does each of this properties contain?

## Example - Cities
Let's refer this wikipedia page to find world's largest cities. `en.wikipedia.org/wiki/List_of_largest_cities`

From this page, let's design a table containing city, country,  area and population.

Let's ask the fundamental questions:
1. What kind of thing we are storing? Cities
2. What properties does this thing have? city, country, area, population
3. What type of data each of this properties contain?
- city: string
- country: string
- area: number
- population: number


So we should create a table named `cities` \
It should have the following columns: name, country, area, population

