# JobSort

[JobSort](https://jobsort.com) is a fast job search engine built by developers for developers. JobSort crawls the Internet for new jobs every day to create its jobs database. JobSort is powered by a custom filtering language called JobSort Query Language (JSQL) that enables deep searching.

Thanks to those who have given words of advice over the past months to guide future development. If you're curious, the name "JobSort" derives from the well-known sorting algorithm "QuickSort."

## Features

*   The database has more than 20 000 jobs that are constantly refreshed.
*   The flexible **JobSort Query Language (JSQL)** enables deep searching inside the big database. It'll almost feel like coding when you're searching.
*   Negative filtering!
*   **"Job health-checks"** test if each job is still available as you scroll through the results. If the job is dead, it gets stricken through so you don't land on a 404 page.

### JobSort Query Language

```
[-]keyword [[-]lang:string] [[-]tech:string] [[-]hq:string] [remote:ok] [days:<uint] [size:<uint] [sort:datetime|traffic]
```

Use the `-` operator to negate the meaning of most filters. For example, when searching for `java`, search engines also return less relevant `javascript` matches. Thus, search for [`java -javascript`](https://jobsort.com/search?q=java+-javascript) to filter out `javascript` matches when looking for `java` jobs.

Filter | Syntax | Type | Examples
---|---|---|---
Keyword[^1] | `[-]keyword` | `string` | [`java`](https://jobsort.com/search?q=java), [`java -javascript`](https://jobsort.com/search?q=java+-javascript)
Programming Language[^3] | `[-]lang:` | `string`, see [languages.tsv](languages.tsv) | [`lang:go`](https://jobsort.com/search?q=lang:go), [`frontend -lang:php`](https://jobsort.com/search?q=frontend+-lang:php)
Tech Stack[^4] | `[-]tech:` | `string`, see [technologies.tsv](technologies.tsv) | [`tech:django`](https://jobsort.com/search?q=tech:django), [`sysadmin -tech:linux`](https://jobsort.com/search?q=sysadmin+-tech:linux)
Headquarters | `[-]hq:` | `string` | [`hq:california -hq:"san francisco"`](https://jobsort.com/search?q=hq:california+-hq:'san+francisco')
Remote[^2] | `remote:` | `ok` | [`remote:ok`](https://jobsort.com/search?q=remote:ok)
Recency[^5] | `days:<` | `uint` | [`days:<7`](https://jobsort.com/search?q=days:<7)
Company Size | `size:<`, `size:>` | `uint` (employees) | [`size:<100`](https://jobsort.com/search?q=size:<100)
Sort Order[^6] | `sort:` | `datetime\|random\|traffic` | [`sort:datetime`](https://jobsort.com/search?q=sort:datetime), [`sort:random`](https://jobsort.com/search?q=sort:random), [`sort:traffic`](https://jobsort.com/search?q=sort:traffic)

#### Example Searches

*   [`java -javascript`](https://jobsort.com/search?q=java+-javascript) for when `java` matches `javascript` results but you're not a frontend engineer, thus it's useful to remove `javascript` results.
*   [`hq:california -hq:"san francisco"`](https://jobsort.com/search?q=hq:california+-hq:'san+francisco') for when you want to find a job somewhere in `California` but living in `San Francisco` is just too expensive.
*   [`size:<100`](https://jobsort.com/search?q=size:<100) if you like working in small companies with less than 100 employees.
*   [`size:>1000`](https://jobsort.com/search?q=size:>1000) if you like working in large companies with more than 1000 employees.

[^1]: Search like on Google.
[^2]: Returns only remote jobs; `ok` is the only enum value for `remote:`.
[^3]: Useful when you search for programming languages that are common English words.
[^4]: Useful when you love Django on Windows, but dislike Linux.
[^5]: Returns only jobs found in the last two days.
[^6]: Sorts the results either by its crawl time in ascending order or its traffic in descending order.
