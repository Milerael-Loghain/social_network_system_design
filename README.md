# Traveler Social Network - System Design
Homework for course by System Design

### Functional requirements:

- Posting travel updates with photos, brief descriptions, and location tagging.
- Rating and commenting on posts from other travelers.
- Following other travelers to keep up with their activities.
- Searching for popular travel destinations and viewing posts from those locations.
- Browsing a feed of posts from other travelers and a personalized feed based on subscriptions, displayed in reverse chronological order.


### Non-functional requirements:

- 10 000 000 DAU +
- CIS countries only
- User data is always stored
- Availability 99,95%
- Seasonal - vacations, holidays, etc
- Service should support both web and mobile devices
- User Activities:
  - During a season, one user posts 5 updates per day with 2 photos
  - One user rates 10 updates per day
  - One user comments on 2 update per day
  - One user starts following 1 other user per week
  - One user reads 75 updates in a feed per day
  - During a season, one user uses search 25 times per day (looking for a travel destination before the season)
- Timings:
  - Posting should take no more than 5 seconds
  - Commenting should take no more than 2 seconds
  - Fetching a search result should take no more than 3 seconds
  - Loading a feed page should take no more than 1 seconds (feed page is 5 posts)
- Limits:
  - Images should take no more than 5 Mb of storage space
  - 1-10 images per update
  - 300 characters message limit for comments
  - 750 characters message limit for an update desription
  - 100 posted updates per day

## Basic calculations

RPS (Posting updates):

    Base:
    RPS = 10 000 000 * 1 / 7 / 86 400 ~= 20 
   
    During a season:
    RPS = 10 000 000 * 5 / 86 400 ~= 600 

    Transaction:
      - id
      - created_at
      - user_id
      - geo_position
      - description_text (750 characters)
      - pictures (2 on average, 5mb max each)
      
    Traffic = ~ 10,5 MB

    Base traffic/s  = 10,5 MB * 20 ~= 210 MB/s
    Seasonal traffic/s = 10,5 MB * 600 ~= 6 GB/s

RPS (Rating):

    RPS = 10 000 000 * 10 / 86 400 ~= 1200 

    Transaction:
      - id
      - user_id
      - update_id
      
    Traffic = ~ 48 B

    Traffic/s  = 48B * 1200 ~= 56 KB/s

RPS (Comments):

    RPS = 10 000 000 * 2 / 86 400 ~= 250 

    Transaction:
      - id
      - created_at
      - user_id
      - update_id
      - message (300 characters)

    Traffic = ~ 360 B
    Traffic/s  = 360B * 250 ~= 90 KB/s    

RPS (Follows):

    RPS = 10 000 000 * 1 / 7 / 86 400 ~= 20 

    Transaction:
      - id
      - user_id
      - followed_user_id
      
    Traffic = ~ 48 B

    Traffic/s  = 48B * 20 ~= 960 B/s
    
RPS (Feed):

    RPS = 10 000 000 * 75 / 86 400 ~= 8700

    Transaction:
      - id
      - created_at
      - user_id
      - geo_position
      - description_text (750 characters)
      - pictures (2 on average, 5mb max each)
      
    Traffic = ~ 10,5 MB
    Traffic/s  = 10,5MB * 8700 ~= 91,5 GB/s
    
RPS (Search):

    Base:
    RPS = 10 000 000 * 2 / 86 400 ~= 250

    During a season:
    RPS = 10 000 000 * 25 / 86 400 ~= 3000

    Traffic I guess depends on the implementation (?)
    
