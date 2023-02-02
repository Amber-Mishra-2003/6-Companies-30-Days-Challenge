# Tweet Counts Per Frequency

Problem Link :- [Link](https://leetcode.com/problems/tweet-counts-per-frequency/description/)

<h3>
Problem :- A social media company is trying to monitor activity on their site by analyzing the number of tweets that occur in select periods of time. These periods can be partitioned into smaller time chunks based on a certain frequency (every minute, hour, or day).

For example, the period [10, 10000] (in seconds) would be partitioned into the following time chunks with these frequencies:

  * Every minute (60-second chunks): [10,69], [70,129], [130,189], ..., [9970,10000]
  
  * Every hour (3600-second chunks): [10,3609], [3610,7209], [7210,10000]
  
  * Every day (86400-second chunks): [10,10000]
  
Notice that the last chunk may be shorter than the specified frequency's chunk size and will always end with the end time of the period (10000 in the above example).

Design and implement an API to help the company with their analysis.

Implement the TweetCounts class:

  * TweetCounts() Initializes the TweetCounts object.
  
  * void recordTweet(String tweetName, int time) Stores the tweetName at the recorded time (in seconds).
  
  * List<Integer> getTweetCountsPerFrequency(String freq, String tweetName, int startTime, int endTime) Returns a list of integers representing the number of tweets with tweetName in each time chunk for the given period of time [startTime, endTime] (in seconds) and frequency freq.
  
    * freq is one of "minute", "hour", or "day" representing a frequency of every minute, hour, or day respectively.
</h3>


**Solution :-**
```
class TweetCounts {
    unordered_map<string, vector<int>> m;
public:
    TweetCounts() 
    {
        m.clear();
    }
    
    void recordTweet(string tweetName, int time) 
    {
        m[tweetName].push_back(time);
    }
    
    vector<int> getTweetCountsPerFrequency(string freq, string tweetName, int startTime, int endTime) \
    {
        if(freq=="minute")
        {
            vector<int> count((endTime-startTime)/60 + 1, 0);
            for(auto a:m[tweetName])
            {
                if(startTime<=a && a<=endTime) count[(a-startTime)/60]++;
            }
            return count;
        }
        else if(freq=="hour")
        {
            vector<int> count((endTime-startTime)/3600 + 1, 0);   
            for(auto a:m[tweetName])
            {
                if(startTime<=a && a<=endTime) count[(a-startTime)/3600]++;
            }
            return count;
        }
        else
        {
            vector<int> count((endTime-startTime)/86400 + 1, 0);
            for(auto a:m[tweetName])
            {
                if(startTime<=a && a<=endTime) count[(a-startTime)/86400]++;
            }
            return count;
        }
    }
};
```
