---
dg-publish: true
---
# Class usage guides

```dataviewjs

let pages = dv.pages('"Class Usage Guides"');

let results = [];

for (let page of pages) {
    if (page["dg-metatags"]) {
        let description = page["dg-metatags"]["og:description"];
        results.push([page.file.link, description]);
    }
}

dv.table(["File", "Description"], results);

```

---
# Class Obtaining Guides

```dataviewjs

let pages = dv.pages('"Class Obtain Guides"');

let results = [];

for (let page of pages) {
    if (page["dg-metatags"]) {
        let description = page["dg-metatags"]["og:description"];
        results.push([page.file.link, description]);
    }
}

dv.table(["File", "Description"], results);

```

---
# Ultra Guides

```dataviewjs

let pages = dv.pages('"Ultra Guides"');

let results = [];

for (let page of pages) {
    if (page["dg-metatags"]) {
        let description = page["dg-metatags"]["og:description"];
        results.push([page.file.link, description]);
    }
}

dv.table(["File", "Description"], results);

```

---
# Item Guides

```dataviewjs

let pages = dv.pages('"Item Guides"');

let results = [];

for (let page of pages) {
    if (page["dg-metatags"]) {
        let description = page["dg-metatags"]["og:description"];
        results.push([page.file.link, description]);
    }
}

dv.table(["File", "Description"], results);

```

---
# Other Guides

```dataviewjs

let pages = dv.pages('"Other Guides"');

let results = [];

for (let page of pages) {
    if (page["dg-metatags"]) {
        let description = page["dg-metatags"]["og:description"];
        results.push([page.file.link, description]);
    }
}

dv.table(["File", "Description"], results);

```
