```markdown
                                                       pyscrobble

pyscrobble is a Python library for interacting with the Last.fm API. It allows you to fetch detailed information about artists, albums, tracks, and users. The library includes rate limiting to avoid exceeding API usage limits and supports various Last.fm endpoints.
```

## Installation

You can install `pyscrobble` via pip:

```bash
pip install pyscrobble
```

## Usage

Here’s how to use the `pyscrobble` library to interact with the Last.fm API:

### Importing the Library

```python
from pyscrobble import Handler
```

### Initializing the Handler

```python
api_key = 'your_lastfm_api_key'
handler = Handler(api_key)
```

### Fetching Artist Information

```python
artist = handler.get_artist('Radiohead')
print(artist)
```

### Fetching Album Information

```python
album = handler.get_album('OK Computer', 'Radiohead')
print(album)
```

### Fetching Track Information

```python
track = handler.get_track('Creep', 'Radiohead')
print(track)
```

### Fetching User Information

```python
user = handler.get_user('someusername')
print(user)
```

### Fetching Top Artists for a User

```python
top_artists = handler.get_top_artists('someusername')
for artist in top_artists:
    print(artist)
```

### Example with a Discord Bot

Here’s a simple example of how to use `pyscrobble` in a Discord bot using `discord.py`:

```python
import discord
from discord.ext import commands
from pyscrobble import Handler

# Initialize the bot
intents = discord.Intents.default()
intents.message_content = True
bot = commands.Bot(command_prefix='!', intents=intents)

# Initialize the Handler with your Last.fm API key
api_key = 'your_lastfm_api_key'
handler = Handler(api_key)

@bot.event
async def on_ready():
    print(f'Logged in as {bot.user.name}')

@bot.command(name='artist')
async def fetch_artist(ctx, artist_name: str):
    try:
        artist = handler.get_artist(artist_name)
        await ctx.send(f"Artist: {artist.name}\nBio: {artist.bio}")
    except Exception as e:
        await ctx.send(f"Error: {str(e)}")

@bot.command(name='album')
async def fetch_album(ctx, album_name: str, artist_name: str):
    try:
        album = handler.get_album(album_name, artist_name)
        await ctx.send(f"Album: {album.title}\nArtist: {album.artist.name}\nRelease Date: {album.release_date}\nURL: {album.url}")
    except Exception as e:
        await ctx.send(f"Error: {str(e)}")

@bot.command(name='track')
async def fetch_track(ctx, track_name: str, artist_name: str):
    try:
        track = handler.get_track(track_name, artist_name)
        await ctx.send(f"Track: {track.title}\nArtist: {track.artist.name}\nAlbum: {track.album.title}\nDuration: {track.duration} seconds\nURL: {track.url}")
    except Exception as e:
        await ctx.send(f"Error: {str(e)}")

# Run the bot with your Discord token
bot.run('your_discord_bot_token')
```

## Methods

### `get_artist(artist_name)`
Fetches information about an artist.

### `get_album(album_name, artist_name)`
Fetches information about an album.

### `get_track(track_name, artist_name)`
Fetches information about a track.

### `get_user(user_name)`
Fetches information about a user.

### `get_top_artists(user_name, period='overall')`
Fetches the top artists for a user for a specified period.

### `get_top_albums(user_name, period='overall')`
Fetches the top albums for a user for a specified period.

### `get_top_tracks(user_name, period='overall')`
Fetches the top tracks for a user for a specified period.

### `get_friends(user_name)`
Fetches a list of friends for a user.

### `get_neighbours(user_name)`
Fetches a list of neighbours for a user.

### `get_now_playing(user_name)`
Fetches the currently playing track for a user.

### `get_recent_tracks(user_name)`
Fetches recent tracks listened to by a user.

### `get_loved_tracks(user_name)`
Fetches tracks that a user has loved.

### `get_attended_events(user_name)`
Fetches events attended by a user.

### `get_shouts(user_name)`
Fetches shouts (user comments) for a user.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.



Replace placeholders like `your_package_name`, `your_lastfm_api_key`, and `your_discord_bot_token` with your actual package name and credentials.
