# Week 39th
## Algorithm
### [811. Subdomain Visit Count](https://leetcode.com/problems/subdomain-visit-count/description/)

### Description
A website domain like "discuss.leetcode.com" consists of various subdomains. At the top level, we have "com", and at the lowest level, "discuss.leetcode.com". When we visit a domain like "discuss.leetcode.com", we will also visit the parent domains "leetcode.com" and "com" implicitly.  

Now, call a "count-paired domain" to be a count-paired domains. We would like a list of count-paired domains, (in the same format as the input, and in any order), that explicitly counts the number of visits to each subdomain.  

### Example 1
```
Input: ["9001 discuss.leetcode.com"]
Output: ["9001 discuss.leetcode.com", "9001 leetcode.com", "9001 com"]
Explanation: We only have one website domain: "discuss.leetcode.com". As discussed above, the subdomain "leetcode.com" and "com" will also be visited. So they will all be visited 9001 times.
```

### Example 2
```
Input: ["900 google.mail.com", "50 yahoo.com", "1 intel.mail.com", "5 wiki.org"]
Output: ["901 mail.com, "50 yahoo.com", "900 google.mail.com", "5 wiki.org", "5 org", "1 intel.mail.com", "951 com"]
Explanation: Well will visit "google.mail.com" 900 times, "yahoo.com" 50 times, "intel.mail.com" once and "wiki.org" 5 times. For the subdomains, we will visit "mail.com" 900 + 1 = 901 times, "com" 900 + 50 + 1 = 951 times, and "org" 5 times.
```

### Note
- The length of `cpdomains` will not exceed `100`.
- The length of each domain name will not exceed `100`.
- Each address will have either 1 or 2 "." characters.
- The input count in any count-paired domain will not exceed `10000`.
- The answer output can be returned in any order.

### Solution
```javascript
/**
 * @param {String[]} cpdomains
 * @returns {String[]}
 */
const subdomainVisits = (cpdomains) => {
	const map = new Map();
	const outcome = [];
	for (let paire of cpdomains) {
		const space = paire.indexOf(' ');
		const visit = parseInt(paire.substr(0, space));
		const domain = paire.substr(space + 1);
		const length = domain.length;
		const beenVisit = map.get(domain) ? map.get(domain) : 0;
		map.set(domain, beenVisit + visit);
		for (let i = 0; i < length; i++) {
			if (domain.charAt(i) === '.') {
				const subdomain = domain.substr(i + 1);
				const subvisit = map.get(subdomain) ? map.get(subdomain) : 0;
				map.set(subdomain, subvisit + visit);
			}
		}
	}
	for (let [key, value] of map) {
		outcome.push(`${value} ${key}`);
	}
	return outcome;
};
```
This is a `Map` problem.
1. restructure array elements into map.
2. mean time set the element level domain visit status.
3. set subdomain visit status.

## Review
[How JavaScript works: Storage engines + how to choose the proper storage API](https://blog.sessionstack.com/how-javascript-works-storage-engines-how-to-choose-the-proper-storage-api-da50879ef576)  

[Tutorial – SessionStack Blog](https://blog.sessionstack.com/tagged/tutorial) this link to a series article on **How JavaScript Works**.  

Cookie as the only option of client side storage was long behind. We now have so many ways to store data for our customer on the browser side.  

**File system API** web app can create, read, navigate, and write to a sandboxed section of use’s local file system. BUT not recommended, due to the lack of different vendor of browsers.  

**Local Storage** for Key/Value model, device persistence,  93% browsers supported, no transactions support, sync operation.  

**Session Storage** for Key/Value model, session persistence, 93% browsers supported, no transactions support, sync operation. 

**Cookie** for structured model, device persistence,  100% browsers supported, no transactions support, sync operation.  

**Cache** for Key/Value model, device persistence,  60% browsers supported, no transactions support, async operation.  

**IndexedDB** hybrid model supported, , device persistence,  83% browsers supported, with transactions support, async operation.  

So chose these API wisely, one app may need not only one kind API, for those need offline storage, use **Cache API** for network server-generated content and use **IndexedDB** for user-generated content. 

## Technique
This week share a Tampermonkey script, for optimize the UX on [LeetCode - The World’s Leading Online Programming Learning Platform](https://leetcode.com/), You’re welcome LeetCode.  
```javascript
/**
 * CHANGELOG
 * @version 0.1
 * I'm in China, the region switcher is so annoying stick on the bottom occupy a whole row space,
 * so I wrote this script using leetcode's own `hide` class, hide that f***ing UX breaking monster.
 */
(function () {
	'use strict';

	// Your code here...
	const hideRegionSwitcher = () => {
		const aside = document.querySelector('#region_switcher');
		aside.classList.add('hide');
	}

	window.addEventListener('load', hideRegionSwitcher);
})();
```


## Share
One concept, comment tells why and code tells how.
