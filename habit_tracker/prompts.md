# Project: Habit Tracker

> - **Files:** habit-tracker.html
> - **Dates:** 2026-11-02 → 2026-11-02 (about 22 min of work in total, timed by me)
> - **Defaults:** Claude Code · model TBD · medium effort
> - **Status:** keeper
> - **Use:** tried on the live GitHub Pages site 2026-11-02
> - **Reusability:** artifact high · prompt pattern medium
> - **Tags:** single-file-html, productivity, localStorage, export-import
> - **Takeaway:** Settling storage, number-habit goals and what happens to past days before any code meant the whole app came out of one build prompt.
> - **Story value:** anecdote
> - **Surprises:** With no save button I wasn't sure anything was saved, but the ✔ marks that appear as each habit is done turned out to be enough confirmation. Asking up front what removing a habit should do to past days settled the trickiest design question before any code was written.

# Prompt 1 (app idea and clarifying questions):

> - **Tool:** 2026-11-02
> - **Session:** continued · attached: none
> - **Verified:** not-run
> - **Human edits:** none

The second idea I have for an app is a daily habit tracker app. This app should do the following:

* List a bunch of habits, here are some
   * Meditation
   * Prayer
   * Exercise
   * Eat healthy
   * Neck stretches
   * Caffeine (mg)
   * Hours of sleep


