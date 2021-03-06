---
layout: page
title: "JavaScript similar_text function"
comments: true
sharing: true
footer: true
sidebar: false
alias:
- /functions/view/similar_text:902
- /functions/view/similar_text
- /functions/view/902
- /functions/similar_text:902
- /functions/902
---
<!-- Generated by Rakefile:build -->
A JavaScript equivalent of PHP's similar_text

{% codeblock strings/similar_text.js lang:js https://raw.github.com/kvz/phpjs/master/functions/strings/similar_text.js raw on github %}
function similar_text (first, second, percent) {
  // http://kevin.vanzonneveld.net
  // +   original by: Rafał Kukawski (http://blog.kukawski.pl)
  // +   bugfixed by: Chris McMacken
  // +   added percent parameter by: Markus Padourek (taken from http://www.kevinhq.com/2012/06/php-similartext-function-in-javascript_16.html)
  // *     example 1: similar_text('Hello World!', 'Hello phpjs!');
  // *     returns 1: 7
  // *     example 2: similar_text('Hello World!', null);
  // *     returns 2: 0
  // *     example 3: similar_text('Hello World!', null, 1);
  // *     returns 3: 58.33
  if (first === null || second === null || typeof first === 'undefined' || typeof second === 'undefined') {
    return 0;
  }

  first += '';
  second += '';

  var pos1 = 0,
    pos2 = 0,
    max = 0,
    firstLength = first.length,
    secondLength = second.length,
    p, q, l, sum;

  max = 0;

  for (p = 0; p < firstLength; p++) {
    for (q = 0; q < secondLength; q++) {
      for (l = 0;
      (p + l < firstLength) && (q + l < secondLength) && (first.charAt(p + l) === second.charAt(q + l)); l++);
      if (l > max) {
        max = l;
        pos1 = p;
        pos2 = q;
      }
    }
  }

  sum = max;

  if (sum) {
    if (pos1 && pos2) {
      sum += this.similar_text(first.substr(0, pos2), second.substr(0, pos2));
    }

    if ((pos1 + max < firstLength) && (pos2 + max < secondLength)) {
      sum += this.similar_text(first.substr(pos1 + max, firstLength - pos1 - max), second.substr(pos2 + max, secondLength - pos2 - max));
    }
  }
  
  if (!percent) {
    return sum;
  } else {
    return (sum * 200) / (firstLength + secondLength);
  }
}
{% endcodeblock %}

 - [view on github](https://github.com/kvz/phpjs/blob/master/functions/strings/similar_text.js)
 - [edit on github](https://github.com/kvz/phpjs/edit/master/functions/strings/similar_text.js)

### Example 1
This code
{% codeblock lang:js example %}
similar_text('Hello World!', 'Hello phpjs!');
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
7
{% endcodeblock %}

### Example 2
This code
{% codeblock lang:js example %}
similar_text('Hello World!', null);
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
0
{% endcodeblock %}

### Example 3
This code
{% codeblock lang:js example %}
similar_text('Hello World!', null, 1);
{% endcodeblock %}

Should return
{% codeblock lang:js returns %}
58.33
{% endcodeblock %}


### Other PHP functions in the strings extension
{% render_partial _includes/custom/strings.html %}
## Legacy comments
These were imported from our old site. Please use disqus below for new comments
<div style="overflow-y: scroll; max-height: 500px;">
{% render_partial functions/similar_text/_comments.html %}
</div>
