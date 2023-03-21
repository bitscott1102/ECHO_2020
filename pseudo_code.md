# Update Tweets.
```
This program calls Standard search API to fill in the existing gap, and get new Tweets for each topic. 

function query_tweet:
    Call API to get the remaning request. Assign the quota to each topic.
    Get last tweet ID of current topic.
    Call API with quota, query logic, since ID, max ID (if given) to get latest tweets.

function work_backlog:
    Get all remaning tasks for the gaps.
    Get Standard search API config.
    Connect to DB.
    Get all topics in DB.

    for task_id = 0 TO len(tasks):
        Get topic query, since_id, and max_id based on task_id
        call query_tweet() with max_id. 
        task_id = task_id + 1
    Update all new Tweets to DB.
    Disconnect DB.

function update_tweets
    Get Standard search API config.
    Connect to DB.
    Get topics in DB, including query, since_id.
   
    For topic_id=1 TO len(topic)-1:
         call query_tweet() without max_id
         topic_id = topic_id + 1.
    Update all new Tweets to DB.
    Disconnect DB.

{
In the main function
    call function work_backlog every 15 minutes
    call function update_tweets every 15 munites
}


```

# Update botscore.
```
This program calls Botometer API to get botscore for 600 users per hour.

function update_botscores
    Connect to DB.
    Store current botscore of users avilable in JSON file to DB.
        Fetch all users without botscore, and sort by influence score.
    Take the first 600 users and call the Botometer API to get botscore.
    Log the API response, and store the result to DB.
    Disconnect DB.
}

{
In the main function
    call function update_botscores every hour
}

```