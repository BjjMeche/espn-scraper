# ESPN Scraper

ESPN Scraper is a simple gem for scraping teams and scores from `ESPN`'s website. Please note that `ESPN` is not involved with this gem or me in any way. I chose `ESPN` because it is a leader in sports statistics and has a robust website. 

![](https://fbcdn-sphotos-e-a.akamaihd.net/hphotos-ak-prn1/72415_10151558558197269_312200662_n.jpg)

```
ESPN.responding?
# => true
```

Lets begin...

#### Supported leagues

The gem only supports the following leagues:

```
ESPN.leagues
# => [ "nfl", "mlb", "nba", "nhl", "ncf", "ncb" ]
```

Which are the NFL, MLB, NBA, NHL, NCAA D1 Football, NCAA D1 Men's Basketball respectively.

#### Scrape teams

You can get the teams in each league by acronym. It returns a hash of each division with an array of hashes for each team in the division.

```
ESPN.get_teams_in('nba')
# => {
#   "atlantic"=> [ 
#     { :name => "Boston Celtics", :data_name => "bos" },  
#     { :name => "Brooklyn Nets", :data_name => "bkn" }, 
#     { :name => "New York Knicks", :data_name => "ny" }, 
#     { :name => "Philadelphia 76ers", :data_name => "phi" }, 
#     { :name => "Toronto Raptors", :data_name => "tor" }
#   ]
#   "pacific" => ...
# }
```

#### Scraping scores

One issue with scraping scores is that football goes by year and week, and baseball, basketball and hockey go by date.

All score requests return an array of hashes. Here's an example NFL score hash:

```
{
  league: 'nfl',
  game_date: #<Date: 2012-10-25>,
  home_team: 'min',
  home_score: 17,
  away_team: 'tb',
  away_score: 36
}
```

You'll notice the `data_name` from before is used to identify teams. 

###### weekly (football)

Pattern is `ESPN.get_league_scores(year, month)`. This is for nfl and ncb:

```
ESPN.get_nfl_scores(2012, 8)
ESPN.get_ncb_scores(2011, 3)
```

###### daily (baseball, basketball, hockey)

Pattern is `ESPN.get_league_scores(date)`. This is for mlb, nba, nhl, ncb:

```
ESPN.get_mlb_scores( Date.parse('Aug 13, 2012') )
ESPN.get_nba_scores( Date.parse('Dec 25, 2011') )
ESPN.get_nhl_scores( Date.parse('Feb 14, 2009') )
ESPN.get_ncb_scores( Date.parse('Mar 15, 2012') )
```

## Installing

Add the gem to your `Gemfile`

```
gem 'espn_scraper', git: 'git://github.com/aj0strow/espn-scraper.git'
```

or

```
gem "espn_scraper", github: 'aj0strow/espn-scraper'
```

## Contributing

Please report back if something breaks on you! 

Also please let me know if any of the data names get outdated. For instance a bunch of NFL data names were recently changed. You can make fixes temporarily with the following:

```
ESPN::DATA_NAME_FIXES['nfl']['gnb'] = 'gb'
```

Future plans:
- Get start and end dates of a season




