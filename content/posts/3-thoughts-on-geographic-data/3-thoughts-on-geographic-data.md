---
title: "Thoughts on Geographic Data: ZIP Codes vs. Census Tracts"
date: 2024-02-07T00:00:00+00:00
# weight: 1
# aliases: ["/first"]
tags: ["Geographic Data"]
author: "Diao"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
# description: "Desc Text."
canonicalURL: "https://canonical.url/to/page"
disableHLJS: true # to disable highlightjs
disableShare: false
disableHLJS: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: false
ShowRssButtonInSectionTermList: true
UseHugoToc: true
# menu:
#   main:
#     identifier: "posts"
cover:
    image: "<image path/url>" # image path/url
    alt: "<alt text>" # alt text
    caption: "<text>" # display caption under cover
    relative: false # when using page bundles set this to true
    hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/<path_to_repo>/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

Do you care about lines and points or polygons? ZIP Codes vs. Census Tracts for analysis, when to use which? 

Some thoughts on answering the above questions...

## ZIP Codes
ZIP Codes are 5-digit numbers developed by USPS to represent individual post offices across the US. The term "ZIP" in ZIP Code stands for "Zone Improvement Plan."

USPS segmented the country into 10 (0-9) ZIP Code areas from the northeast to the northwest. The 5-digit numbers represent three things:
- **First digit**: national area, usually a state
- **Second and third digit**: sectional center or large city postal office, usually a county or city 
- **Forth and fifth digit**: associate postal office or delivery area

{{< figure src="/posts/3-thoughts-on-geo-analysis/zip_code_zones.png" alt="ZIP Codes Zone Map" caption="Fig. 1. U.S. ZIP Codes Zone Map. (Image source: By Smarty, https://www.smarty.com/docs/zip-codes-101.)" align="center" >}}


### Characteristics
- **Lines Not Shapes**: ZIP Codes are groups of lines (mail routes) and points (commercial address or large PO box). 
- **No Boundaries**: ZIP Codes do not draw boundaries of an area. They may not align well with natural or administrative boundaries.
- **Area Overlap**: Areas in different states may share the same ZIP Code. For example, 97635 includes portions of Lake County, Oregon, and Modoc County, California.
- **Not Static**: ZIP Codes may change frequently, especially for areas with fast population growth or delivery volume growth. USPS issues annual reports on changes they made over the year, but the change could happen at any day and any time. 
- **Not Designed for Statistics**: ZIP Codes are not designed for statistical analysis, thus use for statistical analysis is heavily criticized for numerous reasons and advised against as a cartographic practice. To solve this issue, U.S. Census Bureau calculates approximate boundaries of ZIP Code areas to match with census blocks, which it calls ZIP Code Tabulation Areas (ZCTAs) and is updated every 5 years. 

### Pros
- **Widely Used**: ZIP Codes are commonly used and understood by the general population, making them useful for communication and analysis.
- **Accessibility**: ZIP Code data is readily available in datasets, especially for addressing and location-based information.
- **Granularity**: ZIP Codes provides a level of detail for localized analysis and mapping.

### Cons
- **Lack of Boundaries**: ZIP Codes do not have clear boundaries, making them unsuitable for precise area representation. Also, ZIP Codes may not align well with natural or administrative boundaries, leading to challenges when aggregating data across larger geographic regions.
- **Heterogeneity**: ZIP Code boundaries can vary widely in size and population, leading to issues with homogeneity within ZIP Code areas.
- **Temporal Instability**: Subject to frequent changes, impacting historical or time-series analyses.
- **Limited Demographic Insights**: Not ideal for detailed demographic or economic analysis due to their lack of area representation, especially when dealing with sensitive data or small populations.

### What causes change? 
Changes to ZIP Code boundaries may occur due to factors such as:

- **Population Growth**: Rapid population growth in certain areas may necessitate the creation of new ZIP Codes or the realignment of existing ones to better serve the increased population.

- **Urban Development**: Urban development projects, such as the construction of new neighborhoods or business districts, can lead to changes in ZIP Code boundaries to accommodate the new developments.

- **Administrative Changes**: Occasionally, administrative decisions or reorganizations may prompt adjustments to ZIP Code boundaries. This could include changes in municipal or county boundaries, which may in turn affect ZIP Code assignments.

