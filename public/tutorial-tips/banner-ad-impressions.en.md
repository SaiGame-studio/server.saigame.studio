A banner ad earns money for each **impression** (each time an ad is shown), not for how long it stays on screen. Keeping players on a screen longer does not make a banner earn more.

## How a banner is counted

- An impression is counted when the ad is displayed and the ad SDK reports it. Many ad networks also require the ad to be **viewable**: at least 50% of the banner on screen for about 1 continuous second.
- Revenue is roughly **impressions × eCPM** (earnings per 1,000 impressions). A banner shown for 1 second and a banner shown for 10 seconds both count as one impression.
- Banners **refresh** on their own, usually every 30 to 60 seconds, set in your mediation dashboard. Each refresh shows a new ad and counts a new impression.

## Do not hold players just for a banner

Making players wait, for example on a screen after login, only to show a banner:

- adds no revenue unless the banner refreshes while they wait,
- makes the game feel slow, and players may leave,
- can break ad network policies. Some networks, such as Google AdMob, restrict ads on loading or waiting screens where players have nothing to do. This can lower the value of your ads or get your account warned.

## A better approach

1. Show the banner as soon as the screen opens, for example right after login succeeds.
2. Wait until the ad SDK reports that the banner is displayed, plus about 1 second so the impression can count as viewable.
3. Set a maximum wait, for example 3 seconds. If the banner loads slowly or no ad is available, continue to the game anyway.

Put banners on screens where players already spend time, such as menus or results screens, instead of adding waiting screens for them.
