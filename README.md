# Kaggle Competition Stats

## Number of participants per competition

![Number of participants per competition](https://raw.githubusercontent.com/usuyama/kaggle_competitions_stats/master/num_participants_per_competition.png)

## Total prize money per competition

### Scraping the list of competitions

1. Open the Kaggle competitions page https://www.kaggle.com/competitions
2. Open Chrome DevTools (F12)
3. Inject JQuery
"""
var jq = document.createElement('script');
jq.src = "https://ajax.googleapis.com/ajax/libs/jquery/2.1.4/jquery.min.js";
document.getElementsByTagName('head')[0].appendChild(jq);
"""
4. Find the div elements
* NOTE: it seems that the class labels (e.g. .iNFwoU) get updated dynamically. Find the correct class labels using the element inspector in DevTools.
"""
jQuery.noConflict();

competitions =
jQuery("div.competition-info").map(function(i, r) {
  return [
   [
     jQuery('.iNFwoU', r).text(),
     jQuery('.jGAkhp p', r)[0].title,
     jQuery('.edWFFg', r).text(),
     jQuery('.brOicV span', r).map(function(i, x) { return x.title }).toArray()
   ]
  ];
}).toArray();

JSON.stringify(competitions)
"""
5. Save the data to json and visualize using the notebook