- **Postal Efficiency**: The USPS may periodically review and adjust ZIP Code boundaries to optimize mail delivery efficiency and streamline postal operations.

### When to use? 
- **Targeting Specific Markets**: If you need to analyze data at a relatively localized level, such as targeting customers or assessing market demand in specific areas, zip codes may be more appropriate due to their smaller geographic scale.

- **Accessibility and Familiarity**: If accessibility and familiarity is concerned, Zip codes are widely recognized and understood by the general population, making them convenient for communication and analysis, especially in marketing or business contexts.

- **Postal-Related Analysis**: Zip codes are primarily used by postal services for mail delivery purposes, so they are well-suited for analyzing mail delivery patterns, shipping logistics, or other postal-related phenomena.

## ZIP+4 Codes
ZIP+4 is an upgraded version of ZIP Codes, which uses the basic five-digit code plus four additional digits to identify a geographic segment within the five-digit delivery area, such as a city block, a group of apartments, an individual high-volume receiver of mail, a post office box, or any other unit that could use an extra identifier to aid in efficient mail sorting and delivery. 

## Census Tracts
Census tracts are specially designed geographic regions for the purpose of taking census and statistical analysis. 

### Characteristics
- They cover the entire U.S. landscape from wall to wall as polygons.
- A census tract has a min population of 1200 and a max population of 8000. All census tracts average about 4,000
inhabitants.
- It gets updated every 10 years. 
- It splits the entire U.S. more evenly. 

### Pros
- **Homogeneity**: Census tracts are designed to be relatively homogenous in terms of population characteristics, which can be advantageous for certain types of analysis, such as demographic profiling or public health research.
- **Standardization**: Census tracts are defined by the U.S. Census Bureau and have standardized boundaries, facilitating consistent analysis and comparison across different regions.
- **Statistical Rigor**: Census tracts are designed for statistical reliability, making it suitable for in-depth analyses.
- **Periodic Updates**: While not frequent, U.S. Census Bureau updates them every decade provide relatively recent demographic snapshots.
- **Detailed Demographic Data**: Census tracts are associated with detailed demographic data collected by the Census Bureau, providing rich information for analysis.
- **Alignment with Policy**: Census tracts often align with administrative boundaries and are used in policy-making and resource allocation.

### Cons
- **Availability**: Census tract data may not be as readily available as zip code data.
- **Less Familiarity**: Census tracts are less commonly understood by the general public compared to zip codes, which may hinder communication or dissemination of results.
- **Limited Temporal Insight**: Updates every 10 years may not capture rapid demographic changes.
- **Lack of Precision**: Census tracts cover larger geographic areas compared to zip codes, which may limit their usefulness for analyzing localized phenomena or targeting specific markets.
- **Complexity in Integration**: Combining census tract data with other datasets may require advanced spatial processing.

### When to use?
- **Detailed Demographic Analysis**: Census tracts are associated with detailed demographic data collected by the Census Bureau, making them valuable for analyzing population characteristics, socioeconomic indicators, or public health outcomes.

- **Homogeneity in Population Characteristics**: Census tracts are designed to be relatively homogenous in terms of population characteristics, making them useful for analyzing trends or disparities within specific communities.

- **Policy and Planning**: Census tracts are commonly used in policy-making, resource allocation, and urban planning due to their alignment with administrative boundaries and detailed demographic information.

- **Longitudinal Studies**: Census tracts provide stable geographic units over time, making them suitable for longitudinal studies or tracking changes in population dynamics, urban development, or socioeconomic conditions.


## References

[1] Wikipedia. “[ZIP Code](https://en.wikipedia.org/wiki/ZIP_Code)" 
[2] Smarty. “[ZIP Codes 101](https://www.smarty.com/docs/zip-codes-101)" 
[3] U.S. Census Bureau. “[2020 Census Tract Maps](https://www.census.gov/geographies/reference-maps/2020/geo/2020pl-maps/2020-census-tract.html)" 
[4] Service Objects. “[ZIP Codes are not boundaries](https://www.serviceobjects.com/blog/zip-codes-are-not-boundaries/)" 
