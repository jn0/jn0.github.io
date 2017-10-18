---
published: true
layout: post
title: Python Code I18N and L10N Notes
---
# Python Code I18N and L10N Notes

- pygettext.py lives in python-tools in CentOS 7
- In, say, intel-manager-for-lustre/cluster-sim/cluster_sim run  
`pygettext.py -d cluster_sim -p locale/ -v -a *.py`  
to make locale/cluster_sim.pot with strings denoted with `_(…)`.
- Use `:.,$s/\(['"]\{1,1\}\)[^'"]\+\1/_(&)/gc` in vim to find-n-destroy the strings.

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
