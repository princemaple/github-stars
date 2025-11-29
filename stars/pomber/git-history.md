---
project: git-history
stars: 13655
description: Quickly browse the history of a file from any git repository
url: https://github.com/pomber/git-history
---

Git History
===========

Quickly browse the history of files in any git repo:

1.  Go to a file in **GitHub** (or **GitLab**, or **Bitbucket**)
2.  Replace `github.com` with `github.githistory.xyz`
3.  There's no step three

Try it

> If you like this project consider backing my open source work on Patreon!  
> And follow @pomber on twitter for updates.

Extensions
----------

### Browsers

You can also add an `Open in Git History` button to GitHub, GitLab and Bitbucket with the Chrome and Firefox extensions.

Or you can use a bookmarklet.

javascript: (function() {
  var url \= window.location.href;
  var regEx \= /^(https?\\:\\/\\/)(www\\.)?(github|gitlab|bitbucket)\\.(com|org)\\/(.\*)$/i;
  if (regEx.test(url)) {
    url \= url.replace(regEx, "$1$3.githistory.xyz/$5");
    window.open(url, "\_blank");
  } else {
    alert("Not a Git File URL");
  }
})();

### Local Repos

You can use Git History for local git repos with the CLI or with the VS Code extension.

Support Git History
-------------------

### Sponsors

Support this project by becoming a sponsor. Your logo will show up here with a link to your website. \[Become a sponsor\]

### Backers

Thank you to all our backers! 🙏 \[Become a backer\]

### Thanks

Browser testing via

### Credits

Based on these amazing projects:

-   Prism by Lea Verou
-   jsdiff by Kevin Decker
-   Night Owl by Sarah Drasner

License
-------

MIT
