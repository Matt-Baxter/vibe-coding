# Project: Movie Picker

> - **Files:** movie-picker.html, movies-data.js, build_data.py
> - **Dates:** 2026-11-01 → 2026-11-01
> - **Defaults:** Claude Code · model TBD
> - **Status:** prototype
> - **Use:** none yet
> - **Reusability:** artifact TBD · prompt pattern TBD
> - **Tags:** dataset, productivity
> - **Takeaway (draft):** Asking for clarifying questions before any code surfaced the one real decision (where the IMDb data comes from) before it could derail the build.
> - **Story value:** TBD
> - **Surprises:** The cloud sandbox blocked IMDb's download site until I added it to the environment's allowed domains. Brand-new releases with inflated early ratings (e.g. a 2026 film at 9.2) show up near the top of the default list.

# Prompt 1 (app idea and clarifying questions):

> - **Tool:** Claude Code · model TBD · 2026-11-01
> - **Session:** continued · attached: SEIS_606_--_week_8_homework.pdf (earlier in the session)
> - **Verified:** not-run (questions only, no code yet)
> - **Human edits:** none

Okay, here's the first app idea I have.

I want to create a website called movie_picker or movie_selector or something like that. These are the things I want the website to be able to do.

* Goal: Help the user pick a movie to watch

* User inputs a number of filters, e.g.
   * Movie genre
   * Movie length
   * Minimum Imdb rating
   * Movie age (i.e. the year it was made)
* The app then outputs a table of possible movies to watch. The table of outputs should have the following columns
   * Index (1, 2, 3, 4, 5, ...)
   * Movie Title
   * Genre
   * Year it was released
   * Score on IMDB


I am assuming that you may have to do some research online to find a database of movies and their IMDB scores in order for the app to be able to do that. The IMDB scores are actually pretty important since it's often how often I filter which movie(s) are good vs not (often with a threshold around 8 for good movies or 7 as a minimum for decent movies)

Before we start the code, let me know if you have any important questions to address, then after the next prompt, we'll start the code. Keep the questions simple and only if necessary. Please remember to follow the guidelines laid out in CONVENTIONS, and the homework instructions, e.g. only one main file, etc.

"Fork this repo and following my process (see CONVENTIONS.md and existing files & folders), “vibe code” and document at least three of your own little apps. They don’t have to be HTML files like my examples, but should be fairly small (aim for one file, or one main code file with supporting images/data/etc.)."

## Output 1:

Before coding, I need answers to three questions.

**1. Where should the movie data come from?** This one matters most. A website can't search IMDb live; IMDb has no free public search API. The usual approach is to download IMDb's free official data files once and save a trimmed copy next to the app as a supporting data file. A small helper script would produce that copy, and you'd re-run it whenever you want fresher scores. This fits the homework's "one main code file with supporting data."

My cloud environment blocks the IMDb download site, `datasets.imdbws.com`. Pick one:
- **(a) Unblock it (recommended).** Open the cloud environment menu in this session's title bar, choose **Edit**, then **Network access**, and add `datasets.imdbws.com` under **Allowed domains**. The steps are at https://code.claude.com/docs/en/cloud-environments#network-access. This gives current ratings for thousands of movies.
- **(b) Skip the change** and I'll use a free IMDb movie list someone has posted on GitHub. Those are usually a few years out of date and limited to about the top 1,000 movies.

IMDb's data is licensed for personal, non-commercial use, which covers a homework project.

**2. What should the folder be called?** I suggest folder `movie_picker/` with app file `movie-picker.html`, matching the existing projects.

**3. Should obscure movies be filtered out?** I plan to skip movies with only a few IMDb votes, so a 9.4 from 30 people doesn't top your list. My default is at least 25,000 votes. If you want, I can make that a filter in the app instead.

If I don't hear otherwise, I'll show exactly your five columns and sort by IMDb score, highest first.

**For the record:** I haven't created the folder or `prompts.md` yet, since the name isn't settled. Once you choose, I'll set it up with your message above as Prompt 1, word for word, and this reply as Output 1.

# Prompt 2 (answers and first build):

> - **Tool:** Claude Code · model TBD · 2026-11-01
> - **Session:** continued · attached: none
> - **Verified:** agent-tested
> - **Human edits:** none to the files. Before this prompt I added `datasets.imdbws.com` to the cloud environment's allowed domains.

I unblocked it (I believe I have followed the instructions you listed accurately), movie_picker is fine, let's try 10k votes default (feels less arbitary than 25k)

## Output 2:

The movie picker is built, documented in `movie_picker/prompts.md`, and pushed to your branch. I tested it in a headless browser: every filter, sorting, the random pick and the "show more" button worked, with no errors. I haven't tested it on a real phone.

The new `movie_picker/` folder has three files:
- **`movie-picker.html`** is the app itself. Double-click it to open; it needs no setup or internet connection.
- **`movies-data.js`** holds the movie data: 19,236 movies with at least 5,000 IMDb votes, downloaded today (about 1 MB). It's a `.js` file rather than `.json` because browsers block a page opened by double-click from reading a separate `.json` file.
- **`build_data.py`** re-downloads IMDb's data and rebuilds the data file. Run it whenever you want fresher scores:

```bash
python3 movie_picker/build_data.py
```

**The filters**
- **Genre:** click one or more genres. Results can match *any* or *all* of the ones you pick.
- **Length:** a minimum and maximum in minutes, with quick buttons such as "Short (≤100)".
- **Minimum IMDb rating:** starts at 7, with quick buttons for 7+ and 8+.
- **Year released:** a from and to year, with quick buttons such as "Since 2015".
- **Minimum IMDb votes:** starts at 10,000, as you asked. You can go as low as 5,000 or as high as 500,000.

**The results table** has your five columns: #, Movie Title, Genre, Year and IMDb Score. It's sorted by score, highest first, and clicking the Title, Year or Score header re-sorts it. Scores of 8 and up show in green, and 7 to 7.9 in yellow. Each title links to its IMDb page. The table shows 100 movies at a time, with a "Show more" button. With the default filters, 4,958 movies match.

**Beyond what you asked for:**
- A **🎲 Pick one for me** button picks a random movie from your current results.
- Adult titles are excluded from the data.

**Something to watch for:** brand-new releases sometimes get inflated early ratings. For example, *You Can See Everything* (2026) is currently #3 at 9.2. Raising the vote minimum or setting an end year filters these out.

**Documentation:**
- I added a new `dataset` tag to the tag table in `CONVENTIONS.md`, since no existing tag fit.
- In `prompts.md`, Output 2 says "TBD" for now; I'll paste this message in with your next prompt.
- Still needed from you: the model name in place of "model TBD", and an update to Verified once you've used the app yourself.
