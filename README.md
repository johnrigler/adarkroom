A Dark Room
===========
> "awake. head throbbing. vision blurry. come light the fire."

a minimalist text adventure game for your browser

[Click to play](http://adarkroom.doublespeakgames.com)

<table>
<tr><th colspan=4>Available Languages</tr>
<tr>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=zh_cn">Chinese (Simplified)</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=zh_tw">Chinese (Traditional)</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=en">English</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=fr">French</a></td>
</tr><tr>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=de">German</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=el">Greek</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=id">Indonesian</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=it">Italian</a></td>
</tr><tr>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=ja">Japanese</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=ko">Korean</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=nb">Norwegian</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=pl">Polish</a></td>
</tr><tr>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=pt">Portuguese</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=pt_br">Portuguese (Brazil)</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=ru">Russian</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=es">Spanish</a></td>
</tr><tr>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=sv">Swedish</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=th">Thai</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=tr">Turkish</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=uk">Ukrainian</a></td>
</tr><tr>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=vi">Vietnamese</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=lt_LT">Lithuanian</a></td>
	<td><a href="http://adarkroom.doublespeakgames.com/?lang=gl">Galician</a></td>
</tr>
</table>

or play the latest on [GitHub](http://doublespeakgames.github.io/adarkroom)

<a href="https://itunes.apple.com/us/app/a-dark-room/id736683061"><img src="http://i.imgur.com/DMdnDYq.png" height="50"></a>
<a href="https://play.google.com/store/apps/details?id=com.yourcompany.adarkroom"><img src="http://i.imgur.com/bLWWj4r.png" height="50"></a>
<a href="https://store.steampowered.com/app/2460660/A_Dark_Room/"><img src="https://i.imgur.com/yz6cnU0.png" height="50"></a>


This fork
---------

The first change in this fork is [fork-audit.html](fork-audit.html), a standalone
vanilla-JavaScript audit of the A Dark Room fork network.

The audit:

- loads the public fork list from GitHub;
- ranks likely candidates without treating inherited timestamps as original work;
- compares candidate branches directly against the upstream default branch;
- reports commits and changed files that are actually ahead of upstream;
- flags possible identity, wallet, signing, Web3, and blockchain work;
- exports the result as JSON.

It has no build process, framework, server component, account system, analytics,
or external JavaScript dependency. It can be opened locally or served as a static
file from GitHub Pages or IPFS. A live audit still depends on GitHub's public API
and its unauthenticated rate limit.

Identity experiment
-------------------

A self-sovereign identity can be useful in a single-player game, but it cannot
make an untrusted browser client honest.

The player controls the JavaScript, clock, local storage, imported save data, and
execution environment. A player can therefore fabricate state. A digital
signature proves that a particular key signed a record. It does not prove that
the record resulted from unmodified gameplay.

The useful model is **attested play**, not verified play. An identity may sign a
sequence of game-state checkpoints containing:

- the player's public identifier;
- the game version or source commit;
- a hash of the previous checkpoint;
- a hash of the current save state;
- an optional event log or declared modification list;
- a local timestamp and monotonically increasing sequence number;
- the player's signature.

This creates attributable histories and branches. Honest runs, experiments,
mods, impossible states, and cheating can all remain visible without pretending
that the software can distinguish them perfectly.

Possible trust classes are:

1. **Declared** — a player signs a state or score.
2. **Reproducible** — the player also publishes an event log that a deterministic
   game engine can replay.
3. **Refereed** — an independent service, trusted device, or cryptographic proof
   validates execution.

Only the first class belongs in the initial implementation. The other classes
add complexity and, in the case of a central referee, can recreate the dependency
this experiment is intended to avoid.

The identity layer should remain optional. Anonymous offline play must continue
to work. Private keys must never be placed in save data, game code, or blockchain
transactions. Identity should establish continuity and authorship across copies
of the game, not ownership of the game or permission to play it.
