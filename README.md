# Mountain Project Database Builder
This project is a web crawler built using [Scrapy](https://scrapy.org/) that aims to pull important metadata about both areas and routes from [Mountain Project](https://mountainproject.com) into a database to serve as the backbone for a 3rd party
API. The ultimate goal of this project is to allow 3rd party developers to provide supplementary services for Mountain Project users.

## Prerequisites
- Python 3.x
- A MongoDB database

## Installation
  1. Clone the repository
  2. Navigate to your cloned repository
  3. Run `pip install -r requirements.txt`

## Usage
The spider can be started with:

`scrapy crawl mp -s MONGO_URI=<YOUR_MONGO_URI> -s MONGO_DATABASE=<YOUR_MONGO_DATABASE_NAME>`

Note that this command will both log debug output to console, and log your configured level to your configured logfile

As Mountain Project contains a rather impressive amount of areas and routes, expect this crawler to take several hours. I
highly recommend using [Scrapy's built in job manager](https://docs.scrapy.org/en/latest/topics/jobs.html) so that you can stop
the crawl without losing where you left off. By default the logging level is `INFO` the log file is `log.txt`. These values are
configurable in `mp_scraper/settings.py`. For more information on settings check [Scrapy's docs](https://docs.scrapy.org/en/latest/topics/settings.html#log-enabled)

## What if I don't want to use MongoDB?
If MongoDB doesn't suit your needs, creating a new serialization pipeline is fairly trivial. I recommend looking at
[Scrapy's Item Pipeline docs](https://docs.scrapy.org/en/latest/topics/item-pipeline.html) as a starting place. All items coming
into the pipeline are defined in `mp_scraper/items.py`.
