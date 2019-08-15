# Setting up my bots

Generally, the following things have to be done to set up a bot, other than writing the part that actually generates stuff:

- Set up a bare repo on the note-taker server.
- Set up a repo on the note-taker server and set its origin to the bare repo.
- Set up a [note-taker config](https://github.com/jimkang/note-taker/tree/master/configs) to point to the repo and configure RSS, deploy and restart note-taker.
- Add [posting with post-it](https://github.com/jimkang/selftagger/commit/fe025e510a32437d62c458575146b7b1aa9445fd#diff-d960da6d95212a2f05f7abf900eb7507R154) to note-taker to bot code.
- Schedule bot runs in cron.
- Schedule pushes of bot repo to origin in cron.
- Clone bare repo on backup server (git clone ssh://user@server/bare/repo/location) so that [archiving-tasks](https://github.com/jimkang/archiving-tasks/blob/master/update-repos.sh) will periodically update it by pulling from the bare repo on the bot server.
- Add bot to [bot-index JSON file](https://github.com/jimkang/bot-index/blob/master/bot-list.json). Build and deploy.
- Add to [build-html target in email-rss-sample](https://github.com/jimkang/email-rss-sample/blob/master/Makefile#L23) to get it into the daily emails.
- Maybe use [observatory-editor](https://jimkang.com/observatory-editor/) to add notes and categorization details about it to [observatory-meta](https://github.com/jimkang/observatory-meta).
- Post to notes about it.
- Post to Patreon about it.
- Include it in newsletter.
