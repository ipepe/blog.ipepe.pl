---
title: Gibbs Rankings Points System
categories: programming
---

For games developers and those of you curious about how the rankings are calculated exactly, <span class="notranslate">Tropic Euro</span> uses a special ranking algorithm called the "Gibbs Ranking Points System", developed by Chris Gibbs. The values start at 1500 and after each ranked game are recalculated as follows:</p>

<p>RP<sub>new</sub> = RP<sub>old</sub> + K<sub> 1</sub> . (RP<sub>game_weighted_average</sub> - RP<sub>old</sub> + S . (1 - G<sub>new_limited</sub> / G<sub>new_limited_total</sub> )<sup>K<sub> 2</sub></sup> )</p>

<p>Further clarification on what the parameters above mean and how they are computed:</p>

<ul>
	<li><strong>G<sub>new_limited</sub>:</strong> the number of games the user/team has played, including the new one and limited to a maximum of G<sub>exp</sub>.<br> (i.e. G<sub>new_limited</sub> = <i>MINIMUM</i>(G<sub>exp</sub>, G<sub>old</sub> + 1)).</li>
	<li><strong>G<sub>new_limited_total</sub>:</strong> the total of G<sub>new_limited</sub> across all players/teams involved in the game.</li>
	<li><strong>RP<sub>game_weighted_average</sub>:</strong> a weighted average of the RP values of all players/teams, using the G<sub>new_limited</sub> values.<br> (i.e. RP<sub>game_weighted_average</sub> = RP<sub>old</sub> . G<sub>new_limited</sub> summed over all players and then all divided by G<sub>new_limited_total</sub> )</li>
	<li><strong>S:</strong> indicates the level of success for the player/team in this particular game. It is set to a value between + K<sub> 3</sub> (first place) and - K<sub> 3</sub> (last place).</li>
</ul>

<p>This ranking points system is broadly based on the <a href="http://en.wikipedia.org/wiki/Elo_rating_system">Elo rating system</a>, except with some improvements. The original Elo formula has fixed K values for different rating values and number of games played, whereas the Gibbs algorithm effectively has a K value that dynamically adjusts according to the relative number of games of each player - this allows new users to quickly gain RP against more experienced players, and decreases as the system gains more confidence about a player's level of ability.</p>

<p>The use of weighted averages also means that experienced players can play new players with only a small reduction in RP if they lose the game (and likewise only a small gain if they win), to reflect the fact that the system is yet to accurately determine the new player's skill level.</p>

<p>The algorithm has four parameters that can be used to adjust the RP calculations and distribution of values:</p>

<ul>
	<li><strong>K<sub> 1</sub>:</strong> Affects the maximum amount of RP that can be gained/lost in a single game. This is set on a per-game basis according to the number of players, to reflect that 5 player games take longer to complete than 3 player games.<br><i>(Current values: 3P = 0.07, 4P = 0.08, 5P = 0.09, 1v1 = 0.07, 2v2 = 0.12)</i></li>
	<li><strong>K<sub> 2</sub>:</strong> An optional parameter that can be used to alter the way that the level of success (S) is affected by the user's games as a proportion of the total games across all players. A <u>reduction</u> in this value (the most likely use of this parameter) means that experienced players will gain/lose <u>more</u> RP against players with fewer than G<sub>exp</sub> games. <i>(Current value = 1.0)</i></li>
	<li><strong>K<sub> 3</sub>:</strong> Primarily represents the maximum difference between a player's RP and the weighted average that could reasonably occur in a game, but also affects the max gain/loss in RP. This means that if a player has between 0.5 K<sub> 3</sub> and K<sub> 3</sub> RP more than the weighted game average (depending on the number of players/games) then they will not be able to gain RP, regardless of the game outcome. In future this will be solved in <span class="notranslate">Tropic Euro</span> by having separate game rooms for players of different RP / experience levels. <i>(Current value = 503)</i></li>
	<li><strong>G<sub>exp</sub>:</strong> A number of games after which the system considers it has enough "experience" to accurately represent the player's skill level. It allows new users to gain/lose RP more quickly and results in the maximum base gain/loss decreasing to a stable value as the limit is reached. Note that the weighted game average still has a large impact on the calculations, both before and (especially) after the limit is reached. <i>(Current value = 25)</i></li>
</ul>

<p><strong>Note to games developers:</strong> you are welcome to use this formula as a ranking system in your own games completely free of charge - a link back to this page (although not necessary) would be appreciated in return.</p>




				</div>
			</td>

<h2>Rankings - The Basics</h2>

<p><span class="notranslate">Tropic Euro</span> uses a system of ranking points (RP) for assessing each player's relative skill level:</p>

<ol>
	<li>Your ranking starts at 1500 RP and is updated whenever you play a ranked game.</li>
	<li>A ranked game on the server is one where all islands are controlled by a unique human player (i.e. no computer players).</li>
	<li>Winning a ranked game will in general increase your RP, although coming in second place for a 4 or 5 player game will normally increase your ranking as well.</li>
	<li>If you do well in a game against players with higher RP scores then your ranking will go up more than if you outperform players with lower RP scores.</li>
	<li>The server maintains your RP scores separately for different types of game, including 3 to 5 player games (3-5P) and 2 player (1v1) games.</li>
</ol>

Sources:
 * <http://www.tropiceuro.com/rankings.php>
 * <https://github.com/ipepe/foosball-open-ranking/blob/master/app/models/player.rb>
