# InstabotJS

Automatic Instagram-Bot with [Node.js][nodejs] project in [TypeScript][typescript] [3.0][typescript-30].

What's included:

* [TypeScript][typescript] [3.0][typescript-30],
* [TSLint 5][tslint] with [Microsoft rules][tslint-microsoft-contrib],
* [Prettier][prettier] to enforces a consistent code style (but it's optional),
* [NPM scripts for common operations](#available-scripts),
* .editorconfig for consistent file format.

## Config

These configuration setting should be set inside the src [bot-config.json](/src/bot-config.json) file when you are compiling the project with `npm run watch`. When you are only editing the configuration without compiling it, just edit the [bot-config.json](/build/src/bot-config.json) in the `build/src` directory.

* hashtags
  > hashtags, list of hashtags the bot should search for, without '#' prefix
* sleepStart
  > sleepStart, time to send the bot to sleep only in this format 'hh:mm' or 'h:mm'
* sleepEnd
  > sleepEnd, time to wake the bot up again only in this format 'hh:mm' or 'h:mm'
* botModes
  > botModes, list of names of modes to start, format: 'routine1, routine2, routine3, ...'
  > available botModes, see **strategies**
* maxLikesPerHashtag
  > maxLikesPerHashtag, maximum likes the bot is allowed to make per hashtag per 24 hours when the limit is reached, the bot takes another hashtag
* maxLikesPerDay
  > maxLikesPerDay, maximum likes the bot is allowed to make per 24 hours
* maxDislikesPerDay
  > maxDislikesPerDay, maximum dislikes per 24 hours
* minDislikeWaitTime
  > minDislikeWaitTime, minimum time to wait to dislike a mediapost the bot liked before
  > (time in minutes)
* maxFollowsPerDay
  > maxFollowsPerDay, max people to follow in 24 hours
* maxUnfollowsPerDay
  > maxUnfollowsPerDay, max people to unfollow in 24 hours
* minUnfollowWaitTime
  > minUnfollowWaitTime, minimum time to wait to unfollow a user the bot followed before
  > (time in minutes)
* maxFollowsPerHashtag
  > maxFollowsPerHashtag, maximum follows the bot is allowed to make per hashtag per 24 hours when the limit is reached, the bot takes another hashtag (only used by sinlge follow mode)
* followerOptions
  * unwantedUsernames
    > unwantedUsernames, list of strings containing full or parts of usernames that are not wanted to be followed
  * followFakeUsers
    > followFakeUsers, if bot should follow users that the bot thinks are fake users
  * followSelebgramUsers
    > followSelebgramUsers, if bot should follow users that the bot thinks are selebgram users
  * followPassiveUsers
    > followPassiveUsers, if bot should follow users that the bot thinks are passive (inactive) users
  * unfollowOnlyWhenFollowingMe
    > unfollowOnlyWhenFollowingMe, only let bot unfollow user if user is following user
* postOptions
  * maxLikesToLikeMedia
    > maxLikesToLikeMedia, maximum likes a post is allowed to have to be liked by the bot
  * minLikesToLikeMedia
    > minLikesToLikeMedia, minimum likes a post is allowed to have to be liked by the bot
* waitTimeBeforeDelete
  > waitTimeBeforeDelete, minutes to wait before delete stored data (only unfollowed and disliked images) this option is only available to prevent an enormous data stored as json
  > (time in minutes)
* isTesting
  > isTesting, used only to let bot be checkable by automated tests

### Strategies

Strategies or botModes (reference in bot-config.json) can be used to configure the behaviour of the bot while online. One maybe just wants to like pictures every day, the other only wants to follow
users automatically. There are a few strategies to use to complete different kind of behaviours. All strategies can be used together.

* like-classic-mode
* follow-classic-mode
* unfollow-classic-mode

## Actions frequency restrictions

* **Likes limit**: no more than one like every 28 – 36 seconds (1000 likes at a time for a period of 24 hours);

* **Followers limit**: no more than one like every 28 – 36 seconds and no more than 200 followers an hour (1000 followers at a time for a period of 24 hours);

* **Followers + Likes limit**: no more than 2000 (1000 + 1000) every 24 hours with the interval of 28 – 38 seconds;

* **Unfollow limit**: the interval of 12-22 seconds, no more than 1000 every 24 hours from unmutual and 1000 from mutual;

* **Mentions limit**: 5 nicks in a message with the interval of 350-450 seconds;

* **Comments limit**: no more than 12-14 an hour with the interval of 350 – 400 seconds, overlimit might be treated as spam;

* **Publishing images**: you shouldn’t add too many images to a new Instagram account, the best practice is to publish no more than 2-3 images a day, and for older accounts this figure is 9-12 images.

### New account limitations

You should keep these in mind in case you’re not sure that Instagram treats your account as a trusted one, or if you want to secure your account from getting blocked to the full.

* The actions interval for the first 12-20 days is 36-48 seconds;
* The total limit for all kinds of actions (follow, unfollow, like) is 500 every 24 hours.

The best strategy for new accounts would be to publish 2 or 3 images and let the account settle in for 2 or 3 weeks.

## Available scripts

* `clean` - remove coverage data, Jest cache and transpiled files,
* `build` - transpile TypeScript to ES6,
* `watch` - interactive watch mode to automatically transpile source files,
* `lint` - lint source files and tests,
* `test` - run tests,
* `test:watch` - interactive watch mode to automatically re-run tests
