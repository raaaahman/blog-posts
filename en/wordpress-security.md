# WordPress Security : An open talk with Julio Potier

During the Paris WordCamp 2019, there was lots of great talks. Although you will be able to watch those again on wordpress.tv, there was also some more informal talks, in which participants seated in sofas and on chairs around low table and discussed predefined topics, supported by a coordinator.

I want to report to you one of these open talks, as I found the information exposed could be pretty useful. It was about WordPress security, and our coordinator was [Julio Potier](https://profiles.wordpress.org/juliobox/), founder of the security plugin [SecuPress](http://secupress.pro/), director of the *WPFR* organization, and *WordPress* consultant for years (between other roles...). Needless to say, that we all had lots of question to ask him.

## The WordPress Community, our greatest strength

One thing that Julio introduced immediately is how big our community is, and how it provides us all a great flow of knowledge upon attacks and means of defense with our shared tool, WordPress. Indeed, as much as the big share of websites powered by WordPress may attract lots of hackers, it has helped developed, through the years, a great network of professionals sharing their knowledge, either openly or during consulting jobs. We are not alone in this task, and Julio didn't miss on an occasion to remember us that fact during the whole talk.

Another great benefits from using such a popular and open tool, is that updates are frequents. That means that newly found weaknesses can be addressed quickly. Indeed, anybody can look up the code or can do some testing on his own, and then report the discovered security breach, and even try to fix it and submit a request to modify WordPress core.

## Security plugins, are they good enough ?

A question that was quickly asked, is the utility of security plugins, and more precisely, to their free versions. WordPress has a few of these, and they seem used a lot by the community, but do we need all the  functionalities from a Pro (understand: paid) plugin?

The answer is : "it depends on the website you are building". Indeed, from the simple blogging tool WordPress was at is beginning, it has evolved to be used for many purposes nowadays. All the sites vary greatly in functionalities, and these various functionalities may need several different protections.

You're building an e-commerce? That means you're going to need several personal data from your users, and you need to protect them well! You're blogging? Better be sure that you won't be spammed in the comments.

There's no one-fits-all solution when it come to security, and the better would always be to ask for an audit to somebody with an experience in either web security or the type of website you're building, and even better if such a person knows both! 

## The plugins, potential backdoor for hackers

Talking about plugins, WordPress literally thrive on them, and I'm not sure we'd be able to find somewhere a WordPress site using no plugin at all. Though they are the main way attackers sneak in. It can be explained quite easily, as plugins development teams and contributors are not as many as working on WordPress core, and everyone of them is not necessarily an experienced developer neither. So how can we protect against such vulnerabilities?

The first answer is to rely on the community. News spread fast, and by doing consistent reading, you might be aware of the newly found breaches before it become a problem. Information on that matter wouldn't be hard to find, either on the [wordpress.org blog](https://wordpress.org/news/category/security/) which have a *security* tag for that matter, the community maintained website [WP Vuln DB](https://wpvulndb.com/) or even the blogs of the different security plugins could be very helpful.

Another great benefit of our very active community, is the patch frequency. So be sure to patch your websites to the latest version of WordPress core. Do it on a test environment first though, as you can't be sure that all your plugins have already caught up, even if they say to have been updated, they might have been modified in some way that may not cope with your website as a whole.

But there's more, by being a large community of users, we can easily distinguish popular plugins in the WordPress ecosystem, and that's really an insight of whether you should trust or not such plugins. Because users wouldn't stick with a plugin that make their sites vulnerable. Also, attackers would probably aim for the most used plugins, in order to able to target the more sites they can. So if you hadn't heard of an attack on a plugin with half a million of actives installations, well that plugin is probably safe for you to use.

## Our responsibility as plugin developers

Like in the previous paragraph, the main defense against any kind of attack, is to be aware about them. So it is a wise thing to get the habit of reading about security, or even WordPress development in general. It's not just about blog posts and newsletters, you can also read code! Want to implement a new feature, there potential several plugins already doing almost the same thing, and they may be open source, so don't hesitate to take example on those. Particularly for widely used and well-known plugins, like *WooCommerce*, for example.

Talking about features, certain are obviously more risky than others. Basically everything that will put information into the database have to be meticulously verified. But not only, every time you read information from an url, or from a form, attackers might try to inject code in it. This is something that happened recently, to the *Easy SMTP*, like discussed on WordFence's blog [here](https://www.wordfence.com/blog/2019/03/hackers-abusing-recently-patched-vulnerability-in-easy-wp-smtp-plugin/). I will not list every kind of vulnerabilities can arise from our developments, as it is not the goal of this post, and I'm not an expert in the field, but be aware that the *OWASP* non-profit foundation update on a year basis a list of the ten most abused vulnerabilities in websites, which is called the [Top Ten Project](https://www.wordfence.com/blog/2019/03/hackers-abusing-recently-patched-vulnerability-in-easy-wp-smtp-plugin/).

Fortunately, there's a very high chance *WordPress* already created functions for the usage you are planning for. Such functions would be already secured, so you better use those than reinventing the wheel. Once again, do not hesitate to search into WordPress core, or other plugins' code to find what you need. And, as WordPress is an open community, you may be well guided by asking for help on the forums.

There's also a tool used for verifying that your code comply to the WordPress standards (a sniffer), called [WPCS](https://packagist.org/packages/wp-coding-standards/wpcs#user-content-introduction), that will also warn you for potential security breaches in your code. It indeed helps, but it's not an ultimate solution neither, especially when you start inserting annotations in your code for it to ignore some false-positives (a feature from *WPCS*). Do not refrain from asking other developers for code reviews, as en experienced eye might notice something a machine won't. Then again, with the size of our community, you get plenty place to seek such help: your company, forums, live meetings, co-working spaces...

## Back-up plan, a mandatory consideration

Eventually, we have to be prepared that all our security measures might not be enough. Being hacked is a probability we all have to accept when you decide to host our content on the web. 

The most obvious measure is to have a back-up of your database. Some hosting providers do make regular copy of your databases, or even your file system, but you can do it by yourself also. There are plugins dedicated to exporting or making online stored back-up of your database, search for the solution that suits you the best.

But that's not the only data you want to back-up, you may need to be able your uploads also (images, pdf documents and the like), and every custom code you created. Then again, there are several solutions to choose, from having your images stored online, versioning your code and/or using a WordPress plugin.

This may be overlooked by some people, but having a testing site distinct from your actual public site, aside from the usefulness it brings when developing your site, may also help you to get back in the business very quickly, as you would just have to make a copy of this testing site on your public hosting and then insert the data back in it. Well, you will have to solve issues related to your server first, obviously.

Maybe there are much topics discussed above that you are not familiar with, and there's no shame to admit it. In fact, this talk opened my eyes with good practices I don't actually do, and field we're I'm weaker. That's normal, you can have all the knowledge by yourself, but you're not alone in this endeavor! So the last advice is to keep contact with specialized people, friends, acquaintances, business partners, that may help you patch up your website in the areas that you're not very confident with. Don't hesitate if you need to pay for such services, or if you do, ask yourself, how much a downtime on your server, or a data leak will cost you instead.

## Summing up

There's been quite some leads exposed in this post, and it may not make perfect sense to you already (even if I hope I had gave you the curiosity to investigate further). If I had to sum it up, I would use these words: read, ask, report. 

The community is what can really get us up from trouble. By sharing our knowledge and experience, each of us can grow stronger and we can strengthen our tools and process also. So find good source of information, stay tuned and bring your contribution. See you there! 