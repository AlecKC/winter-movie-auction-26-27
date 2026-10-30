# Winter 2026–2027 Movie Auction Tracker

A static website for tracking the winter 2026–2027 movie auction leaderboard with player totals and daily domestic box office updates. The season runs November 27, 2026 through March 29, 2027. Player and movie data are stored in `data/movies.json`.

## Edit Your Movie List

Update `data/movies.json`:

```json
{
  "id": "mission-impossible-final-reckoning",
  "title": "Mission: Impossible - The Final Reckoning",
  "owner": "Alec",
  "releaseDate": "2025-05-23",
  "domesticGross": 0,
  "dailyChange": 0,
  "revenueUrl": "https://www.the-numbers.com/movie/Mission-Impossible-The-Final-Reckoning-(2025)#tab=box-office",
  "source": "the-numbers.com"
}
```

Use a stable movie page from The Numbers or Box Office Mojo in `revenueUrl`. If no URL is provided, the site keeps that movie as a manual entry.

## Run Locally

```bash
npm install
npm start
```

Then open `http://localhost:5173`.

## Update Revenues

```bash
npm run update:revenues
```

The script fetches each `revenueUrl` starting November 27, 2026 through the inclusive March 29, 2027 cutoff, finds the domestic total, updates `domesticGross`, calculates `dailyChange`, and stamps `lastUpdated`. Before the start date or after the cutoff it does not fetch revenue; after the cutoff it removes any previously stored values later than the cutoff.
It also stores each daily value in `movie.history` and records player/movie snapshots in `data/history.json`, which powers the cumulative line graph over the season.

## Deploy With GitHub Pages

Create the public repository `AlecKC/winter-movie-auction-26-27`, push the `main` branch, then set **Settings → Pages → Build and deployment → Source** to **GitHub Actions**. The Pages workflow publishes the static site at `https://aleckc.github.io/winter-movie-auction-26-27/`.

## Daily Updates

The included GitHub Actions workflow runs once per day at 13:20 UTC. You can also trigger it manually from the Actions tab.
