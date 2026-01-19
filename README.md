# Readwise Reader Calibre Recipe

A Calibre recipe that fetches articles from your [Readwise Reader](https://readwise.io/read) inbox and converts them into an e-book for your Kindle or other e-reader.

## Features

- Fetches articles from your Readwise Reader **inbox** (unprocessed items)
- Filters to **articles only** (excludes podcasts, videos, PDFs, tweets, etc.)
- Uses Readwise's clean, parsed HTML for optimal reading experience
- Configurable number of articles (default: 20)
- **Read-only**: Does not archive or modify articles in your Readwise account

## Prerequisites

- [Calibre](https://calibre-ebook.com/) installed on your computer
- A [Readwise Reader](https://readwise.io/read) account
- Your Readwise API access token

## Installation

1. **Download the recipe file**

   Download `readwise-reader.recipe` from this repository.

2. **Add to Calibre**

   - Open Calibre
   - Go to **Fetch news** → **Add a custom news source**
   - Click **Load recipe from file**
   - Select the downloaded `readwise-reader.recipe` file
   - Click **Add**

## Configuration

### Getting Your API Token

1. Log in to your Readwise account
2. Visit [https://readwise.io/access_token](https://readwise.io/access_token)
3. Copy your access token

### Setting Up Credentials in Calibre

1. Go to **Fetch news** → **Schedule news download**
2. Find **Readwise Reader** in the list
3. Click **Download now** or **Schedule**
4. When prompted for credentials:
   - **Username**: Leave blank (or enter anything)
   - **Password**: Paste your Readwise API token
5. Click **OK**

### Configuring Options

You can configure the maximum number of articles to fetch:

1. Go to **Fetch news** → **Add a custom news source**
2. Select **Readwise Reader** from your custom sources
3. Find **Maximum articles** option
4. Enter your desired number (default: 20)

## Usage

### Manual Download

1. In Calibre, go to **Fetch news**
2. Find **Readwise Reader** under your custom sources
3. Click **Download now**
4. Wait for the download to complete
5. The e-book will appear in your Calibre library

### Scheduled Downloads

1. Go to **Fetch news** → **Schedule news download**
2. Select **Readwise Reader**
3. Configure your preferred schedule
4. Enable the schedule

### Sending to Kindle

After downloading:

1. Connect your Kindle or configure email delivery in Calibre
2. Select the downloaded Readwise Reader book
3. Click **Send to device** or use **Connect/share** → **Email to...**

## Command Line Usage

You can also use the recipe from the command line:

```bash
# Convert to EPUB
ebook-convert readwise-reader.recipe output.epub \
  --username "" \
  --password "YOUR_API_TOKEN"

# Convert to MOBI (for older Kindles)
ebook-convert readwise-reader.recipe output.mobi \
  --username "" \
  --password "YOUR_API_TOKEN"

# Test mode (downloads only a few articles for testing)
ebook-convert readwise-reader.recipe test.epub \
  --username "" \
  --password "YOUR_API_TOKEN" \
  --test -vv
```

## Troubleshooting

### "Invalid API token" error

- Verify your token at [https://readwise.io/access_token](https://readwise.io/access_token)
- Make sure you copied the entire token without extra spaces
- Regenerate your token if needed

### "No articles found" message

- Check that you have articles in your Readwise Reader inbox
- The recipe only fetches items with `location=new` (inbox)
- PDFs, videos, podcasts, and tweets are excluded

### "Rate limited" error

- Readwise has API rate limits
- Wait a few minutes and try again
- Avoid running the recipe too frequently

### Empty or malformed articles

- Some articles may not have HTML content available
- These are automatically skipped
- Check the Calibre log for details

### Viewing Logs

To see detailed logs:

1. In Calibre, go to **Preferences** → **Miscellaneous**
2. Click **Debug device detection**
3. Or use command line with `-vv` flag for verbose output

## How It Works

1. The recipe connects to the Readwise Reader API
2. Fetches articles from your inbox (`location=new`)
3. Filters to article category only (`category=article`)
4. Retrieves the clean, parsed HTML content
5. Packages everything into an e-book format

The recipe is **read-only** and does not modify your Readwise library. Articles remain in your inbox after downloading.

## API Reference

This recipe uses the [Readwise Reader API v3](https://readwise.io/reader_api):

- Endpoint: `GET https://readwise.io/api/v3/list/`
- Parameters used:
  - `location=new` (inbox items)
  - `category=article` (articles only)
  - `withHtmlContent=true` (include parsed HTML)

## Contributing

Contributions are welcome! Please feel free to submit issues or pull requests.

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Acknowledgments

- [Readwise](https://readwise.io) for their excellent Reader app and API
- [Calibre](https://calibre-ebook.com/) for the powerful e-book management platform
