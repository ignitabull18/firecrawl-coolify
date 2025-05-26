# FireCrawl Coolify Deployment

This repository contains a Docker Compose configuration for deploying [FireCrawl](https://github.com/mendableai/firecrawl) with the [FireCrawler UI](https://github.com/sammcj/firecrawler) on Coolify.

## Features

- ✅ Full FireCrawl API with Playwright support
- ✅ Redis queue management
- ✅ Worker service for processing crawl jobs
- ✅ Community Web UI for easy interaction
- ✅ Bull Dashboard for job monitoring
- ✅ Ready for Coolify deployment

## Prerequisites

- Coolify instance running
- Domain names configured:
  - `firecrawl.yourdomain.com` for the API
  - `firecrawl-ui.yourdomain.com` for the Web UI (optional)

## Quick Deploy to Coolify

1. In Coolify, create a new service and select **"Docker Compose Empty"**

2. Copy the contents of `docker-compose.yml` from this repository

3. Configure environment variables:
   - `BULL_AUTH_KEY`: Set a secure password for Bull Dashboard
   - `TEST_API_KEY`: Set your API key for authentication
   - Other optional variables as needed

4. Set up domains:
   - Main domain: `firecrawl.yourdomain.com` → Port 3002
   - UI domain: `firecrawl-ui.yourdomain.com` → Port 3003

5. Deploy!

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `BULL_AUTH_KEY` | Yes | Password for Bull Dashboard access |
| `TEST_API_KEY` | Yes | API key for FireCrawl authentication |
| `USE_DB_AUTHENTICATION` | No | Set to `true` for database auth (default: `false`) |
| `NUM_WORKERS_PER_QUEUE` | No | Number of concurrent workers (default: `8`) |
| `OPENAI_API_KEY` | No | For AI-powered features |
| `LLAMAPARSE_API_KEY` | No | For PDF parsing |

## Access Points

After deployment, you can access:

- **FireCrawl API**: `https://firecrawl.yourdomain.com`
- **API Documentation**: `https://firecrawl.yourdomain.com/docs`
- **Bull Dashboard**: `https://firecrawl.yourdomain.com/admin/@/queues` (password: `BULL_AUTH_KEY`)
- **Web UI**: `https://firecrawl-ui.yourdomain.com`

## Usage

### Via Web UI
Navigate to your FireCrawl UI domain and use the interface to:
- Scrape single URLs
- Crawl entire websites
- Extract structured data

### Via API

```bash
# Scrape a single page
curl -X POST https://firecrawl.yourdomain.com/v1/scrape \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -d '{"url": "https://example.com", "formats": ["markdown", "html"]}'

# Start a crawl job
curl -X POST https://firecrawl.yourdomain.com/v1/crawl \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
  -d '{"url": "https://example.com", "limit": 10}'
```

## Troubleshooting

### Build Issues
If Coolify has trouble building from GitHub contexts, you can:
1. Fork this repository
2. Remove the `build:` sections and use pre-built images
3. Or build the images locally and push to your registry

### Memory Issues
FireCrawl can be memory-intensive. Monitor your server resources and adjust `NUM_WORKERS_PER_QUEUE` if needed.

## Credits

- [FireCrawl](https://github.com/mendableai/firecrawl) by Mendable
- [FireCrawler UI](https://github.com/sammcj/firecrawler) by sammcj