The app should then track your responses each day (not sure if it'd require a login then?) And you should be able to view your history for each day. Each day should have a % for how many habits you did successfully. You should ideally be able to add more habits to the list I made, or remove habits if you don't want to track them anymore. Each day should have the most updated list of habits.

Let me know if you have any questions

## Output 1:

Good idea. I have four questions before building.

**1. Does it need to work across devices?** It doesn't need a login. Your site on GitHub Pages can't run a server, so the simplest option is to save your answers in your browser, on that device only. That's private, needs no account, and works offline. The trade-off is that your phone and laptop would keep separate histories, and clearing your browser data erases it. Pick one:
- **(a) Browser only, with backup (recommended).** Add **Export** and **Import** buttons that save your history to a file and load it back. That also covers moving it to another device by hand.
- **(b) Automatic sync between devices.** This needs a login and an online database. It's much more work, and it no longer fits "one small file."

**2. What counts as a success for the number habits?** I'll let you set a goal for each number habit and change it later. Are these starting goals right?
- **Caffeine:** 200 mg or less
- **Hours of sleep:** 7 or more

The yes/no habits, like Meditation and Exercise, count as a success when checked.

**3. What should removing a habit do to past days?** I plan to keep history as it was. If you remove "Neck stretches" today, past days still show it, and their percentages don't change. Today and every day after use your current list. Does that match what you meant by "each day should have the most updated list of habits"?

**4. What should the folder be called?** I suggest folder `habit_tracker/` with app file `habit-tracker.html`.

I'll also add a way to fill in or fix earlier days, in case you forget to log one.

**For the record:** as with the movie picker, I'll create the folder once the name is settled. Your message above becomes Prompt 1, and this reply becomes Output 1. The model name will only go in the Defaults line, so it's a one-line edit for you at the end.

# Prompt 2 (answers and first build):

> - **Tool:** 2026-11-02
> - **Session:** continued · attached: none
> - **Verified:** human-tested
> - **Human edits:** none. Verified raised from agent-tested after I used the live site (Prompts 3–4).

1. Browser only works for now to keep it simple
2. Yes exactly. 200 mg or less for caffeine, 8 hrs or more for sleep
3. Removing a habit should not impact past days. Yes, today and every day after use your current list
4. habit_tracker is good.

## Output 2:

The habit tracker is built and pushed to `main`. Once the site updates, it'll be at **https://matt-baxter.github.io/vibe-coding/habit_tracker/habit-tracker.html** (hard refresh with Ctrl + Shift + R if you see an old copy). I tested it in a headless browser, including setting the clock forward a day to check past days, with no errors. Phone layout tested at phone size.

It's one file, `habit_tracker/habit-tracker.html`, with three tabs:

**Today**
- Your seven habits. The yes/no ones have checkboxes; Caffeine and Hours of sleep have number boxes with their goal shown underneath (at most 200 mg, at least 8 hrs).
- A ✔ appears next to each habit as soon as it's done or its goal is met.
- A ring shows the day's percentage, such as "3 of 7 habits done, 43%".
- The ◀ ▶ arrows and the date picker let you go back and fill in or fix a past day. Future days are blocked.

**History**
- Every day you've logged, newest first, with its percentage, a bar, and one dot per habit (filled in when done). Click a day to open it.
- Summary tiles: days logged, average day, last 7 days, perfect days, and your current streak.

**Habits**
- Add a habit, either yes/no or a number with a unit and an "at least" or "at most" goal.
- Remove habits, reorder them with ↑ ↓, and change number goals.
- **Export backup** downloads your history as a file, and **Import backup** loads one back in. Use these for safekeeping or to move to another device.

**How past days work:** the first time you log a day, it saves a copy of your habit list and goals at that moment. Changes you make later apply to today and every day after, but never rewrite a past day. In my test, I logged 7.5 hours of sleep on Nov 1, then removed "Neck stretches" and lowered the sleep goal to 7 on Nov 2. Nov 1 still showed "Neck stretches", still counted 7.5 hours as a miss, and kept its 43%. If you go back to a day you never logged, it starts from your current list.

**Things to know:**
- **Storage:** your data is saved in this browser only. Your phone and laptop keep separate histories, and clearing browser data erases it, so export a backup now and then.
- **Empty number habits:** a number habit left blank counts as not done for that day.
- **Streak:** counts consecutive days with at least one habit done. Today counts once you've logged something; until then the streak runs through yesterday.

**Documentation:** I created `habit_tracker/prompts.md` with your first message as Prompt 1, my questions as Output 1, and your answers as Prompt 2. Output 2 says "TBD" for now; I'll paste this message in with your next prompt. The status is `prototype` until you've used it, so it isn't on the home page yet. As before, the model name only needs filling in on line 5.

# Prompt 3 (does it autosave?):

> - **Tool:** 2026-11-02
> - **Session:** continued · attached: none
> - **Verified:** not-run
> - **Human edits:** none

Do the habits inputted autosave? I don't see a save button

## Output 3:

Yes, everything saves automatically to your browser as you go. There's no save button because there's nothing to save by hand.

- **Checkboxes** save the moment you click them.
- **Number boxes** (Caffeine, Hours of sleep) save when you leave the box: press Enter, Tab, or click anywhere else. The ✔ and the percentage update at the same moment, which is a handy sign that it saved.
- **Changes on the Habits tab** (adding, removing, reordering, goals) also save straight away. A short "Goal updated" or "Added …" message confirms each one.

Saved data survives closing the tab, reloading, and restarting your browser. I checked this in testing.

**One gap:** if you type a number and close the tab without leaving the box first, that number isn't saved. I can make number boxes save on every keystroke and add a small "Saved ✓" note so you can always see that it worked. That's a small change; just say the word.

**Documentation:** I pasted Output 2 into `habit_tracker/prompts.md` and recorded this question as Prompt 3. Output 3 says "TBD" for now; I'll paste this message in with your next prompt.

# Prompt 4 (mark as keeper, add to home page):

> - **Tool:** 2026-11-02
> - **Session:** continued · attached: none
> - **Verified:** agent-tested
> - **Human edits:** none

I think it's good how it is. The check marks are good confirmation for if something is saved or not. I think we can mark this as a keeper and add the site. This one we've spent 22 minutes on

## Output 4:

The habit tracker is now a `keeper` and has a card on the home page, and it's pushed to `main`. Give the site a minute, then hard refresh with **Ctrl + Shift + R**. I tested the home page in a headless browser: it shows "4 projects", and clicking the Habit Tracker card opens the app.

**Home page:** the new card has a thumbnail at `_thumbs/habit-tracker.png`, showing a sample day at 86%.

**`habit_tracker/prompts.md` header:**
- **Status:** `keeper`
- **Dates:** includes your 22 minutes, noted as timed by you.
- **Use:** "tried on the live GitHub Pages site 2026-11-02"
- **Takeaway:** "(draft)" removed.
- **Prompt 2:** Verified raised to `human-tested`, with a note in Human edits.

**I filled in three fields with my own judgment.** You asked me to do that last time; change any you disagree with:
- **Reusability:** `artifact high · prompt pattern medium`. You'll likely keep using the app. Asking questions first, then building, worked well on both apps.
- **Story value:** `anecdote`.
- **Surprises:** that the ✔ marks were enough confirmation without a save button, and that asking what removing a habit does to past days settled the trickiest design question before any code was written.

**Record kept up to date:** I pasted Output 3 and recorded this message as Prompt 4. Output 4 will be added with your next message. As before, the model name only needs filling in on line 5.

That's two of the three apps. Send idea #3 whenever you're ready.
