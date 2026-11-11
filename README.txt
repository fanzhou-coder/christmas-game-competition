SafeDriver Group Christmas Challenge — competition prototype

WHAT CHANGED
- Nickname required (1–16 characters), remembered on this browser.
- English / Deutsch selector beside the nickname field. Language is remembered.
- All 50 wishes and the full game interface are available in both languages.
- One shared leaderboard, one player identity, and one best score across languages.
  Choosing a language does not change the course or create another player.
- Change name / language after a run to switch; language is locked during play.
- 10 gift bricks across a scrolling 1,560-pixel course.
- Four increasingly difficult sections: higher gifts, moving targets, wider gaps, faster snowmen.
  The first two gifts are stationary and forgiving. The remaining eight move
  horizontally with increasing range and speed; the final gifts sit near maximum
  jump height. Moving gifts stop once hit, keeping their tree and wish together.
  Ten snowmen patrol the course: two from gift three, then groups of two
  on longer ground sections. Short icy ledges each have one snowman.
  The first two gift areas have no snowmen.
  Players landing on an unopened moving gift ride along with it.
  Personal bests for this harder course are separate from earlier course versions.
- Identical starting positions, movement patterns, and hazards on every run for fair comparison.
- All 50 original wishes preserved. Each run chooses 10 without repetitions.
- 60 real seconds and 3 lives. Time continues when switching tabs.
- Tap once per jump; no automatic bouncing when Jump is held.
- Each wish appears in a speech bubble above the growing Christmas tree.
  The newest bubble follows its tree while scrolling and stays for 6.5 seconds.
  Wishes also remain below the game and in the end-of-run collection.
- Replay as often as you like. Best score wins, then shortest time taken. For example, 10 gifts in 25 seconds
  ranks above 10 gifts in 35 seconds. The leaderboard displays time taken;
  scores are still stored as remaining milliseconds for compatible server ranking.
- Santa-hat driver in a yellow car with ennooRental lettering on its side.
  Car and lettering are scaled down together by 12%.
  The visible front tyre determines gap entry in both driving directions.
  The bumper can overhang safely; a fall starts as soon as the front tyre
  touches the gap. A complete fall costs a life.
- Each gift displays one of five original company logos in a larger white label.
  Original SVGs are bundled locally. Logo loading errors fall back to brand text.
  The canvas keeps a stable 640 × 360 drawing resolution across screen sizes.
- Enlarged, bold black ennooRental lettering sits on a white car door panel.
- Start brings the game into view on small screens; English/German start and replay
  flows have automated checks, including a simulated SVG loading failure.
- Roadside signs read Stresemann Str. 74 at the start and sixth gift.
- Berlin skyline, gifts, trees, and snow remain.
- Local personal best works immediately. Shared scores need Supabase setup.

TRY IT FIRST
Open index.html in a browser. It needs config.js next to it.
Without Supabase configuration, the page clearly labels itself as an
unconnected preview; it does not invent leaderboard entries.

CONNECT THE SHARED LEADERBOARD
1. Create a Supabase project.
2. In Authentication > Sign In / Providers, enable Anonymous Sign-Ins.
3. Open SQL Editor and run supabase/setup.sql once in a fresh project.
4. In config.js set supabaseUrl to your project's HTTPS URL and
   supabasePublishableKey to its PUBLIC publishable key (or legacy anon key).
   Never put a secret key, database password, or service-role key in this file.
5. Upload index.html and config.js to your GitHub repository. Enable GitHub
   Pages from that branch/folder. No Node, build step, or npm packages needed.
6. Play and submit a run. Open the deployed game in another browser to check
   both players see the same leaderboard. A second browser is a new player.

Supabase uses anonymous authentication to associate scores with a browser.
Only nicknames, gifts, and remaining time are exposed by the public leaderboard.
Direct writes to tables are blocked; authenticated server functions manage runs
and replace a player's best only when the new attempt is better. Refresh and
automatic idle refresh show the current top 50. Equal scores and exact remaining
times share rank. Reusing someone else's nickname does not overwrite their score.
Clearing browser storage, switching browsers, or using another device creates a
new player. Nicknames are not verified company identities and may be duplicated.

VALIDATION LIMITS
This prototype checks score ranges, run ownership, elapsed time, and minimum
travel time on the server. Submissions are idempotent and concurrent attempts
are serialized per player. Browser games still permit client tampering; these
checks do not prove every brick was hit. Before using substantial prizes, add
server-side replay verification and a stronger participant identity rule.
Supabase Anonymous Sign-Ins can also create many users: configure abuse limits
and monitor usage for your expected event audience.
The live database integration still needs an actual Supabase project and an
end-to-end test. No shared leaderboard has been deployed from this package.

GAMEPLAY TUNING FOR THE NEXT STEP
T=60, TOTAL=10, WORLD=1560 are near the start of the inline game script.
reset() defines the fixed brick heights, gap locations, and snowman speeds.
All gifts can be hit from safe ground at the right point in their movement cycle.
The highest moving targets require precise timing, and snowmen guard later landings.
Playtest with coworkers before deciding whether 60 seconds is the final limit.
Brand SVG assets are sourced from safedriver.de and included in assets/.
The car body is 52 pixels wide; every ice gap is still jumpable.
The address on both signs preserves the user-requested spelling and number.
