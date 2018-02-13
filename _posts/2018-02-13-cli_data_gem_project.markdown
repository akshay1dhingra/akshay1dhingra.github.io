---
layout: post
title:      "CLI Data Gem Project"
date:       2018-02-13 14:24:39 -0500
permalink:  cli_data_gem_project
---


I decided to create my project on Cryptocurrency data. Being a timid investor myself, I thought this would be a fun and useful gem for me to have on my machine.

The gem scrapes off of www.coinranking.com and prints out the top 50 coins and their attributes such as name, price, market cap, change, and description. 

**Setting Up **

At the beginning, I decided to create the gem locally instead of IDE. I installed Atom, Bash, and uploaded my machines' SSH key to my github account. I quickly learned that windows and BASH do not work well together at all. This, I later found out, is due to the fact that BASH is supposed to be used with UNIX based OS. I added `STDOUT.sync = true` at the beginning of my CLI class so that my BASH flushes out its memory onto the command prompt as the program computes the data. I also found out that I could use the Command Prompt that comes with Windows to circumvent this issue all together. This is why most web developers choose to work on Macs or Linux instead of windows. 

Once the local environment is set up, the next step is to set up the gem. This is easily done by typing `bundle gem [your project name]` into your terminal or command prompt. This creates your gem project with all the necessary files and folders in whichever folder you are `cd` into. You then `git init` to initialize your git repository so that you can `git commit -m "first commit"` your first commit and begin saving changes. It is also wise to add a .gitignore file to your project if you wish to keep your repository neat and clean. Next step is to add your dependencies to your gemspec file for example `pec.add_development_dependency "pry"` and `pec.add_development_dependency "nokogiri"`. 

**Project **

The trickiest part about this project is using Nokogiri to scrape the web page. Please open www.coinranking.com then right-click and inspect the page. To make my project work, I need to scrape all 50 coins names, price, market cap, change, and if you click on the name it takes you to another page and towards the bottom I needed to scrape the description. In order for me to access these individual attributes, I need to build an array. 

In my scraper class, I built a scraper method with the following 

```
doc = Nokogiri::HTML(open("https://coinranking.com/"))
```

This opens coinranking.com and  exposes its XML notation.  If you look in the inspection side of your screen, in order for me to collect each of the coins attributes I need to find the tag that holds that data, and extract the text from it. This is found in the `.coin-list__body` tag. But I cant just collect EVERY coins information and put that in an array, that would be a nightmare to sort through the attributes and assign them to their corresponding coin. The other tag that can be used is `.coin-list__body__row` which gives us all the attributes PER ROW. This will allow for each row of coins to be put in an array and seperated from each other like so `doc.css(".coin-list__body .coin-list__body__row")`. Next you will be wondering, how can I access each of the coins AND their attributes individually so that I can assign them to my coin objects attribute? Lets look at the code step by step

```
coins = doc.css(".coin-list__body .coin-list__body__row").collect do |row|
      each_coin = row.css("span").collect do |text|
        text.text
      end
	end
```

the coins variable is assigned to the data that is collected within the `.coin-list__body__row` tag which is then collected and placed in an array. Remember, each element in this array has the coins name, price, etc together and we need them seperated. We can accomplish this by iterating through that array, collected each row and parsing each of the attributes into their own elements within that array. 

`coins.text` will give us => 

```
["1Bitcoin$8,592.01$144,883,410,564\n\t1.16%\n\t", 
"2Ethererum$6565$5465\n\t1.55%\n\t,
....
]
```

On the web page, you can see that each of the texts that we need is enclosed by a `span` tag. We can iterate through `coins` elements', parse and collect using our `span` tag to seperate each of these attributes and assign them to an individual coin. 

`each_coin` will give us => 
```
["1",
"Bitcoin",
"$8,592.01",
"$255,99,520,564",
""
"1.16%"]
```

Great! Now `each_coin` gives us an array with elements that can be accessed individually. This is now all inside the `coins` array which is then iterated again and instanstiated with the `Coin.new` object shown in the code below 

```
coins.each do |coin|
      new_coin = Crypto::Coin.new(name = coin[2], price = coin[3], market_cap = coin[6], change = coin[9].gsub("\t","").gsub("\n",""), description = coin[11])
      Crypto::Coin.all << new_coin #@all_coins << new_coin
    end
```

Figuring out how to properly scrape was the hardest part of the lab. You can dig through my code and see how my different objects interact with each other in a simple and straightforward way. 

Here are a few helpful tips:

* Make the code work firs tthen refactor and optimize
* Commit every few lines of code you create
* Work on one problem or one object at a time - dont get distracted
* Keep your classes and methods in separate files to help you stay organized and focused

The code of my project can be found here
https://github.com/akshay1dhingra/akshaydhingra-cli-app

In conclusion, this lab was my first attempt at building a program from scratch without any tests to tell me what my boundaries were. It was tough and frustrating at times, but if you are comfortable with `Pry` you can pretty much build anything you want. 

