# RedFin Property Scraper

## Overview
This project is a web scraping bot designed to extract detailed property information from [RedFin](https://www.redfin.com/) using Selenium and `undetected_chromedriver`. The script leverages multi-threading to scrape multiple listings efficiently.

## Features
- Uses **Selenium** with `undetected_chromedriver` to bypass bot detection.
- Extracts property details such as location, price, amenities, agent details, images, and more.
- Implements **multi-threading** for faster execution.
- Uses **Geopy's ArcGIS** for geocoding addresses.
- Saves scraped data in **CSV format**.
- Handles dynamic elements using explicit and implicit waits.

## Installation

### Prerequisites
Ensure you have the following installed:
- Python 3.x
- Google Chrome (latest version)
- ChromeDriver (compatible with your Chrome version)

### Required Python Libraries
Install dependencies using:

```sh
pip install selenium undetected-chromedriver geopy pandas fake-useragent webdriver-manager
```

## File Structure
```
.
├── RedFinBot.py      # Main script containing the bot logic
├── HelpingBot.py     # Parent class with reusable Selenium functions
├── data/             # Folder to store CSV files
└── README.md         # Project documentation
```

## Usage

### Running the Script
You can start scraping by executing the script with multithreading:

```python
th1 = Thread(target=implement_multithreading_on_redfin, args=[6563, "C:\\Users\\anwaa\\Downloads\\11 file links Redfin\\Beverly Hills.csv", "./RedfinData/Beverly Hills.csv", "Beverly Hills"])
th1.start()
time.sleep(25)
th2 = Thread(target=implement_multithreading_on_redfin, args=[6590, "C:\\Users\\anwaa\\Downloads\\11 file links Redfin\\Anaheim Santa Anna Irvine.csv", "./RedfinData/Anaheim Santa Anna Irvine.csv", "Anaheim Santa Anna Irvine"])
th2.start()
th1.join()
th2.join()
```

This will start two parallel threads to scrape property data for **Beverly Hills** and **Anaheim Santa Anna Irvine**.

### Key Functions

#### `HelpingBot` Class
This is a helper class that provides methods for common Selenium actions such as:
- `simple_finding(xpath)`: Finds a single element.
- `simple_findings(xpath)`: Finds multiple elements.
- `dynamic_finding(xpath, wait_time)`: Waits and finds an element.
- `click_element(xpath)`: Clicks an element.
- `click_element_by_action(xpath)`: Clicks an element using `ActionChains`.

#### `RedFinBot` Class
Inherits from `HelpingBot` and implements RedFin-specific scraping methods:
- `land_targeted_page(targeted_url)`: Navigates to the target listing page.
- `scrape_property(**kwarg)`: Extracts property details.
- `close_driver()`: Closes the Selenium driver.

#### `implement_multithreading_on_redfin(id, read_path, write_path, state_name)`
- Reads property URLs from a CSV file.
- Visits each listing and scrapes data.
- Saves the extracted data to a new CSV file.

## Extracted Data Fields
The script extracts the following property details:
- **Location Details**: Address, latitude, longitude
- **Property Details**: Price, beds, baths, size
- **Amenities**: In-unit, community, and unique amenities
- **Listing Agent Details**: Name, phone, email
- **Images**: Extracts image URLs

## Output Format
The extracted data is stored in CSV format with the following structure:

```
group_id,state,usa_islands,rental_type,group_name,post_location,lat,lon,property_price,property_beds,property_baths,sleeps,size,group_desc,total_reviews,attendees,in_unit_amenities,community_ammenities,uniques_amenities,amenities_dropdown,host_name,host_phone_number,host_email,images,user_id,post_link
```

## Notes
- The script runs in **incognito mode** to reduce tracking.
- Uses **implicit waits** to ensure elements load properly.
- **Geopy's ArcGIS** is used for geolocation but may return `None` if an address is ambiguous.
- Ensure your IP is not blocked by using **rotating proxies** if needed.

## Disclaimer
This project is intended for educational and research purposes only. Scraping RedFin or any other website without permission may violate their **terms of service**. Use responsibly.

## Author
**Anwaar Mirza**

## License
MIT License

