# Alex Zhirkov

## Contact Info: 
* Email: keane3192@gmail.com
* Telegram and Phone: +7 903 004 02 66

## Summary: 
My knowledge of Kotlin is not great ,but i have a will to improve that. At the moment I have got an expireince in:

Development of parsers in JavaScript with Pupeteer. Collecting information from  YandexMap.

Development of an simple Telegram Bot using Python.

Development of website using WordPress.

## Skills: 
JavaScript, MySQL, PHP, jQuery, WordPress, Node.js, Python,Vue.js, Python.

## Code Examples: 
```javascript
const { Cluster } = require('puppeteer-cluster');

(async () => {
    const cluster = await Cluster.launch({
        concurrency: Cluster.CONCURRENCY_CONTEXT,
        maxConcurrency: 2,
		monitor:true,
    });

    // Extract title of page
    const extractTitle = async ({ page, data }) => {
        const { url, position } = data;
        await page.goto(url);
        const pageTitle = await page.evaluate(() => document.title);
        console.log(`Page title of #${position} ${url} is ${pageTitle}`);
    };

    // Crawl the Google page
    await cluster.task(async ({ page, data }) => {
        const { searchTerm, offset } = data;
        await page.goto(
            'https://www.google.com/search?q=' + searchTerm + '&start=' + offset,
            { waitUntil: 'domcontentloaded' }
        );

        console.log('Extracting Google results for offset=' + offset);

        // Extract the links and titles of the search result page
        (await page.evaluate(() => {
            return [...document.querySelectorAll('#ires .g .rc > .r a')]
                .map(el => ({ url: el.href, name: el.innerText }));
        })).forEach(({ url, name }, i) => {
            // Put them into the cluster queue with the task "extractTitle"
            console.log(`  Adding ${name} to queue`);
            cluster.queue({
                url,
                position: (offset + i+1)
            }, extractTitle);
        });
    });

    cluster.queue({ searchTerm: 'puppeteer-cluster', offset: 0 });
    cluster.queue({ searchTerm: 'puppeteer-cluster', offset: 10 });

    await cluster.idle();
    await cluster.close();
})();
```

## Exprience: 
Made a parser using library Pupeteer.js.
Know how to make Telegram bot.
Know how to make SQL query.

## Education: 
Practiced on Javascript and MySQL courses from Udemy. Read a book on PHP.

## English: 
My knowledge of english language is not bad in my opinion. I learned english in school and by listening to english videos.
