---
layout: post
title:  "Constructing GET Request using Python"
date:   2019-06-05 09:55:36 +0800
categories: API Python
---
Creating your **API GET Request** can be be [hassle-free, easy and quick][1] with *Python*!
The entire process can be completed by running a 80-line code .py file

```javascript
const Razorpay = require('razorpay');

let rzp = Razorpay({
	key_id: 'KEY_ID',
	secret: 'name'
});

// capture request
rzp.capture(payment_id, cost)
	.then(function (data) {
		return 2;
	})
```

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
