---
published: true
layout: post
title: Python Code I18N and L10N Notes
---
# Python Code I18N and L10N Notes

- Use `:.,$s/\(['"]\{1,1\}\)[^'"]\+\1/_(&)/gc` in vim to find-n-destroy the strings.
- `pygettext.py` lives in `python-tools` in CentOS 7
- In, say, `intel-manager-for-lustre/cluster-sim/cluster_sim` run  
`pygettext.py -d cluster_sim -p locale/ -v -a *.py`  
to make `locale/cluster_sim.pot` with strings denoted with `_(…)`.
- edit the `locale/cluster_sim.pot` file to insert `cluster_sim` value as `Project-Id-Version` (and fill up other header fields)
- now `mkdir -p locale/ru/LC_MESSAGES && cp locale/cluster_sim.pot locale/ru/LC_MESSAGES/cluster_sim.po`
- edit the `.po` file to add `msgstr` values to respective `msgid` entries (i.e. translate it)
- run `msgfmt.py locale/ru/LC_MESSAGES/cluster_sim.po` to get `locale/ru/LC_MESSAGES/cluster_sim.mo`
- setup your application [as described](https://docs.python.org/2/library/gettext.html)
- (don't forget about [locale](https://docs.python.org/2/library/locale.html) setup!)
- run something like `LANG=ru_RU python myapp.py` to see it in action
- here you are!

# Sample module to illustrate i18n/l10n approach

Use it as:
```python
from i18n import _
```
at the start of any source file being localized.

<script src="https://gist.github.com/jn0/6b9d2661529f6a67ac62a6cbc66e8b65.js"></script>

# Comments

<div id="disqus_thread"></div>
<script>

/**
*  RECOMMENDED CONFIGURATION VARIABLES: EDIT AND UNCOMMENT THE SECTION BELOW TO INSERT DYNAMIC VALUES FROM YOUR PLATFORM OR CMS.
*  LEARN WHY DEFINING THESE VARIABLES IS IMPORTANT: https://disqus.com/admin/universalcode/#configuration-variables*/
/*
var disqus_config = function () {
this.page.url = PAGE_URL;  // Replace PAGE_URL with your page's canonical URL variable
this.page.identifier = PAGE_IDENTIFIER; // Replace PAGE_IDENTIFIER with your page's unique identifier variable
};
*/
(function() { // DON'T EDIT BELOW THIS LINE
var d = document, s = d.createElement('script');
s.src = '//jn0.disqus.com/embed.js';
s.setAttribute('data-timestamp', +new Date());
(d.head || d.body).appendChild(s);
})();
</script>
<noscript>Please enable JavaScript to view the <a href="https://disqus.com/?ref_noscript">comments powered by Disqus.</a></noscript>
