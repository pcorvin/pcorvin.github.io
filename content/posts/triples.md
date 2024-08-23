+++
title = "Are triples into LF all errors?"
date = 2024-08-02
weight = "20"
meta = "false"
+++

## Introduction

I started this post quite a while ago and already back then started to discuss it with a friend with some interest in baseball. The initial hypothesis I put out was: "*Triples into left field are much more common than you think*". He directly countered that the physical path when hitting a triple into the left field is much shorter. Thus the probability of getting caught running the bases is higher than the ball landing on the other side.

Note that the probability of hitting a triple in the 2023 season at a plat appearance was 3.8‰ (you read that right), representing a minor footnote. On the other hand, this makes it even more special. 

He was right, as statistically a strong majority (93%) of triples land in right field. The one question though presisted: How do triples into left field actually happen?

## Watching triples

Baseball is a data-driven sport. A plethora of metrics exist to quantify whatever circumstance in the game (even luck), where MLB is offering a [visual interface](https://baseballsavant.mlb.com/visuals) for better accessibility. This is sadly the only possibility to further assess how the triples came together: watching tape. Which I did for this article. You are welcome, but hold your horses: only for 2023 & 2024. I decided to make it as simple as possible and divide all scenarios into two.

Actual Triple: The hitter had a nice hit and actually hit a triple into left or center field.

Error by Fielder(s): Fielders were able to catch the ball but fumbled & let the triple happen. 

Note that only triples into left & center field were taken into account. Those were scraped of the play-by-play CSV export of all players with 5+ PA in 2023/2024. The link to the query can be found [here](https://baseballsavant.mlb.com/statcast_search?hfPT=&hfAB=triple%7C&hfGT=R%7C&hfPR=hit%5C.%5C.into%5C.%5C.play%7C&hfZ=&hfStadium=&hfBBL=7%7C8%7C&hfNewZones=&hfPull=&hfC=&hfSea=2024%7C2023%7C&hfSit=&player_type=batter&hfOuts=&hfOpponent=&pitcher_throws=&batter_stands=&hfSA=&game_date_gt=&game_date_lt=&hfMo=&hfTeam=&home_road=&hfRO=&position=&hfInfield=&hfOutfield=&hfInn=&hfBBT=&hfFlag=&metric_1=&group_by=name&min_pitches=0&min_results=0&min_pas=5&sort_col=ba&player_event_sort=api_p_release_speed&sort_order=desc&chk_stats_abs=on&chk_stats_hits=on&chk_stats_ba=on#results).

## A lot of errors

It is a tough verdict:

{{< figure src="/triples_errors.png" class="mid"  caption="29.7% of triples into left & left center field are fielder errors" >}}

Part of the analysis is to redefine what an error is. Errors are defined as "in the judgment of the official scorer,[...] a fielder fails to convert an out on a play that an average fielder should have made". I thought baseball was data-driven, yet the human touch (not only umpires) persits.

I therefore redefined what an error is, which is more restrive. To give you an idea, this is an [error](https://baseballsavant.mlb.com/sporty-videos?playId=7d62d974-e14d-4cd6-a2c1-45744caeed2c), [this](https://baseballsavant.mlb.com/sporty-videos?playId=5ec9ea5c-e2e0-4fb6-a85c-b605029a9734) is not.

Out of the 74 triples, 22 were deemed errors with 52 clear triples. Most of the errors happen as fielders do not hold on to the ball, which is at the tip of their glove. Other notorious errors are the deflection of the ball on the floor or miscommunication between fielders.

This is additionally reflected in secondary stats: Nearly all (92%) balls are "hard hit" i.e. the ball is hit with 150 kph. Ball speed is often paired with launch angle, concluding in "barrels", which have a high probability to end up as home runs. The barrel probability of all triples analyzed is 32.8%, where 15%+ barrel rate is considered elite.

Nevertheless, the outcome of the balls in play does not directly translate into an automatic triple and not even a double. xSLG highlights the expected outcome of all balls put in play by a player. [This](https://miniwebtool.com/slugging-percentage-calculator/) is a helpful tool to understand what slugging (SLG) means, where xSLG is the expected outcome based on the player's exit velocity & launch angle. Despite the high barrel rate, the average xSLG is 1.243, which translates into an automatic single (reaching first base) but not beyond that. This is validated by comparing SLG & xSLG, boasting an average difference of 1.757. 

## Umpires are humans too

Based on the statistical analysis, we can understand that triples into left field are somewhat dependent on the performance of fielders, letting go of balls in play even though they should normally have it. At the end, multiple factors, which go beyond this high-level overview, such as sprint speed help to score triples even when the probabilities are lower. The comparison to force outs at third base would also highlight how many players got caught in the process.

Overall, triples into left field are still a fraction (13.4%) of all triples happening in the game, where right field is a better location to hit them (although the SLG-xSLG is still high). And they happen way more often due to errors than you think. Blame the umpires for that.