# github-fork-bookmarklet
A JS bookmarklet that determines which branches are ahead or behind the original branch.

## Code
```JavaScript
javascript:(async () => {
  const aTags = [...document.querySelectorAll('div.repo a:last-of-type')].slice(1);
  for (const aTag of aTags) {
    await fetch(aTag.href)
      .then(x => x.text())
      .then(html => aTag.outerHTML += `${html.match(/This branch is.*/).pop().replace('This branch is', '').replace(/([0-9]+ commits? ahead)/, '<font color="#0c0">$1</font>').replace(/([0-9]+ commits? behind)/, '<font color="red">$1</font>')}`)
      .catch(console.error);
  }
})();
```
## Usage
After clicking "Insights" on top and then "Forks" on the left, the following [bookmarklet](https://github.com/halogod35/github-fork-bookmarklet/blob/main/script.js) prints the info directly onto the web page like this:
![](https://i.stack.imgur.com/O14HC.png)
